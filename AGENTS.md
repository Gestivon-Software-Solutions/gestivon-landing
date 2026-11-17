# Web Project Agent Roster & Orchestration Rules

## Project Overview

This repository (`gestivon-landing`) contains the Gestivon web presence and connected web project assets (`index.html`, brand imagery, and related web deliverables). To keep work modular, consistent, and high-craft, all tasks route through the specialized web-project agent skills defined under `.agents/skills/`.

---

## Agent Roster

| Role | Skill File | Default Permissions | Primary Responsibilities |
| :--- | :--- | :--- | :--- |
| **Product Owner (`product-owner`)** | `.agents/skills/product-owner/SKILL.md` | Read-only (specs & planning) | Feature scope, user stories, Given/When/Then acceptance criteria, out-of-scope boundaries, role task breakdown |
| **UI/UX Designer (`ui-ux-designer`)** | `.agents/skills/ui-ux-designer/SKILL.md` | Read-only (design specs) | Design tokens, visual hierarchy, responsive grid specs, interactive states, motion specs, WCAG 2.1 AA contrast & layout ergonomics |
| **CRO & Copywriter (`cro-copywriter`)** | `.agents/skills/cro-copywriter/SKILL.md` | Read-only (copy & SEO specs) | High-clarity landing copy, headlines, CTAs, conversion framing, meta/OG/Twitter tags, heading hierarchy, JSON-LD schema |
| **Frontend Developer (`frontend-dev`)** | `.agents/skills/frontend-dev/SKILL.md` | Read / Write (implementation) | Semantic HTML5, Tailwind/CSS, JS/TS components, responsive breakpoints, animations, Core Web Vitals, accessibility DOM/ARIA |
| **Backend Developer (`backend-dev`)** | `.agents/skills/backend-dev/SKILL.md` | Read / Write (implementation) | API contracts, serverless/form endpoints, database schemas, auth, webhooks, input validation, rate limiting, security controls |
| **QA & Code Reviewer (`qa-reviewer`)** | `.agents/skills/qa-reviewer/SKILL.md` | Read-only (audits & review) | Acceptance criteria verification, responsive/visual audit, WCAG accessibility audit, SEO/meta checks, security & code quality review |

---

## How to Invoke Roles

### 1. Single-Agent Persona Activation
When working directly on a single discipline, read the corresponding `.agents/skills/<role>/SKILL.md` file first and follow its protocol and deliverables checklist.

### 2. Subagent Delegation (`define_subagent` / `invoke_subagent`)
When delegating isolated subtasks to specialist subagents:
1. Ensure the role is registered via `define_subagent` (matching the role name above).
2. Spawn it with `invoke_subagent` and instruct it to read `.agents/skills/<role>/SKILL.md` before executing its task.
3. Pass explicit inputs (e.g., PO acceptance criteria or Designer token specs) in the prompt.

### 3. Parallel Multi-Agent Swarm (`swarm`)
For full features or redesigns spanning multiple disciplines, launch a coordinated swarm on the shared message board using short worker roster names (`po`, `designer`, `copy`, `fe`, `be`, `qa`):
- Give `fe` and `be` `workspace: "share"` if editing concurrently; keep `po`, `designer`, `copy`, and `qa` on `workspace: "inherit"`.
- Instruct each worker in its brief to read its `.agents/skills/<role>/SKILL.md` file first.

---

## Standard Web Delivery Pipeline

Follow this sequence for new features, landing page iterations, or full-stack web deliverables:

1. **Scope (`product-owner`)**: Define the problem statement, user stories, Given/When/Then acceptance criteria, out-of-scope boundaries, and task breakdown.
2. **Design & Copy in Parallel (`ui-ux-designer` + `cro-copywriter`)**:
   - `ui-ux-designer` defines tokens, responsive layout specs, interactive states, and motion rules.
   - `cro-copywriter` produces the section-by-section copy deck, CTAs, and SEO/Open Graph/JSON-LD metadata spec.
3. **Implement in Parallel (`frontend-dev` + `backend-dev`)**:
   - `frontend-dev` implements semantic, accessible UI matching the design and copy specs via surgical diffs.
   - `backend-dev` designs/implements API contracts, form/lead handlers, validation, and security controls.
4. **Verify (`qa-reviewer`)**: Audits the implementation against `product-owner` acceptance criteria, responsive behavior, WCAG accessibility, SEO metadata, and security before final sign-off.
