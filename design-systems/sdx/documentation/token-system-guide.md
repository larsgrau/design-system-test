# SDX Token System Guide

**For AI Testing & Code Generation**  
**Version**: 1.0 (Based on Figma Analysis, Dec 3, 2024)  
**Status**: ⚠️ **UNVERIFIED** - Awaiting GitHub repository confirmation

---

## ⚠️ Important Notice

This guide is based on **Figma analysis only**. Token names and usage patterns **must be verified** against the actual SDX codebase once GitHub access is granted.

**Do not use for production code generation until verified.**

---

## Primary Token System (Recommended)

Based on our Figma analysis, use this token format:

### Format
```
{category}/{subcategory}/{variant}
```

### Transform to CSS Variables (Assumed)
```
Figma Token:    spacing/3
CSS Variable:   var(--spacing-3)
or possibly:    var(--sdx-spacing-3)
```

**⚠️ Needs verification from code repository.**

---

## Token Categories Quick Reference

### ✅ Spacing Tokens
```css
/* Use these: */
spacing/1 = 4px   → var(--spacing-1)
spacing/2 = 8px   → var(--spacing-2)
spacing/3 = 16px  → var(--spacing-3)
spacing/4 = 24px  → var(--spacing-4)

/* Padding variants: */
padding/1 = 4px   → var(--padding-1)
padding/3 = 16px  → var(--padding-3)
padding/4 = 24px  → var(--padding-4)
```

**Device-Responsive Pattern** (discovered in Figma):
- Desktop: `padding/4` (24px)
- Mobile: `padding/3` (16px)

---

### ✅ Typography Tokens

#### Individual Properties
```css
/* Font Sizes (Numeric) */
fontSize/12, /16, /18, /20, /24, /28, /32, /40, /48, /64, /80, /104

/* Font Sizes (Semantic) */
fontSize/heading/XS → 18px
fontSize/heading/S  → 20px
fontSize/heading/M  → 24px
fontSize/heading/L  → 32px
fontSize/heading/XL → 40px
fontSize/body/Base  → 16px

/* Line Heights (match font size scale) */
lineHeight/heading/M → 32px
lineHeight/body/Base → 24px

/* Letter Spacing */
letterspacing/heading/M → -0.2px
letterspacing/body/Base → 0

/* Font Weights */
fontWeight/semilight → 400
fontWeight/semibold  → 600
fontWeight/bold      → 700

/* Font Family */
fontFamily/TheSans → TheSans
```

#### Composite Styles (Preferred)
```css
/* Use composite tokens when available: */
heading/M        /* Full heading medium style */
heading/L        /* Full heading large style */
body/Base        /* Full body base style */
display/M        /* Full display medium style */
```

**CSS Usage** (assumed):
```css
/* Individual properties: */
font-size: var(--font-size-heading-m);
line-height: var(--line-height-heading-m);

/* Composite (if supported): */
font: var(--heading-m);
```

---

### ✅ Color Tokens

#### Brand Colors
```css
color/brand/navy → #001155
```

#### Surface Colors
```css
surface/ui/01               → #ffffff (base surface)
surface/ui/light/01         → #ffffff (light theme variant?)
surface/interaction/default → #0445c8 (interactive elements)
surface/error/emphasis      → #ff855a (error state)
```

**⚠️ Issue**: `surface/ui/01` vs `surface/ui/light/01` - unclear semantic difference.  
**Recommendation**: Use `surface/ui/01` until clarified.

#### Border Colors
```css
borderColor/ui/02               → #cecdd3
borderColor/neutral/01          → #55545b
borderColor/neutral/02          → #cecdd3 (same as ui/02?)
borderColor/interaction/default → #0445c8
```

**⚠️ Issue**: `borderColor/ui/02` vs `borderColor/neutral/02` - same value.  
**Recommendation**: Use `borderColor/neutral/02` (more semantic).

#### Text Colors
```css
textColor/body              → #222126 (primary text)
textColor/inactive          → #b7b6bc (disabled state)
textColor/neutral/default   → #55545b (secondary text?)
textColor/onEmphasis        → #ffffff (text on colored bg)
textColor/inverse           → #ffffff (inverted theme)
textColor/heading           → #001155 (headings)
```

**⚠️ Issue**: `textColor/body` vs `textColor/neutral/default` - unclear difference.  
**Recommendation**: Use `textColor/body` for main content.

---

### ✅ Border & Radius Tokens

```css
/* Border Radius */
borderRadius/small → 4px  (inputs, checkboxes)
borderRadius/large → 12px (cards, buttons)
borderRadius/full  → 80px (badges, pills)

/* Border Width */
borderWidth/thin → 1px
```

**⚠️ Missing**: `borderRadius/medium` (8px) exists only in SDX-prefixed system.  
**Recommendation**: Request SDX team to add `borderRadius/medium: 8px` to primary system.

---

## ❌ DO NOT USE (Until Verified)

### SDX-Prefixed System
```css
/* Avoid these tokens: */
sdx/font/size/h2
sdx/font/weight/h2
sdx/font/line-height/h2
sdx/border/radius-medium
sdx/forms/color/dropdown/option-hover

/* And composite styles: */
SDX/H2/Desktop
SDX/Standard/Desktop
```

**Reason**: Alternative token system found in some Figma components, but unclear if used in code.

---

### Legacy System
```css
/* Never use these: */
space_old/baseline/2 → Use spacing/3 instead
```

**Reason**: Marked as deprecated but still present in some Figma components.

---

## Token Usage Examples

### Example 1: Card Component
```css
.card {
  /* ✅ Good */
  padding: var(--padding-4);           /* 24px on desktop */
  border-radius: var(--border-radius-large); /* 12px */
  background: var(--surface-ui-01);    /* white */
  border: 1px solid var(--border-color-neutral-02);
  
  /* ❌ Bad */
  padding: 24px;                       /* Hardcoded */
  border-radius: 12px;                 /* Hardcoded */
  background: #ffffff;                 /* Hardcoded */
}

/* Responsive */
@media (max-width: 768px) {
  .card {
    padding: var(--padding-3);         /* 16px on mobile */
  }
}
```

---

### Example 2: Typography
```css
.heading {
  /* ✅ Good - Composite (if available) */
  font: var(--heading-m);
  color: var(--text-color-heading);
  
  /* ✅ Good - Individual properties */
  font-family: var(--font-family-thesans);
  font-size: var(--font-size-heading-m);
  line-height: var(--line-height-heading-m);
  letter-spacing: var(--letter-spacing-heading-m);
  font-weight: var(--font-weight-semibold);
  
  /* ❌ Bad */
  font-size: 24px;
  line-height: 32px;
  font-weight: 600;
}
```

---

### Example 3: Button Component
```css
.button {
  /* ✅ Good */
  padding: var(--spacing-2) var(--padding-4);
  border-radius: var(--border-radius-large);
  background: var(--surface-interaction-default);
  color: var(--text-color-on-emphasis);
  font-size: var(--font-size-body-base);
  
  /* ❌ Bad */
  padding: 8px 24px;
  border-radius: 12px;
  background: #0445c8;
  color: white;
}
```

---

## Testing Checklist

When testing AI-generated code:

### ✅ Token Usage
- [ ] All spacing uses `spacing/*` or `padding/*` tokens
- [ ] All typography uses `fontSize/*`, `lineHeight/*`, etc. tokens
- [ ] All colors use `color/*`, `surface/*`, `textColor/*`, `borderColor/*` tokens
- [ ] All border radii use `borderRadius/*` tokens
- [ ] No hardcoded values (px, rem, hex colors)

### ❌ Forbidden Patterns
- [ ] No `sdx/font/*` tokens (until verified)
- [ ] No `space_old/*` tokens (legacy)
- [ ] No hardcoded `24px`, `#ffffff`, `600` values
- [ ] No mixing of token systems

### ⚠️ Consistency Issues to Flag
- [ ] Using `surface/ui/01` instead of `surface/ui/light/01` (or vice versa)
- [ ] Using `borderColor/ui/02` instead of `borderColor/neutral/02`
- [ ] Using `textColor/body` instead of `textColor/neutral/default`
- [ ] Mixing primary and SDX-prefixed systems

---

## Verification Needed (After GitHub Access)

1. **CSS Variable Naming Convention**
   - [ ] Confirm transform: `spacing/3` → `--spacing-3` or `--sdx-spacing-3`?
   - [ ] Check for any prefix conventions
   - [ ] Verify kebab-case conversion

2. **Token System Used in Code**
   - [ ] Which token system does code actually use?
   - [ ] Are SDX-prefixed tokens in code or Figma-only?
   - [ ] Are composite tokens implemented?

3. **Token Values**
   - [ ] Verify all numeric values match Figma
   - [ ] Check for any additional tokens in code
   - [ ] Identify any Figma-only tokens

4. **Deprecated Tokens**
   - [ ] Are `space_old/*` tokens still in codebase?
   - [ ] Any migration warnings or comments?
   - [ ] Clear deprecation markers?

5. **Responsive Patterns**
   - [ ] Confirm desktop/mobile token switching pattern
   - [ ] Check for breakpoint definitions
   - [ ] Verify device-specific token usage

---

## Update History

| Version | Date | Changes | Status |
|---------|------|---------|--------|
| 1.0 | Dec 3, 2024 | Initial guide based on Figma analysis | ⚠️ Unverified |
| 1.1 | TBD | After GitHub verification | Pending |

---

## Related Documents

- [../../memory-bank/techContext.md](../../memory-bank/techContext.md) - Full technical context
- [../../docs/guides/token_documentation_requirements.md](../../docs/guides/token_documentation_requirements.md) - Recommendations for SDX team
- [../analysis/complete-analysis.md](../analysis/complete-analysis.md) - Complete Figma findings
- [../analysis/summary.md](../analysis/summary.md) - Executive summary

