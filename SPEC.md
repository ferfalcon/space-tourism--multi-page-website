# Space Tourism Website — SPEC.md

## 1. Purpose

This document translates the reviewed source design artifacts and `DESIGN.md` into a technical product specification for the Space Tourism multi-page website. The wording is intentionally tool-agnostic so the visual source can later move between design files, screenshots, exported mockups, or other approved reference formats.

The final production target is a WordPress block theme. Astro is an intermediate implementation layer for UI precision, responsive validation, accessibility review, token refinement, and data-model clarification before the WordPress translation.

This document defines what the product must contain and how it must behave. It does not define the implementation plan and does not include component code.

---

## 2. Source references

### 2.1 Existing design document

This specification is aligned with:

- `DESIGN.md`
- Title: `Space Tourism Website — DESIGN.md`

`DESIGN.md` defines the visual direction, design tokens, responsive observations, design risks, and component-level design interpretation. This `SPEC.md` converts those findings into product contracts and technical requirements.

---

## 3. Product scope

The product is a responsive, multi-page, editorial-style space tourism website with four top-level sections:

1. Home
2. Destination
3. Crew
4. Technology

The site must present immersive space-themed content with full-bleed imagery, shared navigation, elegant typography, and page-specific visual layouts.

The product must support:

- static route-based navigation
- responsive layouts for mobile, tablet, and desktop
- data-driven repeated page families
- accessible keyboard and screen-reader behavior
- design tokens suitable for later WordPress `theme.json` translation
- content/data structures that can later map to WordPress pages, patterns, block attributes, or custom post types

---

## 4. Non-goals

The following are explicitly out of scope for this specification:

- Implementation planning or task sequencing.
- Component code.
- Astro file structure decisions beyond naming conceptual responsibilities.
- WordPress PHP implementation details.
- Gutenberg block registration details.
- Database design.
- CMS admin editing workflows beyond content/data requirements.
- Animations beyond simple interaction states.
- User authentication, booking, payments, or real space travel inventory.
- Search functionality.
- Footer implementation, because the reviewed source-design footer reference is empty.
- Client-side tab behavior unless route-based navigation is rejected.
- Tailwind or any utility-first CSS system unless explicitly requested later.

---

## 5. Assumptions

The specification relies on these assumptions:

1. The source design artifacts are the visual source of truth.
2. `DESIGN.md` is the current design interpretation source of truth.
3. Astro will be used only as an intermediate design-engineering layer, not as the final production target.
4. The production target will be a WordPress block theme.
5. The repeated page families should be data-driven rather than manually duplicated.
6. Destination, Crew, and Technology item switching should be implemented as route navigation, not JavaScript-only tabs/carousels.
7. The mobile menu open state is not present in the reviewed reference mockups, so only the closed mobile menu state is visually specified.
8. The footer should be omitted until a real footer design is provided.
9. Generated design-export code is measurement reference only and must not define the production architecture.
10. Images shown in the source design artifacts represent the required art direction and crop behavior, but final asset filenames and formats may differ.
11. Mobile navigation must be functional even though the open menu visual is not specified. A minimal accessible inferred menu is acceptable until an approved open-state reference is provided.
12. Tablet-specific image assets are required when the tablet crop is visually distinct; otherwise a documented mobile-or-desktop fallback may be used and verified.

---

## 6. Open questions

These questions must be resolved before final implementation decisions:

1. Should tablet navigation show section numbers for all items, hide them for all items, or follow the inconsistent Home tablet frame where active `HOME` appears without `00`?
2. What should the opened mobile navigation look like? The reviewed reference mockups only show the hamburger closed state.
3. Are Destination, Crew, and Technology pages expected to be separate routes, or should they behave as in-page interactive panels?
4. Should the Home `EXPLORE` CTA link to `/destination/moon`?
5. Are all source images available as local project assets, or must they be exported from the current source design artifacts?
6. Should WordPress content be modeled as normal pages, custom post types, patterns, or a hybrid approach?
7. Are the page titles and section labels editable content, or fixed theme strings?
8. Should the site include any footer content not visible in the source design artifacts?
9. Are hover states beyond the active/default source-design states required from the original challenge/design system?
10. Is motion allowed for the Explore CTA halo and menu transitions, or should all motion be minimal/static?
11. Should the inferred mobile menu open state be a right-side overlay, full-screen panel, or another pattern?
12. What visual tolerance is acceptable during QA: exact pixel match at the reference widths, or a small documented tolerance for browser/font rendering differences?
13. Are tablet-specific background and content image assets available for every page family, or should tablet use documented fallbacks?

---

## 7. Page inventory and routing requirements

### 7.1 Required routes

The product must expose the following user-facing pages:

| Section | Route | Content source |
| --- | --- | --- |
| Home | `/` | Home content |
| Destination | `/destination/moon` | Moon destination |
| Destination | `/destination/mars` | Mars destination |
| Destination | `/destination/europa` | Europa destination |
| Destination | `/destination/titan` | Titan destination |
| Crew | `/crew/douglas-hurley` | Douglas Hurley |
| Crew | `/crew/mark-shuttleworth` | Mark Shuttleworth |
| Crew | `/crew/victor-glover` | Victor Glover |
| Crew | `/crew/anousheh-ansari` | Anousheh Ansari |
| Technology | `/technology/launch-vehicle` | Launch Vehicle |
| Technology | `/technology/spaceport` | Spaceport |
| Technology | `/technology/space-capsule` | Space Capsule |

### 7.2 Section landing behavior

If a user visits a section root, the site must resolve to a default item:

| Requested route | Required behavior |
| --- | --- |
| `/destination` | Resolve or redirect to `/destination/moon` |
| `/crew` | Resolve or redirect to `/crew/douglas-hurley` |
| `/technology` | Resolve or redirect to `/technology/launch-vehicle` |

### 7.3 Not-found behavior

Invalid slugs must not render empty or broken templates.

Required behavior:

- unknown destination slugs must resolve to a not-found state or redirect to the default destination
- unknown crew slugs must resolve to a not-found state or redirect to the default crew member
- unknown technology slugs must resolve to a not-found state or redirect to the default technology item

Assumption: a proper 404 is preferred over silent fallback, but this depends on final routing strategy.

---

## 8. Global responsibilities

### 8.1 Product responsibilities

The website must:

- communicate the space tourism concept clearly
- preserve the cinematic editorial design language from the source design artifacts
- present all required content items
- support navigation between all page sections and item states
- remain usable across mobile, tablet, and desktop
- preserve accessible semantics and keyboard behavior
- avoid unnecessary JavaScript for content that can be route-driven
- maintain a data model that can later map cleanly to WordPress

### 8.2 Design system responsibilities

The design system must define:

- color tokens
- typography tokens
- spacing tokens
- page container widths
- page background behavior
- navigation states
- sub-navigation states
- image usage rules
- focus styles

### 8.3 Astro layer responsibilities

The Astro layer must:

- validate page layouts against the source design artifacts
- validate responsive behavior at key breakpoints
- validate image crops and asset needs
- validate accessible HTML semantics
- validate data-driven rendering requirements
- keep content and layout separate enough for WordPress migration

### 8.4 WordPress target responsibilities

The WordPress block theme must eventually support:

- global design tokens through `theme.json`
- template-level layout through block templates and template parts
- reusable sections through patterns or template parts
- content-driven pages or content types
- minimal custom PHP only where block theme capabilities are insufficient

This specification does not decide the final WordPress architecture.

---

## 9. Global content requirements

### 9.1 Site identity

Required content:

| Field | Required | Notes |
| --- | --- | --- |
| Site logo | Yes | White circular star mark |
| Site name | Optional | Useful for metadata and alt/fallback text |
| Primary navigation items | Yes | Home, Destination, Crew, Technology |

### 9.2 Primary navigation content

Each navigation item requires:

| Field | Required | Example |
| --- | --- | --- |
| `index` | Yes | `00` |
| `label` | Yes | `HOME` |
| `href` | Yes | `/` |
| `section` | Yes | `home` |

Navigation items must remain stable across all pages.

### 9.3 Page background content

Each page family requires breakpoint-specific background imagery:

| Page family | Mobile | Tablet | Desktop |
| --- | --- | --- | --- |
| Home | Required | Required | Required |
| Destination | Required | Required | Required |
| Crew | Required | Required | Required |
| Technology | Required | Required | Required |

Required background behavior:

- images are decorative
- images must not be announced by screen readers
- fallback background color must be `#0B0D17`
- image crop must be validated per breakpoint

---

## 10. Global data model requirements

### 10.1 Navigation item

Data shape:

```ts
NavigationItem {
  index: string
  label: string
  href: string
  section: 'home' | 'destination' | 'crew' | 'technology'
}
```

Required fields:

- `index`
- `label`
- `href`
- `section`

Optional fields:

- `ariaLabel`, only when visible text is insufficient
- `shortLabel`, only if tablet/mobile variants require shorter labels

Validation rules:

- `index` must be two digits.
- `label` must be uppercase in output or provided uppercase.
- `href` must map to an existing route or default section route.
- `section` must match one of the known top-level sections.

### 10.2 Responsive image set

Data shape:

```ts
ResponsiveImageSet {
  mobile: string
  tablet?: string
  desktop: string
  alt?: string
}
```

Required fields:

- `mobile`
- `desktop`

Optional fields:

- `tablet`
- `alt`
- `width`
- `height`

Validation rules:

- Decorative backgrounds must not require `alt`.
- Content images must provide meaningful `alt` text.
- If `tablet` is missing, fallback behavior must be explicitly defined and visually checked at the tablet reference width.
- If a tablet crop differs meaningfully from both mobile and desktop, `tablet` becomes required for visual parity.

### 10.3 Page shell contract

Conceptual props/data:

```ts
PageShellProps {
  pageType: 'home' | 'destination' | 'crew' | 'technology'
  activeSection: 'home' | 'destination' | 'crew' | 'technology'
  background: ResponsiveImageSet
  title?: string
}
```

Required fields:

- `pageType`
- `activeSection`
- `background`

Optional fields:

- `title`, for document metadata
- `description`, for document metadata

Responsibilities:

- provide shared background behavior
- provide the top-level layout shell
- expose a semantic main content region
- support navigation active state

---

## 11. Shared layout rules

### 11.1 Viewport behavior

All pages must:

- use a dark background fallback
- fill at least the visible viewport height
- avoid fixed viewport heights copied from the source design artifacts
- avoid horizontal scrolling
- preserve visual composition at 375px, 768px, and 1440px target widths

Required viewport rule:

- page shell minimum height must use a modern dynamic viewport unit such as `100svh` or equivalent behavior.

### 11.2 Containers

Required layout widths:

| Token | Value | Use |
| --- | ---: | --- |
| Main container | `1110px` | Home, Destination, Crew desktop content |
| Technology container | `1275px` | Technology desktop content |
| Narrow content | `445px` | Destination explanation content |
| Medium content | `540px` | Home columns and crew support |
| Tablet content | `512px` | Centered tablet text content |
| Mobile max content | `514px` | Mobile content max width where applicable |

### 11.3 Spacing

The site must use the source-design-derived spacing scale:

| Token | Value |
| --- | ---: |
| `space-100` | `8px` |
| `space-150` | `12px` |
| `space-200` | `16px` |
| `space-300` | `24px` |
| `space-400` | `32px` |
| `space-500` | `40px` |
| `space-600` | `48px` |
| `space-800` | `64px` |
| `space-1600` | `128px` |

Spacing must not be replaced by arbitrary values unless the source design layout requires a specific exception.

---

## 12. Visual token requirements

### 12.1 Colors

Required color tokens:

| Token | Value | Use |
| --- | --- | --- |
| `blue-900` | `#0B0D17` | Base background and dark text on white CTA |
| `blue-300` | `#D0D6F9` | Body copy, inactive labels, inactive tabs, hamburger |
| `white` | `#FFFFFF` | Headings, active states, dividers, CTA background |

Required translucent values:

| Use | Value |
| --- | --- |
| Navigation glass | `rgba(255,255,255,0.05)` |
| Dividers | `rgba(255,255,255,0.25)` |
| Inactive control borders | `rgba(255,255,255,0.25)` |
| Crew role / technology eyebrow opacity | `50%` white |
| Page title index opacity | `25%` white |

### 12.2 Typography

Required font families:

| Role | Font |
| --- | --- |
| Display headings | Bellefair |
| Labels/navigation/tabs | Barlow Condensed |
| Body copy | Barlow |

Required desktop type roles:

| Role | Font | Size | Line height | Letter spacing |
| --- | --- | ---: | ---: | ---: |
| Home heading | Bellefair | `144px` | `1` | `0` |
| Destination heading | Bellefair | `96px` | `1` | `0` |
| Crew/Technology item heading | Bellefair | `56px` | `1` | `0` |
| CTA / role / eyebrow large | Bellefair | `32px` | `1` | `0` |
| Page title | Barlow Condensed | `28px` | `1` | `4px` |
| Stat value | Bellefair | `28px` | `1` | `0` |
| Stat label | Barlow Condensed | `14px` | `1` | `2px` |
| Navigation/tab | Barlow Condensed | `16px` | `1` | `2px` |
| Body | Barlow | `18px` | `1.8` | `0` |

Required mobile type roles:

| Role | Font | Size | Notes |
| --- | --- | ---: | --- |
| Home heading | Bellefair | `80px` | line-height `1` |
| Destination heading | Bellefair | `56px` | line-height `1` |
| Crew/Technology item heading | Bellefair | `24px` | uppercase |
| CTA / role / technology eyebrow | Bellefair | `18px` | line-height `1` |
| Page title / home eyebrow | Barlow Condensed | `16px` | letter spacing around `2.4px` |
| Destination tab | Barlow Condensed | `14px` | letter spacing around `2.1px` |
| Body | Barlow | `15px` | line-height `1.8` |

---

## 13. Shared header and navigation specification

### 13.1 Responsibilities

The shared header must:

- display the site logo
- display primary navigation on tablet and desktop
- display a hamburger trigger on mobile
- visually identify the active top-level section
- preserve the glass navigation style on tablet and desktop
- support keyboard navigation
- expose correct navigation semantics

### 13.2 Content requirements

Primary nav items:

| Index | Label | Default href | Section |
| --- | --- | --- | --- |
| `00` | `HOME` | `/` | `home` |
| `01` | `DESTINATION` | `/destination/moon` | `destination` |
| `02` | `CREW` | `/crew/douglas-hurley` | `crew` |
| `03` | `TECHNOLOGY` | `/technology/launch-vehicle` | `technology` |

### 13.3 Required fields

Header requires:

- logo asset
- navigation item collection
- active section
- mobile menu label

### 13.4 Optional fields

Header may support:

- custom logo alt text
- custom navigation aria label
- mobile menu open state label
- mobile menu close state label

### 13.5 Layout rules

Desktop:

- top padding: `40px`
- logo size: `48px`
- left padding: `64px`
- logo-to-divider gap: `64px`
- divider height: `1px`
- divider opacity: `25%`
- nav panel height: `96px`
- nav panel minimum width: about `664px`
- nav panel horizontal padding: `64px`
- nav item gap: `48px`
- active underline: `3px` white

Tablet:

- logo size: `48px`
- left padding: `40px`
- no visible divider
- nav panel height: `96px`
- nav panel horizontal padding: `40px`
- nav item gap: `48px`, reducible only if needed for overflow

Mobile:

- logo size: `40px`
- header vertical padding: `24px`
- horizontal padding: `24px`
- hide desktop/tablet nav links
- show hamburger button
- hamburger visual: three bars, each about `24px × 3px`

### 13.6 Accessibility requirements

The header must:

- be inside a semantic `<header>` landmark
- include a `<nav aria-label="Primary">` for primary navigation
- use links for route navigation
- mark active link with `aria-current="page"` or equivalent route-current state
- preserve the same element type for active and inactive navigation items
- expose the mobile hamburger as a real button
- include `aria-expanded` and `aria-controls` on the mobile menu trigger if a menu is implemented
- provide visible focus states for all links and buttons

### 13.7 Interaction behavior

Primary nav links:

- default: white text
- hover: visible hover affordance
- focus-visible: keyboard-visible focus state
- active: persistent white underline

Mobile menu trigger:

- default: visible hamburger
- focus-visible: visible focus ring/outline
- must open or reveal a functional mobile navigation experience
- trigger toggles `aria-expanded` when controlling a menu
- Escape closes the menu
- focus returns to the trigger after the menu closes

Assumption: because mobile hides the desktop/tablet nav links, the hamburger cannot be decorative-only.

### 13.8 Edge cases

- If tablet nav overflows, spacing may compress but labels must remain readable.
- If the Home tablet number inconsistency remains unresolved, implement consistent nav behavior and mark the source-design inconsistency in review notes.
- If backdrop blur is unsupported, nav glass must fall back to a translucent background.
- If the mobile open-menu visual is still unapproved at implementation time, use a minimal accessible inferred menu and flag it for visual review.

---

## 14. Page title specification

### 14.1 Responsibilities

The page title pattern must:

- identify the current content section
- display a muted two-digit section index
- display an uppercase section label
- align differently across breakpoints according to page family

### 14.2 Data model / props

```ts
PageTitleProps {
  index: string
  label: string
  align?: 'start' | 'center'
}
```

Required fields:

- `index`
- `label`

Optional fields:

- `align`

Validation rules:

- `index` must be two digits.
- `label` must be uppercase in visual output.
- The index must be visible but visually secondary.

### 14.3 Layout rules

Desktop:

- index and label displayed inline
- gap: `24px`
- text size: `28px`
- label letter spacing: `4px`
- index letter spacing: about `4.725px`
- index opacity: `25%`

Mobile:

- usually centered
- text size: `16px`
- letter spacing: about `2.4px`
- gap remains visually close to `24px`

---

## 15. Home page specification

### 15.1 Responsibilities

The Home page must:

- introduce the space tourism concept
- display the primary brand hero message
- provide a clear path into the Destination section
- establish the full-screen immersive visual language

### 15.2 Content requirements

Required content:

| Field | Required | Value |
| --- | --- | --- |
| Eyebrow | Yes | `SO, YOU WANT TO TRAVEL TO` |
| Heading | Yes | `SPACE` |
| Body | Yes | `Let’s face it; if you want to go to space, you might as well genuinely go to outer space and not hover kind of on the edge of it. Well sit back, and relax because we’ll give you a truly out of this world experience!` |
| CTA label | Yes | `EXPLORE` |
| CTA href | Yes | Assumed `/destination/moon` |
| Background image set | Yes | Home mobile/tablet/desktop |

### 15.3 Data model / props

```ts
HomeContent {
  eyebrow: string
  heading: string
  body: string
  cta: {
    label: string
    href: string
  }
  background: ResponsiveImageSet
}
```

Required fields:

- `eyebrow`
- `heading`
- `body`
- `cta.label`
- `cta.href`
- `background.mobile`
- `background.desktop`

Optional fields:

- `background.tablet`
- `seoTitle`
- `seoDescription`

### 15.4 Layout rules

Desktop:

- target frame: `1440 × 1024`
- main container max width: `1110px`
- main vertical padding: `128px`
- hero uses two columns
- text column max width: `540px`
- CTA column max width: `540px`
- text aligns left
- CTA aligns right
- content sits toward the lower area of the viewport

Tablet:

- target frame: `768 × 1024`
- layout stacks vertically
- text block width about `512px`
- text aligns center
- CTA remains `272px`
- main horizontal padding: `40px`
- main vertical padding: `128px`

Mobile:

- target frame: `375 × 812`
- layout stacks vertically
- text aligns center
- page padding: `24px`
- CTA size: `144px`
- content must remain readable without horizontal scrolling

### 15.5 Responsive typography

Desktop:

- eyebrow: `28px`, Barlow Condensed, `4px` letter spacing
- heading: `144px`, Bellefair
- body: `18px`, Barlow, line-height `1.8`
- CTA: `32px`, Bellefair

Mobile:

- eyebrow: `16px`, Barlow Condensed, about `2.4px` letter spacing
- heading: `80px`, Bellefair
- body: `15px`, Barlow, line-height `1.8`
- CTA: `18px`, Bellefair

### 15.6 Interaction behavior

Explore CTA:

- must behave as a link
- must navigate to the Destination default page
- must have default, hover, and focus-visible states
- hover/focus may include the expected translucent halo
- must remain usable with reduced motion enabled

### 15.7 Edge cases

- If viewport height is short, content must not overlap the header or CTA.
- If the background image fails, text must remain readable on the dark fallback color.
- If body text wraps differently on very narrow widths, maintain centered layout and adequate line height.

### 15.8 Acceptance criteria

- Home page renders all required content.
- CTA is a real link and is keyboard focusable.
- Background uses breakpoint-appropriate crop.
- Typography matches the visual hierarchy in the source design artifacts.
- Layout matches mobile, tablet, and desktop compositions.

---

## 16. Destination template specification

### 16.1 Responsibilities

The Destination template must:

- present a selected travel destination
- allow navigation between all destinations
- show destination image, description, average distance, and estimated travel time
- preserve the shared destination layout across all destination items

### 16.2 Destination collection requirements

The product must include four destination items:

1. Moon
2. Mars
3. Europa
4. Titan

Each item must have:

- slug
- display name
- description
- average distance
- estimated travel time
- destination image
- image alt text

### 16.3 Data model / props

```ts
DestinationItem {
  slug: string
  name: string
  description: string
  distance: string
  travelTime: string
  image: {
    src: string
    alt: string
    width?: number
    height?: number
  }
}

DestinationPageProps {
  item: DestinationItem
  items: DestinationItem[]
  activeSlug: string
  pageTitle: {
    index: '01'
    label: 'PICK YOUR DESTINATION'
  }
  background: ResponsiveImageSet
}
```

Required fields:

- `slug`
- `name`
- `description`
- `distance`
- `travelTime`
- `image.src`
- `image.alt`
- `items`
- `activeSlug`
- `background.mobile`
- `background.desktop`

Optional fields:

- `image.width`
- `image.height`
- `background.tablet`
- `seoTitle`
- `seoDescription`

Validation rules:

- `items` must contain exactly the visible destination navigation items unless design changes.
- `activeSlug` must match one item in `items`.
- `name` should render uppercase visually.
- `distance` and `travelTime` must be non-empty strings.

### 16.4 Content requirements

Reviewed Moon reference content:

| Field | Value |
| --- | --- |
| Name | `MOON` |
| Description | `See our planet as you’ve never seen it before. A perfect relaxing trip away to help regain perspective and come back refreshed. While you’re there, take in some history by visiting the Luna 2 and Apollo 11 landing sites.` |
| Distance label | `AVG. DISTANCE` |
| Distance | `384,400 km` |
| Travel time label | `EST. TRAVEL TIME` |
| Travel time | `3 days` |

Content for Mars, Europa, and Titan must be provided in the same shape.

### 16.5 Layout rules

Desktop:

- target frame: `1440 × 1024`
- content container max width: `1110px`
- page title appears above content
- page title aligns left
- main content uses two columns
- column gap: `32px`
- planet image column centers image
- explanation column max width: about `445px`
- planet image visual size: about `480px` for Moon reference
- tabs appear above destination name
- stats display as two columns

Tablet:

- content stacks vertically
- composition centers horizontally
- planet image is between mobile and desktop scale
- tabs are centered
- destination text is centered
- stats may remain two columns if width supports it

Mobile:

- target frame: `375 × 880`
- flow order:
  1. header
  2. page title
  3. planet image
  4. destination nav/tabs
  5. destination name
  6. description
  7. divider
  8. statistics
- page padding: `24px`
- page title centered
- planet image visual size: about `150px`
- tabs horizontal with `32px` gap
- stats stack vertically and center

### 16.6 Sub-navigation requirements

Destination navigation must display:

- `MOON`
- `MARS`
- `EUROPA`
- `TITAN`

If implemented as routes:

- each destination control is a link
- active item uses `aria-current="page"`
- active item has white text and `3px` underline
- inactive items use `blue-300`

If implemented as tabs later:

- must follow ARIA tabs pattern
- must support arrow-key navigation
- must connect tabs and panels through ARIA attributes

Assumption: route links are preferred.

### 16.7 Accessibility requirements

- Page must have a single logical main heading for the destination name or page context.
- Planet image must have meaningful alt text, e.g. `The Moon`.
- Destination navigation must be keyboard accessible.
- Active destination must be announced through `aria-current` or ARIA tab state.
- Statistics must be readable as label/value pairs.

### 16.8 Interaction behavior

Destination controls:

- default inactive: blue-300 text
- hover/focus: clear visual affordance
- active: white text and white underline
- selecting another destination navigates or updates selected content depending on final route strategy

### 16.9 Edge cases

- Long destination names must not break the layout unexpectedly.
- Longer descriptions must maintain readable line length.
- Missing distance or travel time should not render empty visual labels; missing data must be handled explicitly.
- If a planet image fails, text content and navigation must remain usable.
- Destination tabs may overflow on very narrow screens if labels or spacing change; overflow must be avoided.

### 16.10 Acceptance criteria

- All four destinations are accessible from destination navigation.
- Active destination state is visually and semantically clear.
- Destination layout matches the reviewed reference mockups at mobile, tablet, and desktop reference widths.
- Planet image size and position follow the visual intent.
- Stats render as two columns on desktop and stacked on mobile.

---

## 17. Crew template specification

### 17.1 Responsibilities

The Crew template must:

- present a selected crew member
- show role, name, biography, and portrait
- allow navigation between all crew members
- preserve the shared Crew layout and pagination behavior

### 17.2 Crew collection requirements

The product must include four crew members:

1. Douglas Hurley
2. Mark Shuttleworth
3. Victor Glover
4. Anousheh Ansari

Each crew member must have:

- slug
- name
- role
- bio
- portrait image
- image alt text

### 17.3 Data model / props

```ts
CrewMember {
  slug: string
  name: string
  role: string
  bio: string
  image: {
    src: string
    alt: string
    width?: number
    height?: number
  }
}

CrewPageProps {
  member: CrewMember
  members: CrewMember[]
  activeSlug: string
  pageTitle: {
    index: '02'
    label: 'MEET YOUR CREW'
  }
  background: ResponsiveImageSet
}
```

Required fields:

- `slug`
- `name`
- `role`
- `bio`
- `image.src`
- `image.alt`
- `members`
- `activeSlug`
- `background.mobile`
- `background.desktop`

Optional fields:

- `image.width`
- `image.height`
- `background.tablet`
- `seoTitle`
- `seoDescription`

Validation rules:

- `members` must contain the four visible pagination items unless design changes.
- `activeSlug` must match one member.
- `role` and `name` should render uppercase visually.
- `bio` must be clean text and must not include generated design-export empty paragraphs.

### 17.4 Content requirements

Reviewed Douglas Hurley reference content:

| Field | Value |
| --- | --- |
| Role | `Commander` |
| Name | `Douglas Hurley` |
| Bio | `Douglas Gerald Hurley is an American engineer, former Marine Corps pilot and former NASA astronaut. He launched into space for the third time as commander of Crew Dragon Demo-2.` |

Content for the remaining crew members must be provided in the same shape.

### 17.5 Layout rules

Desktop:

- target frame: `1440 × 1024`
- content container max width: `1110px`
- page title appears above content
- main content uses two columns
- left column contains role/name/bio and dot pagination
- right column contains crew portrait
- role/name/bio align left
- portrait aligns to the lower portion of the content area
- dot pagination sits near the lower part of the left column

Tablet:

- target frame: `768 × 1024`
- content should remain centered rather than switching too early to the desktop two-column layout
- role/name/bio should appear before pagination and portrait unless an approved tablet reference says otherwise
- dot pagination stays close to the text block
- portrait remains below or visually subordinate to the text block
- vertical spacing must prevent the bio, dots, and portrait from colliding on shorter tablet-height viewports

Assumption: the tablet Crew experience follows the small-screen reading order because the reviewed smaller-screen references prioritize text before portrait.

Mobile:

- target frame: `375 × 880`
- flow order:
  1. header
  2. page title
  3. role/name/bio
  4. dot pagination
  5. portrait image
- page padding: `24px`
- content aligns center
- role size: `18px`
- name size: `24px`
- bio size: `15px`, line-height `1.8`
- dot size: `10px`
- dot gap: `16px`
- portrait reference height: about `340px` for Douglas frame

### 17.6 Pagination requirements

Crew pagination must represent four crew members with dot controls.

If implemented as routes:

- each dot is a link
- each dot has an accessible label, e.g. `View Douglas Hurley`
- active dot uses `aria-current="page"`
- active dot is white
- inactive dots are white at reduced opacity

### 17.7 Accessibility requirements

- Crew portrait must have meaningful alt text, e.g. `Douglas Hurley`.
- Dot controls must not be unlabeled.
- The active crew member must be communicated semantically.
- Text content must remain selectable and readable as text.
- Focus states must be visible for dot controls.

### 17.8 Interaction behavior

Crew dot controls:

- inactive: low-opacity white
- hover/focus: stronger white opacity or visible focus state
- active: white
- selecting a dot navigates to or displays the selected crew member

### 17.9 Edge cases

- Long crew names must not overflow on mobile.
- Long bios must not overlap the portrait.
- Portraits with different aspect ratios must align consistently with the design.
- Missing portrait must not break layout.
- The mobile order must follow the reviewed source-design order unless intentionally changed later.

### 17.10 Acceptance criteria

- All four crew members are reachable.
- Active crew member state is visually and semantically clear.
- Dot controls have accessible labels.
- Mobile order matches the reviewed reference mockups.
- generated design-export empty paragraph artifacts are not present.

---

## 18. Technology template specification

### 18.1 Responsibilities

The Technology template must:

- present a selected technology item
- show terminology eyebrow, item name, description, and image
- allow navigation between all technology items
- preserve the major responsive layout shift between desktop and mobile

### 18.2 Technology collection requirements

The product must include three technology items:

1. Launch Vehicle
2. Spaceport
3. Space Capsule

Each technology item must have:

- slug
- name
- description
- portrait image
- landscape image
- image alt text

### 18.3 Data model / props

```ts
TechnologyItem {
  slug: string
  name: string
  description: string
  images: {
    portrait?: string
    landscape?: string
    alt: string
  }
}

TechnologyPageProps {
  item: TechnologyItem
  items: TechnologyItem[]
  activeSlug: string
  pageTitle: {
    index: '03'
    label: 'SPACE LAUNCH 101'
  }
  eyebrow: 'THE TERMINOLOGY…'
  background: ResponsiveImageSet
}
```

Required fields:

- `slug`
- `name`
- `description`
- `images.alt`
- at least one of `images.portrait` or `images.landscape`
- `items`
- `activeSlug`
- `eyebrow`
- `background.mobile`
- `background.desktop`

Optional fields:

- `background.tablet`
- `seoTitle`
- `seoDescription`

Validation rules:

- `items` must contain exactly the three visible technology controls unless design changes.
- `activeSlug` must match one item.
- `name` should render uppercase visually.
- `portrait` and `landscape` are both expected for production visual parity because the responsive crop changes significantly.
- If one orientation is missing, the fallback must be documented and flagged as a visual QA risk.

### 18.4 Content requirements

Reviewed Launch Vehicle reference content:

| Field | Value |
| --- | --- |
| Eyebrow | `THE TERMINOLOGY…` |
| Name | `LAUNCH VEHICLE` |
| Description | `A launch vehicle or carrier rocket is a rocket-propelled vehicle used to carry a payload from Earth's surface to space, usually to Earth orbit or beyond. Our WEB-X carrier rocket is the most powerful in operation. Standing 150 metres tall, it's quite an awe-inspiring sight on the launch pad!` |

Content for Spaceport and Space Capsule must be provided in the same shape.

### 18.5 Layout rules

Desktop:

- target frame: `1440 × 1024`
- container max width: about `1275px`
- page title aligns left
- content row contains numbered pagination, text content, and image
- pagination and text area minimum width: about `635px`
- pagination is vertical
- pagination/text gap: `64px`
- content/image gap: `32px`
- image is positioned on the right
- desktop image uses portrait crop
- image frame height: about `600px`

Tablet:

- target frame: `768 × 1024`
- landscape image appears above pagination and text
- numbered pagination is horizontal
- text content is centered
- description width remains constrained for readability
- image crop must be validated separately from desktop

Assumption: tablet follows the mobile image-first flow rather than the desktop right-side portrait layout unless a future reference confirms otherwise.

Mobile:

- target frame: `375 × 880`
- flow order:
  1. header
  2. page title
  3. landscape image
  4. horizontal numbered pagination
  5. eyebrow/name/description
- page title centered
- image is wide/full-bleed relative to content
- pagination circles are `40px`
- pagination gap: `16px`
- text aligns center
- eyebrow size: `18px`
- name size: `24px`
- body size: `15px`, line-height `1.8`

### 18.6 Pagination requirements

Technology pagination must represent three items with numbered circular controls:

| Number | Item |
| --- | --- |
| `1` | Launch Vehicle |
| `2` | Spaceport |
| `3` | Space Capsule |

If implemented as routes:

- each number is a link
- active number uses `aria-current="page"`
- each number has an accessible label, e.g. `View launch vehicle`

### 18.7 Accessibility requirements

- Technology image must have meaningful alt text, e.g. `Launch vehicle lifting off`.
- Numbered controls must have accessible labels.
- Active item must be communicated semantically.
- The visual number alone is not enough for screen-reader context.
- Focus states must be visible on circular controls.

### 18.8 Interaction behavior

Technology controls:

- active: white circle, dark text
- inactive: transparent circle, white text, translucent white border
- hover/focus: stronger border or visible focus state
- selecting another control navigates to or displays the selected item

### 18.9 Edge cases

- If only one image orientation is available, visual parity with the source design artifacts will likely fail.
- Long technology names must wrap without overlapping pagination or image.
- Long descriptions must maintain readable line length.
- The desktop image must not collapse too small on intermediate widths.
- Mobile landscape image must not cause horizontal scrolling.

### 18.10 Acceptance criteria

- All three technology items are reachable.
- Desktop uses right-side portrait image composition.
- Mobile uses top landscape image composition.
- Active numbered control is visually and semantically clear.
- Text remains readable and centered on mobile.

---

## 19. Interaction specification

### 19.1 Route navigation

All route links must:

- be keyboard focusable
- have visible focus states
- navigate without broken routes
- identify active page/section semantically

### 19.2 Hover states

Where the source design artifacts only show default/active states, hover states must be inferred conservatively:

- nav links may show underline or increased opacity
- destination tabs may move toward white text or underline
- crew dots may increase opacity
- technology circles may strengthen border
- Explore CTA may show a translucent halo

### 19.3 Focus-visible states

Every interactive element must have a visible focus state that does not rely only on subtle opacity changes.

Required focusable elements:

- logo link if logo navigates home
- primary navigation links
- mobile menu trigger
- Explore CTA
- destination links
- crew pagination links
- technology pagination links

### 19.4 Reduced motion

Any transition or animation must respect reduced motion preferences.

Motion must be optional and must not be required to understand state changes.

---

## 20. Accessibility specification

### 20.1 Landmarks

Each page must include:

- skip link to main content
- semantic header
- primary navigation landmark
- semantic main landmark

### 20.2 Headings

Each page must have a coherent heading structure.

Required heading behavior:

- Home should expose `SPACE` as the main page heading.
- Destination pages should expose the selected destination name as the main page heading or ensure equivalent hierarchy.
- Crew pages should expose the selected crew member name as the primary content heading.
- Technology pages should expose the selected technology name as the primary content heading.

The visual page title such as `01 PICK YOUR DESTINATION` may be a label/eyebrow but must not create a confusing heading order.

### 20.3 Images

Decorative images:

- background images must be hidden from assistive technology
- decorative dividers and shapes must not be announced

Content images:

- destination images require descriptive alt text
- crew portraits require descriptive alt text
- technology images require descriptive alt text

### 20.4 Active state semantics

Active state must be communicated using semantic attributes:

| UI | Semantic state |
| --- | --- |
| Main nav active section | `aria-current="page"` or route-aware current state |
| Destination active item | `aria-current="page"` if route-based |
| Crew active item | `aria-current="page"` if route-based |
| Technology active item | `aria-current="page"` if route-based |
| JavaScript tabs, if used | ARIA tabs pattern |

### 20.5 Touch targets

Interactive controls must provide usable touch targets.

Minimum expected behavior:

- small visual dots may have larger invisible clickable area
- mobile hamburger must be easy to tap
- destination tab labels must be comfortably selectable on mobile
- technology circles already meet size requirements visually

### 20.6 Contrast and user preference modes

The implementation must remain usable when:

- browser zoom or text zoom is increased
- reduced motion is enabled
- forced-colors/high-contrast modes are active
- backdrop blur is unavailable

State must not rely only on subtle opacity changes. Use semantic state plus visible focus/active indicators.

---

## 21. Edge case specification

### 21.1 Content edge cases

The UI must handle:

- longer destination descriptions
- longer crew bios
- long crew names
- long technology names
- missing optional image dimensions
- missing optional tablet image fallback
- inconsistent capitalization in source data

Required behavior:

- text may wrap naturally
- layout must not overlap key content
- route controls must remain visible
- missing required content must be caught before rendering or handled with a safe fallback

### 21.2 Layout edge cases

The UI must handle:

- mobile viewport heights shorter than reference frames
- browser chrome changing viewport height
- intermediate widths between 768px and 1440px
- no backdrop-filter support
- high text zoom / browser zoom
- reduced motion users
- slow image loading
- safe-area insets on mobile devices with notches or browser UI overlays
- forced-colors/high-contrast user settings

### 21.3 Data edge cases

The data layer must prevent:

- duplicate slugs
- empty required labels
- active slug with no matching item
- routes pointing to missing content
- unlabeled interactive controls
- content images without alt text

---

## 22. WordPress translation requirements

This section defines product requirements for future WordPress translation without choosing a final implementation method.

### 22.1 Theme token requirements

The final WordPress block theme must be able to express:

- colors from the design token set
- typography families and sizes
- spacing scale
- layout widths
- global background color
- link and focus styles

### 22.2 Template requirements

The final WordPress block theme must support page templates for:

- Home
- Destination detail
- Crew detail
- Technology detail

### 22.3 Template part requirements

The final WordPress block theme must support reusable shared regions:

- Header/navigation
- Page title pattern
- Optional mobile navigation pattern if implemented

### 22.4 Content mapping requirements

The content model must be clear enough to map later to one of these WordPress structures:

- static pages with block patterns
- reusable synced/non-synced patterns
- custom post types for Destination, Crew, and Technology
- block attributes populated by curated data

Open question: the preferred WordPress content model has not been decided.

---

## 23. Acceptance criteria

### 23.1 Global acceptance criteria

The project meets this specification when:

- all required pages/routes exist or have defined route behavior
- all page families match the reviewed reference mockups at the 375px, 768px, and 1440px visual targets
- layouts remain usable at intermediate widths without horizontal scrolling
- global colors, spacing, and typography match `DESIGN.md`
- shared navigation appears consistently across pages and remains functional on mobile
- active navigation state is visually and semantically clear
- backgrounds and content images use appropriate responsive crops or documented fallbacks
- text remains real selectable text
- image alt behavior is correct for decorative vs content imagery
- all interactive elements are keyboard accessible
- all focus states are visible against dark backgrounds
- small visual controls expose larger practical touch/focus targets when needed
- reduced motion preferences are respected
- high-contrast or forced-colors modes do not make controls unusable
- no footer is rendered unless a footer design is provided

### 23.2 Home acceptance criteria

- Home displays eyebrow, `SPACE` heading, body copy, and Explore CTA.
- Explore CTA navigates to the default Destination page.
- CTA size is `272px` on desktop/tablet and `144px` on mobile.
- Home layout is two-column on desktop and centered stacked on tablet/mobile.

### 23.3 Destination acceptance criteria

- Moon, Mars, Europa, and Titan are available.
- Active destination is visually and semantically identified.
- Planet image, description, distance, and travel time render for each destination.
- Stats are two-column on desktop and stacked on mobile.
- Destination navigation remains usable on mobile.

### 23.4 Crew acceptance criteria

- All four crew members are available.
- Active crew member is visually and semantically identified.
- Dot controls have accessible labels.
- Role, name, bio, and portrait render for each crew member.
- Mobile content order follows the reviewed reference mockups: text, pagination, image.

### 23.5 Technology acceptance criteria

- Launch Vehicle, Spaceport, and Space Capsule are available.
- Active technology item is visually and semantically identified.
- Numbered controls have accessible labels.
- Desktop uses right-side portrait image layout.
- Mobile uses top landscape image layout.
- Text content remains centered and readable on mobile.

### 23.6 Accessibility acceptance criteria

- Keyboard users can reach and operate all links and controls.
- Screen-reader users can identify the current page/section/item.
- Decorative imagery is not announced.
- Content imagery has useful alt text.
- Focus indicators are visible against dark backgrounds.
- The mobile menu trigger is a real button and exposes its state when controlling the mobile menu.

---

## 24. Review notes

### First review

The specification was checked against the source design structure, representative Home/Destination/Crew/Technology reference frames, and token definitions. Wrapper-level source artifacts, the empty footer placeholder, tablet nav inconsistency, mobile menu open-state gap, and generated design-export markup limitations are reflected as assumptions, open questions, or edge cases.

### Second review

The specification was checked against `DESIGN.md` for alignment. It preserves the same page inventory, token system, responsive model, accessibility direction, and implementation constraints while avoiding implementation planning or component code.
