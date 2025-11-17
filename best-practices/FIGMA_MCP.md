# FIGMA_MCP.md - Figma MCP Server Best Practices
*Best Practices für die Nutzung des Figma MCP Servers in Cursor*

---

## 🎯 Overview

Dieser Guide definiert, wie du mit dem Figma MCP Server arbeitest, um Designs in Code zu übersetzen.

**Wann relevant:**
- PRD enthält Figma Designs
- User Stories referenzieren Figma Screens
- Du implementierst UI aus Figma

---

## 📋 General-Purpose Rules

### Design System Integration
- ✅ **IMPORTANT: Always use components from your design system when possible**
  - Reuse existing components (buttons, inputs, typography)
  - Don't duplicate functionality
  - Check `/src/components/` first before creating new components

### Figma Fidelity
- ✅ **Prioritize Figma fidelity** to match designs exactly
  - Strive for 1:1 visual parity
  - Validate against screenshots
  - When conflicts arise, prefer design-system tokens and adjust minimally

### Design Tokens
- ✅ **Avoid hardcoded values**, use design tokens from Figma where available
  - Colors → use project's color system
  - Typography → use project's typography scale
  - Spacing → use project's spacing tokens

### Accessibility
- ✅ **Follow WCAG requirements** for accessibility
  - Semantic HTML
  - ARIA labels where needed
  - Keyboard navigation support

### Documentation
- ✅ **Add component documentation**
  - JSDoc comments for components
  - Props documentation
  - Usage examples

### File Organization
- ✅ **Place UI components in your design system directory**
  - Avoid inline styles unless truly necessary
  - Follow project's file structure conventions

---

## 🔄 Required Workflow (Do NOT Skip!)

**Follow this exact sequence for every Figma-driven change:**

### 1. Get Design Context
```
Run get_design_context first to fetch the structured representation
```
- Fetches React + Tailwind code
- Includes asset URLs
- Provides implementation base

**If response too large:**
- Run `get_metadata` to get high-level node map
- Identify specific node IDs
- Re-fetch only required nodes with `get_design_context`

### 2. Get Visual Reference
```
Run get_screenshot for visual reference
```
- Validates what you're implementing
- Use for visual comparison
- Reference during implementation

### 3. Download Assets
```
Only after you have both get_design_context and get_screenshot
```
- Download any required assets
- Use Figma-provided asset URLs
- Don't create placeholders

### 4. Translate to Project Conventions
```
Convert React + Tailwind to project's stack
```
- Replace Tailwind classes with project's utilities
- Use project's design tokens
- Follow existing patterns

### 5. Validate Against Figma
```
Check for 1:1 look and behavior before marking complete
```
- Compare with screenshot
- Test interactions
- Verify responsive behavior

---

## 💻 Implementation Rules

### Treat Figma Output as Design Reference
- ⚠️ **Figma MCP output (React + Tailwind) = design representation, NOT final code style**
- Convert to project's conventions
- Don't copy-paste blindly

### Replace Tailwind with Project Utilities
- Replace Tailwind utility classes with project's preferred utilities
- Use design-system tokens when applicable
- Example:
  ```
  Figma Output: className="bg-gray-100 text-lg"
  Project Style: className={styles.container}
  ```

### Reuse Existing Components
- ✅ Check for existing components first:
  - Buttons
  - Inputs
  - Typography components
  - Icon wrappers
  - Layout components
- ❌ Don't duplicate functionality

### Use Project's Design Tokens
- **Colors:** Use project's color system consistently
- **Typography:** Use project's typography scale
- **Spacing:** Use project's spacing tokens
- Example:
  ```
  Figma: className="text-[#141414]"
  Project: className="text-primary"
  ```

### Respect Existing Patterns
- **Routing:** Follow project's routing patterns
- **State Management:** Use established state management
- **Data Fetching:** Respect existing data-fetch patterns
- **File Structure:** Follow project's organization

### Strive for 1:1 Visual Parity
- Match Figma design exactly
- When conflicts arise:
  1. Prefer design-system tokens
  2. Adjust spacing/sizes minimally
  3. Document any deviations

### Validate Before Completion
- Compare final UI against Figma screenshot
- Test both look AND behavior
- Check responsive breakpoints

---

## 🖼️ Assets Guidance

### Use Figma-Provided Assets
- ✅ **IMPORTANT: If Figma MCP returns a localhost source for image/SVG, use it directly**
  ```typescript
  const imgIcon = "https://www.figma.com/api/mcp/asset/abc123...";
  <img src={imgIcon} alt="..." />
  ```

### DO NOT Import New Icon Packages
- ❌ **DO NOT import/add new icon packages**
- ✅ All assets should be in the Figma payload
- ✅ Use Figma-provided SVGs/images

### DO NOT Create Placeholders
- ❌ **DO NOT use or create placeholders if localhost source is provided**
- Use actual Figma assets
- Download and include in project if needed

---

## 🛠️ Tool Usage Guide

### When to use which tool:

| Tool | Use Case | Output | Best For |
|------|----------|--------|----------|
| `get_screenshot` | Visual reference | PNG screenshot | Quick overview, validation |
| `get_metadata` | Structure overview | XML node tree | Finding node IDs, understanding hierarchy |
| `get_design_context` | Code generation | React + Tailwind code + assets | Implementation |

### Best Practice Workflow:

```markdown
1. get_screenshot (whole page) → Visual overview
2. get_metadata (if needed) → Find specific node IDs
3. get_design_context (specific frames) → Generate code
   - Hero Section
   - Navigation
   - Features
   - etc.
4. Implement section by section
```

**Pro Tip:** Don't fetch entire pages with `get_design_context` - work on specific frames!

---

## 🎨 Custom Rules Template

Use this prompt to generate project-specific rules:

```
Please analyze this codebase thoroughly and provide a comprehensive rules doc
for integrating Figma designs using the Model Context Protocol:

1. Design System Structure
   - Where are design tokens defined?
   - What format/structure is used?

2. Component Library
   - Where are UI components defined?
   - What component architecture is used?

3. Frameworks & Libraries
   - What UI frameworks are used?
   - What styling libraries are used?

4. Asset Management
   - How are assets stored and referenced?
   - Asset optimization techniques?

5. Icon System
   - Where are icons stored?
   - How are icons imported and used?

6. Styling Approach
   - What CSS methodology is used?
   - Global styles?
   - Responsive design approach?

7. Project Structure
   - Overall organization?
   - Feature organization patterns?

Provide structured markdown with code snippets and file paths.
```

---

## ✅ Checklist for Figma Implementation

Before marking Figma-driven work as complete:

- [ ] Ran `get_design_context` for specific node
- [ ] Ran `get_screenshot` for visual reference
- [ ] Downloaded all required assets
- [ ] Converted Tailwind to project's styling system
- [ ] Reused existing components where possible
- [ ] Used project's design tokens (colors, typography, spacing)
- [ ] Followed project's patterns (routing, state, data-fetch)
- [ ] Validated 1:1 visual parity with Figma screenshot
- [ ] Tested interactions and responsive behavior
- [ ] Added component documentation
- [ ] No hardcoded values
- [ ] WCAG accessibility requirements met

---

## 🚨 Common Pitfalls

### ❌ DON'T:
- Copy-paste Figma output without adaptation
- Use Tailwind classes if project doesn't use Tailwind
- Hardcode colors/spacing instead of using tokens
- Create new components when existing ones exist
- Import new icon packages when Figma provides assets
- Skip screenshot validation
- Fetch entire pages (too large!)

### ✅ DO:
- Convert to project's conventions
- Reuse existing components
- Use design tokens consistently
- Download Figma assets directly
- Validate against screenshots
- Work on specific frames
- Follow the Required Workflow

---

*Best Practices from Figma MCP Server Documentation*
*Adapted for Product-Toolkit · Beyond 7 · Cursor*
