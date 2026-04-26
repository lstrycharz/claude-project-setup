# Spec — [Project Name]

> **Purpose of this document:** Capture *what* we're building. This is the ingredients list — the technical or content components that, taken together, will satisfy the PRD. The PRD says "we need a high-converting landing page for product X." The spec says "the page contains these eight sections, follows this layout, includes these specific calls to action, and renders correctly on mobile."

---

## 1. Overview

One paragraph summarizing what this spec covers. Reference the PRD it implements.

PRD reference: [link or filename]

## 2. Components / sections

The discrete pieces that make up the deliverable. For a blog post, these are the sections. For a piece of software, these are the modules or features. For a campaign, these are the assets.

### 2.1. [Component name]

- Purpose:
- Inputs / dependencies:
- Outputs / deliverables:
- Acceptance criteria:

### 2.2. [Component name]

- Purpose:
- Inputs / dependencies:
- Outputs / deliverables:
- Acceptance criteria:

*(Repeat for each component.)*

## 3. Constraints

### Technical constraints

Platforms, languages, formats, file size limits, performance requirements.

### Brand / style constraints

Voice, tone, formatting standards, forbidden terminology, required terminology.

### Compliance / legal constraints

Anything regulatory or legal that affects what can be produced.

## 4. Standards and conventions

References to the rules files this project must comply with. (These are typically in `.claude/references/` — the setup script copies them in based on project type.)

- [ ] Style guide compliance: [link to file]
- [ ] SEO standards: [link to file]
- [ ] Forbidden words list: [link to file]
- [ ] [Domain-specific standard]: [link to file]

## 5. KPIs and milestones

The measurable indicators of progress and success.

### Milestones

| Milestone | Target date | Acceptance criteria |
|-----------|-------------|---------------------|
| Draft 1 complete | | |
| Review pass 1 complete | | |
| Final delivery | | |

### KPIs

| Metric | Target | Measurement method | Cadence |
|--------|--------|---------------------|---------|
| | | | |

## 6. Dependencies

What this project depends on — external data, third parties, tools, content from other sources, decisions waiting on someone else.

## 7. Validation

How each component will be checked before it's considered done. Reference the relevant checklist file. (Per the Alibaba 2025 paper: validation checklists materially improve AI-generated output quality.)

Checklist file: `.claude/checklists/[project-type]-checklist.md`

## 8. Open technical / content questions

Items that need to be resolved before or during execution.

---

*This document is more volatile than the PRD. As you discover details during execution, update the spec — don't let the project drift away from it without acknowledgment.*
