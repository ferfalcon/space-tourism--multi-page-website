# Space Tourism Multi-Page Website

A spec-driven implementation of a responsive space tourism website, based on source design artifacts and prepared for a final WordPress block theme build.

This repository uses Astro as an intermediate design-engineering layer. Astro is not the final product; it is used to refine the UI, validate responsive behavior, clarify the data model, and make pixel-level adjustments with a better developer experience before translating the result into a WordPress block theme.

## Project goals

- Translate the source design artifacts into a polished, responsive website.
- Work from documentation and specifications before implementation.
- Build reusable, accessible UI patterns in Astro first.
- Keep the data layer clean so it can later map to WordPress concepts.
- Prepare the final implementation as a WordPress block theme using `theme.json`, templates, template parts, patterns, global styles, and minimal custom PHP.

## Source of truth

The visual source of truth is the approved source design artifacts. In the current phase, those artifacts are a design file with page frames and a style guide, but the workflow should stay tool-agnostic so the source can later move to Penpot, screenshots, exported mockups, PDFs, or another visual reference format.

Important note: the currently inspected source contains a zero-size wrapper. The usable design content is inside the child sections for the style guide and page frames.

## Terminology

- **Source design artifacts**: the approved visual references used as the visual source of truth. This can include design files, screenshots, exported mockups, or other client-approved references.
- **Reference mockups**: static visual references used to validate layout, spacing, typography, image crops, and responsive behavior.
- **Mock data**: temporary structured content used in the Astro layer before the final WordPress content model is defined.
- **Content model / data model**: the framework-agnostic structure that later maps to WordPress pages, patterns, block attributes, or custom post types.

## Workflow

This project follows a source-design-to-Astro-to-WordPress workflow:

```txt
source design artifacts
  ↓
DESIGN.md
  ↓
SPEC.md
  ↓
REVIEW.md / PLAN.md
  ↓
Astro implementation
  ↓
Responsive and accessibility validation
  ↓
WordPress block theme translation
```

Astro is used as a sandbox for design engineering. The goal is to make layout, spacing, typography, image crops, interaction states, and data structures easier to validate before moving into WordPress.

## Current status

The project is currently in the specification phase.

Completed documentation:

- `DESIGN.md` — visual analysis, design tokens, responsive observations, and implementation risks.
- `SPEC.md` — technical product specification derived from the source design artifacts and `DESIGN.md`.

Implementation is intentionally not started until the design and technical specification are reviewed.

## Site scope

The site includes four top-level sections:

1. Home
2. Destination
3. Crew
4. Technology

Planned routes:

| Section | Route |
| --- | --- |
| Home | `/` |
| Destination | `/destination/moon` |
| Destination | `/destination/mars` |
| Destination | `/destination/europa` |
| Destination | `/destination/titan` |
| Crew | `/crew/douglas-hurley` |
| Crew | `/crew/mark-shuttleworth` |
| Crew | `/crew/victor-glover` |
| Crew | `/crew/anousheh-ansari` |
| Technology | `/technology/launch-vehicle` |
| Technology | `/technology/spaceport` |
| Technology | `/technology/space-capsule` |

## Planned technology stack

### Intermediate implementation layer

- Astro
- HTML
- CSS custom properties
- TypeScript data modules where useful
- No Tailwind unless explicitly added later

### Final production target

- WordPress block theme
- `theme.json`
- block templates
- template parts
- patterns
- global styles
- minimal custom PHP only when needed

## Design principles

- Preserve the source design artifacts as closely as practical.
- Use semantic HTML instead of copying tool-generated markup.
- Keep components small, reusable, and easy to review.
- Use design tokens for color, spacing, typography, and layout values.
- Avoid inline styles unless there is a strong reason.
- Prefer simple CSS over unnecessary abstractions.
- Treat repeated page types as data-driven templates, not duplicated pages.

## Accessibility requirements

The implementation must include:

- semantic page structure
- keyboard-accessible navigation
- visible focus states
- `aria-current="page"` for active navigation links
- accessible labels for icon-only controls
- meaningful alt text for content images
- decorative images hidden from assistive technologies where appropriate
- sufficient color contrast for text and interactive states

## Data model direction

The repeated sections should be modeled as structured data first:

- destinations
- crew members
- technology items
- primary navigation items
- responsive image assets
- page metadata

This makes the Astro layer easier to validate and prepares the content for a later WordPress mapping into pages, patterns, block attributes, or custom post types.

## Documentation files

| File | Purpose |
| --- | --- |
| `DESIGN.md` | Design analysis and visual system documentation |
| `SPEC.md` | Technical product specification |
| `REVIEW.md` | Future review of contradictions, accessibility gaps, and implementation risks |
| `PLAN.md` | Future step-by-step implementation plan |

## Development commands

The repository is not scaffolded yet. Real commands should be added after the Astro project structure is created.

Expected future commands may include:

```bash
pnpm install
pnpm dev
pnpm build
pnpm preview
```

Do not rely on these commands until the project has a real `package.json` and Astro setup.

## WordPress migration direction

After the Astro version is validated, the implementation should be translated into a WordPress block theme.

Expected WordPress mapping:

| Astro/design concept | WordPress block theme equivalent |
| --- | --- |
| design tokens | `theme.json` settings and styles |
| site header | template part |
| page templates | block templates |
| reusable sections | patterns or template parts |
| data-driven content | pages, patterns, block attributes, or custom post types |
| global CSS | theme styles |

The exact WordPress architecture should be decided after the Astro layer proves the layout, content model, and responsive behavior.

## Non-goals

This project does not currently include:

- booking or payment functionality
- user authentication
- live CMS editing in the Astro layer
- complex animation systems
- a footer implementation without an approved footer design
- Tailwind or another styling framework by default

## Repository philosophy

This is not a one-shot design-to-code export. The project is intentionally documentation-first and review-heavy so each step can be validated before implementation.

The desired result is a clean, maintainable, accessible WordPress block theme that faithfully represents the source design artifacts while using Astro to make the design-engineering process faster and more precise.
