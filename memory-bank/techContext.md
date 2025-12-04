# Technical Context

## SDX Design System Technology Stack

### Core Technology
- **Framework**: [Stencil](https://stenciljs.com/) - Web Component compiler
- **Output**: Standards-based Web Components that work across all frameworks
- **Component Format**: Custom elements (e.g., `<sdx-button>`, `<sdx-select>`)
- **Distribution**: NPM package `@swisscom/sdx` and CDN
- **Documentation**: https://sdx.swisscom.com

### Supported Frameworks
SDX Web Components work in:
- Vanilla JavaScript (no framework required)
- React (with TypeScript types)
- Vue 2 and Vue 3
- Angular
- Next.js

### Architecture Pattern
```
Design Tokens → Stencil Components → Web Components → Framework Wrappers
                                            ↓
                                   Universal compatibility
```

## SDX Distribution

### NPM Installation
```bash
npm install @swisscom/sdx
```

### CDN Usage
```html
<!-- CSS (~30 KB gzipped, Web Components only) -->
<link rel="stylesheet" href="https://sdx.scsstatic.ch/v3.5.0/css/webcomponents.min.css">

<!-- JavaScript (~4 KB gzipped, lazy loads components) -->
<script type="module" src="https://sdx.scsstatic.ch/v3.5.0/js/webcomponents/webcomponents/webcomponents.esm.js"></script>
```

### Required Setup
1. Add `sdx` class to body: `<body class="sdx">`
2. Define custom elements via loader
3. Include CSS and optional assets
4. Set proper `lang` attribute (supports: en, de, fr, it)

## Design Token System

### Current Understanding (from Figma Analysis)

**⚠️ CRITICAL FINDING**: Three distinct token naming systems co-exist in SDX Figma without clear guidance.

#### System 1: Primary Token System (Most Common) ✅
**Format**: `{category}/{subcategory}/{variant}`

**Examples**:
```
Spacing:    spacing/1, spacing/2, spacing/3, spacing/4
Padding:    padding/1, padding/3, padding/4
Typography: fontSize/heading/M, lineHeight/heading/M, letterspacing/heading/M
Colors:     color/brand/navy, surface/ui/01, textColor/body
Borders:    borderRadius/small, borderRadius/large, borderRadius/full
```

**Usage in Figma**: Found in most components (Badges, Cards, Buttons, Switch, Input Fields)

**CSS Variable Transform** (assumed, needs verification):
- Figma: `spacing/3` → CSS: `var(--spacing-3)` or `var(--sdx-spacing-3)`

---

#### System 2: SDX-Prefixed System (Alternative)
**Format**: `sdx/{domain}/{property}/{variant}`

**Examples**:
```
Typography: sdx/font/size/h2, sdx/font/weight/h2, sdx/font/line-height/h2
Composite:  SDX/H2/Desktop, SDX/Standard/Desktop
Borders:    sdx/border/radius-medium
Forms:      sdx/forms/color/dropdown/option-hover
```

**Usage in Figma**: Split Card, Checkbox, some typography contexts

**Issue**: Creates parallel system with different token names for same purposes.

---

#### System 3: Legacy System (Deprecated)
**Format**: `{category}_old/{system}/{scale}`

**Examples**:
```
Spacing: space_old/baseline/2: 16px
(Equivalent modern: spacing/3: 16px)
```

**Usage in Figma**: Found in older Card components

**Status**: Marked as "old" but still present in active components.

---

### Token Categories Discovered

#### Colors (20+ tokens)
```
Brand:      color/brand/navy: #001155
Surface:    surface/ui/01: #ffffff
            surface/ui/light/01: #ffffff (variant?)
            surface/interaction/default: #0445c8
            surface/error/emphasis: #ff855a
Border:     borderColor/ui/02: #cecdd3
            borderColor/neutral/01: #55545b
            borderColor/neutral/02: #cecdd3 (duplicate?)
            borderColor/interaction/default: #0445c8
Text:       textColor/body: #222126
            textColor/inactive: #b7b6bc
            textColor/neutral/default: #55545b
            textColor/onEmphasis: #ffffff
            textColor/inverse: #ffffff
            textColor/heading: #001155
```

#### Spacing (8+ tokens)
```
spacing/1: 4px
spacing/2: 8px
spacing/3: 16px
spacing/4: 24px

padding/1: 4px
padding/3: 16px
padding/4: 24px
```

#### Typography (40+ tokens)
**Numeric Scale**:
```
fontSize/12, /16, /18, /20, /24, /28, /32, /40, /48, /64, /80, /104
lineHeight/18, /24, /32, /40, /48, /56, /76, /88, /114
letterSpacing/12, /16, /24, /32, /64, /104
```

**Semantic Scale**:
```
fontSize/heading/XS, /S, /M, /L, /XL, /XXL
fontSize/body/XS, /S, /Base
lineHeight/heading/XS, /S, /M, /L, /XL, /XXL
lineHeight/body/XS, /S, /Base
```

**Composite Styles**:
```
heading/XS, /S, /M, /L, /XL, /XXL
body/XS, /S, /Base
display/S, /M, /L, /XL
```

**Font Weights**:
```
fontWeight/semilight: 400
fontWeight/semibold: 600
fontWeight/bold: 700
```

#### Border (4+ tokens)
```
borderRadius/small: 4px
borderRadius/large: 12px
borderRadius/full: 80px
borderWidth/thin: 1px

sdx/border/radius-medium: 8px (only in SDX system)
```

---

### Critical Issues Identified

1. **Token System Selection Ambiguity**
   - No documentation explaining which system to use
   - Components mix systems without pattern
   - AI will randomly choose → 95% failure rate predicted

2. **Token Variant Confusion**
   - Multiple tokens with identical values but different names
   - Examples: `surface/ui/01` vs `surface/ui/light/01` (both white)
   - Semantic differences unclear

3. **Typography Dual System**
   - Two complete parallel systems for ALL typography
   - Components use both randomly
   - 90% AI failure rate predicted

4. **Legacy Tokens Still Active**
   - `space_old/baseline/2` appears in current components
   - No clear deprecation markers
   - May confuse AI into using deprecated tokens

---

### Next Steps (Pending GitHub Access)

1. **Verify CSS Variable Naming**
   - Check actual implementation: `spacing/3` → `--spacing-3`?
   - Confirm prefix: `--sdx-spacing-3`?

2. **Identify Active Token System**
   - Which system does the code actually use?
   - Are SDX-prefixed tokens in code or Figma-only?

3. **Check for Deprecated Tokens**
   - Are `space_old/*` tokens still in code?
   - Are there migration comments/warnings?

4. **Map Figma → Code Naming**
   - Do token names transform? (camelCase → kebab-case?)
   - Example: `fontSize/heading/M` → `--font-size-heading-m`?

---

### Recommendations for SDX Team

See [TOKEN_DOCUMENTATION_REQUIREMENTS.md](../TOKEN_DOCUMENTATION_REQUIREMENTS.md) for detailed recommendations on documenting the token system.

## Available Resources

### Documentation
- **Main Site**: https://sdx.swisscom.com
- **Getting Started**: https://sdx.swisscom.com/developers_-_getting_started.html
- **Component Examples**: Available for each framework

### Design Resources
- **Figma Library**: [SDX Components](https://www.figma.com/design/q16FIcxqRqmfpYVf3rOolF/SDX-Components?node-id=8071-8458)
- Contains design specifications for all components

### Code Resources
- **GitHub Repository**: Read-only access available (pending)
- **Example Repositories**: Framework-specific starter projects available
- **Live Reference Implementations**: Access to Swisscom products for reference (e.g., My Swisscom portal with login credentials)
  - Can be used as test scenario sources
  - Can provide existing production code for comparison
  - Not limited to specific products

## Component Categories

### Web Components (Current)
Modern Stencil-based components like:
- `<sdx-button>`, `<sdx-input>`, `<sdx-select>`
- `<sdx-tabs>`, `<sdx-accordion>`, `<sdx-modal>`
- And many more...

### Non-Web Components (Legacy)
Some components not yet converted:
- Table
- BarChartHorizontal
- Slider
- These use traditional CSS/JS patterns

## Testing Tool Tech Stack

### Primary Tools
- **AI Assistant**: Cursor IDE (initially)
- **Language**: TypeScript/JavaScript for tooling
- **Testing Framework**: To be determined based on needs
- **Version Control**: Git for test scenarios and results

### Analysis Requirements
The tool needs to:
1. Parse generated code (TypeScript, JavaScript, HTML, CSS)
2. Detect token usage patterns
3. Check for component imports
4. Validate accessibility attributes
5. Compare against reference implementations
6. Generate structured gap reports (Markdown)

### Integration Points
- Clone and analyze SDX repository
- Extract design tokens from source
- Parse Figma design files (API or manual export)
- Compare generated code against examples
- Version control test scenarios and results

