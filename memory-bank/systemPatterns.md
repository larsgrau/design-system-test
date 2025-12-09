# System Patterns

## Testing Methodology

### Three-Way Comparison Pattern
The core pattern for gap detection:

```
┌─────────────┐
│   Figma     │ ← Design Truth (Intent)
│   Design    │
└──────┬──────┘
       │
       ├─────────────────────────────┐
       │                             │
       ▼                             ▼
┌─────────────┐              ┌─────────────┐
│  Existing   │              │     AI      │
│  Code Impl  │              │  Generated  │
└──────┬──────┘              └──────┬──────┘
       │                            │
       └──────────┬─────────────────┘
                  │
                  ▼
           ┌─────────────┐
           │ Gap Analysis│
           └──────┬──────┘
                  │
                  ▼
           ┌─────────────┐
           │Gap Report + │
           │Recommendations│
           └─────────────┘
```

### Test Scenario Structure
Each test scenario contains:
```
test-scenarios/
  {version-name}/
    {scenario-id}/
      input/
        figma-export.png          # Design reference
        specification.md          # UI requirements/description
        prompt.md                 # Exact prompt given to AI
      reference/
        existing-code/            # Current production implementation
      ai-generated/
        code/                     # AI's implementation
        metadata.json             # Generation context (AI version, date, etc.)
      design-systems/{design-system-name}/analysis/
        automated-findings.json   # Automated detection results
        manual-review.md          # Human reviewer notes
      report/
        gap-report.md            # Final gap analysis
```

## Gap Detection Patterns

### 1. Token Misuse Detection
**Pattern**: Find hardcoded values that should use design tokens

```javascript
// Automated checks:
- Scan for hex colors: /#[0-9A-Fa-f]{3,6}/
- Scan for px values: /\d+px/
- Compare against token definitions
- Flag direct values when tokens exist
```

**Example Finding**:
```
❌ Found: color: #0066CC
✓ Should be: color: var(--color-action-primary)
Category: Token Misuse
Impact: High (consistency & maintainability)
```

### 2. Component Import Detection
**Pattern**: Verify proper component usage

```javascript
// Automated checks:
- Detect design system component tags (pattern varies by system)
- Check for proper imports
- Flag custom implementations of standard components
- Verify component is from design system package
```

**Example Finding**:
```
❌ Found: Custom <button> implementation
✓ Should use: <design-system-button>
Category: Component Reinvention
Impact: High (maintenance & consistency)
```

### 3. Pattern Violation Detection
**Pattern**: Validate spacing, layout, typography patterns

```javascript
// Automated checks:
- Compare spacing values against token system
- Verify grid/layout classes (.row, .col)
- Check typography hierarchy usage
- Validate naming conventions
```

**Example Finding**:
```
❌ Found: margin: 16px
✓ Should be: margin: var(--space-4)
Category: Pattern Violation
Impact: Medium (design consistency)
```

### 4. Accessibility Checks
**Pattern**: Ensure accessible implementation

```javascript
// Automated checks:
- Check for aria-* attributes
- Verify semantic HTML structure
- Check for keyboard navigation attributes
- Validate focus management
- Check color contrast ratios
```

**Example Finding**:
```
❌ Missing: aria-label on icon button
✓ Required for: Screen reader accessibility
Category: Accessibility Gap
Impact: Critical (WCAG compliance)
```

### 5. Architecture Pattern Validation
**Pattern**: Match design system's implementation style

```javascript
// Automated checks:
- Detect styling approach (inline vs classes vs CSS-in-JS)
- Verify proper design system scope (varies by system)
- Check for framework-specific best practices
- Validate file structure patterns
```

## Phased Testing Strategy

### Phase 1: Foundation (Tokens)
**Focus**: Design token comprehension
- Test: Generate simple components using only tokens
- Validate: Token usage, semantic naming understanding
- Output: Foundation readiness score

### Phase 2: Core Components
**Focus**: Component library usage
- Test: Build UIs using documented components
- Validate: Proper imports, configuration, composition
- Output: Component discoverability score

### Phase 3: Complete System
**Focus**: Full design system application
- Test: Reproduce complex production UIs
- Validate: All patterns, accessibility, architecture
- Output: Comprehensive readiness assessment

## Version Control Pattern

### Named Versions
Each test run gets a named version for tracking:
```
versions/
  baseline-2024-12/          # Initial assessment
  post-doc-improvements/     # After documentation updates
  post-token-refactor/       # After token system changes
  mcp-integration/           # After MCP server added
```

### Version Metadata
```json
{
  "version_name": "baseline-2024-12",
  "date": "2024-12-03",
  "design_system_version": "1.0.0",
  "ai_tool": "Cursor",
  "ai_model": "claude-sonnet-4",
  "test_scenarios": [
    "button-variants",
    "form-layout",
    "navigation-menu"
  ],
  "overall_scores": {
    "token_usage": 45,
    "component_usage": 60,
    "pattern_compliance": 50,
    "accessibility": 40,
    "architecture": 55
  }
}
```

## Report Generation Pattern

### Gap Report Structure
```markdown
# Design System AI Readiness Gap Report
Version: {version-name}
Date: {date}

## Executive Summary
- Overall readiness score
- Key findings
- Priority recommendations

## Detailed Findings

### 1. Token Misuse
- Number of instances
- Specific examples with code
- Impact assessment

### 2. Component Reinvention
...

## Recommendations

### Priority 1: Critical
1. [Specific actionable improvement]
2. [Expected impact]

### Priority 2: High
...

## Test Scenarios
- Links to specific test cases
- Reproducibility information
```

## Automation Architecture

```
Test Runner
    ↓
Scenario Loader → AI Generation → Code Analyzer
                                        ↓
                                   Findings DB
                                        ↓
                      Manual Review ← Automated Rules
                                        ↓
                                  Report Generator
                                        ↓
                              Markdown + Metadata Output
```

