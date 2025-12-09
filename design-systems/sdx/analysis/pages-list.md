# SDX Core Design Library - Complete Page List

> **⚠️ IMPORTANT**: This file documents the **SDX Core Design Library** (SDX Components).  
> This is the primary Figma file containing design tokens, components, and patterns.  
> There is a separate Figma file ("SDX Documentation") that contains component documentation.

**File**: SDX Components (Core Design Library)  
**URL**: https://www.figma.com/design/fJcQzJgf6IRQQxz9A6DwHt/SDX-Components  
**Date Compiled**: December 2024  
**Source**: User-provided page list + systematic analysis

---

## Node ID Format

Figma URLs use format: `node-id=XXXX-YYYY`  
Internal format: `XXXX:YYYY` (colon separator)

**Example**: `https://www.figma.com/design/fJcQzJgf6IRQQxz9A6DwHt/SDX-Components?node-id=51859-1065`  
Extract: `51859-1065` → Convert to: `51859:1065` (replace `-` with `:`)

---

## All Pages in File (53 Total)

### 📍 Foundation Pages (6 pages)

| # | Page Name | Node ID | Status | Components/Features |
|---|-----------|---------|--------|---------------------|
| 1 | **Cover** | `1550:3005` | ⏭️ Skipped | Title page, project info |
| 2 | **Colors** | `51859:1065` | ✅ Analyzed | 11 color families × 10 tints (~110 color tokens), gradients, 2025/2026 systems. **Critical Finding**: 20+ color tokens, variant naming inconsistencies |
| 3 | **Icons** | `51859:1067` | ✅ Analyzed | 500+ icons across 16 categories (AI, Business, Customer, Food, Freetime, Health, IT, Media, Nature, Planning, Social Media, Sport, Sustainability, UI Navigation, UI Operations, Vehicles). Sizes: 16×16, 24×24, 32×32, 40×40, 48×48, 56×56 |
| 4 | **Typography** | `51859:1064` | ✅ Analyzed | 14 font sizes (12px → 104px), 3 weights (semilight, semibold, bold). Heading styles (6 levels: XS-XXL), Body styles (3 sizes: XS, S, Base), Display styles (4 sizes: S-XL), Desktop/Mobile variants. **Critical Finding**: 40+ typography tokens, **2 parallel token systems** |
| 5 | **Grid** | `51859:1068` | ✅ Analyzed | 6 responsive breakpoints (360, 480, 768, 1024, 1280, 1440px). Simple and clear - no token issues |
| 6 | **Utils** | `8071:8458` | ⏸️ Not analyzed | Utility components |

---

### 🧩 Component Pages (41 pages)

#### Core Form Components (6 pages) ✅ ALL ANALYZED

| # | Page Name | Node ID | Status | Variants/States |
|---|-----------|---------|--------|-----------------|
| 7 | **Button** | `6:19` | ✅ Analyzed | 6 types (Primary, Secondary, Confirmation, Outline, Ghost, Transparent), icon buttons (4 types, 48×48), 2 sizes (Default 48px, Small 36px), states (Default, Hover, Spinner). **Tokens**: 10 tokens extracted |
| 8 | **Input Fields** | `226:278` | ✅ Analyzed | Standard input + Date input. 9 states for standard (Default, Filled, Validated, Mandatory, Focus, Hover, Error, Textfield, Disabled), 7 for date. **Tokens**: 16 tokens extracted. **Critical**: Found `borderWidth`, `borderRadius/small`, `sdx/border/radius-medium` |
| 9 | **Checkbox** | `9:25` | ✅ Analyzed | Variants: Standard, Container (boxed). 8 states including tri-state (indeterminate). **Tokens**: Uses **SDX-prefixed typography heavily** |
| 10 | **Radio Button** | `9:26` | ✅ Analyzed | Variants: Standard, Container. 6 states (no tri-state). Similar to Checkbox but simpler |
| 11 | **Dropdown (select)** | `10:111` | ✅ Analyzed | **Complexity**: HIGH - most complex component. 8 main states, 18 option state combinations. Features: Multiselect, search, option grouping. **Most stateful component in design system** |
| 12 | **Switch** | `583:65` | ✅ Analyzed | Variants: Label left/right. States: Default, Hover × On/Off. 8 total combinations |

#### Remaining Components (35 pages) ⏸️ NOT YET ANALYZED

| # | Page Name | Node ID | Status | Notes |
|---|-----------|---------|--------|-------|
| 13 | **Accordion** | `581:534` | ⏸️ Not analyzed | Expandable content panels |
| 14 | **Badge** | `0:1` | ✅ Partially analyzed | Simple badge variants (in initial analysis) |
| 15 | **Card** | `537:335` | ✅ Partially analyzed | Multiple card types (in initial analysis) |
| 16 | **Content Slider (Carousel)** | `22294:23289` | ⏸️ Not analyzed | Image/content carousel |
| 17 | **Dividers** | `583:1` | ⏸️ Not analyzed | Horizontal/vertical dividers |
| 18 | **Expand & collapse** | `271:0` | ⏸️ Not analyzed | Expand/collapse component |
| 19 | **Filters** | `9908:11419` | ⏸️ Not analyzed | Filter components |
| 20 | **Footer** | `552:351` | ⏸️ Not analyzed | Page footer patterns |
| 21 | **Header** | `2276:4048` | ⏸️ Not analyzed | Page header patterns |
| 22 | **Links** | `745:794` | ⏸️ Not analyzed | Link styles and states |
| 23 | **List** | `281:0` | ⏸️ Not analyzed | List patterns and styles |
| 24 | **Loading Bar** | `1042:410` | ⏸️ Not analyzed | Progress bar component |
| 25 | **Loading Spinner** | `1042:411` | ⏸️ Not analyzed | Loading indicator |
| 26 | **Menu (Flyout)** | `583:52` | ⏸️ Not analyzed | Dropdown menu component |
| 27 | **Modals** | `567:0` | ⏸️ Not analyzed | Dialog/modal windows |
| 28 | **Notification (header)** | `289:195` | ⏸️ Not analyzed | Header notification type |
| 29 | **Notification (modal)** | `597:0` | ⏸️ Not analyzed | Modal notification type |
| 30 | **Notification (inline)** | `7135:5949` | ⏸️ Not analyzed | Inline notification type |
| 31 | **Numeric Stepper** | `609:358` | ⏸️ Not analyzed | Number input with +/- buttons |
| 32 | **Picker (color)** | `1046:257` | ⏸️ Not analyzed | Color picker component |
| 33 | **Picker (date)** | `298:0` | ⏸️ Not analyzed | Date picker component |
| 34 | **Picker (option)** | `302:2` | ⏸️ Not analyzed | Option picker component |
| 35 | **Progress Stepper** | `371:228` | ⏸️ Not analyzed | Multi-step progress indicator |
| 36 | **Search** | `313:0` | ⏸️ Not analyzed | Search input component |
| 37 | **Scroll to top** | `568:30` | ⏸️ Not analyzed | Scroll button component |
| 38 | **Show more** | `1046:408` | ⏸️ Not analyzed | Expand/collapse component |
| 39 | **Sliders** | `600:608` | ⏸️ Not analyzed | Range slider component |
| 40 | **Status Indicator** | `32216:30316` | ⏸️ Not analyzed | Status dots/badges |
| 41 | **Stickers** | `318:228` | ⏸️ Not analyzed | Decorative stickers |
| 42 | **Swisscom Logo** | `266:37` | ⏸️ Not analyzed | Brand logo variants |
| 43 | **Tables** | `609:639` | ⏸️ Not analyzed | Data table component |
| 44 | **Tabs** | `559:0` | ⏸️ Not analyzed | Tab navigation component |
| 45 | **Tags** | `23103:56397` | ⏸️ Not analyzed | Tag/chip components |
| 46 | **Teaser** | `19549:21584` | ⏸️ Not analyzed | Promotional teaser cards |
| 47 | **Toast** | `31541:2` | ⏸️ Not analyzed | Toast notification |
| 48 | **Tooltip** | `603:608` | ⏸️ Not analyzed | Hover tooltip component |
| 49 | **Tour** | `37418:122` | ⏸️ Not analyzed | Product tour component |

---

### 🗂️ Special Sections

| # | Page Name | Node ID | Status | Notes |
|---|-----------|---------|--------|-------|
| 50 | **Deprecated** | `53958:2112` | ⏭️ Separator | Empty page used only to separate deprecated pages below |
| 51 | **Toolbar (Deprecated)** | `609:432` | ⏸️ Not analyzed | Legacy - Non-Web Component |
| 52 | **Empty State (Deprecated)** | `1171:0` | ⏸️ Not analyzed | Legacy - Non-Web Component |
| 53 | **Charts (bar, pie) (Deprecated)** | `604:0` | ⏸️ Not analyzed | Legacy - Non-Web Component |
| 54 | **Countdown (Deprecated)** | `36689:62` | ⏸️ Not analyzed | Legacy - Non-Web Component |

---

## Analysis Coverage Statistics

### By Status

| Status | Count | Percentage |
|--------|-------|------------|
| ✅ Fully Analyzed | 10 pages | 19% |
| ✅ Partially Analyzed | 2 pages | 4% |
| ⏸️ Not Yet Analyzed | 40 pages | 74% |
| ⏭️ Skipped (Cover + Separator) | 2 pages | 4% |
| 🗂️ Special/Legacy | 4 pages | 7% |
| **Total** | **58 pages** | **100%** |

### By Category

| Category | Total | Analyzed | Remaining |
|----------|-------|----------|-----------|
| **Foundation** | 6 | 4 (67%) | 2 |
| **Core Components** | 6 | 6 (100%) | 0 |
| **Additional Components** | 35 | 2 partial (6%) | 33 |
| **Special/Legacy** | 4 | 0 (0%) | 4 |
| **Other** | 1 | 0 (0%) | 1 |
| **Total** | **57** | **12** | **45** |

---

## Priority Tiers for Future Analysis

### TIER 1: Foundation ✅ COMPLETE (4/4)
- ✅ Typography
- ✅ Colors
- ✅ Grid
- ✅ Icons

### TIER 2: Core Form Components ✅ COMPLETE (6/6)
- ✅ Button
- ✅ Input Fields
- ✅ Checkbox
- ✅ Radio Button
- ✅ Dropdown
- ✅ Switch

### TIER 3: Important UI Patterns (0/6)
Recommended for next analysis phase:
- ⏸️ Header
- ⏸️ Footer
- ⏸️ Modals
- ⏸️ Tabs
- ⏸️ Tables
- ⏸️ Notification

### TIER 4: Additional Components (0/22)
Lower priority:
- ⏸️ Accordion
- ⏸️ Card (expand beyond initial analysis)
- ⏸️ Content Slider
- ⏸️ Menu (Flyout)
- ⏸️ Loading (Bar + Spinner)
- ⏸️ Progress Stepper
- ⏸️ Tooltip
- ⏸️ Toast
- ⏸️ [... 14 more components]

### TIER 5: Special/Legacy (0/4)
Optional analysis:
- ⏸️ Deprecated components (document what NOT to use) - 4 pages
- ⏭️ "Deprecated" separator page (empty, skip)
- ⏸️ Legacy non-Web Components

---

## How to Access Pages via MCP

### Getting Metadata for a Specific Page

```typescript
// Use the node ID from the table above
mcp_Figma_Desktop_get_metadata({
  nodeId: "51859:1065",  // Colors page
  clientLanguages: "typescript,javascript",
  clientFrameworks: "web-components"
})
```

### Extracting Node IDs from URLs

Figma URLs have this format:
```
https://www.figma.com/design/[fileKey]/[fileName]?node-id=[nodeId]

Example:
https://www.figma.com/design/fJcQzJgf6IRQQxz9A6DwHt/SDX-Components?node-id=51859-1065

Extract: 51859-1065 → Convert to: 51859:1065 (replace - with :)
```

---

## Complete Node ID Reference

All 53 pages with their node IDs for programmatic access:

| Page | Node ID | URL |
|------|---------|-----|
| Typography | `51859:1064` | `?node-id=51859-1064` |
| Colors | `51859:1065` | `?node-id=51859-1065` |
| Icons | `51859:1067` | `?node-id=51859-1067` |
| Grid | `51859:1068` | `?node-id=51859-1068` |
| Utils | `8071:8458` | `?node-id=8071-8458` |
| Accordion | `581:534` | `?node-id=581-534` |
| Badges | `0:1` | `?node-id=0-1` |
| Button | `6:19` | `?node-id=6-19` |
| Cards | `537:335` | `?node-id=537-335` |
| Input Fields | `226:278` | `?node-id=226-278` |
| Checkbox | `9:25` | `?node-id=9-25` |
| Radio Button | `9:26` | `?node-id=9-26` |
| Dropdown | `10:111` | `?node-id=10-111` |
| Switch | `583:65` | `?node-id=583-65` |
| Content Slider (Carousel) | `22294:23289` | `?node-id=22294-23289` |
| Dividers | `583:1` | `?node-id=583-1` |
| Expand & collapse | `271:0` | `?node-id=271-0` |
| Filters | `9908:11419` | `?node-id=9908-11419` |
| Footer | `552:351` | `?node-id=552-351` |
| Header | `2276:4048` | `?node-id=2276-4048` |
| Links | `745:794` | `?node-id=745-794` |
| List | `281:0` | `?node-id=281-0` |
| Loading Bar | `1042:410` | `?node-id=1042-410` |
| Loading Spinner | `1042:411` | `?node-id=1042-411` |
| Menu (Flyout) | `583:52` | `?node-id=583-52` |
| Modals | `567:0` | `?node-id=567-0` |
| Notification (header) | `289:195` | `?node-id=289-195` |
| Notification (modal) | `597:0` | `?node-id=597-0` |
| Notification (inline) | `7135:5949` | `?node-id=7135-5949` |
| Numeric stepper | `609:358` | `?node-id=609-358` |
| Picker (color) | `1046:257` | `?node-id=1046-257` |
| Picker (date) | `298:0` | `?node-id=298-0` |
| Picker (option) | `302:2` | `?node-id=302-2` |
| Progress Stepper | `371:228` | `?node-id=371-228` |
| Search | `313:0` | `?node-id=313-0` |
| Scroll to top | `568:30` | `?node-id=568-30` |
| Show more | `1046:408` | `?node-id=1046-408` |
| Sliders | `600:608` | `?node-id=600-608` |
| Status Indicator | `32216:30316` | `?node-id=32216-30316` |
| Stickers | `318:228` | `?node-id=318-228` |
| Swisscom Logo | `266:37` | `?node-id=266-37` |
| Tables | `609:639` | `?node-id=609-639` |
| Tabs | `559:0` | `?node-id=559-0` |
| Tags | `23103:56397` | `?node-id=23103-56397` |
| Teaser | `19549:21584` | `?node-id=19549-21584` |
| Toast | `31541:2` | `?node-id=31541-2` |
| Tooltip | `603:608` | `?node-id=603-608` |
| Tour | `37418:122` | `?node-id=37418-122` |
| Deprecated (Separator) | `53958:2112` | `?node-id=53958-2112` | Empty separator page |
| Toolbar (Deprecated) | `609:432` | `?node-id=609-432` |
| Empty State (Deprecated) | `1171:0` | `?node-id=1171-0` |
| Charts (bar, pie) (Deprecated) | `604:0` | `?node-id=604-0` |
| Countdown (Deprecated) | `36689:62` | `?node-id=36689-62` |

---

## Recommendation

**Current Status**: 19% of file analyzed (10/53 pages)

**Sufficient for testing?** ✅ YES
- Foundation fully covered (tokens, colors, typography, grid, icons)
- Core form components complete
- 80+ tokens extracted
- Critical issues identified

**Next Step**: Proceed to GitHub repository analysis rather than analyzing more Figma pages.

**Rationale**:
1. We have enough token samples to compare with code
2. Core components covered
3. Diminishing returns on additional Figma analysis
4. Need to verify Figma tokens match actual code tokens
5. Component naming verification is higher priority

**If you still want more Figma analysis**: Recommend TIER 3 (Header, Footer, Modals, Tabs, Tables, Notification) - ~2-3 hours effort.

---

## MCP Limitations Discovered

The Figma MCP server (`mcp_Figma_Desktop_get_metadata`) does not provide:
- ❌ List all pages function
- ❌ File structure overview
- ❌ Page navigation without node IDs
- ✅ Can access specific pages if you know the node ID
- ✅ Can extract design/code from nodes
- ✅ Can get variable definitions
- ✅ Can generate screenshots

**Workaround**: Use Figma UI to identify page node IDs, then query via MCP.

---

**Last Updated**: December 2024  
**Total Pages**: 53 (excluding Cover page)  
**Analyzed**: 10 (19%)  
**Remaining**: 43 (81%)  
**All Page Names Identified**: ✅ Complete










