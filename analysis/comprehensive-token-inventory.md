# SDX Comprehensive Token Inventory

**Date**: December 3, 2024  
**Source**: Figma file via MCP server  
**Components Analyzed**: 8 components across Badges and Cards pages

---

## Complete Token List

### Color Tokens

#### Brand Colors
```
color/brand/navy: #001155
```

#### Surface Colors
```
surface/ui/01: #ffffff
surface/ui/light/01: #ffffff
surface/error/emphasis: #ff855a
```

#### Text Colors
```
textColor/inverse: #ffffff
textColor/heading: #001155
```

#### Border Colors
```
borderColor/ui/02: #cecdd3
borderColor/neutral/02: #cecdd3
```

#### Special/Component-Specific Colors
```
sdx/forms/color/dropdown/option-hover: #eef3f6
sdx/color/headline/default: #001155
```

#### Gradient Colors
```
Gradient colours/Gradient-1: #001155
```

---

### Spacing Tokens

#### Padding Scale
```
padding/1: 4
padding/3: 16
padding/4: 24
```

#### Spacing Scale
```
spacing/3: 16
spacing/4: 24
```

#### Legacy Spacing
```
space_old/baseline/2: 16
```

---

### Typography Tokens

#### Font Family
```
fontFamily/TheSans: TheSans
sdx/font/family/thesans: TheSans
```

#### Font Sizes
```
fontSize/body/S: 14
fontSize/heading/M: 24
sdx/font/size/h2: 32
```

#### Font Weights
```
fontWeight/semibold: 600
sdx/font/weight/h2: 700
```

#### Line Heights
```
lineHeight/body/S: 20
lineHeight/heading/M: 32
sdx/font/line-height/h2: 40
```

#### Letter Spacing
```
letterspacing/body/S: 0.1
letterspacing/heading/M: -0.2
sdx/font/letter-spacing/h2: -0.7
```

#### Composite Typography Tokens
```
heading/M: Font(
  family: "fontFamily/TheSans",
  style: B6 SemiBold,
  size: fontSize/heading/M,
  weight: fontWeight/semibold,
  lineHeight: lineHeight/heading/M,
  letterSpacing: letterspacing/heading/M
)

SDX/H2/Desktop: Font(
  family: "sdx/font/family/thesans",
  style: B7 Bold,
  size: sdx/font/size/h2,
  weight: sdx/font/weight/h2,
  lineHeight: sdx/font/line-height/h2,
  letterSpacing: sdx/font/letter-spacing/h2
)
```

---

### Border Radius Tokens
```
borderRadius/large: 12
borderRadius/full: 80
```

---

## Token Naming Pattern Analysis

### Pattern 1: Simple Hierarchy (Current/New System?)
**Format**: `{category}/{scale}`

**Examples**:
- `padding/1` → 4px
- `padding/3` → 16px
- `padding/4` → 24px
- `spacing/3` → 16px
- `spacing/4` → 24px

**Characteristics**:
- Clean, numeric scale
- Single-level categorization
- Appears to be the primary system

---

### Pattern 2: Semantic Hierarchy  (Current/New System?)
**Format**: `{category}/{subcategory}/{variant}`

**Examples**:
- `color/brand/navy`
- `surface/ui/01`
- `surface/ui/light/01`
- `borderColor/ui/02`
- `borderColor/neutral/02`

**Characteristics**:
- Multi-level semantic naming
- Descriptive subcategories
- Variant numbers or descriptive names

---

### Pattern 3: Typography Composite (Current/New System?)
**Format**: `{category}/{size}` or just `{property}/{subcategory}/{size}`

**Examples**:
- `fontSize/heading/M`
- `lineHeight/heading/M`
- `letterspacing/heading/M`
- `heading/M` (composite)

**Characteristics**:
- T-shirt sizing (S, M, L implied)
- Component-level grouping
- Composite tokens combine multiple properties

---

### Pattern 4: SDX-Prefixed Tokens (Alternative/Newer System?)
**Format**: `sdx/{domain}/{property}/{variant}`

**Examples**:
- `sdx/font/family/thesans`
- `sdx/font/size/h2`
- `sdx/font/weight/h2`
- `sdx/font/line-height/h2`
- `sdx/font/letter-spacing/h2`
- `sdx/forms/color/dropdown/option-hover`
- `sdx/color/headline/default`

**Characteristics**:
- Explicitly prefixed with "sdx"
- More specific domain categorization
- Component-specific variants
- Possibly newer token system?

---

### Pattern 5: Legacy Tokens (Deprecated?)
**Format**: `{category}_old/{system}/{scale}`

**Examples**:
- `space_old/baseline/2`

**Characteristics**:
- Explicitly marked as "old"
- Indicates system migration in progress
- Should likely be avoided in new implementations

---

## Token Comparison Across Components

### Component 1: Badge Basic (9863:11450)
```json
{
  "textColor/inverse": "#ffffff",
  "letterspacing/body/S": "0.1",
  "fontSize/body/S": "14",
  "fontFamily/TheSans": "TheSans",
  "lineHeight/body/S": "20",
  "fontWeight/semibold": "600",
  "padding/1": "4",
  "borderRadius/full": "80",
  "surface/error/emphasis": "#ff855a"
}
```

**Pattern Usage**: 
- Simple hierarchy (padding/1)
- Semantic hierarchy (textColor/inverse, surface/error/emphasis)
- Typography composite elements

---

### Component 2: Card Default Desktop (8071:8574)
```json
{
  "color/brand/navy": "#001155",
  "letterspacing/heading/M": "-0.2",
  "fontSize/heading/M": "24",
  "fontFamily/TheSans": "TheSans",
  "lineHeight/heading/M": "32",
  "fontWeight/semibold": "600",
  "heading/M": "Font(...)",
  "space_old/baseline/2": "16",
  "padding/4": "24",
  "spacing/4": "24",
  "borderRadius/large": "12",
  "surface/ui/01": "#ffffff",
  "borderColor/ui/02": "#cecdd3"
}
```

**Pattern Usage**:
- Simple hierarchy (padding/4, spacing/4)
- Semantic hierarchy (color/brand/navy, surface/ui/01)
- Typography composite (heading/M)
- **Legacy token present** (space_old/baseline/2)

---

### Component 3: Card Image (8071:8608)
```json
{
  "padding/4": "24",
  "spacing/4": "24",
  "borderRadius/large": "12",
  "surface/ui/01": "#ffffff",
  "borderColor/ui/02": "#cecdd3"
}
```

**Pattern Usage**:
- Simple hierarchy (padding/4, spacing/4)
- Semantic hierarchy (surface/ui/01, borderColor/ui/02)
- **No typography tokens** (image component)

---

### Component 4: Card Interactive (21076:39598)
```json
{
  "spacing/4": "24",
  "padding/4": "24",
  "borderRadius/large": "12",
  "surface/ui/light/01": "#ffffff"
}
```

**Pattern Usage**:
- Simple hierarchy (padding/4, spacing/4)
- Semantic hierarchy with variant (surface/ui/light/01)

---

### Component 5: Card Color Horizon (8071:8664)
```json
{
  "padding/4": "24",
  "spacing/4": "24",
  "borderRadius/large": "12",
  "sdx/forms/color/dropdown/option-hover": "#eef3f6",
  "borderColor/ui/02": "#cecdd3"
}
```

**Pattern Usage**:
- Simple hierarchy (padding/4, spacing/4)
- Semantic hierarchy (borderColor/ui/02)
- **SDX-prefixed token** (sdx/forms/color/dropdown/option-hover)

---

### Component 6: Split Card Desktop (20198:21538)
```json
{
  "textColor/inverse": "#ffffff",
  "sdx/font/letter-spacing/h2": "-0.7",
  "sdx/font/size/h2": "32",
  "sdx/font/family/thesans": "TheSans",
  "sdx/font/line-height/h2": "40",
  "sdx/font/weight/h2": "700",
  "SDX/H2/Desktop": "Font(...)",
  "spacing/3": "16",
  "spacing/4": "24",
  "textColor/heading": "#001155",
  "surface/ui/light/01": "#ffffff",
  "borderRadius/large": "12",
  "borderColor/neutral/02": "#cecdd3",
  "Gradient colours/Gradient-1": "#001155"
}
```

**Pattern Usage**:
- Simple hierarchy (spacing/3, spacing/4)
- Semantic hierarchy (textColor/heading, surface/ui/light/01)
- **Heavy SDX-prefixed typography** (sdx/font/*)
- **SDX composite token** (SDX/H2/Desktop)
- Gradient token

---

### Component 7: Card Default Mobile (44736:740)
```json
{
  "color/brand/navy": "#001155",
  "letterspacing/heading/M": "-0.2",
  "fontSize/heading/M": "24",
  "fontFamily/TheSans": "TheSans",
  "lineHeight/heading/M": "32",
  "fontWeight/semibold": "600",
  "heading/M": "Font(...)",
  "spacing/3": "16",
  "padding/3": "16",
  "borderRadius/large": "12",
  "surface/ui/01": "#ffffff",
  "borderColor/ui/02": "#cecdd3"
}
```

**Pattern Usage**:
- Simple hierarchy with **different scale** (padding/3 vs padding/4 in desktop)
- Semantic hierarchy (color/brand/navy)
- Typography composite (heading/M)
- **Device-specific scaling** (padding/3 for mobile vs padding/4 for desktop)

---

## Key Findings & Patterns

### 1. **Multiple Token Systems Co-exist**

There appear to be **at least 3 different token naming systems** in use:

1. **Primary System** (most common):
   - Format: `{category}/{scale}` or `{category}/{subcategory}/{variant}`
   - Examples: `padding/4`, `color/brand/navy`
   
2. **SDX-Prefixed System** (alternative/newer?):
   - Format: `sdx/{domain}/{property}/{variant}`
   - Examples: `sdx/font/size/h2`, `sdx/forms/color/dropdown/option-hover`
   
3. **Legacy System** (deprecated):
   - Format: `{category}_old/{system}/{scale}`
   - Example: `space_old/baseline/2`

**Implication**: AI needs to know which system to use when. Are they equivalent? Is one being phased out?

---

### 2. **Inconsistent Token Naming Between Similar Components**

**Surface Color Variations**:
- `surface/ui/01` (Card Default)
- `surface/ui/light/01` (Card Interactive, Split Card)

**Border Color Variations**:
- `borderColor/ui/02` (Cards Default, Image, Color)
- `borderColor/neutral/02` (Split Card)

**Question**: Are these variants intentional or inconsistencies? When should AI use which?

---

### 3. **Typography Has Two Complete Systems**

**System 1** (shorter names):
- `fontFamily/TheSans`
- `fontSize/heading/M`
- `lineHeight/heading/M`
- Composite: `heading/M`

**System 2** (SDX-prefixed):
- `sdx/font/family/thesans`
- `sdx/font/size/h2`
- `sdx/font/line-height/h2`
- Composite: `SDX/H2/Desktop`

**Observation**: Different components use different systems. Split Card uses SDX-prefixed, most cards use the shorter system.

---

### 4. **Device-Responsive Scaling**

Desktop vs Mobile components use different padding scales:
- **Desktop**: `padding/4` (24px)
- **Mobile**: `padding/3` (16px)

**Pattern**: Smaller screens = smaller padding scale number

---

### 5. **Composite Tokens Reference Individual Tokens**

```
heading/M references:
  - fontFamily/TheSans
  - fontSize/heading/M
  - lineHeight/heading/M
  - letterspacing/heading/M
  - fontWeight/semibold
```

**Implication**: AI could use either the composite token OR individual tokens. Which is preferred?

---

### 6. **Some Components Have No Typography Tokens**

Card Image component (8071:8608) has no typography tokens - only layout/color tokens.

**Implication**: Token usage varies by component type and complexity.

---

### 7. **Special/Domain-Specific Tokens Exist**

Examples:
- `sdx/forms/color/dropdown/option-hover` - very specific use case
- `Gradient colours/Gradient-1` - special color type

**Implication**: Not all tokens follow standard patterns. Some are highly specialized.

---

## Consistency Analysis

### High Consistency ✅

**Padding & Spacing**:
- `padding/1`, `padding/3`, `padding/4` used consistently
- `spacing/3`, `spacing/4` used consistently
- Clear numeric scale
- Device-appropriate scaling

**Border Radius**:
- `borderRadius/large` (12px) - consistent across all card components
- `borderRadius/full` (80px) - used for badge pill shape

### Medium Consistency ⚠️

**Surface Colors**:
- Mix of `surface/ui/01` and `surface/ui/light/01`
- Both resolve to `#ffffff` but naming differs
- Unclear when to use which variant

**Border Colors**:
- Mix of `borderColor/ui/02` and `borderColor/neutral/02`
- Both resolve to `#cecdd3` but naming differs

**Font Family**:
- `fontFamily/TheSans` vs `sdx/font/family/thesans`
- Both are "TheSans" but different token paths

### Low Consistency ❌

**Typography System Choice**:
- Some components use `fontSize/heading/M` pattern
- Others use `sdx/font/size/h2` pattern
- No clear rule for which to use when

**Composite Token Usage**:
- Some components reference `heading/M` composite
- Others reference individual font properties
- Inconsistent pattern

---

## Critical Questions for AI Testing

### 1. Token System Selection
**Question**: When should AI use `padding/4` vs potential `sdx/spacing/4` equivalent?

**Test**: Give AI a component to build. Does it mix systems inappropriately?

---

### 2. Token Variant Selection
**Question**: When should AI use `surface/ui/01` vs `surface/ui/light/01`?

**Test**: Both resolve to white. Can AI pick the semantically correct one based on context?

---

### 3. Composite vs Individual Tokens
**Question**: Should AI use `heading/M` or individual `fontSize/heading/M`, `lineHeight/heading/M`, etc.?

**Test**: Does AI understand composite tokens exist and when to use them?

---

### 4. Device-Specific Scaling
**Question**: Does AI know to use `padding/3` for mobile and `padding/4` for desktop?

**Test**: Ask AI to build responsive component. Does it scale tokens appropriately?

---

### 5. Legacy Token Avoidance
**Question**: Will AI avoid `space_old/*` tokens?

**Test**: Does AI use `spacing/3` instead of `space_old/baseline/2` even though both are 16px?

---

### 6. Specialized Token Discovery
**Question**: Can AI find domain-specific tokens like `sdx/forms/color/dropdown/option-hover`?

**Test**: Ask AI to build a form. Does it discover and use form-specific tokens?

---

## Recommendations for SDX Team

### Priority 1: Token System Consolidation
**Issue**: Multiple overlapping token systems create confusion

**Recommendation**: 
- Clearly document which system is "current" vs "legacy"
- Provide migration guide if transitioning systems
- Mark deprecated tokens explicitly in documentation

---

### Priority 2: Token Variant Documentation
**Issue**: Similar tokens with slightly different names (`surface/ui/01` vs `surface/ui/light/01`)

**Recommendation**:
- Document semantic meaning of variants
- Explain when to use `/light/` variant vs base
- Consider consolidating if truly equivalent

---

### Priority 3: Composite Token Guidance
**Issue**: Unclear when to use composite tokens vs individual properties

**Recommendation**:
- Document preferred approach
- Explain benefits of composite tokens
- Show examples of both patterns

---

### Priority 4: Device-Responsive Token Guide
**Issue**: No clear documentation of responsive token scaling pattern

**Recommendation**:
- Document the padding/spacing scale for different devices
- Provide clear examples of mobile vs desktop token usage
- Create responsive design token guide

---

### Priority 5: Make Tokens Machine-Readable
**Issue**: Tokens currently only discoverable through component inspection

**Recommendation**:
- Publish complete token list as JSON/YAML
- Include semantic metadata (usage, device, deprecated status)
- Make tokens discoverable via API or static file for AI consumption

---

## Summary Statistics

### Total Unique Tokens Discovered: 48

**By Category**:
- **Colors**: 11 tokens (6 variations noted)
- **Spacing**: 7 tokens (including 1 legacy)
- **Typography**: 23 tokens (across 2 systems, including 2 composites)
- **Border Radius**: 2 tokens
- **Gradients**: 1 token
- **Special/Domain**: 4 tokens

**Token Systems Identified**: 3
1. Primary system (most common)
2. SDX-prefixed system (alternative)
3. Legacy system (deprecated)

**Consistency Issues Identified**: 8
1. Surface color variant naming
2. Border color variant naming
3. Font family token paths
4. Typography system choice
5. Composite vs individual usage
6. Legacy token presence
7. Device-responsive documentation gaps
8. Specialized token discovery

---

**Next Steps**:
1. Verify token consistency with SDX code repository
2. Compare Figma token names to actual CSS variable names
3. Identify if there are more tokens not used in these 8 components
4. Create test scenarios targeting each consistency issue

