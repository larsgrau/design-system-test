# SDX AI Readiness Testing Tool - Refined Concept Document

## Executive Summary

This document outlines a comprehensive testing tool that evaluates SDX's AI readiness through three sequential assessments: (a) design library quality for AI consumption, (b) consistency between Figma design and codebase, and (c) code implementation quality. Results are displayed in a web dashboard with prioritized recommendations, and test runs are logged with KPIs for tracking progress over time.

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

### Three-Phase Assessment Architecture

The tool performs three sequential assessments to comprehensively evaluate SDX's AI readiness:

```
┌─────────────────────────────────────────────────────────┐
│  Phase A: Design Library AI Quality Assessment          │
│  - Token naming consistency                             │
│  - Component documentation clarity                      │
│  - Machine-readability                                  │
│  - Token completeness                                   │
│  - Component discoverability                            │
└────────────────────┬────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────┐
│  Phase B: Design-Code Consistency Assessment            │
│  - Check Figma code references (if available)           │
│  - Count design components linked to code components     │
│  - Token mapping verification (Figma → CSS variables)   │
│  - Component mapping verification (Figma → Web Comp)    │
│  - Identify orphaned components (design or code only)   │
└────────────────────┬────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────┐
│  Phase C: Code Implementation Quality Assessment       │
│  - Token usage patterns                                 │
│  - Component architecture                               │
│  - Code documentation quality                           │
│  - Accessibility implementation                         │
│  - Pattern compliance                                   │
└────────────────────┬────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────┐
│  Dashboard: Metrics + Prioritized Recommendations     │
│  - Overall AI Readiness Score                           │
│  - Design Quality Score                                 │
│  - Code Quality Score                                    │
│  - Design-Code Consistency Score                        │
└─────────────────────────────────────────────────────────┘
```

### Key Differentiators

1. **Comprehensive Assessment**: Three-phase evaluation covering design, consistency, and code quality
2. **Actionable Insights**: Prioritized recommendations for both design library and codebase
3. **Progress Tracking**: Test run logging with KPIs to measure improvement over time
4. **Web Dashboard**: Visual interface with export capabilities (Markdown, PDF)
5. **Advanced Testing**: Once quality thresholds are met, AI generation testing compares AI output to human implementations

---

## 3. Phase A: Design Library AI Quality Assessment

### Objective

Assess how well the Figma design library is structured for AI consumption and understanding.

### Data Sources

The assessment uses multiple data sources to get a comprehensive view:

1. **Figma Design Library** (Component Library)
   - Component definitions, variants, and states
   - Token usage within components
   - Component organization and structure

2. **Figma "SDX Documentation" File**
   - Component documentation pages
   - Usage guidelines and examples
   - Do's and Don'ts
   - Design specifications

3. **Supernova Documentation** (Work in Progress)
   - Official SDX documentation: https://sdx.supernova-docs.io
   - Component documentation
   - Guidelines and standards
   - Foundation documentation

4. **Component Inventory Documentation** (Generated by Tool)
   - Hybrid structure: Overview file + individual component files
   - Complete component catalog with all metadata
   - Serves as reference for assessments

### Metrics to Measure

#### 1. Token Naming Consistency
- Count token systems found (currently 3: Primary, SDX-prefixed, Legacy)
- Calculate percentage of components using each system
- Identify mixed-system usage within components
- **Score**: 0-100 based on system uniformity

#### 2. Component Documentation Clarity
- Check for component descriptions in Figma "SDX Documentation" file
- Verify naming conventions (e.g., `Button_primary` vs `ButtonPrimary`)
- Assess state documentation completeness
- Check for usage examples and guidelines in documentation
- Compare Figma documentation vs Supernova documentation consistency
- **Score**: 0-100 based on documentation coverage and consistency

#### 3. Machine-Readability
- Check for structured metadata (component properties, variants)
- Verify token values are accessible programmatically
- Assess export formats available (JSON, API access)
- Check for semantic annotations
- Evaluate Supernova documentation structure for machine parsing
- **Score**: 0-100 based on structured data availability

#### 4. Token Completeness
- Count hardcoded values in components (colors, spacing, typography)
- Calculate token coverage percentage
- Identify missing token categories
- Check for token gaps in common use cases
- **Score**: 0-100 based on tokenization rate

#### 5. Component Discoverability
- Check component organization (pages, categories)
- Verify naming patterns for AI searchability
- Assess component index/composition
- Check for component relationships and dependencies
- Evaluate documentation discoverability (Figma vs Supernova)
- **Score**: 0-100 based on organizational clarity

#### 6. Documentation Consistency
- Compare component information across sources (Figma Design Library, Figma Documentation, Supernova)
- Identify discrepancies between sources
- Check for missing documentation in any source
- Verify documentation completeness across all sources
- **Score**: 0-100 based on cross-source consistency

### Component Inventory Documentation

As part of Phase A, the tool generates a comprehensive component inventory:

**Structure**: Hybrid approach
- **Overview File**: `components/COMPONENTS_INVENTORY.md`
  - Complete list of all components
  - Summary statistics
  - Quick reference table
  - Links to individual component files

- **Individual Component Files**: `components/{ComponentName}.md`
  - Component name and variants
  - Props/attributes
  - States and interactions
  - Tokens used
  - Figma link (Design Library + Documentation file)
  - Code reference (if available)
  - Documentation links (Supernova)
  - Usage examples
  - Accessibility information
  - Dependencies

**Content per Component**:
- Basic info: Name, category, status
- Variants and states
- Props/attributes with types
- Tokens used (colors, spacing, typography, etc.)
- Figma references (Design Library + Documentation file)
- Code references (repository links)
- Documentation links (Supernova URL)
- Usage guidelines
- Accessibility features
- Dependencies on other components

### Implementation

**Data Sources**:
- Figma API/MCP for component and token extraction (Design Library)
- Figma API/MCP for "SDX Documentation" file analysis
- Supernova documentation scraping/API (if available)
- Manual analysis of Figma structure (pages, organization)
- Token system analysis from existing Figma analysis

**Output**: 
- Design Quality Report with scores and findings
- Component Inventory Documentation (overview + individual files)

---

## 4. Phase B: Design-Code Consistency Assessment

### Objective

Assess how well Figma design components and tokens map to codebase implementations.

### Assessment Steps

#### 1. Check Figma Code References (Primary Method)
- Use Figma API to check if components have `codeReferences` or similar metadata
- Extract linked repository URLs, file paths, component names
- Count: `components_with_code_references / total_components`
- Verify link validity (check if referenced files exist)

#### 2. Component Mapping Verification
- For components with code references: verify link validity
- For components without references: attempt name-based matching
  - Figma: `Button_primary` → Code: `<sdx-button>` or `Button` component
  - Use fuzzy matching for variations (e.g., `ButtonPrimary`, `button-primary`)
- Identify orphaned components:
  - Design-only: Components in Figma with no code equivalent
  - Code-only: Components in code with no Figma equivalent

#### 3. Token Mapping Verification
- Extract tokens from Figma (e.g., `spacing/3`, `color/brand/navy`)
- Extract tokens from codebase (CSS variables, token files)
- Map Figma tokens → Code tokens
- Identify unmapped tokens:
  - Figma-only: Tokens in design not found in code
  - Code-only: Tokens in code not found in design

#### 4. Consistency Metrics
- Component mapping rate: `mapped_components / total_components`
- Token mapping rate: `mapped_tokens / total_tokens`
- Orphan detection: count of design-only and code-only items
- Code reference coverage: `components_with_references / total_components`

### Implementation

**Data Sources**:
- Figma API for code references and component metadata
- Git repository analysis for component files and token definitions
- AST parsing for component exports and token usage

**Output**: Consistency Report with mapping tables and orphan lists

---

## 5. Phase C: Code Implementation Quality Assessment

### Objective

Assess the quality of codebase implementation regarding AI-friendliness and SDX pattern adherence.

### Metrics to Measure

#### 1. Token Usage Patterns
- Detect hardcoded values vs token usage
- Calculate token adoption rate in codebase
- Identify token misuse patterns
- Check for deprecated token usage

#### 2. Component Architecture
- Verify component structure follows SDX patterns
- Check for proper Web Component implementation
- Assess component composition and reusability
- Verify component exports and naming

#### 3. Code Documentation
- Check for JSDoc/TSDoc comments
- Verify prop/attribute documentation
- Assess example code quality
- Check for usage guidelines in code

#### 4. Accessibility Implementation
- Check ARIA attributes
- Verify keyboard navigation
- Assess focus management
- Check semantic HTML usage

#### 5. Pattern Compliance
- Verify spacing/layout patterns
- Check typography usage
- Assess color system usage
- Check for pattern violations

### Implementation

**Data Sources**:
- Git repository code analysis
- AST parsing for code structure
- Static analysis for patterns

**Output**: Code Quality Report with scores and findings

---

## 6. Dashboard Requirements

### Web Application

**Technology Stack**:
- Frontend: React/TypeScript (or similar modern framework)
- Backend: Node.js/TypeScript API
- Database: SQLite or JSON files for test run history
- Export: Markdown and PDF generation libraries

### Dashboard Views

#### 1. Overview Dashboard
- Overall AI Readiness Score (composite of all phases)
- Design Quality Score (Phase A)
- Code Quality Score (Phase C)
- Design-Code Consistency Score (Phase B)
- Trend charts showing progress over time
- Quick stats (total components, tokens, issues found)

#### 2. Design Quality View
- Breakdown of Phase A metrics
- Token system analysis visualization
- Component documentation coverage
- Machine-readability assessment
- Prioritized recommendations for design library improvements

#### 3. Consistency View
- Component mapping visualization (linked vs unlinked)
- Token mapping table (Figma → Code)
- Orphan component lists (design-only, code-only)
- Code reference coverage metrics
- Prioritized recommendations for linking/mapping improvements

#### 4. Code Quality View
- Breakdown of Phase C metrics
- Token usage statistics
- Component architecture analysis
- Documentation coverage
- Prioritized recommendations for code improvements

#### 5. Recommendations View
- Combined prioritized list (design + code)
- Impact scoring (High/Medium/Low)
- Effort estimation
- Implementation suggestions
- Expected impact metrics

### Export Functionality

- **Markdown Export**: Full reports in markdown format
- **PDF Export**: Formatted PDF reports with charts and tables
- **CSV Export**: Raw metrics data for analysis

---

## 7. Test Run Logging

### Test Run Structure

Each test run captures:

- **Run ID**: Unique identifier (timestamp-based or user-defined)
- **Date/Time**: When the assessment was run
- **Data Sources**: 
  - Figma file version/commit
  - Git repository commit hash
  - SDX version (if available)
- **KPIs**: 
  - Overall AI Readiness Score
  - Design Quality Score
  - Code Quality Score
  - Consistency Score
  - Individual metric scores (token consistency, documentation, etc.)
- **Findings**: Count of issues by category
- **Recommendations**: Count by priority level

### Test Run History

- View all historical runs in chronological order
- Compare runs side-by-side
- Track progress metrics over time
- Filter by date range, SDX version, or assessment phase

### Progress Tracking

- Visual indicators showing improvement/regression
- Delta calculations (score changes between runs)
- Trend analysis (improving, stable, declining)
- KPI tracking over time

### Test Run Triggers

- **Manual**: CLI command to run assessments
- **Automatic**: Git webhook or scheduled runs (daily/weekly)
- **On Change**: Triggered when code or design changes are detected

---

## 8. Advanced Testing Mode

### Prerequisites

Advanced testing is enabled when quality thresholds are met:

- Overall AI Readiness Score ≥ threshold (e.g., 75%)
- Design Quality Score ≥ threshold (e.g., 70%)
- Code Quality Score ≥ threshold (e.g., 70%)
- Consistency Score ≥ threshold (e.g., 80%)

### Advanced Test Flow

```
1. Select Design from Figma
   ↓
2. Generate UI Implementation (using AI)
   - Provide design + SDX context to AI
   - Generate code implementation
   ↓
3. Compare Generated UI vs Human Implementation
   - Visual comparison (screenshot diff)
   - Code comparison (token usage, component usage)
   - Functional comparison (accessibility, behavior)
   ↓
4. Generate Gap Report
   - Similar to original concept's gap reports
   - Focus on AI generation quality
   - Track AI generation scores over time
```

### Implementation Notes

- Uses existing codebase implementations as "ground truth"
- Compares AI-generated code against human-written reference implementations
- Generates detailed gap reports for AI generation quality
- Tracks AI generation scores over time
- Only enabled once design and code quality are sufficient

---

## 9. Implementation Plan

### Phase 1: Foundation (Weeks 1-2)
- [ ] Set up project structure (TypeScript, React dashboard, Node.js backend)
- [ ] Implement Figma API/MCP integration for Phase A
  - [ ] Connect to Figma Design Library
  - [ ] Connect to Figma "SDX Documentation" file
- [ ] Implement Supernova documentation integration (scraping/API)
- [ ] Build component inventory extraction and documentation generation
  - [ ] Generate overview file (COMPONENTS_INVENTORY.md)
  - [ ] Generate individual component files
- [ ] Build basic design quality assessment (token analysis)
- [ ] Create initial dashboard structure (web app setup)

### Phase 2: Consistency Assessment (Weeks 3-4)
- [ ] Implement Figma code reference checking
- [ ] Build component mapping logic (name-based + code reference)
- [ ] Implement token mapping verification
- [ ] Add consistency metrics to dashboard

### Phase 3: Code Quality Assessment (Weeks 5-6)
- [ ] Implement code repository analysis
- [ ] Build AST parsing for token/component detection
- [ ] Create code quality metrics
- [ ] Integrate into dashboard

### Phase 4: Dashboard & Logging (Weeks 7-8)
- [ ] Complete dashboard UI with all views
- [ ] Implement test run logging system
- [ ] Add export functionality (Markdown, PDF)
- [ ] Build progress tracking and comparison features

### Phase 5: Advanced Testing (Weeks 9-10)
- [ ] Implement advanced testing mode
- [ ] Build AI generation comparison logic
- [ ] Create gap report generation for AI tests
- [ ] Integrate into dashboard

---

## 10. Success Criteria

1. **Assessment Completeness**: All three phases produce actionable metrics
2. **Dashboard Usability**: Clear visualization of scores and recommendations
3. **Recommendation Quality**: Prioritized, impact-scored suggestions
4. **Progress Tracking**: Test run history enables improvement measurement
5. **Advanced Testing**: Once quality thresholds met, AI generation testing works

---

## 11. Key Files Structure

### New Files to Create
- `src/assessments/design-quality.ts` - Phase A assessment logic
- `src/assessments/consistency.ts` - Phase B assessment logic  
- `src/assessments/code-quality.ts` - Phase C assessment logic
- `src/data-sources/figma-design-library.ts` - Figma Design Library integration
- `src/data-sources/figma-documentation.ts` - Figma "SDX Documentation" file integration
- `src/data-sources/supernova-docs.ts` - Supernova documentation integration
- `src/inventory/component-extractor.ts` - Component data extraction
- `src/inventory/component-doc-generator.ts` - Component documentation generator
- `src/dashboard/` - Web application frontend
- `src/api/` - Backend API for dashboard
- `src/export/` - Markdown and PDF export logic
- `src/test-runs/` - Test run logging and history management
- `src/advanced-testing/` - Advanced AI generation testing

### Generated Documentation Files
- `components/COMPONENTS_INVENTORY.md` - Overview of all components
- `components/{ComponentName}.md` - Individual component documentation files

### Modified Files
- `tool_concept.md` - This document (refined concept)
- `memory-bank/activeContext.md` - Update with new approach
- `memory-bank/systemPatterns.md` - Document new architecture

---

## 12. Open Questions

1. What are the quality thresholds for enabling advanced testing?
2. How should we handle partial assessments (e.g., only design available)?
3. Should the dashboard support real-time updates or batch processing?
4. What authentication/access control is needed for the dashboard?
5. How should we handle multiple SDX versions in the same dashboard?

---

**Document Version**: 2.0 (Refined)  
**Last Updated**: December 3, 2024  
**Author**: Larsen (with AI assistance)  
**Status**: Refined - Ready for Implementation
