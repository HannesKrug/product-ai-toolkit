---
title: CAD Switches - Unified Model State API
status: Draft
version: 1.1
created: 2025-11-28
updated: 2025-11-28
target_release: 3.13.0 (Q1 2026)
authors: Hannes Krug (Senior PM), Maik Thöner, Tim Grasser
stakeholders: Development Team, Grob, Daimler Truck, Mercedes-Benz
jira_project: I3DHUB
confluence_space: 3Dhub (RD)
---

# CAD Switches - Unified Model State API
**Product Requirements Document**

> **Naming Note:** "CAD Switches" is the recommended name (see Section 7 for full analysis). Alternative: "CAD States".

---

## Executive Summary

**Problem:**
instant3Dhub currently handles multiple CAD filtering concepts (Layers, Variants, Reference Sets, LayerIDs) through separate implementations. Each new filter type requires changes across numerous components (l3dGen, webvis, renderer, GeometricService), creating maintenance overhead and limiting scalability. Critical customer requirements from Grob and Daimler Truck for Reference Set support cannot be met without a unified approach.

**Solution:**
CAD Switches introduces a unified, data-driven Filter API that abstracts all filtering concepts into a single extensible interface. By differentiating filter types only at the loader and UI levels, we enable seamless addition of new filter concepts without modifying core components.

**Success Metrics:**
- **Primary:** Feature adoption rate of CAD Switches API (measurable via API usage analytics)
- **Secondary:** Migration from legacy Variants/Layers APIs to CAD Switches API
- **Customer Validation:** Successful deployment at Grob (NX files) and Daimler Truck (JT files)

**Target Release:** 3.13.0 (Q1 2026)

---

## 1. Problem Statement

### Current Situation

instant3Dhub supports multiple CAD filtering concepts, each implemented independently:

- **Layer Filters:** Global visibility control (currently via `LayerFilterAPI`)
- **Variants:** Per-node product configuration (currently via `VariantsAPI`)
- **Reference Sets:** NX/JT concept for part-level visibility (hacked into LayerFilterAPI)
- **LayerIDs:** CAD-native layer identifiers

**Key Pain Points:**

1. **No Reference Set Support:** Critical requirements from Grob (NX) and Daimler Truck (JT) unmet:
   - Cannot load NX-authored default Reference Sets
   - Cannot switch Reference Sets per node
   - Visual clutter due to missing geometry filtering
   - Long load times for large assemblies

2. **Maintenance Overhead:** Each new filter concept requires changes in 6+ components:
   - l3dGen (transcoding)
   - webvis (frontend)
   - hare (renderer)
   - GeometricService (capping)
   - sharedSession, spaceService, spaceStoreService

3. **Semantic Confusion:** Reference Sets currently exposed via `LayerFilterAPI` with "ReferenceSet:" prefix
   - Multi-toggle allowed (incorrect behavior—Reference Sets are exclusive)
   - No per-node control (Reference Sets are node-specific)
   - Poor developer experience

4. **Scalability Limits:** Cannot rapidly respond to new customer filter requirements

### Customer Evidence

**Grob (NX files):**
- **Must-Have Reference Sets:** `Solid`, `Entire Part`, `Empty`
- **Use Case:** Engineers need to switch between detailed ("Entire Part") and simplified ("Solid") views during assembly review
- **Pain Point:** "All geometry is loaded without the option to set a reference set → visual clutter"

**Daimler Truck (JT files):**
- **Must-Have Reference Sets:** `Default`, `FINAL_PART`, `FLATPATTERN_OBJECTS`, `DAI_MASS_PROPERTIES`
- **Use Case:** Manufacturing engineers need flat pattern sketches (not 3D geometry) for laser cutting workflows
- **Current Workaround:** Merging Reference Sets + Layers (hacky implementation)

**Mercedes-Benz (JT files):**
- Already exporting Reference Sets as layers in JT files (validate compatibility)

---

## 2. User Personas & Use Cases

### Primary Persona: Web Developers

**Who:** Frontend developers building 3D visualization apps using webvis.js

**Background:**
- Building configurators, digital twins, inspection tools
- Integrate instant3Dhub into web applications
- Need programmatic control over 3D scene visibility

**Jobs to be Done:**
1. Filter 3D geometry based on CAD metadata (layers, variants, reference sets)
2. Build UI controls for end users to toggle visibility
3. Optimize load times by filtering unnecessary geometry -> not applicable, done by hub
4. Maintain consistent behavior across different CAD formats (NX, JT, PLMXML)

**Pain Points:**
- Inconsistent APIs: `LayerFilterAPI` vs `VariantsAPI` with different patterns
- Cannot address Reference Sets semantically (forced to use layer API) -> Only on track version
- Each new filter concept = learning curve + refactoring 

**Success Criteria:**
- Single, unified API for all filter types
- Consistent method signatures across filter categories
- Easy discoverability (TypeScript autocomplete, docs)
- Backward compatibility with existing Layer/Variant APIs

### Secondary Persona: End Users (Engineers)

**Who:** Engineers, technical sales, QA using web apps built on webvis.js

**Background:**
- Review CAD assemblies in browser (no NX license needed)
- Need to declutter complex assemblies (100s-1000s of parts)
- Switch between views (detailed vs. simplified)

**Jobs to be Done:**
1. Load assemblies quickly (filter unnecessary geometry upfront)
2. Toggle between different visibility states (e.g., "Solid" vs "Entire Part")
3. Focus on relevant geometry for specific tasks (manufacturing, inspection, sales)

**Pain Points:**
- Visual clutter (sketches, datums, construction geometry visible)
- Long load times (entire part loaded even when only solid geometry needed)
- Cannot switch Reference Sets → stuck with default view

**Success Criteria:**
- Load times reduced (only relevant geometry loaded)
- Simple UI controls to switch filters (dropdown in tree)
- Deterministic visibility (exactly one Reference Set active per node)

---

## 3. Solution Overview

### Introducing CAD Switches

**CAD Switches** is a unified, extensible Filter API that abstracts all CAD filtering concepts (Layers, Variants, Reference Sets, future types) into a single data-driven interface.

**Core Principles:**

1. **Unified Interface:** Single API (`FilterAPI`) for all filter types
2. **Category-Based:** Filter types distinguished by `FilterCategory` enum
3. **Data-Driven:** Filter behavior defined by properties (not hardcoded logic) -> unclear whats meant
4. **Extensible:** Add new filter types without modifying components
5. **Format-Agnostic:** Loaders translate format-specific filters to unified representation

**Key Capabilities:**

- **Query Filters:** List all registered filters, filter by category, check enabled state
- **Toggle Filters:** Enable/disable filters globally or per-node
- **Check Membership:** Determine if a node belongs to an enabled filter
- **Category Support:** Layers (global), Variants (per-node), Reference Sets (per-node, exclusive)

**Architecture Highlight:**

```
CAD File (NX/JT/PLMXML)
    ↓
Loader (format-specific) → Translates to FilterProperties
    ↓
l3dCache (unified filter data)
    ↓
webvis FilterAPI (unified interface)
    ↓
Renderer (filter-aware rendering)
```

Differentiation happens **only at the edges** (loader & UI). All intermediate components (cache, API, renderer) work with unified filter data. -> questionable

---

## 4. Requirements

### 4.1 Must-Have (Phase 1 - VC1)

**VC1 Scope: PLMXML + JT Filter Implementation (Layers + Reference Sets)**

#### End-User Requirements

| ID | Requirement | Rationale |
|----|-------------|-----------|
| **EU-0** | Reference Set can be globally set over all nodes | Bulk operations for large assemblies |
| **EU-1** | On initial load, WebVis must load the NX-authored default Reference Set for every part instance | Prevents clutter, matches CAD author intent |
| **EU-2** | Viewer must display exactly one Reference Set per node at any time (exclusivity) | Deterministic state, mirrors NX behavior |
| **EU-3** | User can switch the active Reference Set for an individual node via UI control (e.g. dropdown in tree) | Allows alternate views (Entire Part ↔ Solid) |

#### Web Developer Requirements (API)

| ID | Requirement | Rationale |
|----|-------------|-----------|
| **WD-1** | Endpoint to list available filters for any node | Populate custom UIs, avoid invalid names |
| **WD-2** | Endpoint to query currently active filters per node | Keep external UIs in sync |
| **WD-3** | Endpoint to set/replace active filter per node (exclusive toggle for Reference Sets) | Enable UI actions, automation scripts |
| **WD-4** | All changes are session-local (ephemeral); no persistence after reload | Experimantal scope (persistence = later phase) |

#### Technical Requirements

- **Format Support:** PLMXML and JT files (NX support in future VC)
- **Filter Categories:** LayerFilter, ReferenceSet (Variants deferred to VC2)
- **Backward Compatibility:** NOT required for new API (legacy APIs untouched in frontend, adjusted in backend)
- **Components Affected:** l3dGen, webvis, hare, GeometricService

### 4.2 API Specification

```typescript
interface FilterAPI {
  /**
   * Returns all registered filters and their enabled states.
   */
  requestRegisteredFilters(): Promise<FilterProperties[]>;

  /**
   * Returns currently enabled filters.
   */
  requestEnabledFilters(): Promise<FilterProperties[]>;

  /**
   * Returns all filters for a specific category.
   */
  requestFiltersForCategory(filterCategory: FilterCategory): Promise<FilterProperties[]>;

  /**
   * Checks if a node is part of any enabled filter.
   * @param nodeId - The node ID to check
   * @param filterCategory - Optional: filter by category
   */
  isNodePartOfEnabledFilters(nodeId: number, filterCategory?: FilterCategory): Promise<boolean>;

  /**
   * Sets a filter's enabled state.
   *
   * **Category-Dependent Behavior:**
   *
   * The behavior of this method depends on the FilterCategory of the filter being enabled:
   *
   * - **LAYER_FILTER (Toggling):**
   *   - Multi-select behavior: Multiple layers can be enabled simultaneously
   *   - Enabling a layer does NOT disable other layers
   *   - `nodeId` parameter is ignored (layers are always global)
   *   - Example: Enable both "Layer 1" and "Layer 2" → both are active
   *
   * - **REFERENCE_SET (Switching):**
   *   - Exclusive behavior: Only ONE reference set can be active per node
   *   - Enabling a reference set automatically disables all other reference sets for that node
   *   - `nodeId` parameter is required for per-node control
   *   - Without `nodeId`: applies to all nodes globally (bulk operation)
   *   - Example: Enable "Solid" → automatically disables "Entire Part" for that node
   *
   * - **VARIANT (Toggling - VC2):**
   *   - Multi-select behavior per node: Multiple variants can be enabled for the same node
   *   - `nodeId` parameter required for per-node control
   *   - Deferred to VC2
   *
   * **Usage Examples:**
   *
   * ```typescript
   * // Example 1: Toggle layers (multi-select, global)
   * api.setFilterEnabled(layer1Id, true);   // Enable Layer 1
   * api.setFilterEnabled(layer2Id, true);   // Enable Layer 2 (Layer 1 stays enabled)
   * api.setFilterEnabled(layer1Id, false);  // Disable Layer 1 (Layer 2 stays enabled)
   *
   * // Example 2: Switch reference sets (exclusive, per-node)
   * api.setFilterEnabled(solidRefSetId, true, node123);       // Switch to "Solid" for node 123
   * api.setFilterEnabled(entirePartRefSetId, true, node123);  // Switch to "Entire Part" for node 123
   *                                                            // → "Solid" is automatically disabled
   *
   * // Example 3: Switch reference set globally (all nodes)
   * api.setFilterEnabled(solidRefSetId, true);  // All nodes switch to "Solid"
   * ```
   *
   * **State Update Timing:**
   * - State is updated synchronously (immediately)
   * - Renderer updates visibility on next frame
   *
   * @param id - The filter ID to enable/disable
   * @param enabled - New enabled state (true = enabled, false = disabled)
   * @param nodeId - Optional: The node to apply the filter to
   *                 - Required for REFERENCE_SET per-node operations
   *                 - Ignored for LAYER_FILTER (always global)
   *                 - Omit to apply globally (bulk operation for reference sets)
   */
  setFilterEnabled(id: number, enabled: boolean, nodeId?: number): void;
}

interface FilterProperties {
  id: number;
  name: string;
  enabled: boolean;
  filterCategory: FilterCategory;
}

enum FilterCategory {
  LAYER_FILTER,   // Global, multi-toggle
  VARIANT,        // Per-node, multi-toggle (VC2)
  REFERENCE_SET   // Per-node, exclusive toggle
}
```

**Key Design Decisions:**

- **Promise-based:** Async operations for node checks (may require cache lookups)
- **Optional nodeId:** Global filters (Layers) ignore nodeId; per-node filters (Reference Sets) require it
- **Category-Dependent Behavior:** `setFilterEnabled()` behavior is determined by FilterCategory:
  - **LAYER_FILTER:** Toggling behavior (multi-select, multiple layers can be enabled)
  - **REFERENCE_SET:** Switching behavior (exclusive, enabling one disables others for the same node)
  - **VARIANT:** Toggling behavior per node (multi-select, deferred to VC2)
- **Synchronous State Updates:** Filter state changes are applied immediately; renderer updates on next frame

### 4.3 Out of Scope (Phase 1)

- **NX Native Files:** Deferred to VC2 (PLMXML + JT only in VC1)
- **Variants Integration:** Deferred to VC2 (LayerFilter + ReferenceSet only in VC1)
- **Persistence:** Session-local only (save/restore filter state = future phase)
- **Advanced UI:** Basic dropdown in tree only (advanced filter panels = future)
- **Query API Integration:** Separate concerns (filtering vs. querying)
- **Arrangements (NX concept):** Complex assembly-level feature (low priority)

---

## 5. Success Metrics & Validation

### Primary Metrics

**Feature Adoption Rate:**
- Track API usage via analytics: `FilterAPI.requestRegisteredFilters()`, `setFilterEnabled()` calls
- Target: **50% of new projects** using CAD Switches API within 6 months of 3.13.0 release
- Baseline: Current LayerFilterAPI + VariantsAPI usage

**Migration Rate:**
- Track legacy API deprecation: % of projects migrating from `LayerFilterAPI`/`VariantsAPI` to `FilterAPI`
- Target: **25% migration** of existing projects within 12 months (optional, not enforced)

### Customer Validation

**Grob:**
- ✅ Can load NX assemblies with default Reference Sets (EU-1)
- ✅ Can switch Reference Sets per part (EU-3)
- ✅ Visual clutter reduced (only "Solid" geometry shown by default)

**Daimler Truck:**
- ✅ Can load JT files with `FLATPATTERN_OBJECTS` Reference Set
- ✅ Manufacturing engineers can toggle to flat pattern sketches
- ✅ No more "merged Reference Sets + Layers" workaround needed

**Mercedes-Benz:**
- ✅ Validate compatibility with MB's JT exports (Reference Sets as layers)

### Qualitative Metrics

- **Developer Feedback:** Survey webvis.js developers on API clarity, ease of use
- **Support Tickets:** Reduction in filter-related questions/issues
- **Component Maintenance:** Time to add new filter type (target: <1 sprint)

---

## 6. Technical Architecture (High-Level)

### Affected Components

| Component | Impact | Changes Required |
|-----------|--------|------------------|
| **l3dGen (Transcoding)** | High | Parse Reference Sets from PLMXML/JT, map to FilterProperties, store in cache |
| **l3dCache** | High | New unified filter data structure (filter ID, category, node mapping) |
| **webvis** | Medium | New FilterAPI interface, update UI to use FilterAPI, keep legacy APIs (facade to FilterAPI) |
| **Renderer** | Medium | Filter-aware rendering (respect enabled filters per node) |
| **GeometricService** | Low | Capping respects filter state |
| **sharedSession** | TBD | Sync filter state across users (future phase) |

### Data Flow

1. **Load Time:**
   - Loader (Datakit/JtTk) extracts Reference Sets from PLMXML/JT
   - l3dGen transcodes to unified FilterProperties (id, name, category, node mapping)
   - Cache stores filter metadata + node membership

2. **Runtime:**
   - WebVis requests filters via `FilterAPI.requestFiltersForCategory(REFERENCE_SET)`
   - UI displays dropdown per node with available Reference Sets
   - User selects Reference Set → `setFilterEnabled(id, true, nodeId)` called
   - Renderer updates visibility based on enabled filters

3. **Rendering:**
   - Renderer checks `isNodePartOfEnabledFilters(nodeId, REFERENCE_SET)`
   - Culls nodes not part of enabled Reference Set
   - Intersects with Layer filters (both must be true for visibility)

### Filter Interaction Rules

**Between Categories (AND logic):**
- Node is visible if: `enabledInLayers AND enabledInReferenceSet`
- Example: Layer "1" enabled + ReferenceSet "Solid" enabled → only nodes in both are visible

**Within Reference Set Category (XOR logic):**
- Only one Reference Set per node can be enabled
- Enabling "Entire Part" automatically disables "Solid" for that node

---

## 7. Open Questions & Decisions

### 🔴 Critical: Naming

**Question:** What should we name this feature?

**What the API Actually Does (Current + Future Scope):**

**Phase 1 (3.13.0):**
- Controls visibility/inclusion of geometry (show/hide based on CAD metadata)
- Based on CAD-native concepts: layers, reference sets, variants
- Per-node or global toggling

**Future Phases:**
- ✅ **Color overwrites** (change part colors)
- ✅ **Position overwrites** (adjust part transformations)
- ❌ Does NOT include: camera positions, sectioning, render settings

**Key Constraint:**
- Must avoid "Configuration Management" terminology (established CAD domain with dedicated vendors)
- We're NOT building full configuration management tooling
- Need a name that doesn't overpromise or create market confusion

---

**Options Evaluated (with Future Scope: Visibility + Color/Position Overwrites):**

| Name | Definition | Covers Current + Future? | Market Risk? | Verdict |
|------|-----------|-------------------------|--------------|---------|
| **CAD Switches** | Activates alternative model configurations, such as arrangements, variants, or expression-driven states. Switching changes which configuration is currently active. | ✅ Yes — "switch" naturally covers: switch visibility, switch colors, switch positions | ✅ Safe — no confusion with Config Mgmt vendors | **RECOMMENDED** |
| **CAD States** | Captures a temporary or persistent model condition from applied configurations, switches, or overlays. States represent assembly arrangements, positional alternatives, or logical subsets. | ✅ Yes — "state" includes visibility, appearance, position | ✅ Safe — generic term | **Strong Alternative** |
| **CAD Profiles** | A saved model state that combines visibility rules, configuration logic, and optional overrides. | ✅ Yes — includes overwrites | ⚠️ Minor risk — might sound like "config management lite" | Acceptable |
| **CAD Overwrites** | Apply modifications to the model's appearance or position, such as color changes, transformation adjustments, or other attribute overrides. | ⚠️ Partial — covers future (overwrites) but doesn't capture current scope (filtering is more than overwriting) | ✅ Safe | Not ideal |
| **CAD Schemes** | Defines rules to interpret a model, combining filters, configurations, and overwrites into unified logic. | ✅ Yes — covers broad scope | ⚠️ Minor risk — implies predefined logic (less flexible than individual control) | Acceptable |
| **CAD Configurations** | Represents a defined combination of product options, variants, or expressions that control the structure and content of the model. | ✅ Yes — conceptually perfect for full scope | ❌ **HIGH RISK** — CAD Config Mgmt = huge established domain (Siemens, PTC, etc.). Overpromises, creates market confusion. You're not experts here. | **Not Recommended** |
| **CAD Filters** | Controls which parts of the model are included or hidden, based on CAD-native concepts such as layers, reference sets, construction geometry. | ❌ No — too narrow. Doesn't cover future color/position overwrites. | ✅ Safe | **Not Recommended** (scope mismatch) |
| **CAD Contexts/Views/Layers/Variants** | Various specific concepts | ❌ Too specific or out of scope | N/A | Not recommended |
| **CAD Overlays/Flavours** | Add information (Overlays) or predefined presets (Flavours) | ❌ Wrong concept or too high-level | N/A | Not recommended |

---

**Recommended Name: CAD Switches** ✅

**Why This Wins:**

1. **Covers Full Scope:** "Switch" naturally extends to:
   - Switch visibility (layers, reference sets, variants) ✅ Current
   - Switch colors (part appearance overwrites) ✅ Future
   - Switch positions (transformation adjustments) ✅ Future

2. **Market-Safe:** Zero confusion with "CAD Configuration Management" (Siemens Teamcenter, PTC Windchill, etc.)
   - You're not competing with established vendors
   - Not overpromising expertise you don't claim

3. **Developer-Friendly:**
   - Intuitive: "Switch the reference set", "Switch the color"
   - Action-oriented verb (better than abstract nouns)
   - Already the working title (team familiarity)

4. **Extensible:** Naturally accommodates future concepts without renaming
   - "Switch the filter category" (current)
   - "Switch the appearance" (future)
   - "Switch the arrangement" (future)

5. **CAD-Native Terminology:** "Switch" used in NX/Siemens context (switching reference sets, arrangements)

**Strong Alternative: CAD States**
- **Pros:** Generic, covers all aspects (visibility + appearance + position), safe
- **Cons:** Less action-oriented, more abstract ("set a state" vs. "switch")
- **Use Case:** If "Switches" feels too verb-like for an API, "States" works well

**Why NOT "CAD Configurations":**
- ✅ Conceptually perfect (covers everything)
- ❌ **Fatal flaw:** CAD Configuration Management = massive established market
- ❌ Risk: Users expect Windchill/Teamcenter-level features (variant management, BOM control, change tracking)
- ❌ You're "scratching the surface" — don't want to compete or confuse

**Next Steps:**
1. ✅ **Finalize decision:** "CAD Switches" (recommended) vs. "CAD States" (alternative)?
2. Update API naming: `FilterAPI` → `CADSwitchesAPI` (or `CADStatesAPI`)
3. Update documentation, code comments, UI labels consistently
4. Announce to web developers before 3.13.0 beta
5. Validate naming with 3-5 web developers (quick feedback loop)

**Decision Owner:** Hannes Krug (Senior PM)
**Deadline:** End of Sprint 1 (before API freeze)
**Status:** Recommendation provided, awaiting final approval

**Fallback Plan:**
- If "Switches" and "States" both feel wrong, revisit "CAD Profiles" or "CAD Schemes"
- Avoid "CAD Configurations" due to market risk

---

## 8. Implementation Roadmap

### Value Slice 1 (VC1): PLMXML + JT Implementation
**Target:** 3.13.0 (Q1 2026)

**Scope:**
- Loader support: PLMXML + JT files
- Filter categories: LayerFilter + ReferenceSet
- API: Full FilterAPI implementation
- UI: Basic dropdown in tree
- Testing: Grob (PLMXML), Daimler Truck (JT), Mercedes-Benz (JT) datasets

**Success Criteria:**
- Grob can load NX assemblies via PLMXML with Reference Sets
- DT can load JT files with `FLATPATTERN_OBJECTS` Reference Set
- API adoption: 10+ internal projects using FilterAPI

### Future Value Slices (Post-3.13.0)

**VC2: NX Native + Variants Integration**
- NX Native file support (Datakit loader)
- Variants mapped to FilterCategory.VARIANT
- Advanced per-node toggling UI

**VC3: Persistence & Advanced UI**
- Save/restore filter states across sessions
- Filter presets (e.g., "Manufacturing View", "Sales View")
- Advanced filter panels (multi-select, search)

**VC4: Arrangements & Advanced Concepts**
- NX Arrangements support (assembly-level load optimization)
- PMI/ModelView integration (if needed)

---

## 9. Appendix

### Related Links

- **User Research:** [Reference Sets Research](https://i3dhub.atlassian.net/wiki/spaces/RD/pages/4432461890/)
- **Technical Concept:** [Filter API Technical Concept](https://i3dhub.atlassian.net/wiki/spaces/RD/pages/4478074881/)
- **Existing APIs:**
  - [LayerFilterAPI Docs](https://docs.threedy.io/3.12.0/doc/webvis/interfaces/LayerFilterAPI.html)
  - [VariantsAPI Docs](https://docs.threedy.io/3.12.0/doc/webvis/interfaces/VariantsAPI.html)

### Glossary

- **Reference Set:** Named subset of a CAD part defining which geometries/entities are visible
- **Layer Filter:** Global visibility control based on CAD layer metadata
- **Variant:** Product configuration state (e.g., "Red Interior", "Black Exterior")
- **Filter Category:** Enum distinguishing filter types (Layer, Variant, Reference Set)
- **Exclusive Toggle:** Only one option can be enabled at a time (XOR)

---

**Document History:**
- **v1.0 (2025-11-28):** Initial draft - Hannes Krug

---

*Generated with Claude Code - Product Toolkit*
