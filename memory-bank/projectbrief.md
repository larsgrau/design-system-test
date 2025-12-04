# Project Brief: SDX AI Readiness Testing Tool

## Project Overview
A systematic testing tool to evaluate how well the SDX (Swisscom Design System) is understood and applied by AI coding assistants, specifically targeting "vibe coding" scenarios where developers use AI to generate UI implementations.

## Core Problem
Need to ensure AI assistants understand SDX well enough to:
- Apply design tokens correctly instead of hardcoded values
- Use existing components instead of reinventing them
- Follow documented patterns and constraints
- Generate accessible, production-ready code
- Match the design system's architecture and implementation style

## Primary Goal
Produce a comprehensive gap report that identifies specific improvements needed in SDX to make it more AI-friendly, with actionable recommendations for the design system authors.

## Key Stakeholders
- **Business Owner**: SDX business owner (decision maker)
- **Core Team**: SDX designers and developers (maintainers)
- **Primary Audience**: Combined SDX core team (designers + developers)
- **Secondary Audience**: Swisscom product teams using SDX
- **Context**: Swisscom internal design system (SDX) used across multiple products

## Success Criteria
1. Generate reproducible, version-controlled test scenarios
2. Identify gaps across five categories:
   - Token misuse (hardcoded values vs semantic tokens)
   - Component reinvention (custom implementations vs DS components)
   - Pattern violations (spacing, typography, layout inconsistencies)
   - Accessibility gaps (missing ARIA, keyboard navigation)
   - Architecture mismatches (implementation style inconsistencies)
3. Produce actionable gap reports in Markdown
4. Enable periodic re-testing to measure improvement over time
5. Support named versions for tracking valuable iterations

## Available Resources
- Read-only access to SDX GitHub repository (pending)
- Access to SDX documentation at https://sdx.swisscom.com
- Access to SDX Figma design library
- Access to live Swisscom implementations for reference (e.g., My Swisscom with login credentials)
- Can obtain source code and design files from existing implementations

## Constraints
- Initial focus on Cursor IDE, extensible to other AI tools later
- Testing must be reproducible and version-controlled
- Output must be actionable for SDX core team

## Scope
- **Phase 1**: Foundation (design tokens)
- **Phase 2**: Core components
- **Phase 3**: Complete design system
- **Testing Method**: Three-way comparison (Figma → Existing code → AI-generated)
- **Future**: MCP server integration for enhanced AI context

