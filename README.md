# Space Tourism Multi-Page Website

A spec-driven implementation of a responsive space tourism website based on approved source design artifacts and prepared for a final WordPress block theme build.

This repository uses Astro as an intermediate design-engineering layer. Astro is not the final product: it provides a faster environment for refining UI details, validating responsive behavior, testing accessibility, and clarifying the content model before translating the result into a WordPress block theme.

## Project goals

- Translate the source design artifacts into a polished, responsive website.
- Work from reviewed documentation and specifications before implementing complex UI.
- Build reusable and accessible UI patterns inside the existing Astro application.
- Use the provided project data and assets instead of recreating content manually.
- Keep the data layer framework-agnostic so it can later map to WordPress concepts.
- Prepare the final implementation as a WordPress block theme using `theme.json`, templates, template parts, patterns, global styles, and minimal custom PHP.

## Source of truth

The visual source of truth is the approved set of source design artifacts.

The workflow is intentionally tool-agnostic. Those artifacts may be maintained as design files, Penpot files, screenshots, exported mockups, PDFs, or another approved visual reference format.

When the documentation and visual references differ, the discrepancy should be recorded and resolved before implementation continues.

## Terminology

- **Source design artifacts**: approved visual references used as the visual source of truth.
- **Reference mockups**: static frames or exports used to validate layout, spacing, typography, imagery, and responsive behavior.
- **Source data**: the supplied project content in `docs/assets/data.json`.
- **Mock data**: temporary structured content used only when the supplied source data does not cover an implementation need.
- **Content model / data model**: the framework-agnostic structure that later maps to WordPress pages, patterns, block attributes, or custom post types.

## Workflow

This project follows a source-design-to-Astro-to-WordPress workflow:

```txt
source design artifacts + supplied project data
  ↓
DESIGN.md
  ↓
SPEC.md
  ↓
review and implementation planning
  ↓
Astro implementation in frontend/
  ↓
responsive, accessibility, and visual validation
  ↓
WordPress block theme translation
```

Astro is used as a design-engineering sandbox. The goal is to make layout, spacing, typography, image crops, interaction states, and data structures easier to validate before moving into WordPress.

## Current status

The project is currently in the implementation-planning phase.

The repository already contains an Astro application inside `frontend/`. The starter application is available and should be extended rather than replaced with a second Astro scaffold.

Current baseline:

- Astro is configured in `frontend/`.
- The current entry page is the default starter page at `frontend/src/pages/index.astro`.
- Source content for destinations, crew members, and technology items is available in `docs/assets/data.json`.
- Supporting project assets are stored under `docs/assets/` and must be audited before copying or remapping them for frontend runtime use.
- `DESIGN.md` documents the visual system and responsive interpretation.
- `SPEC.md` defines the product requirements and data contracts.

Implementation should begin by validating this baseline and then replacing the starter page incrementally.

## Repository structure

The important existing directories are:

```txt
.
├── frontend/
│   ├── astro.config.mjs
│   ├── package.json
│   └── src/
│       └── pages/
│           └── index.astro
├── docs/
│   └── assets/
│       ├── data.json
│       └── project images and assets
├── DESIGN.md
├── SPEC.md
└── README.md
```

As implementation progresses, reusable layouts, components, styles, and normalized data modules should be added inside `frontend/src/` while static runtime assets should live in an appropriate location such as `frontend/public/assets/`.

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

## Technology stack

### Intermediate implementation layer

- Astro 7
- HTML
- maintainable CSS
- CSS custom properties for design tokens
- TypeScript data modules where useful
- no Tailwind or other styling framework unless explicitly approved later

The existing frontend package requires Node.js `>=22.12.0`.

### Final production target

- WordPress block theme
- `theme.json`
- block templates
- template parts
- patterns
- global styles
- minimal custom PHP only when needed

## Source data

`docs/assets/data.json` is the initial content source for the repeated page families:

- destinations
- crew members
- technology items

The source file already provides names, descriptions, statistics, roles, biographies, and image references.

The Astro layer should normalize this source rather than duplicating it manually. Normalization may add implementation-specific fields such as:

- route-safe `slug` values
- meaningful image `alt` text
- `travelTime` mapped from the source `travel` field
- runtime-safe asset paths
- page metadata
- navigation metadata

The original source data should remain intact. Any normalization should happen in the frontend data layer so the transformation remains explicit and reviewable.

## Asset strategy

Before building page layouts:

1. Audit the images and fonts available under `docs/assets/`.
2. Compare them with the source design artifacts.
3. Identify missing, duplicated, or differently cropped assets.
4. Copy or map the approved runtime assets into the Astro application.
5. Preserve useful modern formats such as WebP where supplied.
6. Document any asset substitutions or crop compromises.

Paths stored in `docs/assets/data.json` should not be assumed to work directly from Astro routes. They must be deliberately mapped to the final runtime asset locations.

## Design principles

- Preserve the source design artifacts as closely as practical.
- Use semantic HTML instead of copying generated design-export markup.
- Keep components small, reusable, and easy to review.
- Extract abstractions only after repeated structure is proven.
- Use design tokens for color, spacing, typography, and layout values.
- Avoid inline styles unless there is a strong implementation reason.
- Prefer simple CSS over unnecessary abstractions.
- Treat repeated page families as data-driven templates rather than duplicated pages.
- Keep Astro-specific decisions easy to translate into WordPress block-theme concepts.

## Accessibility requirements

The implementation must include:

- semantic page landmarks and heading hierarchy
- a keyboard-accessible primary navigation
- a functional and accessible mobile navigation menu
- visible focus states
- `aria-current="page"` for active navigation links
- accessible names for icon-only controls
- meaningful alt text for content images
- decorative backgrounds hidden from assistive technologies
- sufficiently large interactive targets, even when the visible control is small
- sufficient color contrast for text and interaction states
- reduced-motion handling for non-essential transitions
- usable behavior at text zoom and narrow intermediate widths

## Responsive requirements

The reference mockups provide primary targets at mobile, tablet, and desktop sizes, but the implementation must also behave correctly between those widths.

Responsive work should:

- start mobile-first
- use content-driven breakpoints rather than only copying frame widths
- preserve the intended compositions at approximately 375px, 768px, and 1440px
- prevent horizontal overflow
- use `min-height: 100svh` or equivalent modern viewport behavior where appropriate
- validate background and content-image crops separately
- avoid relying on fixed page heights from the reference frames
- test short, tall, narrow, and intermediate viewport combinations

## Development

Run all Astro commands from the `frontend/` directory.

### Requirements

- Node.js `>=22.12.0`
- pnpm

### Install dependencies

```bash
cd frontend
pnpm install
```

### Start the development server

```bash
pnpm dev
```

### Create a production build

```bash
pnpm build
```

### Preview the production build

```bash
pnpm preview
```

## Documentation files

| File | Purpose |
| --- | --- |
| `DESIGN.md` | Visual analysis, design tokens, responsive observations, and design risks |
| `SPEC.md` | Technical product specification and product contracts |
| `PLAN.md` | Incremental implementation plan; add or update it in the repository as planning decisions are approved |
| `REVIEW.md` | Optional dedicated record for later cross-document or implementation reviews |

## WordPress migration direction

After the Astro version is validated, the implementation should be translated into a WordPress block theme.

Expected mapping:

| Astro/design concept | WordPress block theme equivalent |
| --- | --- |
| design tokens | `theme.json` settings and styles |
| site header | template part |
| page-family layouts | block templates |
| reusable UI sections | patterns or template parts |
| normalized source data | pages, block attributes, patterns, custom post types, or a hybrid model |
| global CSS | theme styles and narrowly scoped theme CSS |

The exact WordPress architecture should be decided after the Astro layer proves the layouts, responsive behavior, accessibility, and content model.

## Non-goals

This project does not currently include:

- booking or payment functionality
- user authentication
- live CMS editing in the Astro layer
- a complex client-side state architecture
- a complex animation system
- a footer implementation without an approved footer design
- Tailwind or another styling framework by default
- premature WordPress PHP or custom block development before the Astro validation phase

## Repository philosophy

This is not a one-shot design-to-code export. The project is intentionally documentation-first and review-heavy so each step can be validated before implementation.

The desired result is a clean, maintainable, accessible WordPress block theme that faithfully represents the source design artifacts while using the existing Astro application to make the design-engineering process faster and more precise.
