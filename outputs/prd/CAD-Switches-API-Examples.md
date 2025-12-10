# CAD Switches API - Developer Examples & Testing
**Practical Code Examples for Requirements Validation**

---

## Document Info

- **Related PRD:** [CAD-Switches-PRD.md](./CAD-Switches-PRD.md)
- **Related Review:** [CAD-Switches-API-Review.md](./CAD-Switches-API-Review.md)
- **Created:** 2025-12-02
- **Persona:** Web Developer (Primary Target User)
- **Purpose:** Validate API design by implementing each requirement with real code

---

## Introduction

This document contains practical code examples for every requirement in the CAD Switches PRD. Each example is written from the perspective of a **web developer** building a 3D visualization app using webvis.js.

**Developer Context:**
- **Name:** Sarah (Senior Frontend Developer)
- **Experience:** 3 years with webvis.js, building configurators and digital twins
- **Goal:** Integrate Reference Set switching into a manufacturing review tool
- **Pain Point:** Current LayerFilterAPI is confusing for Reference Sets

**Testing Approach:**
- ✅ Write code for each requirement
- 📝 Add developer notes/observations
- ⚠️ Flag pain points, confusions, or missing features
- 💡 Suggest improvements

---

## Requirements Testing

### EU-0: Global Reference Set Setting

**Requirement:** Reference Set can be globally set over all nodes

#### Example 1: Switch All Parts to "Solid" View

```typescript
import { FilterAPI, FilterCategory } from '@threedy/webvis';

/**
 * Use case: Engineer wants to quickly switch entire assembly to simplified view
 * Scenario: Large assembly (500+ parts), need to hide sketches/datums globally
 */
async function switchAllPartsToSolidView(api: FilterAPI): Promise<void> {
  // Step 1: Get available Reference Sets
  const referenceSets = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);

  // Step 2: Find "Solid" Reference Set
  const solidRefSet = referenceSets.find(rs => rs.name === 'Solid');

  if (!solidRefSet) {
    throw new Error('Solid Reference Set not found');
  }

  // Step 3: Set globally (no nodeId = applies to all nodes)
  api.setFilterEnabled(solidRefSet.id, true);

  console.log('✅ All parts switched to Solid view');
}
```

**Developer Notes:**

✅ **What works well:**
- Simple API call without nodeId applies globally
- Clear and intuitive behavior

⚠️ **Pain points:**
- ❓ **QUESTION:** How do I know which Reference Sets are available before the model loads?
- ❓ **QUESTION:** What if some parts don't have a "Solid" Reference Set? Does it fail silently?
- ❓ **QUESTION:** Is this operation synchronous? Can I immediately query the state after calling this?

💡 **Improvement suggestions:**
- Add a method to check if a Reference Set exists for all nodes before switching
- Provide feedback on how many nodes were affected
- Consider returning a result object: `{ nodesAffected: number, nodesFailed: number }`

#### Example 2: Bulk Switch with Error Handling

```typescript
/**
 * More robust version with validation
 */
async function switchAllPartsWithValidation(
  api: FilterAPI,
  refSetName: string
): Promise<{ success: boolean; message: string }> {

  // Get all reference sets
  const referenceSets = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);

  // Find target
  const targetRefSet = referenceSets.find(rs => rs.name === refSetName);

  if (!targetRefSet) {
    return {
      success: false,
      message: `Reference Set "${refSetName}" not found. Available: ${referenceSets.map(rs => rs.name).join(', ')}`
    };
  }

  // Apply globally
  api.setFilterEnabled(targetRefSet.id, true);

  // ⚠️ PROBLEM: No way to verify the operation succeeded!
  // ⚠️ PROBLEM: Can't check how many nodes were affected

  return {
    success: true,
    message: `Switched all parts to "${refSetName}"`
  };
}
```

**Developer Notes:**

⚠️ **Critical gap:**
- No feedback mechanism! Can't tell if the operation succeeded
- Can't verify state after the call
- No way to know how many nodes were affected

💡 **Suggested API addition:**
```typescript
// Option A: Make it async with result
setFilterEnabled(id: number, enabled: boolean, nodeId?: number): Promise<{
  nodesAffected: number;
  nodesFailed: number;
}>;

// Option B: Add a verification method
async verifyFilterState(id: number, nodeId?: number): Promise<boolean>;
```

---

### EU-1: Load NX-Authored Default Reference Set

**Requirement:** On initial load, WebVis must load the NX-authored default Reference Set for every part instance

#### Example 3: Verify Default Reference Sets on Load

```typescript
/**
 * Use case: After model loads, verify default Reference Sets are active
 * Scenario: QA engineer wants to confirm correct default view
 */
async function verifyDefaultReferenceSets(api: FilterAPI): Promise<void> {
  // Get all enabled Reference Sets
  const enabledFilters = await api.requestEnabledFilters();
  const enabledRefSets = enabledFilters.filter(f => f.filterCategory === FilterCategory.REFERENCE_SET);

  console.log('Currently enabled Reference Sets:', enabledRefSets.map(rs => rs.name));

  // ⚠️ PROBLEM: How do I know which ones are "default" vs manually enabled?
  // ⚠️ PROBLEM: Can't distinguish between NX-authored defaults and user changes
}
```

**Developer Notes:**

⚠️ **Missing information:**
- No way to identify which Reference Set is the "default"
- `FilterProperties` doesn't have an `isDefault` flag
- Can't restore defaults after user makes changes

💡 **Suggested addition to FilterProperties:**
```typescript
interface FilterProperties {
  id: number;
  name: string;
  enabled: boolean;
  filterCategory: FilterCategory;
  metadata?: {
    isDefault?: boolean;  // ⭐ ADD THIS
    description?: string;
  };
}
```

**Real-world scenario:**
```typescript
/**
 * Build a "Reset to Defaults" button
 */
async function resetToDefaultReferenceSets(api: FilterAPI): Promise<void> {
  const allRefSets = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);

  // ⚠️ PROBLEM: Can't identify defaults!
  // How do I know which ones to enable?

  // Workaround: Store initial state on load
  // But this is error-prone and requires extra code
}
```

---

### EU-2: Exactly One Reference Set Per Node (Exclusivity)

**Requirement:** Viewer must display exactly one Reference Set per node at any time

#### Example 4: Switch Reference Set for Single Part

```typescript
/**
 * Use case: Toggle between detailed and simplified view for a single part
 * Scenario: Engineer reviewing a specific component, wants to see internal details
 */
async function switchPartView(
  api: FilterAPI,
  nodeId: number,
  fromRefSet: string,
  toRefSet: string
): Promise<void> {

  const referenceSets = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);
  const target = referenceSets.find(rs => rs.name === toRefSet);

  if (!target) {
    throw new Error(`Reference Set "${toRefSet}" not found`);
  }

  // Enable new Reference Set for this node
  // According to docs: This automatically disables other Reference Sets for this node
  api.setFilterEnabled(target.id, true, nodeId);

  console.log(`✅ Node ${nodeId} switched from "${fromRefSet}" to "${toRefSet}"`);
}
```

**Developer Notes:**

✅ **What works well:**
- Exclusivity is handled automatically by the implementation
- Developer doesn't need to manually disable the old Reference Set
- Clean API call

❓ **Clarification needed:**
- What if I call `setFilterEnabled(solidId, false, nodeId)` explicitly?
- Does disabling leave the node with NO Reference Set active?
- What's the behavior if no Reference Set is active? Is the node hidden?

#### Example 5: Toggle Between Views with State Tracking

```typescript
/**
 * Track current state and provide toggle functionality
 */
class ReferenceSetController {
  constructor(private api: FilterAPI) {}

  /**
   * Toggle between "Solid" and "Entire Part" for a node
   */
  async toggleDetailView(nodeId: number): Promise<void> {
    // ⚠️ PROBLEM: How do I know which Reference Set is currently active?

    // Missing: api.requestActiveFilterForNode(nodeId, FilterCategory.REFERENCE_SET)

    // Workaround: Query all enabled filters and check manually
    const enabledFilters = await this.api.requestEnabledFilters();
    const enabledRefSets = enabledFilters.filter(f => f.filterCategory === FilterCategory.REFERENCE_SET);

    // ⚠️ PROBLEM: These are ALL enabled Reference Sets globally
    // How do I know which one applies to THIS specific node?

    // Can use isNodePartOfEnabledFilters, but need to check each one:
    for (const refSet of enabledRefSets) {
      const isActive = await this.api.isNodePartOfEnabledFilters(nodeId, FilterCategory.REFERENCE_SET);
      // ⚠️ PROBLEM: This only tells me IF any Reference Set is active, not WHICH ONE!
    }

    // ⚠️ CRITICAL GAP: Cannot determine which specific Reference Set is active for a node!
  }
}
```

**Developer Notes:**

🔴 **CRITICAL GAP CONFIRMED:**
- Cannot query which Reference Set is currently active for a specific node
- `isNodePartOfEnabledFilters()` only returns boolean, not which filter
- `requestEnabledFilters()` returns global state, not per-node

💡 **Required addition:**
```typescript
/**
 * Returns the currently active filter for a node (for exclusive categories)
 */
requestActiveFilterForNode(
  nodeId: number,
  filterCategory: FilterCategory
): Promise<FilterProperties | null>;
```

---

### EU-3: Switch Reference Set for Individual Node via UI

**Requirement:** User can switch the active Reference Set for an individual node via UI control (e.g. dropdown in tree)

#### Example 6: Build a Reference Set Dropdown

```typescript
/**
 * Use case: Build dropdown UI component for Reference Set selection
 * Scenario: Tree view with per-node dropdown to switch Reference Sets
 */
async function buildReferenceSetDropdown(
  api: FilterAPI,
  nodeId: number
): Promise<{ label: string; value: number; isActive: boolean }[]> {

  // Step 1: Get all Reference Sets
  const allReferenceSets = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);

  // ⚠️ PROBLEM: This returns ALL Reference Sets globally
  // Which ones are actually available for THIS node?
  // Different parts may have different Reference Sets!

  // Step 2: Determine which one is currently active
  // ⚠️ PROBLEM: No direct way to get active Reference Set for this node!

  // Workaround: Check each one individually (expensive!)
  const options = await Promise.all(
    allReferenceSets.map(async (refSet) => {
      // ⚠️ ISSUE: isNodePartOfEnabledFilters only tells us IF node is in ANY enabled filter
      // Doesn't tell us which specific filter is active
      const isActive = await api.isNodePartOfEnabledFilters(nodeId, FilterCategory.REFERENCE_SET);

      return {
        label: refSet.name,
        value: refSet.id,
        isActive: isActive // ⚠️ This is wrong! All will return the same boolean
      };
    })
  );

  return options;
}
```

**Developer Notes:**

🔴 **CRITICAL ISSUES:**

1. **Cannot get Reference Sets for specific node**
   - `requestFiltersForCategory()` returns all Reference Sets globally
   - Part A might have: "Solid", "Entire Part", "Empty"
   - Part B might have: "Solid", "Design", "Simplified"
   - API returns union of both, can't filter by node!

2. **Cannot determine active Reference Set**
   - No way to know which Reference Set is currently active for a node
   - `isNodePartOfEnabledFilters()` only returns yes/no for entire category

💡 **Required additions:**
```typescript
// Get Reference Sets applicable to specific node
requestFiltersForNode(
  nodeId: number,
  filterCategory?: FilterCategory
): Promise<FilterProperties[]>;

// Get currently active Reference Set for node
requestActiveFilterForNode(
  nodeId: number,
  filterCategory: FilterCategory
): Promise<FilterProperties | null>;
```

#### Example 7: Dropdown with Required API Additions

```typescript
/**
 * How the dropdown SHOULD work with proposed API additions
 */
async function buildReferenceSetDropdownCorrected(
  api: FilterAPI,
  nodeId: number
): Promise<{ label: string; value: number; isActive: boolean }[]> {

  // ✅ Get Reference Sets for THIS specific node (PROPOSED API)
  const nodeReferenceSets = await api.requestFiltersForNode(nodeId, FilterCategory.REFERENCE_SET);

  // ✅ Get currently active Reference Set (PROPOSED API)
  const activeRefSet = await api.requestActiveFilterForNode(nodeId, FilterCategory.REFERENCE_SET);

  // ✅ Build dropdown options
  const options = nodeReferenceSets.map(refSet => ({
    label: refSet.name,
    value: refSet.id,
    isActive: activeRefSet?.id === refSet.id
  }));

  return options;
}

/**
 * Handle dropdown selection
 */
function handleDropdownChange(api: FilterAPI, nodeId: number, refSetId: number): void {
  // ✅ This works well!
  api.setFilterEnabled(refSetId, true, nodeId);
  console.log(`✅ Switched Reference Set for node ${nodeId}`);
}
```

**Developer Notes:**

✅ **With proposed API additions, this becomes:**
- Clean and intuitive
- Efficient (no redundant queries)
- Easy to implement UI components

---

### WD-1: List Available Filters for Any Node

**Requirement:** Endpoint to list available filters for any node

#### Example 8: Get All Filters for a Node

```typescript
/**
 * Use case: Build advanced filter panel showing all filter types for a node
 * Scenario: Engineer wants to see layers, variants, and reference sets for a part
 */
async function getAllFiltersForNode(api: FilterAPI, nodeId: number): Promise<void> {
  // ⚠️ CURRENT API: Can only get by category globally

  // Get layers (global - these apply to all nodes)
  const layers = await api.requestFiltersForCategory(FilterCategory.LAYER_FILTER);

  // Get Reference Sets (should be per-node, but API returns global)
  const referenceSets = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);

  // ⚠️ PROBLEM: No way to filter results to only those applicable to this node!

  console.log('Layers (global):', layers.map(l => l.name));
  console.log('Reference Sets (global):', referenceSets.map(rs => rs.name));
  console.log('⚠️ Cannot determine which Reference Sets apply to node', nodeId);
}
```

**Developer Notes:**

⚠️ **Gap confirmed:**
- Current API returns global filters only
- Cannot get node-specific filter availability

💡 **Required:**
```typescript
requestFiltersForNode(nodeId: number, filterCategory?: FilterCategory): Promise<FilterProperties[]>;
```

#### Example 9: Build Advanced Filter Panel (Real-World)

```typescript
/**
 * Real-world component: Advanced filter panel for part inspection
 */
interface FilterPanelData {
  layers: FilterProperties[];
  referenceSets: FilterProperties[];
  variants: FilterProperties[];
}

async function getFilterPanelData(
  api: FilterAPI,
  nodeId: number
): Promise<FilterPanelData> {

  // ✅ Layers are global - current API works
  const layers = await api.requestFiltersForCategory(FilterCategory.LAYER_FILTER);

  // ⚠️ Reference Sets should be per-node - need new API
  // Workaround: Get all and hope they're relevant
  const referenceSets = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);

  // Variants (VC2) - would have same issue
  const variants: FilterProperties[] = []; // Not implemented yet

  return {
    layers,
    referenceSets, // ⚠️ May contain irrelevant options for this node!
    variants
  };
}
```

---

### WD-2: Query Currently Active Filters Per Node

**Requirement:** Endpoint to query currently active filters per node

#### Example 10: Get Active Filters for Node

```typescript
/**
 * Use case: Display current filter state in UI
 * Scenario: Status bar showing active filters for selected part
 */
async function getActiveFiltersForNode(
  api: FilterAPI,
  nodeId: number
): Promise<{ layers: string[]; referenceSet: string | null }> {

  // Get all enabled filters
  const enabledFilters = await api.requestEnabledFilters();

  // ⚠️ PROBLEM: This is GLOBAL enabled state, not per-node!

  // Filter by category
  const enabledLayers = enabledFilters
    .filter(f => f.filterCategory === FilterCategory.LAYER_FILTER);

  const enabledRefSets = enabledFilters
    .filter(f => f.filterCategory === FilterCategory.REFERENCE_SET);

  // ⚠️ PROBLEM: Which of these Reference Sets applies to THIS node?
  // Could be multiple Reference Sets enabled for different nodes!

  // Try to check each one (inefficient!)
  let activeRefSet: string | null = null;
  for (const refSet of enabledRefSets) {
    const isPartOf = await api.isNodePartOfEnabledFilters(nodeId, FilterCategory.REFERENCE_SET);
    // ⚠️ PROBLEM: This returns true if node is part of ANY enabled Reference Set
    // Doesn't tell me WHICH one!
    if (isPartOf) {
      activeRefSet = '???'; // Can't determine which one!
      break;
    }
  }

  return {
    layers: enabledLayers.map(l => l.name),
    referenceSet: activeRefSet
  };
}
```

**Developer Notes:**

🔴 **CRITICAL GAP:**
- Cannot query per-node active state
- `requestEnabledFilters()` is global only
- `isNodePartOfEnabledFilters()` doesn't return which filter

💡 **Required:**
```typescript
// Get all active filters for a specific node
requestActiveFiltersForNode(nodeId: number): Promise<FilterProperties[]>;

// Or more specific:
requestActiveFilterForNode(
  nodeId: number,
  filterCategory: FilterCategory
): Promise<FilterProperties | null>;
```

#### Example 11: Status Bar Component (Corrected with Proposed API)

```typescript
/**
 * How it SHOULD work with proposed API
 */
async function getNodeFilterStatus(
  api: FilterAPI,
  nodeId: number
): Promise<string> {

  // ✅ Get active Reference Set for node (PROPOSED)
  const activeRefSet = await api.requestActiveFilterForNode(
    nodeId,
    FilterCategory.REFERENCE_SET
  );

  // ✅ Layers are global - current API works
  const enabledLayers = (await api.requestEnabledFilters())
    .filter(f => f.filterCategory === FilterCategory.LAYER_FILTER);

  // Build status string
  const refSetStatus = activeRefSet ? `RefSet: ${activeRefSet.name}` : 'RefSet: None';
  const layerStatus = `Layers: ${enabledLayers.length} active`;

  return `${refSetStatus} | ${layerStatus}`;
}
```

---

### WD-3: Set/Replace Active Filter Per Node

**Requirement:** Endpoint to set/replace active filter per node (exclusive toggle for Reference Sets)

#### Example 12: Replace Reference Set

```typescript
/**
 * Use case: Switch Reference Sets programmatically
 * Scenario: Automated test switching between views
 */
async function testReferenceSetSwitching(api: FilterAPI, nodeId: number): Promise<void> {
  const referenceSets = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);

  const solid = referenceSets.find(rs => rs.name === 'Solid');
  const entirePart = referenceSets.find(rs => rs.name === 'Entire Part');

  if (!solid || !entirePart) {
    throw new Error('Required Reference Sets not found');
  }

  // ✅ Switch to Solid
  api.setFilterEnabled(solid.id, true, nodeId);

  // ✅ Switch to Entire Part (Solid automatically disabled - documented behavior)
  api.setFilterEnabled(entirePart.id, true, nodeId);

  console.log('✅ Reference Set switching works!');
}
```

**Developer Notes:**

✅ **Works well:**
- API handles exclusivity automatically
- Clean and simple

❓ **Questions:**
- What happens if I call `setFilterEnabled(solidId, false, nodeId)`?
- Does it leave the node with NO active Reference Set?
- Is the node then hidden or does it show some default geometry?

#### Example 13: Edge Case Testing

```typescript
/**
 * Test edge cases
 */
async function testEdgeCases(api: FilterAPI, nodeId: number): Promise<void> {
  const referenceSets = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);
  const solid = referenceSets.find(rs => rs.name === 'Solid')!;

  // Edge Case 1: Enable same Reference Set twice
  api.setFilterEnabled(solid.id, true, nodeId);
  api.setFilterEnabled(solid.id, true, nodeId); // Should be idempotent
  console.log('✅ Edge Case 1: Idempotent (no error)');

  // Edge Case 2: Explicitly disable
  api.setFilterEnabled(solid.id, false, nodeId);
  // ❓ What's the state now? No Reference Set active? Node hidden?
  console.log('⚠️ Edge Case 2: State after explicit disable - unclear');

  // Edge Case 3: Invalid nodeId
  api.setFilterEnabled(solid.id, true, 999999);
  // ❓ Error? Silent fail? How do I know it failed?
  console.log('⚠️ Edge Case 3: Invalid nodeId - no error feedback');

  // Edge Case 4: Layer filter with nodeId (should be ignored)
  const layers = await api.requestFiltersForCategory(FilterCategory.LAYER_FILTER);
  if (layers.length > 0) {
    api.setFilterEnabled(layers[0].id, true, nodeId);
    // ✅ Documented: nodeId is ignored for layers (global)
    console.log('✅ Edge Case 4: Layer with nodeId ignored (documented)');
  }
}
```

**Developer Notes:**

⚠️ **Missing error handling / feedback:**
- No way to know if operation succeeded
- No validation errors for invalid nodeIds
- State after explicit disable is unclear

💡 **Suggestions:**
```typescript
// Option A: Return result
setFilterEnabled(id: number, enabled: boolean, nodeId?: number): Promise<{
  success: boolean;
  nodesAffected: number;
  error?: string;
}>;

// Option B: Throw errors
setFilterEnabled(id: number, enabled: boolean, nodeId?: number): void;
// Throws: InvalidNodeIdError, FilterNotFoundError, etc.
```

---

### WD-4: Session-Local (Ephemeral)

**Requirement:** All changes are session-local (ephemeral); no persistence after reload

#### Example 14: Verify Ephemeral State

```typescript
/**
 * Use case: Verify filter state doesn't persist
 * Scenario: Test that reload resets to defaults
 */
async function testEphemeralState(api: FilterAPI): Promise<void> {
  const referenceSets = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);
  const solid = referenceSets.find(rs => rs.name === 'Solid')!;

  // Make changes
  api.setFilterEnabled(solid.id, true); // Global

  console.log('✅ Changed to Solid view');
  console.log('ℹ️ After page reload, this will reset to defaults');
  console.log('ℹ️ No persistence - as documented in WD-4');

  // ❓ Is there a way to save state for later restore?
  // ❓ Can I export/import filter configurations?
}
```

**Developer Notes:**

✅ **Clear expectation:**
- Documentation states session-local only
- Persistence is out of scope for Phase 1

💡 **Future consideration (VC3):**
```typescript
// Export current filter state
exportFilterState(): string; // JSON

// Restore filter state
importFilterState(state: string): void;

// Save named preset
saveFilterPreset(name: string): void;
loadFilterPreset(name: string): void;
```

---

## Real-World Integration Examples

### Example 15: Complete Manufacturing Review App

```typescript
/**
 * Real-world app: Manufacturing part review tool
 * Features:
 * - Tree view with per-part Reference Set dropdowns
 * - Global "Simplified View" toggle
 * - Status bar showing active filters
 */
class ManufacturingReviewApp {
  constructor(private api: FilterAPI) {}

  /**
   * Initialize app: Load model and set up UI
   */
  async initialize(): Promise<void> {
    // Wait for model to load
    // ✅ EU-1: Default Reference Sets should already be active

    // Verify defaults are loaded
    await this.verifyDefaults();

    // Build tree view with dropdowns
    await this.buildTreeView();

    // Set up global controls
    this.setupGlobalControls();
  }

  /**
   * Verify default Reference Sets are active (EU-1)
   */
  private async verifyDefaults(): Promise<void> {
    const enabledRefSets = (await this.api.requestEnabledFilters())
      .filter(f => f.filterCategory === FilterCategory.REFERENCE_SET);

    console.log('Default Reference Sets loaded:', enabledRefSets.map(rs => rs.name));

    // ⚠️ PROBLEM: Can't verify if these are actually the "defaults"
    // FilterProperties doesn't have isDefault flag
  }

  /**
   * Build tree view with per-node dropdowns (EU-3)
   */
  private async buildTreeView(): Promise<void> {
    const nodeIds = [123, 124, 125]; // From scene graph

    for (const nodeId of nodeIds) {
      // ⚠️ GAP: Can't get Reference Sets for specific node!
      // Would need: api.requestFiltersForNode(nodeId, FilterCategory.REFERENCE_SET)

      // Workaround: Get all and hope they're relevant
      const allReferenceSets = await this.api.requestFiltersForCategory(
        FilterCategory.REFERENCE_SET
      );

      // Build dropdown (may include irrelevant options!)
      const dropdown = this.createDropdown(nodeId, allReferenceSets);

      // ⚠️ GAP: Can't determine which one is currently active!
      // Would need: api.requestActiveFilterForNode(nodeId, FilterCategory.REFERENCE_SET)
    }
  }

  /**
   * Global "Simplified View" toggle (EU-0)
   */
  private setupGlobalControls(): void {
    const simplifiedViewButton = document.getElementById('simplified-view');

    simplifiedViewButton?.addEventListener('click', async () => {
      // ✅ This works well!
      const referenceSets = await this.api.requestFiltersForCategory(
        FilterCategory.REFERENCE_SET
      );
      const solid = referenceSets.find(rs => rs.name === 'Solid');

      if (solid) {
        this.api.setFilterEnabled(solid.id, true); // Global
        console.log('✅ All parts switched to simplified view');
      }
    });
  }

  /**
   * Create dropdown for node
   */
  private createDropdown(nodeId: number, referenceSets: FilterProperties[]): HTMLElement {
    const select = document.createElement('select');

    referenceSets.forEach(refSet => {
      const option = document.createElement('option');
      option.value = refSet.id.toString();
      option.text = refSet.name;

      // ⚠️ GAP: Can't determine if this is the active one!
      // option.selected = ???

      select.appendChild(option);
    });

    select.addEventListener('change', (e) => {
      const refSetId = parseInt((e.target as HTMLSelectElement).value);
      this.api.setFilterEnabled(refSetId, true, nodeId); // ✅ Works well!
    });

    return select;
  }
}
```

**Developer Experience Summary:**

✅ **What works well:**
- Global Reference Set switching (EU-0)
- Per-node switching with `setFilterEnabled()` (EU-3)
- Category-dependent behavior is clear from docs

🔴 **Critical gaps that block implementation:**
1. Cannot get Reference Sets for specific node (breaks dropdown UIs)
2. Cannot query active Reference Set per node (breaks UI state sync)
3. No default Reference Set indicator (can't implement "Reset to Defaults")

⚠️ **Pain points:**
- No operation feedback (success/failure)
- Edge case behaviors unclear
- No validation errors

---

### Example 16: Automated Testing Suite

```typescript
/**
 * Automated tests for Reference Set functionality
 */
describe('CAD Switches API - Reference Sets', () => {

  let api: FilterAPI;

  beforeEach(() => {
    // Initialize API
  });

  test('EU-0: Global Reference Set setting', async () => {
    const referenceSets = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);
    const solid = referenceSets.find(rs => rs.name === 'Solid')!;

    // Set globally
    api.setFilterEnabled(solid.id, true);

    // ⚠️ PROBLEM: Can't verify it was applied!
    // No way to check "all nodes now use Solid"

    // Would need something like:
    // const result = await api.verifyGlobalFilterState(solid.id);
    // expect(result.nodesAffected).toBeGreaterThan(0);
  });

  test('EU-2: Reference Set exclusivity', async () => {
    const nodeId = 123;
    const referenceSets = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);
    const solid = referenceSets.find(rs => rs.name === 'Solid')!;
    const entirePart = referenceSets.find(rs => rs.name === 'Entire Part')!;

    // Enable Solid
    api.setFilterEnabled(solid.id, true, nodeId);

    // Enable Entire Part (should disable Solid)
    api.setFilterEnabled(entirePart.id, true, nodeId);

    // ⚠️ PROBLEM: Can't verify Solid was disabled!
    // Would need:
    // const active = await api.requestActiveFilterForNode(nodeId, FilterCategory.REFERENCE_SET);
    // expect(active?.id).toBe(entirePart.id);
  });

  test('EU-3: Per-node switching', async () => {
    const node1 = 123;
    const node2 = 124;
    const referenceSets = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);
    const solid = referenceSets.find(rs => rs.name === 'Solid')!;
    const entirePart = referenceSets.find(rs => rs.name === 'Entire Part')!;

    // Different Reference Sets for different nodes
    api.setFilterEnabled(solid.id, true, node1);
    api.setFilterEnabled(entirePart.id, true, node2);

    // ✅ Should work (per-node switching)

    // ⚠️ PROBLEM: Can't verify!
    // const active1 = await api.requestActiveFilterForNode(node1, FilterCategory.REFERENCE_SET);
    // const active2 = await api.requestActiveFilterForNode(node2, FilterCategory.REFERENCE_SET);
    // expect(active1?.id).toBe(solid.id);
    // expect(active2?.id).toBe(entirePart.id);
  });

  test('WD-1: List filters for node', async () => {
    const nodeId = 123;

    // ⚠️ BLOCKED: Missing API
    // const nodeFilters = await api.requestFiltersForNode(nodeId, FilterCategory.REFERENCE_SET);
    // expect(nodeFilters.length).toBeGreaterThan(0);

    // Current workaround:
    const allFilters = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);
    // But these might not all apply to nodeId!
  });

  test('Edge case: Invalid nodeId', () => {
    const referenceSets = await api.requestFiltersForCategory(FilterCategory.REFERENCE_SET);
    const solid = referenceSets.find(rs => rs.name === 'Solid')!;

    // ❓ What happens?
    api.setFilterEnabled(solid.id, true, 999999);

    // Should this:
    // - Throw an error? (Option A)
    // - Fail silently? (Option B)
    // - Return error result? (Option C)

    // Currently: Unclear!
  });
});
```

**Testing Challenges:**

🔴 **Cannot write comprehensive tests because:**
1. No way to verify operations succeeded
2. No way to query per-node state
3. Edge case behaviors undefined

💡 **To enable proper testing, need:**
- State verification methods
- Operation result feedback
- Clear error handling

---

## Developer Feedback Summary

### 🎯 Overall Developer Experience

**Complexity Rating:** ⭐⭐⭐⚪⚪ (3/5 - Moderate)

**Time to Productivity:**
- Basic usage (global switching): **10 minutes** ✅
- Per-node switching: **20 minutes** ✅
- Building UI components: **2+ hours** ⚠️ (blocked by missing APIs)
- Production-ready with error handling: **Blocked** 🔴

---

### ✅ What Works Well

1. **Simple global switching** (EU-0)
   - `setFilterEnabled(id, true)` without nodeId is intuitive
   - Clear and concise

2. **Per-node switching** (EU-3)
   - `setFilterEnabled(id, true, nodeId)` is straightforward
   - Exclusivity handled automatically

3. **Category-based organization**
   - Clear separation between Layers, Reference Sets, Variants
   - Enum makes it discoverable

4. **Documentation**
   - Category-dependent behavior well explained
   - Code examples in JSDoc helpful

---

### 🔴 Critical Gaps (Block Implementation)

1. **Cannot get filters for specific node** (WD-1)
   - **Impact:** Cannot build correct dropdown UIs
   - **Workaround:** Show all filters globally (may include irrelevant options)
   - **Blocks:** EU-3 implementation

2. **Cannot query active filter per node** (WD-2)
   - **Impact:** Cannot show current state in UI
   - **Workaround:** None (fundamentally missing)
   - **Blocks:** All UI state synchronization

3. **No default Reference Set indicator** (EU-1)
   - **Impact:** Cannot implement "Reset to Defaults"
   - **Workaround:** Store initial state manually
   - **Blocks:** Common UX pattern

---

### ⚠️ Pain Points (Hurt Developer Experience)

4. **No operation feedback**
   - Can't tell if `setFilterEnabled()` succeeded
   - No validation errors
   - **Impact:** Hard to debug, can't write tests

5. **Edge cases undefined**
   - What happens when explicitly disabling?
   - Behavior with invalid nodeId?
   - **Impact:** Defensive coding required, uncertainty

6. **No bulk operations**
   - Setting 1000 nodes requires 1000 calls
   - **Impact:** Performance concerns for large assemblies

---

### 💡 Required API Additions

**Priority 1 (Critical):**
```typescript
// Get filters for specific node
requestFiltersForNode(
  nodeId: number,
  filterCategory?: FilterCategory
): Promise<FilterProperties[]>;

// Get active filter for node (exclusive categories)
requestActiveFilterForNode(
  nodeId: number,
  filterCategory: FilterCategory
): Promise<FilterProperties | null>;
```

**Priority 2 (High):**
```typescript
// Add to FilterProperties
interface FilterProperties {
  // ... existing fields
  metadata?: {
    isDefault?: boolean;  // For EU-1
  };
}
```

**Priority 3 (Medium):**
```typescript
// Batch operations
setFilterEnabledBatch(
  id: number,
  enabled: boolean,
  nodeIds: number[]
): void;

// Operation feedback (make async)
setFilterEnabled(
  id: number,
  enabled: boolean,
  nodeId?: number
): Promise<{ nodesAffected: number }>;
```

---

## Recommendations

### For API Finalization

1. **Add Priority 1 methods immediately**
   - Without these, web developers cannot implement requirement EU-3
   - Blocks dropdown UI component (primary use case)

2. **Add `isDefault` to FilterProperties**
   - Supports EU-1 verification
   - Enables "Reset to Defaults" UX pattern

3. **Define edge case behaviors**
   - Document what happens when explicitly disabling
   - Document invalid nodeId handling
   - Update JSDoc with edge cases

4. **Consider operation feedback**
   - Either make methods async with results
   - Or add verification methods
   - Enables proper error handling and testing

### For VC1 Implementation

1. **Start with basic per-node switching**
   - Focus on `setFilterEnabled()` with nodeId
   - Get exclusivity working correctly

2. **Add query methods in parallel**
   - Critical for UI development
   - Web developers blocked without these

3. **Create example app**
   - Manufacturing review tool (from Example 15)
   - Use as integration test
   - Gather developer feedback early

### For Developer Documentation

1. **Provide complete examples**
   - Include this document in docs
   - Show real-world integration patterns

2. **Document all edge cases**
   - Explicit disable behavior
   - Invalid nodeId handling
   - State after errors

3. **Migration guide**
   - From LayerFilterAPI to FilterAPI
   - From current Reference Set hacks to proper API

---

## Next Steps

1. **Team Review** (This Week)
   - Discuss Priority 1 API additions
   - Decide on operation feedback approach
   - Finalize edge case behaviors

2. **API Update** (Week 2)
   - Implement Priority 1 methods
   - Add `isDefault` to FilterProperties
   - Update TypeScript definitions

3. **Developer Testing** (Week 3)
   - Build example app (Manufacturing Review)
   - Real-world integration with actual web developers
   - Collect feedback

4. **Documentation** (Week 4)
   - Complete API reference
   - Migration guide
   - Example gallery

---

## Document History

- **v1.0 (2025-12-02):** Initial examples document - Web Developer perspective
  - All requirements tested with code examples
  - Critical gaps identified and documented
  - Real-world integration scenarios included

---

*Generated for CAD Switches API Development*
*Developer Persona: Sarah, Senior Frontend Developer*
*Related: [CAD-Switches-PRD.md](./CAD-Switches-PRD.md) | [CAD-Switches-API-Review.md](./CAD-Switches-API-Review.md)*
