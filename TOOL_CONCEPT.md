# SDX AI Readiness Testing Tool - Concept Document

## Executive Summary

This document outlines the concept for a testing tool that evaluates how well AI coding assistants understand and apply the SDX design system. The tool uses a three-way comparison methodology (Figma design → Existing implementation → AI-generated code) to identify gaps and generate actionable recommendations for improving SDX's AI-friendliness.

---

## 1. Problem Statement

### Current Challenge
As AI assistants become primary coding tools, design systems must be optimized for machine consumption, not just human documentation. When AI generates code using SDX, common failures occur:

- **Token Misuse**: Hardcoded values (`#0066CC`) instead of semantic tokens (`var(--color-action-primary)`)
- **Component Reinvention**: Custom implementations instead of using existing SDX components
- **Pattern Violations**: Non-standard spacing, layout, or architecture choices
- **Accessibility Gaps**: Missing ARIA labels, keyboard navigation, focus management
- **Architecture Mismatch**: Implementation styles that don't match SDX patterns

### Business Impact
- Inconsistent implementations across Swisscom products
- Technical debt from AI-generated code
- Maintenance burden from undocumented patterns
- Accessibility compliance risks
- Lost design system investment ROI
- SDX core team time spent fixing AI-generated code issues

---

## 2. Solution Overview

### Core Concept
**Three-Way Comparison Testing**

```
┌───────────────┐
│ Figma Design  │ ← Ground truth (design intent)
└───────┬───────┘
        │
        ├──────────────────────────────┐
        │                              │
        ▼                              ▼
┌───────────────┐            ┌─────────────────┐
│  Existing     │            │  AI-Generated   │
│  Production   │            │  Code           │
│  Code         │            │  (Cursor)       │
└───────┬───────┘            └────────┬────────┘
        │                             │
        └─────────────┬───────────────┘
                      │
                      ▼
              ┌───────────────┐
              │  Automated    │
              │  Analysis     │
              └───────┬───────┘
                      │
                      ▼
              ┌───────────────┐
              │  Manual       │
              │  Review       │
              └───────┬───────┘
                      │
                      ▼
              ┌───────────────┐
              │  Gap Report   │
              │  with         │
              │  Recommendations│
              └───────────────┘
```

### Key Differentiators
1. **Evidence-Based**: Real code comparisons, not theoretical assessments
2. **Reproducible**: Version-controlled test scenarios with named iterations
3. **Actionable**: Specific recommendations for SDX improvements
4. **Measurable**: Quantified scores track improvement over time
5. **Phased**: Incremental testing from tokens → components → full system

---

### Data Sources & Figma Access

**File-Based Approach for Testing**

All test scenarios use **static file-based Figma data** stored in version control. This ensures:
- **Reproducibility**: Same design data across all test runs
- **Version Control**: Track design changes over time with clear diffs
- **Offline Testing**: No dependency on Figma access or network connectivity
- **CI/CD Ready**: Tests can run in automated pipelines without external dependencies
- **Stable Comparisons**: Design data doesn't change between baseline and post-improvement test runs

**Figma Data Format**

Test scenarios include structured Figma exports in JSON format containing:
- Token definitions with metadata (name, value, category, system, status)
- Component specifications (name, variants, props, usage examples)
- Design specs for test scenarios (layout, spacing, typography, colors)
- Version/timestamp information
- Source reference (Figma file URL, export date)

**MCP as Optional Exploration Tool**

Figma MCP (Model Context Protocol) integration is **optional** and used only for:
- **Initial Discovery**: One-time exploration of Figma library structure
- **Data Extraction**: Initial export of tokens and components to structured format
- **Analysis**: Real-time queries during development and analysis phases

**Important**: MCP is **not used during test execution**. All test scenarios must have complete file-based data in the `reference/` directory. MCP is a convenience tool for initial setup and exploration, not a dependency for running tests.

---

## 3. Testing Methodology

### Phase 1: Foundation (Tokens)
**Objective**: Assess AI's understanding of design token system

**Test Scenarios**:
- Build simple components using only design tokens
- Create color palettes from semantic tokens
- Implement spacing and layout with token system

**Success Metrics**:
- % of values using tokens vs hardcoded
- Correct semantic token selection rate
- Token naming convention adherence

**Example Test**:
```
Input: "Create a primary button with standard padding and brand color"
Expected: Uses --color-action-primary, --space-3, etc.
Measure: Token usage rate and semantic correctness
```

### Phase 2: Core Components
**Objective**: Assess AI's ability to discover and use SDX components

**Test Scenarios**:
- Build common UI patterns (forms, navigation, cards)
- Compose complex components from SDX primitives
- Configure components with proper props/attributes

**Success Metrics**:
- % of SDX components used vs custom implementations
- Proper component import and usage
- Correct prop/attribute configuration

**Example Test**:
```
Input: "Create a form with text input, select dropdown, and submit button"
Expected: Uses <sdx-input>, <sdx-select>, <sdx-button>
Measure: Component discovery and usage accuracy
```

### Phase 3: Complete System
**Objective**: Assess full design system application in complex scenarios

**Test Scenarios**:
- Reproduce pages from real Swisscom products (e.g., My Swisscom, other internal tools)
- Build complex layouts with multiple patterns
- Implement accessible, production-ready UIs

**Success Metrics**:
- Overall pattern compliance score
- Accessibility compliance rate
- Architecture match percentage
- Visual similarity to reference design

**Example Test**:
```
Input: Screenshot + description of a complex Swisscom product page
Expected: Faithful reproduction using SDX components and patterns
Measure: Comprehensive gap analysis across all categories
```

---

## 4. Gap Detection Framework

### Automated Detection Rules

#### 1. Token Misuse Detection
```javascript
const tokenChecks = {
  colors: {
    pattern: /#[0-9A-Fa-f]{3,6}|rgb\(|rgba\(/,
    expected: /var\(--color-/,
    severity: 'high'
  },
  spacing: {
    pattern: /margin|padding:\s*\d+px/,
    expected: /var\(--space-/,
    severity: 'medium'
  },
  typography: {
    pattern: /font-size:\s*\d+px/,
    expected: /var\(--font-size-/,
    severity: 'medium'
  }
};
```

#### 2. Component Import Detection
```javascript
const componentChecks = {
  sdxImports: {
    pattern: /from ['"]@swisscom\/sdx['"]/,
    components: /<sdx-\w+/g,
    severity: 'high'
  },
  customImplementations: {
    pattern: /<button|<input|<select/,
    expectedAlternative: 'sdx-button|sdx-input|sdx-select',
    severity: 'high'
  }
};
```

#### 3. Pattern Validation
```javascript
const patternChecks = {
  layout: {
    expectedClasses: ['row', 'col', 'container'],
    sdxScope: /class=["'].*sdx.*["']/,
    severity: 'medium'
  },
  styling: {
    avoidInlineStyles: true,
    preferredApproach: 'CSS variables',
    severity: 'low'
  }
};
```

#### 4. Accessibility Checks
```javascript
const a11yChecks = {
  ariaLabels: {
    required: ['button[aria-label]', '[role]'],
    severity: 'critical'
  },
  semanticHTML: {
    preferredTags: ['header', 'nav', 'main', 'section'],
    severity: 'high'
  },
  keyboardNav: {
    attributes: ['tabindex', 'aria-describedby'],
    severity: 'critical'
  }
};
```

### Manual Review Checklist

**Visual Comparison**:
- [ ] Layout matches Figma design
- [ ] Spacing and proportions accurate
- [ ] Typography hierarchy correct
- [ ] Color usage semantically correct

**Functional Comparison**:
- [ ] Interactive states work (hover, focus, active)
- [ ] Components behave as documented
- [ ] Responsive behavior appropriate

**Architecture Review**:
- [ ] Code structure follows SDX patterns
- [ ] File organization logical
- [ ] Naming conventions consistent
- [ ] Comments and documentation adequate

**Accessibility Audit**:
- [ ] Keyboard navigation functional
- [ ] Screen reader compatibility
- [ ] Focus management appropriate
- [ ] ARIA attributes correct

---

## 5. Test Scenario Structure

### Directory Organization
```
test-scenarios/
├── versions/
│   ├── baseline-2024-12/
│   │   ├── metadata.json
│   │   ├── overall-report.md
│   │   └── scenarios/
│   │       ├── 001-button-variants/
│   │       ├── 002-form-layout/
│   │       └── 003-navigation-menu/
│   │
│   ├── post-doc-improvements/
│   │   └── ...
│   │
│   └── post-mcp-integration/
│       └── ...
│
└── templates/
    └── scenario-template/
```

### Individual Scenario Structure
```
001-button-variants/
├── input/
│   ├── design.png              # Figma export or screenshot
│   ├── specification.md        # What to build (description)
│   └── prompt.md               # Exact prompt given to AI
│
├── reference/
│   ├── figma-data.json         # Structured Figma export (tokens, components, specs)
│   ├── figma-specs.md          # Human-readable design specifications (derived from JSON)
│   └── existing-code/          # Production implementation
│       ├── component.tsx
│       └── styles.css
│
├── ai-generated/
│   ├── code/                   # AI's implementation
│   │   ├── component.tsx
│   │   └── styles.css
│   └── metadata.json           # Context (AI model, date, etc.)
│
├── analysis/
│   ├── automated-findings.json # Automated detection results
│   ├── manual-review.md        # Human reviewer notes
│   └── comparison-screenshots/ # Visual diffs if needed
│
└── report/
    └── gap-report.md           # Scenario-specific gap report
```

### Metadata Schema
```json
{
  "scenario_id": "001-button-variants",
  "version": "baseline-2024-12",
  "date_generated": "2024-12-03T10:30:00Z",
  "phase": "1-foundation",
  "sdx_version": "3.5.0",
  "ai_context": {
    "tool": "Cursor",
    "model": "claude-sonnet-4",
    "cursor_version": "0.42.0"
  },
  "test_type": "component-usage",
  "complexity": "simple",
  "reviewer": "larsen",
  "scores": {
    "token_usage": 45,
    "component_usage": 60,
    "pattern_compliance": 50,
    "accessibility": 40,
    "architecture": 55,
    "overall": 50
  }
}
```

---

## 6. Gap Report Format

### Structure
```markdown
# Gap Report: {Scenario Name}
**Version**: {version-name}  
**Date**: {date}  
**Phase**: {1-foundation | 2-components | 3-complete}  
**Overall Score**: {0-100}

---

## Executive Summary
Brief overview of test, key findings, and priority recommendations.

---

## Test Details

### Input
- **Design Reference**: [Link to Figma or screenshot]
- **Prompt Given**: [Exact prompt]
- **Expected Outcome**: [What good looks like]

### Comparison Sources
- **Figma Design**: [Link/screenshot]
- **Existing Implementation**: [Link to production code]
- **AI Generated**: [Link to generated code]

---

## Gap Analysis

### 1. Token Misuse (Score: X/100)

#### Findings
- **Found**: 12 instances of hardcoded colors
- **Expected**: Use of semantic color tokens

#### Examples

**❌ AI Generated**:
```css
.button {
  color: #0066CC;
  padding: 16px 24px;
}
```

**✅ Should Be**:
```css
.button {
  color: var(--color-action-primary);
  padding: var(--space-4) var(--space-6);
}
```

#### Impact
- **Severity**: High
- **Affects**: Consistency, maintainability, theme support
- **Effort to Fix**: Low (search/replace in generated code)

---

### 2. Component Reinvention (Score: X/100)

#### Findings
- **Found**: Custom button implementation
- **Expected**: Usage of `<sdx-button>`

#### Examples

**❌ AI Generated**:
```tsx
<button className="custom-btn" onClick={handleClick}>
  Click Me
</button>
```

**✅ Should Be**:
```tsx
<sdx-button theme="primary" onClick={handleClick}>
  Click Me
</sdx-button>
```

#### Impact
- **Severity**: Critical
- **Affects**: Component library adoption, maintenance
- **Effort to Fix**: Medium (component replacement)

---

### 3. Pattern Violations (Score: X/100)
[Similar structure...]

### 4. Accessibility Gaps (Score: X/100)
[Similar structure...]

### 5. Architecture Mismatch (Score: X/100)
[Similar structure...]

---

## Recommendations

### Priority 1: Critical (Do First)
1. **Improve Component Discoverability**
   - **Issue**: AI doesn't find `<sdx-button>` component
   - **Recommendation**: Add clear component index to documentation
   - **Expected Impact**: 40% improvement in component usage
   - **Effort**: Low (documentation update)

2. **Document Token System More Prominently**
   - **Issue**: AI uses hardcoded values instead of tokens
   - **Recommendation**: Create "Tokens First" guide in getting started
   - **Expected Impact**: 50% reduction in token misuse
   - **Effort**: Medium (documentation + examples)

### Priority 2: High (Do Soon)
[...]

### Priority 3: Medium (Nice to Have)
[...]

---

## Reproducibility

### Test Environment
- SDX Version: 3.5.0
- AI Tool: Cursor 0.42.0
- AI Model: Claude Sonnet 4
- Date: 2024-12-03

### Rerun Instructions
1. Use exact prompt from `input/prompt.md`
2. Compare against reference code in `reference/existing-code/`
3. Run automated analysis: `npm run analyze:scenario 001-button-variants`
4. Review findings and update scores

---

## Attachments
- [Figma Design Link]
- [Visual Comparison Screenshots]
- [Full Code Diff]
- [Automated Analysis JSON]
```

---

## 7. Tooling Architecture

### System Components

```
┌─────────────────────────────────────────────────────────┐
│                     Test Runner CLI                      │
│  Commands: init, run, analyze, report, compare          │
└────────────────────────┬────────────────────────────────┘
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        ▼                ▼                ▼
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│  Scenario    │  │    Code      │  │   Report     │
│  Manager     │  │   Analyzer   │  │  Generator   │
└──────┬───────┘  └──────┬───────┘  └──────┬───────┘
       │                 │                  │
       ▼                 ▼                  ▼
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│  Version     │  │   Finding    │  │  Comparison  │
│  Control     │  │   Store      │  │   Engine     │
└──────────────┘  └──────────────┘  └──────────────┘
```

### CLI Interface

```bash
# Initialize new test version
sdx-test init --version "baseline-2024-12"

# Create new test scenario
sdx-test scenario create \
  --id "001-button-variants" \
  --phase "1-foundation" \
  --design "./designs/buttons.png" \
  --prompt "Create all button variants from the design"

# Import Figma data from file
sdx-test import-figma \
  --scenario "001-button-variants" \
  --file "./figma-exports/buttons-export.json"
# Imports structured Figma data (tokens, components, specs) into scenario

# Export current Figma data for a scenario (if using MCP for extraction)
sdx-test export-figma \
  --scenario "001-button-variants" \
  --output "./figma-exports/"
# Exports current Figma data to structured JSON format

# Run AI generation (interactive)
sdx-test run --scenario "001-button-variants"
# This opens Cursor with the prompt, user does the vibe coding

# Analyze generated code
sdx-test analyze --scenario "001-button-variants"
# Runs automated detection, outputs findings JSON

# Manual review (opens editor)
sdx-test review --scenario "001-button-variants"
# Opens manual review checklist in editor

# Generate gap report
sdx-test report --scenario "001-button-variants"
# Combines automated + manual findings into gap report

# Generate version summary
sdx-test report --version "baseline-2024-12"
# Aggregates all scenarios into version-level report

# Compare versions
sdx-test compare \
  --baseline "baseline-2024-12" \
  --current "post-doc-improvements"
# Shows improvement metrics across versions
```

### Code Analyzer Implementation

**Technology**: Node.js / TypeScript

**Key Modules**:
1. **Parser**: AST parsing for JavaScript/TypeScript/HTML/CSS
2. **Token Detector**: Regex + AST patterns for token usage
3. **Component Detector**: Import analysis + tag detection
4. **Pattern Validator**: Rule-based pattern matching
5. **A11y Checker**: ARIA attribute validation
6. **Scorer**: Weighted scoring algorithm

**Example Detection Logic**:
```typescript
interface Finding {
  category: 'token-misuse' | 'component-reinvention' | 'pattern-violation' | 'a11y-gap' | 'architecture-mismatch';
  severity: 'critical' | 'high' | 'medium' | 'low';
  location: {
    file: string;
    line: number;
    column: number;
  };
  found: string;
  expected: string;
  impact: string;
  recommendation: string;
}

async function analyzeCode(scenarioPath: string): Promise<Finding[]> {
  const findings: Finding[] = [];
  
  // Load AI-generated code
  const generatedCode = await loadGeneratedCode(scenarioPath);
  
  // Load SDX reference (tokens, components)
  const sdxReference = await loadSDXReference();
  
  // Run detection rules
  findings.push(...detectTokenMisuse(generatedCode, sdxReference));
  findings.push(...detectComponentReinvention(generatedCode, sdxReference));
  findings.push(...detectPatternViolations(generatedCode, sdxReference));
  findings.push(...detectA11yGaps(generatedCode));
  findings.push(...detectArchitectureMismatches(generatedCode, sdxReference));
  
  return findings;
}
```

---

## 8. Implementation Phases

### Phase 0: Setup (Week 1)
- [x] Create memory bank
- [x] Define tool concept
- [ ] Get stakeholder approval
- [ ] Access SDX repository
- [ ] Define Figma data export format/schema (structured JSON with tokens, components, specs)
- [ ] Create tooling to extract structured data from Figma (via MCP or manual export)
- [ ] Document file format specification
- [ ] Extract token definitions
- [ ] Analyze component structure

### Phase 1: Foundation Testing (Week 2-3)
- [ ] Build code analyzer (token detection)
- [ ] Create 3-5 token-focused test scenarios
- [ ] Run baseline tests
- [ ] Generate first gap reports
- [ ] Present findings to SDX team

### Phase 2: Component Testing (Week 4-5)
- [ ] Enhance analyzer (component detection)
- [ ] Create 5-10 component-focused scenarios
- [ ] Run component tests
- [ ] Generate component gap reports
- [ ] Iterate on recommendations

### Phase 3: Complete System Testing (Week 6-7)
- [ ] Full analyzer implementation
- [ ] Create complex UI scenarios (myswisscom pages)
- [ ] Run comprehensive tests
- [ ] Generate complete gap reports
- [ ] Present comprehensive findings

### Phase 4: Iteration & Measurement (Week 8+)
- [ ] SDX team implements improvements
- [ ] Run Version 2 tests
- [ ] Generate comparison report
- [ ] Measure improvement
- [ ] Refine testing approach

---

## 9. Success Metrics

### Tool Quality Metrics
- **Accuracy**: % of automated findings validated as true positives in manual review
- **Coverage**: % of actual gaps detected by automation
- **Actionability**: % of recommendations implemented by SDX team
- **Reproducibility**: Ability to re-run tests with consistent results

### SDX Improvement Metrics
- **Token Usage Rate**: % of generated code using tokens (target: 90%+)
- **Component Discovery Rate**: % of scenarios using SDX components (target: 85%+)
- **Pattern Compliance**: % adherence to documented patterns (target: 80%+)
- **Accessibility Score**: % of a11y checks passed (target: 95%+)
- **Overall Readiness Score**: Composite score (target: 85%+)

### Version Comparison Metrics
```
Baseline → Post-Improvements

Token Usage:        45% → 85% (+89% improvement)
Component Discovery: 60% → 90% (+50% improvement)
Pattern Compliance: 50% → 80% (+60% improvement)
Accessibility:      40% → 95% (+137% improvement)
Overall:           50% → 85% (+70% improvement)
```

---

## 10. Future Enhancements

### Near Term (3-6 months)
- **Multiple AI Tools**: Test against GitHub Copilot, Claude Code, etc.
- **Visual Regression**: Automated screenshot comparison
- **CI/CD Integration**: Run tests automatically on SDX updates
- **Dashboard**: Visual tracking of metrics over time

### Long Term (6-12 months)
- **MCP Server Integration**: Optional tool for exploration and one-time data extraction (not used during test execution - all scenarios use file-based data)
- **Design Token API**: Machine-readable token definitions
- **Component Discovery Service**: API for AI to query available components
- **Pattern Library**: Machine-readable constraints and rules
- **Auto-fix Suggestions**: Generate code patches for common gaps

### Research Areas
- **Prompt Engineering**: Optimize prompts for better AI output
- **Context Optimization**: What context helps AI the most?
- **Documentation Structure**: How should docs be organized for AI?
- **Semantic Annotations**: Markup to help AI understand intent

---

## 11. Risk Mitigation

### Technical Risks

**Risk**: Automated detection has too many false positives
- **Mitigation**: Tune rules iteratively, focus on high-confidence patterns
- **Fallback**: Increase manual review, treat automation as suggestions

**Risk**: Test scenarios too simple/complex
- **Mitigation**: Phased approach with increasing complexity
- **Fallback**: Adjust difficulty based on early results

**Risk**: AI behavior inconsistent across runs
- **Mitigation**: Version control prompts, test multiple times
- **Fallback**: Focus on patterns rather than individual instances

### Process Risks

**Risk**: SDX team doesn't have bandwidth for improvements
- **Mitigation**: Prioritize recommendations, start with quick wins
- **Fallback**: Focus on documentation improvements (low effort)

**Risk**: Tool maintenance burden too high
- **Mitigation**: Keep tooling simple, leverage existing libraries
- **Fallback**: Manual review with structured checklists

**Risk**: Results not representative of real usage
- **Mitigation**: Use real Swisscom product pages as test cases
- **Fallback**: Interview developers about real pain points

---

## 12. Open Questions for Discussion

1. **Scope**: Should we test only web components, or also legacy components?

2. **Prioritization**: Which component categories are most critical? (buttons, forms, navigation, etc.)

3. **Baseline**: What's the minimum acceptable AI readiness score?

4. **Cadence**: How often should we run full test suites? (monthly, quarterly, on major releases?)

5. **Ownership**: Who will maintain the testing tool long-term?

6. **Integration**: Should this be integrated with existing SDX tooling/pipelines?

7. **Public/Private**: Should test results be public or internal only?

8. **Standards**: Are there industry benchmarks we should align with?

---

## 13. Next Steps

1. **Review & Feedback**: You review this concept and provide feedback
2. **Refinement**: Adjust approach based on your input
3. **Approval**: Get green light to proceed with implementation
4. **Repository Access**: Obtain and analyze SDX repository
5. **Prototype**: Build first version of code analyzer
6. **Pilot Test**: Run 1-2 test scenarios manually
7. **Iterate**: Refine based on pilot learnings
8. **Scale**: Roll out full Phase 1 testing

---

## Appendix A: Related Work

### Industry Examples
- **Shopify Polaris**: Documentation with code snippets for AI consumption
- **Material Design**: Machine-readable design tokens
- **Radix UI**: Accessible component primitives with clear APIs

### Research
- "Design Systems for AI" (Nielsen Norman Group)
- "Machine-Readable Design Systems" (Figma Blog)
- "Documentation for AI Assistants" (GitHub Research)

---

## Appendix B: Glossary

- **Design Token**: Named variable representing a design decision (e.g., `--color-primary`)
- **Component Reinvention**: Creating custom implementation instead of using design system component
- **Pattern Violation**: Code that works but doesn't follow documented best practices
- **AI Readiness**: How well a design system can be understood and applied by AI assistants
- **Three-Way Comparison**: Comparing Figma design, existing code, and AI-generated code
- **Gap Report**: Document identifying differences between expected and actual AI behavior
- **Named Version**: User-defined label for a test run (e.g., "baseline-2024-12")

---

**Document Version**: 1.0  
**Last Updated**: December 3, 2024  
**Author**: Larsen (with AI assistance)  
**Status**: Draft - Awaiting Review

