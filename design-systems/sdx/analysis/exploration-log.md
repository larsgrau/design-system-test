# SDX Figma File - Systematic Exploration Log

**Date**: December 3, 2024  
**File**: https://www.figma.com/design/fJcQzJgf6IRQQxz9A6DwHt/SDX-Components

## Exploration Process

### Method
Using Figma MCP server to systematically explore:
1. Identify all pages/canvases
2. Document component structure on each page
3. Extract design tokens from representative components
4. Compare patterns across components

---

## Pages Discovered

### Page 1: Badges (Canvas 0:1)
**Components Found**:
- Badge Basic (9863:11450)
- Badge Icon (9863:11458)
  - state=default (9863:11467)
  - state=hover (15510:24356)

**Variants**:
- Light/Dark themes
- States: default, hover

**Frame Structure**:
- Light frames: 41370:20064, 41370:20125
- Dark frames: 41370:20066, 41370:20127

---

### Page 2: Cards (Canvas 537:335)
**Components Found**:
- Card_default (8071:8575)
- Card_image (12317:22996)
- Card_notification (8071:8796)
- Card_colour (8071:8663)
- Card_interaction (21076:39597)
- Split Card (20198:21535)

**Variants**:
- Light/Dark themes
- Desktop/Mobile devices
- Default/Hover states
- Default/Small sizes
- Colors: Horizon, Blue, Orchid
- Types: Text only, With Icon, With Image

---

## Exploration Complete

### Pages Accessible via MCP
1. **Cover** (1550:3005) - Title page
2. **Badges** (0:1) - Badge components
3. **Cards** (537:335) - Card components

**Note**: MCP server requires knowing specific node IDs to explore pages. Without a complete page list, systematic exploration is limited to components we can discover through known node IDs.

---

## Components Analyzed in Detail

### From Badges Page
1. Badge Basic (9863:11450) ✅
2. Badge Icon state=default (9863:11467)

### From Cards Page
1. Card_default Desktop (8071:8574) ✅
2. Card_default Mobile (44736:740) ✅
3. Card_image (8071:8608) ✅
4. Card_colour Horizon (8071:8664) ✅
5. Card_interaction (21076:39598) ✅
6. Split Card Desktop (20198:21538) ✅

**Total Components Analyzed**: 8 components
**Token Extraction**: Successful from all components

---

## Key Discoveries

### 1. Multiple Token Systems
Found **3 distinct token naming systems**:
- Primary: `{category}/{scale}` or `{category}/{subcategory}/{variant}`
- SDX-prefixed: `sdx/{domain}/{property}/{variant}`
- Legacy: `{category}_old/{system}/{scale}`

### 2. Token Inconsistencies
- Surface colors: `surface/ui/01` vs `surface/ui/light/01` (both #ffffff)
- Border colors: `borderColor/ui/02` vs `borderColor/neutral/02` (both #cecdd3)
- Typography: Two complete systems exist in parallel

### 3. Device-Responsive Patterns
- Desktop uses `padding/4` (24px)
- Mobile uses `padding/3` (16px)
- Clear responsive scaling pattern

### 4. Composite Tokens
Found 2 composite typography tokens that reference multiple individual tokens:
- `heading/M` 
- `SDX/H2/Desktop`

### 5. Total Unique Tokens: 48
- Colors: 11 tokens
- Spacing: 7 tokens (including 1 legacy)
- Typography: 23 tokens (2 systems, 2 composites)
- Border Radius: 2 tokens
- Other: 5 tokens

---

## Critical Findings for AI Testing

### High-Priority Issues
1. **Token System Confusion**: AI may not know which system to use
2. **Variant Ambiguity**: Multiple tokens for same value with different names
3. **Legacy Token Trap**: AI might use deprecated `space_old/*` tokens
4. **Composite Token Awareness**: AI may not know composite tokens exist
5. **Device Scaling**: AI may not apply responsive token scaling

### Test Scenario Priorities
1. Token system selection (mixing systems inappropriately)
2. Semantic token choice (correct variant for context)
3. Legacy token avoidance
4. Composite token usage
5. Responsive/device-aware token selection

---

## Complete Analysis
See [token-inventory.md](./token-inventory.md) for:
- Complete token list with values
- Token pattern analysis
- Component-by-component comparison
- Consistency analysis
- Recommendations for SDX team

