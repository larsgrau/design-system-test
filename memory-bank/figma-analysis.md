# Figma Design System Analysis

## File Information
- **Figma File**: SDX Components
- **URL**: https://www.figma.com/design/fJcQzJgf6IRQQxz9A6DwHt/SDX-Components
- **Analysis Date**: December 3, 2024
- **MCP Server**: Connected and functional

## Component Structure Discovered

### Cards Page (Currently Analyzed)
The Cards page contains a comprehensive card component system with multiple variants:

#### Component Types
1. **Card_default** (Node: 8071:8575)
   - Basic card with content placeholder
   - Devices: Desktop, Mobile

2. **Card_image** (Node: 12317:22996)
   - Card with image support
   - Devices: Desktop, Mobile

3. **Card_notification** (Node: 8071:8796)
   - Types: Error, Warning, Info
   - Used for system notifications

4. **Card_colour** (Node: 8071:8663)
   - Color variants: Horizon, Blue, Orchid
   - States: Default, Hover
   - Devices: Desktop, Mobile

5. **Card_interaction** (Node: 21076:39597)
   - Types: Text only, With Icon, With Image
   - States: Default, Hover
   - Sizes: Default, Small
   - Devices: Desktop, Mobile

6. **Split Card** (Node: 20198:21535)
   - Special split layout variant
   - Devices: Desktop, Mobile

#### Variant System
- **Themes**: Light and Dark
- **Devices**: Desktop and Mobile  
- **States**: Default, Hover
- **Sizes**: Default, Small
- **Colors**: Horizon, Blue, Orchid
- **Types**: Text only, With Icon, With Image

## Design Token Structure

### Token Categories Identified

#### 1. Color Tokens
```
color/brand/navy: #001155
surface/ui/01: #ffffff
borderColor/ui/02: #cecdd3
```

**Pattern**: `{category}/{subcategory}/{variant}`

#### 2. Typography Tokens
```
fontFamily/TheSans: TheSans
fontSize/heading/M: 24
fontWeight/semibold: 600
lineHeight/heading/M: 32
letterspacing/heading/M: -0.2
```

**Pattern**: `{property}/{category}/{size}`

**Composite Token**:
```
heading/M: Font(
  family: "fontFamily/TheSans",
  style: B6 SemiBold,
  size: fontSize/heading/M,
  weight: fontWeight/semibold,
  lineHeight: lineHeight/heading/M,
  letterSpacing: letterspacing/heading/M
)
```

#### 3. Spacing Tokens
```
padding/4: 24
spacing/4: 24
space_old/baseline/2: 16
```

**Pattern**: `{type}/{scale}` or `{type}/{system}/{scale}`

#### 4. Border Tokens
```
borderRadius/large: 12
```

**Pattern**: `{property}/{size}`

## Token Naming Conventions

### Observed Patterns
1. **Semantic Naming**: `color/brand/navy`, `surface/ui/01`
2. **Scale-based**: `padding/4`, `spacing/4`, `fontSize/heading/M`
3. **State-based**: `borderColor/ui/02`
4. **Legacy markers**: `space_old/baseline/2` (indicates migration in progress)

### Token Structure
```
{category}/{subcategory}/{variant|scale}
```

Examples:
- `color/brand/navy` → category: color, subcategory: brand, variant: navy
- `fontSize/heading/M` → category: fontSize, subcategory: heading, scale: M
- `padding/4` → category: padding, scale: 4

## Component Implementation Pattern

### Card Base Component Example

**Generated Structure** (from Figma MCP):
```jsx
<div className="content-stretch flex flex-col items-start relative size-full">
  <div className="
    bg-[var(--surface/ui/01,#ffffff)]
    border border-[var(--bordercolor/ui/02,#cecdd3)]
    px-[var(--padding/4,24px)]
    py-[var(--spacing/4,24px)]
    rounded-[var(--borderradius/large,12px)]
    gap-[var(--space_old/baseline/2,16px)]
  ">
    <p className="
      font-[family-name:var(--fontfamily/TheSans,'TheSans:B6_SemiBold',sans-serif)]
      text-[length:var(--fontsize/heading/m,24px)]
      leading-[var(--lineheight/heading/m,32px)]
      tracking-[var(--letterspacing/heading/m,-0.2px)]
      text-[color:var(--color/brand/navy,#001155)]
    ">
      [-- PLACEHOLDER --]
    </p>
  </div>
</div>
```

**Key Observation**: Figma generates CSS variables with fallback values:
- Format: `var(--token-name, fallback-value)`
- Example: `var(--padding/4, 24px)`

## Implications for AI Testing

### What This Tells Us

#### 1. Token Complexity
The design system has **multi-level token structure** (category/subcategory/variant), which may be challenging for AI to discover and apply correctly without proper documentation.

#### 2. Token Fallbacks
Figma includes fallback values in CSS variables, which could lead AI to:
- Use the fallback hardcoded value instead of the variable
- Not understand the semantic meaning of tokens

#### 3. Legacy Tokens
Presence of `space_old` suggests the design system is evolving. AI needs to know:
- Which tokens are current vs deprecated
- Migration paths from old to new tokens

#### 4. Composite Tokens
The `heading/M` composite token shows sophisticated token relationships. AI needs to understand:
- When to use composite tokens vs individual tokens
- How composite tokens map to implementation

### Test Scenario Ideas

Based on this analysis, we should create test scenarios that check:

1. **Token Discovery**: Can AI find and use `padding/4` instead of hardcoding `24px`?
2. **Token Semantics**: Does AI understand `color/brand/navy` is for brand elements, not just "a navy color"?
3. **Token Hierarchy**: Does AI use the correct token level (e.g., `heading/M` vs individual font tokens)?
4. **Legacy Handling**: Does AI use `spacing/4` instead of deprecated `space_old/baseline/2`?
5. **Composite Tokens**: Can AI properly apply typography composite tokens?

## Next Steps for Analysis

### Pages to Explore
We've only seen the Cards page. Need to explore:
- [ ] Buttons
- [ ] Forms/Inputs
- [ ] Navigation components
- [ ] Typography system
- [ ] Color palette
- [ ] Spacing/layout system
- [ ] Icons

### Token Extraction
- [ ] Extract complete token list from Figma variables
- [ ] Map Figma tokens to SDX code implementation
- [ ] Identify any mismatches between design and code tokens
- [ ] Document token usage patterns across components

### Component Inventory
- [ ] Create complete list of available components
- [ ] Document component variants and props
- [ ] Identify component naming conventions
- [ ] Map Figma component names to code component names (e.g., `Card_default` → `<sdx-card>`)

## Comprehensive Analysis Complete ✅

**Date**: December 3, 2024

### Components Analyzed
- **8 components** across Badges and Cards pages
- **48 unique tokens** discovered
- **3 token systems** identified
- **8 consistency issues** found

### Key Files Generated
1. **[figma-exploration-log.md](../analysis/figma-exploration-log.md)** - Systematic exploration process
2. **[comprehensive-token-inventory.md](../analysis/comprehensive-token-inventory.md)** - Complete token analysis (detailed)

### Major Findings

#### 1. Multiple Token Systems Co-exist ⚠️
**Three distinct systems found**:
- **Primary**: `padding/4`, `color/brand/navy` (most common)
- **SDX-prefixed**: `sdx/font/size/h2`, `sdx/forms/color/dropdown/option-hover`
- **Legacy**: `space_old/baseline/2` (marked deprecated)

**Problem**: AI won't know which system to use without guidance.

#### 2. Token Name Inconsistencies ⚠️
Same values, different token names:
- `surface/ui/01` vs `surface/ui/light/01` (both = #ffffff)
- `borderColor/ui/02` vs `borderColor/neutral/02` (both = #cecdd3)
- `fontFamily/TheSans` vs `sdx/font/family/thesans` (both = TheSans)

**Problem**: AI might pick wrong variant or mix inconsistently.

#### 3. Typography Has Dual Systems 📚
**System A** (shorter): `fontSize/heading/M`, composite: `heading/M`  
**System B** (SDX): `sdx/font/size/h2`, composite: `SDX/H2/Desktop`

Different components use different systems with no clear pattern.

**Problem**: AI won't know which typography system to use.

#### 4. Device-Responsive Scaling Pattern Discovered ✅
- Desktop: `padding/4` (24px)
- Mobile: `padding/3` (16px)

Clear pattern: smaller screens = lower scale number.

**Problem**: AI may not discover this pattern without documentation.

#### 5. Composite Tokens Exist 💡
`heading/M` and `SDX/H2/Desktop` bundle multiple properties.

**Problem**: AI may not know composite tokens exist or when to use them vs individual tokens.

## Critical Questions for SDX Repository Analysis

1. **Token Format Mismatch**: Figma uses `/` in token names (e.g., `padding/4`). How does this translate in actual SDX code? CSS variables likely use `--padding-4` or similar.

2. **Token System Priority**: Are the 3 token systems equivalent? Is one being phased out? Which should AI prefer?

3. **Token Completeness**: We found 48 tokens from 8 components. How many total tokens exist in SDX?

4. **Token Variant Semantics**: What's the semantic difference between `surface/ui/01` and `surface/ui/light/01`? When to use which?

5. **Component Naming Mapping**: How do Figma names map to code?
   - `Card_default` → `<sdx-card>` ?
   - `Badge Basic` → `<sdx-badge>` ?

6. **Variant Properties Mapping**: How do Figma variants map to Web Component props/attributes?

7. **Legacy Migration Path**: Is `space_old/*` deprecated? What's the migration strategy?

8. **Composite Token Usage**: When should developers use composite tokens vs individual properties?

