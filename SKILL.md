---
name: personal-ai-workbench
description: Help beginners plan, build, polish, test, and deploy a personal digital workspace or AI-powered workbench. Use when a user asks for a personal dashboard, life/work/study management hub, habit tracker, finance tracker, content creator workspace, or a custom web app to organize recurring activities.
---

# Personal AI Workbench Builder

## Mission

Turn a short, plain-language request into a useful personal digital workspace. The user should not need to know programming, database design, UI terminology, or prompt engineering.

Build a working product—not just a mockup. The result should be understandable, responsive, usable on mobile and desktop, and designed around the user's real recurring tasks.

A workbench may be a standalone HTML app, a small web application, or an extension of an existing project. Choose the simplest reliable architecture that meets the user's needs. Do not force a single-file HTML implementation if the requested functionality or existing project calls for a framework, backend, authentication, collaboration, or cloud sync.

## When to Activate

Activate this skill when the user asks to:
- Build a personal workspace, workbench, dashboard, or personal operating system.
- Make a tracker for tasks, habits, study, fitness, finances, reading, or projects.
- Organize work, study, content creation, or daily life in one place.
- Turn a spreadsheet or recurring manual workflow into a simple web app.
- Create a mobile-friendly personal web app that can be saved to a phone's home screen.

## 1. Beginner-First Conversation

### Core rules
1. Accept a short request such as "make me a study dashboard" as sufficient to begin.
2. Infer sensible modules and defaults from the use case.
3. Ask no more than two concise questions before producing a first working version, and only ask questions whose answers materially affect the result.
4. Prefer simple choices over open-ended technical questions.
5. If the user is unsure, choose sensible defaults, explain them briefly, and start building.
6. Deliver a useful first version quickly, then improve it iteratively.
7. Never ask the user to specify database schemas, CSS details, component libraries, or implementation architecture unless they explicitly want to.

If the request is too broad to infer the use case, ask what they mainly want to manage (study, work, content creation, money, health, or everyday life) and whether a simple first version with three core sections is acceptable. Do not ask questions already answered by the user.

## 2. Route Requests to a Workspace Type

Use these as starting points, not rigid templates. Adapt to the user's context.

| Workspace type | Useful first modules | Possible visual direction |
|---|---|---|
| Everyday life hub | Today's tasks, habits, notes | Calm, premium, uncluttered |
| Personal finance tracker | Transactions, budgets, savings goals | Clear, trustworthy, restrained |
| Study and exam planner | Study plan, revision tracker, mistake log | Focused, readable, encouraging |
| Fitness and wellness tracker | Activity log, goals, progress | Calm, motivating, data-led |
| Content creator workspace | Idea bank, content pipeline, performance review | Editorial, visual, efficient |
| Work and project hub | Tasks, project status, notes | Professional, structured |
| Reading and knowledge hub | Reading list, notes, highlights | Quiet, typography-led |
| Family learning hub | Learning activities, progress, rewards | Friendly, accessible, age-appropriate |
| Personal growth hub | Goals, habits, reflection | Warm, motivating, simple |

Start with approximately 3–4 core modules. Explain which additional features can be added later. Add one substantial module per iteration unless the user asks for a larger build and the scope is manageable.

## 3. Product Planning

Before coding, briefly define:
- Target user and primary use case.
- The main job the workbench should help the user complete.
- Three or four first-release modules.
- The key data each module needs to store.
- The most important actions users take.
- Whether data should remain local or sync across devices/users.
- Whether the app needs sharing, login, permissions, or deployment.

Keep planning lightweight. Do not block implementation with a long specification document unless requested.

## 4. Information Architecture and Interface

### Dashboard

The home screen should answer:
- What needs my attention today?
- What is in progress?
- What is coming up?
- How am I progressing?

Where relevant, place a "Today" or "Needs attention" section near the top. It can show overdue items, tasks due today, and upcoming deadlines. Do not silently discard unfinished tasks; preserve them and make their status clear.

### Navigation
- Desktop: a compact sidebar or top navigation.
- Tablet: responsive top navigation or collapsible sidebar.
- Mobile: bottom navigation or a compact menu.
- Keep the most frequently used actions easy to reach.
- Avoid deep navigation for everyday tasks.

### Visual quality
- Establish a consistent design system: color tokens, typography, spacing, radii, shadows, and icon style.
- Use a clear visual hierarchy and restrained decoration.
- Use whitespace to separate sections.
- Prefer readable cards and compact summaries over dense dashboards.
- Use real icons from a consistent icon set or inline SVG; do not use emoji as a substitute for interface icons unless the user requests that style.
- Provide empty, loading, success, and error states.
- Avoid generic AI-generated layouts and unnecessary charts.

## 5. Data and Persistence

Choose storage based on the actual requirements.

### Local-only personal workspace
For a simple single-user app that runs in one browser:
- Use localStorage for small, structured preferences and lightweight records.
- Consider IndexedDB for larger datasets, files, or more complex offline data.
- Use stable, namespaced storage keys.
- Version the stored data and handle migrations when the schema changes.
- Validate imported data before replacing existing records.
- Make it clear that browser-local data may not automatically sync to another device or browser.

### Multi-device or collaborative workspace
Use a backend/database and authentication when the user needs sync across devices, multiple users, shared workspaces, centralized backups, permissions, roles, or remote access to shared data.

Do not pretend localStorage provides cloud sync, encryption, or server-side backup.

### Data safety requirements
For any app that stores user-created records:
- Provide export and import/restore where practical.
- Prefer a portable JSON backup format.
- Add CSV export when tabular data (such as transactions) benefits from it.
- Confirm before destructive actions such as clearing all data.
- Distinguish sample/demo records from the user's own records.
- Never silently overwrite user data during an update.
- Explain storage location and backup limitations in plain language.

## 6. Starter Content and First-Run Experience

- Do not leave the first screen looking broken or unfinished.
- If useful, include a small set of clearly labelled sample records.
- Make sample data easy to remove without deleting user-created data.
- If the user has supplied real data, use it carefully and do not fabricate missing facts.
- Provide a clear first action so the user knows how to begin.
- Do not invent overdue tasks, financial transactions, health measurements, or personal history as if they were real. Any examples must be visibly marked as sample data.

## 7. Responsive and Accessible Behavior

- Design mobile-first when the user is likely to use the workspace on a phone.
- Ensure touch targets are comfortably tappable (aim for at least 44 × 44 CSS pixels).
- Use readable font sizes; avoid input text smaller than 16 CSS pixels on iOS.
- Respect device safe areas.
- Prevent horizontal overflow and clipped content.
- Make forms keyboard-accessible and label inputs.
- Provide visible focus states and sufficient color contrast.
- Do not rely on color alone to communicate status.
- Respect reduced-motion preferences.
- Test narrow mobile, tablet, and desktop widths.

## 8. Optional Progressive Enhancements

Only add these when useful or requested:
- Light/dark theme toggle.
- Search, filters, sorting, and tags.
- Calendar or timeline views.
- Charts and progress summaries.
- Attachments and image uploads.
- Bilingual interface.
- Password gate or sign-in.
- PWA installation and offline support.
- Cloud backup or synchronization.
- Shareable deployment link.
- Notifications or reminders, with clear permission handling.

Explain trade-offs before adding features that introduce accounts, external services, recurring costs, or privacy implications.

## 9. Technical Implementation Rules

1. Inspect the existing project before editing.
2. Reuse its framework, components, styling conventions, and dependencies where practical.
3. For a new simple workspace, prefer the smallest maintainable implementation.
4. A single HTML file with inline CSS and JavaScript can be suitable for a lightweight local tool, but it is not a universal requirement.
5. Do not use external CDNs or remote assets if the app is expected to work fully offline.
6. If using external libraries, choose established dependencies and explain why they are needed.
7. Keep business logic separate from presentation where appropriate.
8. Use semantic HTML and accessible controls.
9. Handle malformed data, empty states, storage failures, and asynchronous errors.
10. Do not claim deployment, persistence, backup, or functionality has been verified unless it has actually been tested.

## 10. Build and Delivery Workflow

### Phase A — Understand
Identify the use case, route to a suitable workspace type, select sensible first-release modules, and ask at most two essential questions if needed.

### Phase B — Plan
Outline the dashboard and navigation, define the main data records and user actions, choose local or cloud persistence based on needs, and state important assumptions.

### Phase C — Build
Implement the core experience first. Make primary workflows functional, label sample data clearly, include backup/export where appropriate, and make the layout responsive.

### Phase D — Polish
Refine typography, spacing, colors, icons, and visual hierarchy. Add meaningful micro-interactions. Avoid decorative motion that slows down common tasks. Ensure empty, loading, success, and error states are clear.

### Phase E — Test
Verify main navigation and primary actions; create, edit, complete, delete, and restore flows where relevant; persistence after refresh; import/export; destructive-action confirmation; mobile/tablet/desktop layouts; keyboard accessibility; reduced motion; and absence of obvious console errors or broken routes.

### Phase F — Deliver
Provide the working files or app preview. Explain how to open and use it, where data is stored, and how to back it up. If deployment is requested, use only an available authorized service and verify the published URL before claiming success. Explain how to add the app to a phone's home screen if it is installable as a PWA or web shortcut.

## 11. Reusable Prompts

### Prompt A — Build a personal workspace from scratch

> Build me a polished personal digital workspace for [use case].
>
> Assume I am a beginner and do not make me write a technical specification. Choose sensible defaults and start with 3–4 useful modules.
>
> The workspace should have a clear dashboard showing today's priorities and useful summaries; simple, intuitive navigation; mobile, tablet, and desktop support; consistent professional visual design; real create, edit, complete, and delete actions; appropriate data persistence with a plain-language explanation; export and restore where practical; and clearly labelled sample data only if it helps demonstrate the app.
>
> Inspect the environment and choose the simplest reliable implementation. Build a working application, not a static mockup. Test the main workflows and report any limitations.

### Prompt B — Improve an existing workspace

> Review and improve the current personal workspace. First inspect the project structure and identify its framework, existing features, data model, and styling conventions. Do not rewrite working parts unnecessarily.
>
> Improve information hierarchy and dashboard usefulness, navigation and mobile responsiveness, visual consistency and readability, empty/loading/success/error states, data persistence and backup where appropriate, and accessibility and interaction feedback.
>
> Preserve existing user data and business logic. Make focused changes, test the main workflows, and summarize what changed.

### Prompt C — Add a new module safely

> Add one new module called [module name] to the existing workspace. Inspect the current architecture, data storage, navigation, and shared components before editing. Match the existing design system. Implement real data operations where relevant, use backward-compatible data changes, do not reset or overwrite existing data, add empty and error states, update responsive navigation, and test both the new module and existing core workflows.

### Prompt D — Prepare a workspace for mobile use

> Prepare this workspace for comfortable mobile use. Use a mobile-first responsive layout, compact phone navigation, comfortably tappable targets, no horizontal overflow or clipped content, iOS safe-area and input considerations, and usable forms, tables, cards, and charts on narrow screens. Consider PWA installation only if supported. Test phone, tablet, and desktop widths. Preserve existing functionality and data.

### Prompt E — Add backup and restore

> Implement reliable backup and restore. Export user data in a documented JSON format; validate imported files before applying them; show a preview or confirmation before replacing existing data; never silently overwrite current records; handle malformed files and incompatible versions; preserve relationships and timestamps; add CSV export for relevant tabular modules; explain where data is stored and what the backup includes. Test export, import, invalid-file handling, and recovery.

## 12. Completion Checklist

- [ ] The workspace solves the user's primary use case.
- [ ] The first release is focused rather than overloaded.
- [ ] The dashboard makes priorities easy to understand.
- [ ] Navigation works across mobile, tablet, and desktop.
- [ ] Main actions operate on real data.
- [ ] Data persistence matches the stated requirements.
- [ ] Backup and restore are available where practical.
- [ ] Sample data is clearly distinguished from real user data.
- [ ] Destructive actions require confirmation.
- [ ] Accessibility and reduced motion have been considered.
- [ ] Main workflows have been tested.
- [ ] Delivery instructions and data limitations are clear.

## Final Agent Instruction

Make the user's personal workspace genuinely useful, not merely attractive. Reduce setup effort, choose sensible defaults, build a working first version quickly, protect user data, and improve it in small, testable iterations.

Never claim that data is permanently safe, encrypted, synced, backed up, or deployed unless the implementation actually provides and verifies that capability.
