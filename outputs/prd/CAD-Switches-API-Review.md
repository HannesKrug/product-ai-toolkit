# CAD Switches API - Design Review & Validation
**API Specification Review & Scalability Analysis**

---

## Document Info

- **Related PRD:** [CAD-Switches-PRD.md](./CAD-Switches-PRD.md)
- **Review Date:** 2025-12-02
- **Last Updated:** 2025-12-02 (Resolved Gap 2 & State Update Timing)
- **Reviewers:** Hannes Krug (Senior PM), Frontend Dev Team
- **Status:** In Progress - 2 of 3 critical gaps resolved
- **Target Release:** 3.13.0 (Q1 2026)

---

## Purpose

This document provides a structured validation framework for the CAD Switches API specification (FilterAPI) to ensure:
1. Complete coverage of requirements from the PRD
2. Future-proof design that scales without breaking changes
3. Clear developer experience for web developers using webvis.js

---

## 1. Requirements Traceability Matrix

### Current API Coverage Analysis

| Requirement | API Method | Coverage Status | Gaps/Risks |
|------------|------------|-----------------|------------|
| **EU-0:** Global Reference Set setting | `setFilterEnabled(id, enabled)` (no nodeId) | ✅ Covered | ⚠️ Bulk operation efficiency unclear (1000+ nodes) |
| **EU-1:** Load NX default Reference Set | Backend/Loader concern | N/A | Need loader contract definition |
| **EU-2:** Exactly one Reference Set per node (exclusivity) | `setFilterEnabled()` with category-dependent behavior | ✅ Documented | ✅ **Resolved: Comprehensive JSDoc added explaining switching behavior for REFERENCE_SET** |
| **EU-3:** Switch Reference Set per node | `setFilterEnabled(id, enabled, nodeId)` | ✅ Covered | Clear |
| **WD-1:** List available filters per node | `requestFiltersForCategory()` | ⚠️ Partial | 🔴 **Missing: Per-node filter availability query** |
| **WD-2:** Query active filters per node | `requestEnabledFilters()` | ⚠️ Global only | 🔴 **Missing: Per-node active filter query** |
| **WD-3:** Set/replace active filter | `setFilterEnabled()` | ✅ Covered | Clear |
| **WD-4:** Session-local (ephemeral) | Not in API contract | N/A | Should document in API comments |

### Summary
- **2 Critical Gaps** remain (marked 🔴) - down from 3
- **2 Partial implementations** need clarification (marked ⚠️)
- **3 Requirements** fully covered (marked ✅) - **EU-2 resolved with comprehensive documentation**

---

## 2. Critical API Gaps

### Gap 1: Per-Node Filter Queries Missing 🔴

**Problem:**
`requestFiltersForCategory()` returns global filters, but Reference Sets are per-node. Developers cannot determine which Reference Sets are available for a specific node.

**Developer Pain Point:**
```typescript
// Scenario: Build dropdown of Reference Sets for node 123
const filters = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);
// ^ Returns ALL Reference Sets globally
// But which ones actually apply to node 123?
// Different parts may have different Reference Sets available!
```

**Suggested Solution:**
```typescript
/**
 * Returns filters applicable to a specific node.
 * For Reference Sets, returns only those available for the node's part.
 * @param nodeId - The node to query
 * @param filterCategory - Optional: filter by category
 */
requestFiltersForNode(
  nodeId: number,
  filterCategory?: FilterCategory
): Promise<FilterProperties[]>;

/**
 * Returns the currently active filter for a node (for exclusive categories like REFERENCE_SET).
 * @param nodeId - The node to query
 * @param filterCategory - The category to query (must be exclusive toggle type)
 * @returns The active filter, or null if none active
 */
requestActiveFilterForNode(
  nodeId: number,
  filterCategory: FilterCategory
): Promise<FilterProperties | null>;
```

**Impact if not addressed:**
- Developers build incorrect UIs (showing inapplicable Reference Sets)
- Need workarounds to filter results manually
- Poor developer experience

---

### Gap 2: Exclusivity Behavior Not Explicit ✅ RESOLVED

**STATUS: RESOLVED (2025-12-02)**

The PRD has been updated with comprehensive documentation explaining category-dependent behavior:
- LAYER_FILTER = Toggling (multi-select)
- REFERENCE_SET = Switching (exclusive)
- Includes detailed JSDoc comments with code examples
- See PRD Section 4.2 (lines 238-316)

**Original Problem:**
From PRD line 265: _"Exclusive toggle enforced... -> not entirely clear, needs refinement from Tim G"_

The original API signature didn't communicate exclusivity:
```typescript
setFilterEnabled(id: number, enabled: boolean, nodeId?: number): void;
```

**Unclear Behaviors:**
1. When I call `setFilterEnabled(refSetA, true, node123)`, does it auto-disable refSetB?
2. What if I explicitly call `setFilterEnabled(refSetB, false)`? Is that allowed?
3. How do I know if I'm "toggling" (multi-select) vs "switching" (exclusive)?
4. Does behavior differ by FilterCategory? (Layers = multi-toggle, Reference Sets = exclusive)

**Developer Confusion Scenario:**
```typescript
// Developer wants to switch from "Solid" to "Entire Part"
// Current API - unclear intent:
api.setFilterEnabled(solidId, false, node1);        // Do I need this?
api.setFilterEnabled(entirePartId, true, node1);   // Or just this?

// vs. explicit switch method:
api.switchFilter(entirePartId, node1); // Clear intent!
```

**Suggested Solutions (3 options):**

**Option A: Add Explicit Switch Method** (Recommended)
```typescript
/**
 * Switches to a different filter for exclusive categories (e.g., REFERENCE_SET).
 * Automatically disables other filters in the same category for the node.
 * @param id - The filter to switch to
 * @param nodeId - Optional: the node to apply to (required for per-node categories)
 */
switchFilter(id: number, nodeId?: number): void;

// Keep setFilterEnabled for multi-toggle categories (Layers)
setFilterEnabled(id: number, enabled: boolean, nodeId?: number): void;
```

**Option B: Document Behavior Clearly**
```typescript
/**
 * Sets a filter's enabled state.
 *
 * **Category-Specific Behavior:**
 * - LAYER_FILTER: Multi-toggle (multiple layers can be enabled)
 * - REFERENCE_SET: Exclusive toggle (enabling one auto-disables others on same node)
 * - VARIANT: Multi-toggle per node (VC2)
 *
 * @param id - The filter ID
 * @param enabled - New enabled state
 * @param nodeId - Optional: apply per-node (ignored for global filters like Layers)
 */
setFilterEnabled(id: number, enabled: boolean, nodeId?: number): void;
```

**Option C: Separate Methods Per Category**
```typescript
// Different methods make behavior explicit
setLayerEnabled(id: number, enabled: boolean): void;              // Multi-toggle, global
switchReferenceSet(id: number, nodeId: number): void;            // Exclusive, per-node
toggleVariant(id: number, nodeId: number, enabled: boolean): void; // Multi-toggle, per-node
```

**Original Recommendation:** **Option A** (add `switchFilter()` alongside `setFilterEnabled()`).

**RESOLUTION IMPLEMENTED: Option B** (Document behavior clearly)

The team decided to use **Option B** - keeping the single `setFilterEnabled()` method but with comprehensive documentation that explains the category-dependent behavior. The updated API includes:

```typescript
/**
 * Sets a filter's enabled state.
 *
 * **Category-Dependent Behavior:**
 * - LAYER_FILTER (Toggling): Multi-select behavior, multiple layers can be enabled
 * - REFERENCE_SET (Switching): Exclusive behavior, enabling one disables others
 * - VARIANT (Toggling - VC2): Multi-select per node
 *
 * **Usage Examples:**
 * // Layers: Multi-select
 * api.setFilterEnabled(layer1Id, true);   // Enable Layer 1
 * api.setFilterEnabled(layer2Id, true);   // Layer 1 stays enabled
 *
 * // Reference Sets: Exclusive switching
 * api.setFilterEnabled(solidRefSetId, true, node123);
 * api.setFilterEnabled(entirePartRefSetId, true, node123);  // Solid auto-disabled
 *
 * **State Update Timing:**
 * - State updates synchronously (immediately)
 * - Renderer updates on next frame
 */
setFilterEnabled(id: number, enabled: boolean, nodeId?: number): void;
```

**Benefits of this approach:**
- ✅ Single, consistent API method (simpler for developers)
- ✅ Behavior is clearly documented with examples
- ✅ No API fragmentation (vs Option C)
- ✅ Implementation handles complexity (not developer)

**Note:** If developer feedback indicates confusion persists, Option A (`switchFilter()`) can be added later without breaking changes.

---

### Gap 3: Bulk Operations 🟡

**Problem:**
EU-0 requires "Reference Set can be globally set over all nodes", but current API requires per-node calls.

**Performance Concern:**
```typescript
// Setting "Solid" Reference Set for 1000 nodes:
for (const nodeId of nodeIds) {
  api.setFilterEnabled(solidId, true, nodeId);
}
// Issues:
// - 1000 individual API calls
// - No atomicity (what if 500th call fails?)
// - Potential sync issues with renderer
// - Poor performance
```

**Suggested Solution:**
```typescript
/**
 * Sets a filter for multiple nodes atomically.
 * @param id - The filter ID
 * @param enabled - New enabled state
 * @param nodeIds - Array of nodes to apply to
 */
setFilterEnabledBatch(
  id: number,
  enabled: boolean,
  nodeIds: number[]
): void;

/**
 * Sets a filter for ALL nodes in the scene (convenience for EU-0).
 * @param id - The filter ID
 * @param enabled - New enabled state
 * @param filterCategory - The category to apply to (ensures correct scope)
 */
setFilterForAllNodes(
  id: number,
  enabled: boolean,
  filterCategory: FilterCategory
): void;
```

**Alternative:** Document that `setFilterEnabled()` without `nodeId` applies globally.
Need backend team confirmation on feasibility.

---

## 3. Future-Proofing Analysis

### Planned Future Features (from PRD Section 7)

| Future Feature | Current API Support | Scalability Risk | Recommended Action |
|----------------|---------------------|------------------|-------------------|
| **Color overwrites** (VC3+) | ❌ `FilterProperties` has no color field | 🔴 **Would require breaking change** | Add extensible properties now |
| **Position overwrites** (VC3+) | ❌ `FilterProperties` has no transform field | 🔴 **Would require breaking change** | Add extensible properties now |
| **Variants** (VC2) | ✅ `FilterCategory.VARIANT` exists | ✅ Supported | No action needed |
| **NX Arrangements** (VC4) | ⚠️ Would need new `FilterCategory` | ✅ Enum extensible | No action needed |
| **Filter persistence** (VC3) | ❌ No save/load methods | 🟡 Would need separate API | Plan persistence API separately |
| **Filter presets** (VC3) | ❌ No preset concept | 🟡 Would need new structure | Plan preset API separately |
| **Multi-node batch queries** | ❌ Only single-node `isNodePartOfEnabledFilters()` | 🟡 Performance issue for large scenes | Add batch query methods |

### Critical Issue: FilterProperties Not Extensible

**Current Definition (PRD Section 4.2):**
```typescript
interface FilterProperties {
  id: number;
  name: string;
  enabled: boolean;
  filterCategory: FilterCategory;
}
```

**Problem:**
No way to add color/position/transform data without breaking changes. Future requirements (color/position overwrites) would require:
1. Adding new fields → breaks existing consumers
2. Creating separate API → loses unified interface promise
3. Using parallel data structures → complexity, sync issues

**Recommended Solution: Make Extensible Now**

```typescript
interface FilterProperties {
  id: number;
  name: string;
  enabled: boolean;
  filterCategory: FilterCategory;

  // Option 1: Generic property bag (most flexible)
  properties?: Record<string, unknown>;

  // Option 2: Structured metadata (more type-safe)
  metadata?: {
    isDefault?: boolean;        // For EU-1 (default Reference Set indicator)
    color?: string;              // Future: color overwrites
    transform?: Transform;       // Future: position overwrites
    description?: string;        // Future: tooltips/help text
    thumbnailUrl?: string;       // Future: visual previews
    // Extend as needed without breaking changes
  };
}
```

**Recommendation:** Use **Option 2** (structured metadata).
- More type-safe than generic bag
- Still extensible (add new optional fields)
- Better developer experience (autocomplete, docs)
- Can validate known fields while allowing unknowns

---

## 4. Validation Exercises

### Exercise A: Implement Requirements with Current API

**Test:** Can each requirement be implemented cleanly?

```typescript
// EU-3: Switch Reference Set for individual node
async function switchReferenceSetForNode(
  api: FilterAPI,
  nodeId: number,
  refSetName: string
) {
  const refSets = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);
  const targetRefSet = refSets.find(rs => rs.name === refSetName);

  // ⚠️ Issue 1: How do I know if this refSet applies to this node?
  //            (Gap 1 - missing per-node query)

  // ⚠️ Issue 2: Do I need to manually disable other refSets first?
  //            (Gap 2 - exclusivity unclear)

  api.setFilterEnabled(targetRefSet.id, true, nodeId);
}

// WD-1: List available Reference Sets for a node
async function getAvailableReferenceSetsForNode(
  api: FilterAPI,
  nodeId: number
): Promise<FilterProperties[]> {
  const allRefSets = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);

  // ⚠️ Issue: No way to filter by node applicability!
  //           Must return all, even if irrelevant to this node.
  //           (Gap 1 - missing per-node query)

  return allRefSets; // Incorrect result!
}

// WD-2: Get currently active Reference Set for a node
async function getActiveReferenceSet(
  api: FilterAPI,
  nodeId: number
): Promise<FilterProperties | null> {
  const enabledFilters = await api.requestEnabledFilters();
  const refSets = enabledFilters.filter(f => f.filterCategory === FilterCategory.REFERENCE_SET);

  // ⚠️ Issue: This returns ALL enabled Reference Sets globally.
  //           How do I know which one applies to THIS node?
  //           (Gap 1 - missing per-node query)

  // Hack: Check each one manually?
  for (const refSet of refSets) {
    const isApplicable = await api.isNodePartOfEnabledFilters(nodeId, FilterCategory.REFERENCE_SET);
    if (isApplicable) {
      return refSet; // But which one if multiple enabled? Unclear!
    }
  }

  return null;
}
```

**Result:** All 3 requirements struggle with current API → validates gaps identified.

---

### Exercise B: Edge Case Testing

Document expected behavior for edge cases:

| Edge Case | Expected Behavior | Currently Defined? |
|-----------|-------------------|-------------------|
| Enable same Reference Set twice | Should be idempotent (no-op on second call) | ❌ Not specified |
| Enable Layer filter with nodeId | Should ignore nodeId (Layers are global) | ❌ Not specified |
| Enable Reference Set without nodeId | Should apply to all nodes? Or error? | ❌ Not specified (relates to EU-0) |
| Node has no Reference Sets | `requestFiltersForNode()` returns empty array? | ❌ Method doesn't exist (Gap 1) |
| Disable all Reference Sets for a node | Should renderer hide the node? Or show default? | ❌ Not specified (relates to EU-1) |
| Call `setFilterEnabled()` during async operation | What's the state update timing? Event-driven? | ❌ Not specified (sync/async unclear) |

**Recommendation:** Document edge cases explicitly in API specification.

---

### Exercise C: Future Feature Mockup

**Test:** Can we implement "Color Overwrites" (PRD Section 7) without breaking changes?

**Current API (WITHOUT extensible properties):**
```typescript
// ❌ Cannot extend FilterProperties without breaking change
interface ColoredFilterProperties extends FilterProperties {
  color: string; // ❌ Not possible - existing code expects base interface
}

// Would need to:
// 1. Create separate ColorAPI (loses unified interface promise)
// 2. Use parallel data structure (complexity, sync issues)
// 3. Break existing consumers (unacceptable)
```

**With Extensible Properties (PROPOSED):**
```typescript
// ✅ Can add color without breaking changes
interface FilterProperties {
  id: number;
  name: string;
  enabled: boolean;
  filterCategory: FilterCategory;
  metadata?: {
    color?: string; // ✅ Added in VC3, optional, no breakage
    // ...
  };
}

// Existing code ignores unknown fields (no breakage)
// New code can access color:
const filter = await api.requestFiltersForNode(nodeId, FilterCategory.VARIANT);
if (filter.metadata?.color) {
  // Apply color overwrite
}
```

**Result:** Extensible properties design PASSES future-proofing test.

---

## 5. Additional Concerns from PRD

### Unresolved TODOs from PRD

The PRD itself flags these concerns:

| PRD Line | Concern | Status |
|----------|---------|--------|
| **Line 152** | "Data-Driven: Filter behavior defined by properties (not hardcoded logic) -> unclear whats meant" | ❓ **Needs clarification from Tim G** |
| **Line 177** | "Differentiation happens only at the edges (loader & UI). All intermediate components work with unified filter data. -> questionable" | ❓ **Needs architecture validation** |
| **Line 265** | "Exclusive Toggle: setFilterEnabled() enforces Reference Set exclusivity -> not entirely clear, needs refinement from Tim G" | 🔴 **Covered in Gap 2 above** |

**Recommendation:** Resolve these before API freeze. Schedule sync with Tim G.

---

### Async vs. Sync Confusion

**Observation:**
```typescript
// Query methods are async (Promise-based):
requestRegisteredFilters(): Promise<FilterProperties[]>
isNodePartOfEnabledFilters(nodeId: number): Promise<boolean>

// But mutation is synchronous (void):
setFilterEnabled(id: number, enabled: boolean, nodeId?: number): void
```

**Questions:**
1. When does the state update actually apply? Immediately? Next frame?
2. If I call `setFilterEnabled()` then immediately `requestEnabledFilters()`, is the change reflected?
3. Should there be events/callbacks for state changes?
4. How does UI stay in sync?

**Suggested Documentation:**
```typescript
/**
 * Sets a filter's enabled state.
 *
 * **State Update Timing:**
 * - State is updated synchronously (immediately)
 * - Renderer updates on next frame
 * - Subscribe to [TBD event] for change notifications
 *
 * **Thread Safety:**
 * - Safe to call from any thread
 * - Multiple calls batched automatically (TBD)
 */
setFilterEnabled(id: number, enabled: boolean, nodeId?: number): void;
```

**Alternative:** Make mutation async too for consistency:
```typescript
setFilterEnabled(id: number, enabled: boolean, nodeId?: number): Promise<void>;
```

---

## 6. Recommended Action Plan

### Phase 1: API Refinement (Week 1)

**Priority Tasks:**

1. **Add Missing Methods** (Gap 1)
   - [ ] `requestFiltersForNode(nodeId, filterCategory?)`
   - [ ] `requestActiveFilterForNode(nodeId, filterCategory)`
   - [ ] Update TypeScript definitions

2. **Clarify Exclusivity** (Gap 2)
   - [ ] Sync with Tim G on exclusive toggle behavior
   - [ ] Choose approach: Option A (add switchFilter), B (document), or C (separate methods)
   - [ ] Update API specification

3. **Make FilterProperties Extensible** (Future-proofing)
   - [ ] Add `metadata?: { ... }` field to `FilterProperties`
   - [ ] Add `isDefault?: boolean` for EU-1 support
   - [ ] Document extensibility pattern for future features

4. **Address Bulk Operations** (Gap 3)
   - [ ] Add `setFilterEnabledBatch()` or
   - [ ] Clarify that `setFilterEnabled()` without nodeId = global
   - [ ] Confirm backend feasibility with rendering team

5. **Document Edge Cases**
   - [ ] Specify behavior for all edge cases from Exercise B
   - [ ] Add JSDoc comments with examples
   - [ ] Create "API Behavior Specification" document

**Deliverable:** Updated API specification (version 2.0)

---

### Phase 2: Validation (Week 2)

**Validation Tasks:**

1. **Write Example Code**
   - [ ] Create `examples/filter-api-examples.ts`
   - [ ] Implement each requirement (EU-0 through WD-4)
   - [ ] If any example is hard to write → API needs more work

2. **Create Integration Test Suite**
   ```typescript
   describe('FilterAPI Requirements', () => {
     describe('End-User Requirements', () => {
       it('EU-0: Sets Reference Set globally for all nodes');
       it('EU-1: Loads NX-authored default Reference Set');
       it('EU-2: Enforces Reference Set exclusivity per node');
       it('EU-3: Switches Reference Set for individual node');
     });

     describe('Web Developer Requirements', () => {
       it('WD-1: Lists available filters per node');
       it('WD-2: Queries currently active filters per node');
       it('WD-3: Sets/replaces active filter');
       it('WD-4: State is session-local (ephemeral)');
     });

     describe('Edge Cases', () => {
       it('Handles enabling same Reference Set twice (idempotent)');
       it('Ignores nodeId for global filters (Layers)');
       it('Returns empty array for nodes without Reference Sets');
       it('Maintains consistency during concurrent calls');
     });
   });
   ```

3. **Mock Future Features**
   - [ ] Implement "Color Overwrites" mock using extensible properties
   - [ ] Implement "Filter Presets" mock
   - [ ] Validate that changes don't break existing code

4. **Performance Testing**
   - [ ] Test bulk operations with 1000+ nodes
   - [ ] Measure query performance for large scenes
   - [ ] Identify bottlenecks

**Deliverable:** Test suite + performance report

---

### Phase 3: Stakeholder Review (Week 3)

**Review Sessions:**

1. **Web Developer Review** (2-3 developers)
   - [ ] Present updated API specification
   - [ ] Live coding session: build sample UI using API
   - [ ] Collect feedback on clarity, usability
   - [ ] Iterate based on feedback

2. **Backend Team Sync** (Tim G + rendering team)
   - [ ] Confirm loader contract (what data goes into FilterProperties?)
   - [ ] Validate bulk operations feasibility
   - [ ] Resolve PRD TODOs (lines 152, 177, 265)
   - [ ] Agree on state update timing (sync/async)

3. **UI Team Review** (webvis UI developers)
   - [ ] Validate that API supports planned UI (dropdown in tree)
   - [ ] Discuss event/callback mechanisms for UI sync
   - [ ] Identify any missing UI-facing methods

4. **PM Review** (Hannes Krug)
   - [ ] Verify all requirements (EU-0 through WD-4) covered
   - [ ] Confirm future-proofing for VC2+ features
   - [ ] Sign-off on API specification v2.0

**Deliverable:** Final API specification (version 2.0) with sign-offs

---

### Phase 4: Documentation (Week 4)

**Documentation Tasks:**

1. **API Reference Documentation**
   - [ ] Complete JSDoc comments for all methods
   - [ ] Add code examples for each method
   - [ ] Document edge case behaviors
   - [ ] Generate TypeDoc documentation

2. **Developer Guide**
   - [ ] "Getting Started with FilterAPI" tutorial
   - [ ] Common use cases (switch Reference Set, toggle layers, etc.)
   - [ ] Migration guide from LayerFilterAPI/VariantsAPI
   - [ ] Best practices

3. **Architecture Documentation**
   - [ ] Update PRD Section 6 (Technical Architecture)
   - [ ] Document loader contract (format-specific → FilterProperties)
   - [ ] Diagram data flow (load time, runtime, rendering)
   - [ ] Document filter interaction rules (AND/XOR logic)

**Deliverable:** Complete API documentation package

---

## 7. Open Questions for Discussion

### Critical Questions (Need Answers Before API Freeze)

1. ~~**Exclusivity Implementation** (Gap 2)~~ ✅ **RESOLVED**
   - ~~Should we add explicit `switchFilter()` method?~~
   - ~~OR: Keep `setFilterEnabled()` and document behavior clearly?~~
   - ~~OR: Separate methods per category (`switchReferenceSet()`, `setLayerEnabled()`)?~~
   - **Resolution:** Option B - Document behavior clearly with comprehensive JSDoc
   - **Decided:** 2025-12-02
   - **See:** Decision Log Section 9

2. **Global Reference Set Setting** (EU-0)
   - Does `setFilterEnabled(id, enabled)` without nodeId apply globally?
   - OR: Do we need explicit `setFilterForAllNodes()` method?
   - What's the performance impact (1000+ nodes)?
   - **Decision Maker:** Tim G + Rendering team
   - **Deadline:** End of Week 1

3. **Per-Node Queries** (Gap 1)
   - Should `requestFiltersForNode()` return only applicable filters?
   - OR: Return all filters with applicability metadata?
   - How is "applicability" determined? (Loader provides this?)
   - **Decision Maker:** Tim G + Backend team
   - **Deadline:** End of Week 1

4. ~~**State Update Timing** (Async/Sync)~~ ✅ **RESOLVED**
   - ~~Should `setFilterEnabled()` be synchronous (void) or async (Promise)?~~
   - ~~When does renderer see the update? Immediately? Next frame?~~
   - ~~Should there be change events/callbacks?~~
   - **Resolution:** Keep synchronous (void), state updates immediately, renderer updates next frame
   - **Decided:** 2025-12-02
   - **See:** Decision Log Section 9

### Non-Critical Questions (Can Defer)

5. **Default Reference Set Handling** (EU-1)
   - Should `FilterProperties.metadata.isDefault` be added now?
   - OR: Handle in loader/backend only?
   - **Decision Maker:** Tim G
   - **Deadline:** Before VC1 implementation

6. **Filter Categories Beyond Phase 1**
   - Should we define `FilterCategory.VARIANT` behavior now?
   - OR: Defer to VC2?
   - **Decision Maker:** Hannes Krug (PM)
   - **Deadline:** Before VC1 implementation

7. **Backward Compatibility**
   - Should we keep `LayerFilterAPI` / `VariantsAPI` as facades?
   - OR: Deprecate immediately?
   - What's the migration timeline?
   - **Decision Maker:** Hannes Krug (PM) + Customer Success
   - **Deadline:** Before 3.13.0 beta

---

## 8. Risk Summary

| Risk | Severity | Probability | Mitigation | Owner | Status |
|------|----------|-------------|------------|-------|--------|
| **Per-node queries missing** | 🔴 High | High | Add `requestFiltersForNode()` | Frontend Dev | 🟡 Open |
| ~~**Exclusivity logic unclear**~~ | ~~🔴 High~~ | ~~High~~ | ~~Sync with Tim G, add `switchFilter()`~~ | ~~Frontend Dev + Tim G~~ | ✅ **RESOLVED (2025-12-02)** |
| **FilterProperties not extensible** | 🟡 Medium | High | Add `metadata` field now | Frontend Dev | 🟡 Open |
| **No bulk operations** | 🟡 Medium | Medium | Add batch methods or clarify global behavior | Frontend + Rendering | 🟡 Open |
| **Edge cases undefined** | 🟡 Medium | High | Document all edge cases | Frontend Dev | 🟡 Open |
| **Performance (1000+ nodes)** | 🟡 Medium | Low | Test early, add batch methods if needed | Rendering team | 🟡 Open |
| ~~**State update timing unclear**~~ | ~~🟡 Medium~~ | ~~Medium~~ | ~~Document sync/async behavior~~ | ~~Rendering + Frontend~~ | ✅ **RESOLVED (2025-12-02)** |
| **PRD TODOs unresolved** | 🟡 Medium | Medium | Schedule sync with Tim G | Hannes Krug | ⚠️ Partially resolved (line 265 done) |

---

## 9. Decision Log

### Decisions to be Made

| Decision | Options | Recommended | Status | Owner |
|----------|---------|-------------|--------|-------|
| ~~Exclusivity API design~~ | ~~A) Add switchFilter()<br>B) Document only<br>C) Separate methods~~ | ~~**Option A**~~ | ✅ **DECIDED: Option B** (2025-12-02) | ~~Tim G + Frontend~~ |
| Per-node query methods | A) Add requestFiltersForNode()<br>B) Use existing with metadata | **Option A** | 🟡 Pending | Frontend Dev |
| FilterProperties extensibility | A) Add metadata field<br>B) Use generic properties bag<br>C) Don't extend yet | **Option A** | 🟡 Pending | Frontend Dev |
| Bulk operations | A) Add batch methods<br>B) Clarify global behavior<br>C) Both | **Option C** | 🟡 Pending | Frontend + Rendering |
| ~~State update timing~~ | ~~A) Keep void (sync)<br>B) Make Promise (async)~~ | ~~**Option A** + document~~ | ✅ **DECIDED: Option A** (2025-12-02) | ~~Rendering team~~ |

### Decisions Made

**Decision: Exclusivity API Design**
- **Date:** 2025-12-02
- **Decided by:** Hannes Krug (PM) + Frontend Dev
- **Chosen option:** Option B (Document behavior clearly)
- **Rationale:**
  - Single consistent API method is simpler for developers
  - Category-dependent behavior can be clearly explained in documentation
  - Avoids API fragmentation (vs separate methods per category)
  - Implementation handles switching logic, not developer
  - Can add explicit `switchFilter()` later if developer feedback indicates confusion
- **Action items:**
  - ✅ Updated PRD Section 4.2 with comprehensive JSDoc (lines 238-316)
  - ✅ Updated Key Design Decisions section
  - 🟡 Monitor developer feedback in VC1 beta
  - 🟡 Consider adding `switchFilter()` if confusion persists

**Decision: State Update Timing**
- **Date:** 2025-12-02
- **Decided by:** Frontend Dev Team
- **Chosen option:** Option A (Keep synchronous void return, document timing)
- **Rationale:**
  - Consistent with other state-changing methods in webvis.js
  - Simpler developer experience (no need to await)
  - State updates are immediate, renderer updates on next frame
  - Documented clearly in JSDoc comments
- **Action items:**
  - ✅ Documented in PRD Section 4.2
  - 🟡 Ensure backend implementation matches documented behavior
  - 🟡 Add event/callback system for state change notifications (future enhancement)

### Decision Template

When a decision is made, update this section:

```markdown
**Decision: [Topic]**
- **Date:** YYYY-MM-DD
- **Decided by:** [Names]
- **Chosen option:** [A/B/C]
- **Rationale:** [Why this option]
- **Action items:** [What needs to be done]
```

---

## 10. Next Steps

### Immediate Actions (This Week)

1. **Share this document** with team (Hannes, Tim G, Frontend team, Rendering team)
2. **Schedule sync meeting** (1-2 hours) to discuss critical gaps
3. **Assign owners** for each open question (Section 7)
4. **Create Jira tickets** for:
   - [ ] Add per-node query methods (Gap 1)
   - [ ] Define exclusivity behavior (Gap 2)
   - [ ] Add metadata field to FilterProperties
   - [ ] Document edge cases
   - [ ] Write example code
   - [ ] Create test suite template

### Follow-Up Meeting Agenda

**Attendees:** Hannes Krug (PM), Tim G (Backend/Rendering), Frontend Lead, Rendering Lead

**Agenda (90 min):**
1. Review critical gaps (15 min)
2. Discuss exclusivity approach - switchFilter() vs documented behavior (20 min)
3. Confirm per-node query design - data structure and performance (15 min)
4. Resolve PRD TODOs (lines 152, 177, 265) (15 min)
5. Decide on bulk operations approach (10 min)
6. Assign owners and deadlines (10 min)
7. Open discussion (5 min)

**Expected Outcome:** Decisions made for all 🔴 high-priority items.

---

## Document History

- **v1.0 (2025-12-02):** Initial API review - Hannes Krug (PM) + Frontend Dev
- **v1.1 (2025-12-02):** Updated to reflect resolved gaps:
  - ✅ Gap 2 (Exclusivity Behavior) - Resolved with comprehensive JSDoc documentation
  - ✅ State Update Timing - Documented as synchronous with next-frame rendering
  - Updated Requirements Traceability Matrix (EU-2 now covered)
  - Updated Risk Summary (2 risks resolved)
  - Updated Decision Log (2 decisions made)
  - Updated Open Questions (2 questions resolved)
- **Next review:** TBD (after team discussion on remaining gaps)

---

*Generated for CAD Switches API Design Review*
*Related: [CAD-Switches-PRD.md](./CAD-Switches-PRD.md)*
