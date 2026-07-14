# Space Tourism Website — DESIGN.md

## 1. Purpose

This document translates the inspected source design artifacts into a practical design specification for implementation. The wording is intentionally tool-agnostic: source design artifacts may be design files, screenshots, exported mockups, Penpot files, PDFs, or another approved visual reference.

The goal is not to copy the design tool's generated React/Tailwind-like output. The goal is to preserve the visual design, interaction model, responsive behavior, and accessibility intent while implementing the site in a maintainable Astro + HTML + CSS architecture.

---

## 2. Product and visual direction

The website is an immersive editorial-style space tourism experience. It should feel premium, cinematic, calm, and spacious.

The design relies on:

- dark full-bleed space photography
- elegant serif display typography
- narrow uppercase labels
- generous negative space
- minimal UI chrome
- subtle glassmorphism in the navigation
- large expressive imagery
- clear page-level hierarchy

The UI should not feel like a dashboard or app interface. It should feel like a polished editorial landing experience with simple interactive navigation.

---

## 3. Page inventory

The current source design artifacts contain the following pages and responsive reference frames.

### Home

- Mobile: 375 × 812
- Tablet: 768 × 1024
- Desktop: 1440 × 1024

### Destination

The destination pages share one template.

- Moon
  - Mobile
  - Tablet
  - Desktop
- Mars
  - Mobile
  - Tablet
  - Desktop
- Europa
  - Mobile
  - Tablet
  - Desktop
- Titan
  - Mobile
  - Tablet
  - Desktop

### Crew

The crew pages share one template.

- Douglas Hurley
  - Mobile
  - Tablet
  - Desktop
- Mark Shuttleworth
  - Mobile
  - Tablet
  - Desktop
- Victor Glover
  - Mobile
  - Tablet
  - Desktop
- Anousheh Ansari
  - Mobile
  - Tablet
  - Desktop

### Technology

The technology pages share one template.

- Launch Vehicle
  - Mobile
  - Tablet
  - Desktop
- Spaceport
  - Mobile
  - Tablet
  - Desktop
- Space Capsule
  - Mobile
  - Tablet
  - Desktop

---

## 4. Core design system

### 4.1 Colors

Use a very small color system. Do not create additional color tokens unless the implementation proves they are needed.

```css
:root {
  --color-blue-900: #0b0d17;
  --color-blue-300: #d0d6f9;
  --color-white: #ffffff;
}
```

Usage guidance:

- `--color-blue-900` is the base page background and fallback behind images.
- `--color-blue-300` is used for body copy, inactive labels, inactive tab text, and the mobile menu icon.
- `--color-white` is used for primary headings, active states, borders, dividers, and the Home CTA background.
- Translucent white is used for navigation glass and inactive controls.

Recommended utility-like aliases:

```css
:root {
  --color-nav-glass: rgb(255 255 255 / 0.05);
  --color-divider: rgb(255 255 255 / 0.25);
  --color-control-border: rgb(255 255 255 / 0.25);
  --color-focus-ring: #ffffff;
}
```

### 4.2 Typography

The design uses three typefaces:

```css
:root {
  --font-serif: "Bellefair", serif;
  --font-sans: "Barlow", sans-serif;
  --font-condensed: "Barlow Condensed", sans-serif;
}
```

Typography roles:

- Bellefair: display headings, destination names, crew names, technology names, CTA text, stat values, pagination numbers.
- Barlow Condensed: navigation, page labels, eyebrow text, tab labels, stat labels.
- Barlow: body copy.

#### Desktop typography tokens

```css
:root {
  --text-preset-1-size: 9rem;      /* 144px */
  --text-preset-2-size: 6rem;      /* 96px */
  --text-preset-3-size: 3.5rem;    /* 56px */
  --text-preset-4-size: 2rem;      /* 32px */
  --text-preset-5-size: 1.75rem;   /* 28px */
  --text-preset-6-size: 1.75rem;   /* 28px */
  --text-preset-7-size: 0.875rem;  /* 14px */
  --text-preset-8-size: 1rem;      /* 16px */
  --text-preset-9-size: 1.125rem;  /* 18px */
}
```

#### Mobile typography tokens

```css
:root {
  --mobile-text-preset-1-size: 5rem;       /* 80px */
  --mobile-text-preset-2-size: 3.5rem;     /* 56px */
  --mobile-text-preset-3-size: 1.5rem;     /* 24px */
  --mobile-text-preset-4-size: 1.125rem;   /* 18px */
  --mobile-text-preset-6-size: 1rem;       /* 16px */
  --mobile-text-preset-8-size: 0.875rem;   /* 14px */
  --mobile-text-preset-9-size: 0.9375rem;  /* 15px */
}
```

#### Typography classes

Recommended global classes:

```css
.text-display-xl {
  font-family: var(--font-serif);
  font-size: var(--text-preset-1-size);
  font-weight: 400;
  line-height: 1;
  color: var(--color-white);
}

.text-display-lg {
  font-family: var(--font-serif);
  font-size: var(--text-preset-2-size);
  font-weight: 400;
  line-height: 1;
  color: var(--color-white);
}

.text-display-md {
  font-family: var(--font-serif);
  font-size: var(--text-preset-3-size);
  font-weight: 400;
  line-height: 1;
  color: var(--color-white);
}

.text-display-sm {
  font-family: var(--font-serif);
  font-size: var(--text-preset-4-size);
  font-weight: 400;
  line-height: 1;
}

.text-page-title {
  font-family: var(--font-condensed);
  font-size: var(--text-preset-5-size);
  font-weight: 400;
  line-height: 1;
  letter-spacing: 4px;
  text-transform: uppercase;
}

.text-nav {
  font-family: var(--font-condensed);
  font-size: var(--text-preset-8-size);
  font-weight: 400;
  line-height: 1;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.text-nav-index {
  font-family: var(--font-condensed);
  font-size: var(--text-preset-8-size);
  font-weight: 700;
  line-height: 1;
  letter-spacing: 2.7px;
}

.text-body {
  font-family: var(--font-sans);
  font-size: var(--text-preset-9-size);
  font-weight: 400;
  line-height: 1.8;
  color: var(--color-blue-300);
}
```

Mobile adjustments should be applied per component, not by blindly scaling everything. The Home title, destination title, crew name, technology name, and body copy each have specific mobile values.

### 4.3 Spacing

Use the spacing tokens found in the source design artifacts.

```css
:root {
  --space-100: 0.5rem;   /* 8px */
  --space-150: 0.75rem;  /* 12px */
  --space-200: 1rem;     /* 16px */
  --space-300: 1.5rem;   /* 24px */
  --space-400: 2rem;     /* 32px */
  --space-500: 2.5rem;   /* 40px */
  --space-600: 3rem;     /* 48px */
  --space-800: 4rem;     /* 64px */
  --space-1600: 8rem;    /* 128px */
}
```

### 4.4 Layout widths

Important fixed/max widths from the design:

```css
:root {
  --container-main: 1110px;
  --container-technology: 1275px;
  --content-narrow: 445px;
  --content-medium: 540px;
  --content-tablet: 512px;
  --content-mobile-max: 514px;
}
```

---

## 5. Breakpoints and responsive model

The reference frames imply three primary breakpoints:

```css
:root {
  --breakpoint-mobile: 375px;
  --breakpoint-tablet: 768px;
  --breakpoint-desktop: 1440px;
}
```

Recommended implementation breakpoints:

```css
/* Mobile first */
@media (min-width: 48rem) {
  /* tablet and up: 768px */
}

@media (min-width: 64rem) {
  /* desktop layout starts here when space allows */
}

@media (min-width: 90rem) {
  /* large desktop: 1440px design target */
}
```

Use fluid CSS where possible, but preserve the design proportions at the three inspected frame widths.

Use `min-height: 100svh` for pages instead of fixed viewport heights. The desktop reference target is 1024px high, but the browser must adapt to real viewport height.

---

## 6. Recommended implementation architecture

Do not implement every reference frame as a separate component. The source design artifacts contain multiple page states that should become reusable templates.

Recommended Astro structure:

```txt
src/
  components/
    layout/
      PageShell.astro
      SiteHeader.astro

    navigation/
      MainNav.astro
      MobileMenuButton.astro

    common/
      BackgroundPicture.astro
      PageTitle.astro

    home/
      HomeHero.astro
      ExploreButton.astro

    destination/
      DestinationLayout.astro
      DestinationTabs.astro
      DestinationStats.astro

    crew/
      CrewLayout.astro
      CrewPagination.astro

    technology/
      TechnologyLayout.astro
      TechnologyPagination.astro

  data/
    navigation.ts
    destinations.ts
    crew.ts
    technology.ts

  styles/
    tokens.css
    typography.css
    global.css
```

Recommended route model:

```txt
/
/destination/moon
/destination/mars
/destination/europa
/destination/titan
/crew/douglas-hurley
/crew/mark-shuttleworth
/crew/victor-glover
/crew/anousheh-ansari
/technology/launch-vehicle
/technology/spaceport
/technology/space-capsule
```

The destination tabs, crew pagination, and technology pagination should be implemented as route links unless the project intentionally requires client-side state changes.

---

## 7. Shared page shell

All pages share these requirements:

- dark base background: `--color-blue-900`
- full-bleed background image
- fixed visual brand/navigation region at the top
- main content above background imagery
- no visible footer in the inspected designs
- page content should sit within responsive containers
- decorative background images should not be announced by screen readers

Recommended shell responsibilities:

- set page-level background variant
- render `SiteHeader`
- render page content in a semantic `<main>`
- provide `min-height: 100svh`
- prevent horizontal overflow caused by wide imagery/crops

Example shell semantics:

```html
<body>
  <div class="page-shell page-shell--home">
    <header class="site-header">...</header>
    <main id="main-content">...</main>
  </div>
</body>
```

---

## 8. Navigation design

### 8.1 Shared behavior

Navigation contains four main sections:

| Index | Label | Route |
| --- | --- | --- |
| 00 | Home | `/` |
| 01 | Destination | `/destination/moon` |
| 02 | Crew | `/crew/douglas-hurley` |
| 03 | Technology | `/technology/launch-vehicle` |

Use `<nav aria-label="Primary">`.

Use real links for navigation items. The active link should use `aria-current="page"` or `aria-current="location"` depending on route strategy.

### 8.2 Desktop navigation

Desktop measurements:

- top padding: `40px`
- logo size: `48px`
- left padding: `64px`
- logo-to-line gap: `64px`
- divider height: `1px`
- divider opacity: `25%`
- nav panel height: `96px`
- nav panel min width: about `664px`
- nav panel horizontal padding: `64px`
- nav item gap: `48px`
- active underline: `3px solid white`
- nav glass: `rgba(255,255,255,0.05)` with `backdrop-filter: blur(40px)`

Expected visual behavior:

- logo sits left
- divider extends behind/toward the nav glass area
- nav glass occupies the right side
- active section is indicated by a white underline at the bottom of the 96px nav item height

### 8.3 Tablet navigation

Tablet measurements:

- logo size: `48px`
- logo area left padding: `40px`
- no visible horizontal divider
- nav glass remains visible
- nav panel padding: `40px`
- nav gap: `48px`
- nav height: `96px`

Design inconsistency to resolve:

In the inspected Home tablet frame, the active `HOME` link appears without the `00` prefix while the other links still include their numbers. Desktop includes `00 HOME`. Treat this as a design inconsistency unless confirmed otherwise. Recommended implementation: keep the index behavior consistent for all tablet links, or intentionally hide all indexes on tablet if the layout becomes crowded.

### 8.4 Mobile navigation

Mobile measurements:

- header vertical padding: `24px`
- logo size: `40px`
- horizontal page padding: `24px`
- hamburger icon: three bars, `24px × 3px`
- hamburger bar color: `--color-blue-300`
- bars separated by about `6px`

The hamburger must be a real button:

```html
<button
  class="mobile-menu-button"
  type="button"
  aria-label="Open navigation"
  aria-controls="mobile-navigation"
  aria-expanded="false"
>
  ...
</button>
```

If implementing an opened mobile menu, include:

- Escape key closes menu
- focus moves into menu when opened
- focus returns to trigger when closed
- active route is visible and announced
- background scroll lock if menu overlays the page

The inspected reference frames show only the closed hamburger state, not the open mobile menu panel.

---

## 9. Home page design

### 9.1 Content

Home contains:

- eyebrow: `SO, YOU WANT TO TRAVEL TO`
- heading: `SPACE`
- body: `Let’s face it; if you want to go to space...`
- primary CTA: `EXPLORE`

CTA should link to the first destination route: `/destination/moon`.

### 9.2 Desktop layout

Desktop target: `1440 × 1024`.

Main layout:

- content container max width: `1110px`
- main vertical padding: `128px`
- hero sits toward the lower part of the viewport
- hero is two columns
- left text column max width: `540px`
- right CTA column max width: `540px`
- columns are vertically aligned toward the bottom
- CTA is right-aligned within its column

Text measurements:

- eyebrow: Barlow Condensed, `28px`, `letter-spacing: 4px`, color `--color-blue-300`
- heading: Bellefair, `144px`, line-height `1`, color white
- body: Barlow, `18px`, line-height `1.8`, color `--color-blue-300`
- text stack gap: `24px`

CTA measurements:

- circle size: `272px`
- background: white
- text: Bellefair, `32px`, uppercase, color `--color-blue-900`
- shape: fully round

### 9.3 Tablet layout

Tablet target: `768 × 1024`.

- layout becomes vertical
- content is centered
- text block width: about `512px`
- text alignment: center
- CTA remains `272px`
- main content horizontal padding: `40px`
- main vertical padding: `128px`

### 9.4 Mobile layout

Mobile target: `375 × 812`.

- layout remains vertical
- content is centered
- page padding: `24px`
- heading size: `80px`
- eyebrow size: `16px`
- eyebrow letter spacing: `2.4px`
- body size: `15px`
- CTA size: `144px`
- CTA text size: `18px`

### 9.5 Home implementation notes

The tool-generated output uses a full-size image layer. In production, prefer a responsive background strategy:

```css
.page-shell--home {
  background-color: var(--color-blue-900);
  background-image: image-set(...);
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}
```

Use separate mobile/tablet/desktop assets when available. Background crop is important and should be verified visually at each breakpoint.

### 9.6 Home interactions

Explore button:

- default: white circle
- hover/focus-visible: should show a large translucent halo around the circle if implementing the expected component state
- focus-visible must be keyboard-visible, even if hover halo is subtle

Recommended interaction CSS:

```css
.explore-button {
  position: relative;
  isolation: isolate;
}

.explore-button::before {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: inherit;
  background: rgb(255 255 255 / 0.1);
  transform: scale(1);
  opacity: 0;
  transition: transform 180ms ease, opacity 180ms ease;
  z-index: -1;
}

.explore-button:hover::before,
.explore-button:focus-visible::before {
  transform: scale(1.55);
  opacity: 1;
}
```

---

## 10. Destination template

### 10.1 Content model

Each destination needs:

```ts
interface Destination {
  slug: string;
  name: string;
  description: string;
  distance: string;
  travelTime: string;
  images: {
    png?: string;
    webp?: string;
  };
}
```

The inspected Moon content:

- name: `MOON`
- description: `See our planet as you’ve never seen it before. A perfect relaxing trip away to help regain perspective and come back refreshed. While you’re there, take in some history by visiting the Luna 2 and Apollo 11 landing sites.`
- average distance: `384,400 km`
- estimated travel time: `3 days`

### 10.2 Desktop layout

Desktop target: `1440 × 1024`.

- main content container max width: `1110px`
- page title at top of content
- page title gap: `24px` between number and label
- content below title uses two columns
- column gap: `32px`
- left image column centers the planet
- right explanation column max width: about `445px`

Page title:

- number: `01`, Barlow Condensed Bold, `28px`, `letter-spacing: 4.725px`, opacity `25%`
- label: `PICK YOUR DESTINATION`, Barlow Condensed Regular, `28px`, `letter-spacing: 4px`

Planet image:

- Moon desktop image visual size: about `480px`
- mobile image visual size: about `150px`

Tabs:

- horizontal
- gap: `32px`
- height: `32px`
- active tab: white text + `3px` bottom border
- inactive tabs: `--color-blue-300`
- type: Barlow Condensed, `16px`, `letter-spacing: 2px`, uppercase

Text:

- destination name: Bellefair, `96px`, line-height `1`
- description: Barlow, `18px`, line-height `1.8`, color `--color-blue-300`
- text stack gap: `16px`

Divider:

- height: `1px`
- width: full explanation width
- color: white at `25%` opacity

Stats:

- desktop layout: two columns
- gap: `24px`
- label: Barlow Condensed, `14px`, `letter-spacing: 2px`, color `--color-blue-300`, uppercase
- value: Bellefair, `28px`, color white, uppercase
- label/value gap: `12px`

### 10.3 Tablet layout

The Destination tablet frames follow the same conceptual flow as mobile/desktop but with larger spacing and centered composition.

Recommended behavior:

- content stacks vertically
- page title remains visible near top
- planet image larger than mobile and smaller than desktop
- explanation block is centered
- tabs centered
- text centered
- stats can remain two columns if width allows

### 10.4 Mobile layout

Mobile target: `375 × 880`.

Flow:

1. page title
2. planet image
3. destination tabs
4. destination name
5. description
6. divider
7. stats stacked vertically

Measurements:

- page padding: `24px`
- page title centered
- page title type: `16px`, `letter-spacing: 2.4px`
- planet image: `150px`
- tabs gap: `32px`
- tab text: about `14px`, `letter-spacing: 2.1px`
- destination name: `56px`
- body: `15px`, line-height `1.8`
- stats: one column, centered, gap `24px`

### 10.5 Destination accessibility

If destinations are pages/routes:

- use links for destination tabs
- active tab gets `aria-current="page"`
- planet image should have meaningful alt text, e.g. `alt="The Moon"`

If destinations become client-side tabs:

- use the ARIA tabs pattern
- include arrow-key navigation
- active panel must be connected with `aria-controls`
- this is more complex and unnecessary if routing is acceptable

Recommended: use routes.

---

## 11. Crew template

### 11.1 Content model

Each crew member needs:

```ts
interface CrewMember {
  slug: string;
  name: string;
  role: string;
  bio: string;
  image: string;
}
```

The inspected Douglas Hurley content:

- role: `Commander`
- name: `Douglas Hurley`
- bio: `Douglas Gerald Hurley is an American engineer, former Marine Corps pilot and former NASA astronaut. He launched into space for the third time as commander of Crew Dragon Demo-2.`

### 11.2 Desktop layout

Desktop target: `1440 × 1024`.

- content container max width: `1110px`
- page title: `02 MEET YOUR CREW`
- main content: two columns
- left column: explanation and pagination
- right column: crew image
- role/name block is uppercase
- image aligns to lower part of content area

Page title:

- number: `02`, Barlow Condensed Bold, `28px`, `letter-spacing: 4.725px`, opacity `25%`
- label: `MEET YOUR CREW`, Barlow Condensed Regular, `28px`, `letter-spacing: 4px`

Text:

- role: Bellefair, `32px`, opacity `50%`, uppercase
- name: Bellefair, `56px`, uppercase
- body: Barlow, `18px`, line-height `1.8`, color `--color-blue-300`
- role/name gap: `16px`
- text stack gap: `24px`

Pagination:

- four dot controls
- desktop dot size: `15px`
- gap: `40px`
- active dot: white
- inactive dots: white with low opacity
- pagination appears near the lower part of the left column

### 11.3 Mobile layout

Mobile target: `375 × 880`.

Flow in inspected reference mockups:

1. mobile header
2. page title
3. crew text content
4. dot pagination
5. crew image

Measurements:

- page padding: `24px`
- page title centered
- role: `18px`
- name: `24px`
- bio: `15px`, line-height `1.8`
- text alignment: center
- dot size: `10px`
- dot gap: `16px`
- image height around `340px` for Douglas frame

Important implementation note:

The tool-generated output includes empty paragraphs/zero-width content in the mobile bio. Do not copy that markup. Store and render clean text from data.

### 11.4 Crew accessibility

If crew members are pages/routes:

- pagination dots should be links
- active dot gets `aria-current="page"`
- each dot must have an accessible label, e.g. `View Douglas Hurley`
- crew image should use meaningful alt text, e.g. `alt="Douglas Hurley"`

Avoid unlabeled dots.

---

## 12. Technology template

### 12.1 Content model

Each technology item needs:

```ts
interface TechnologyItem {
  slug: string;
  name: string;
  description: string;
  images: {
    portrait: string;
    landscape: string;
  };
}
```

The inspected Launch Vehicle content:

- eyebrow: `THE TERMINOLOGY…`
- name: `LAUNCH VEHICLE`
- description: `A launch vehicle or carrier rocket is a rocket-propelled vehicle used to carry a payload from Earth's surface to space, usually to Earth orbit or beyond. Our WEB-X carrier rocket is the most powerful in operation. Standing 150 metres tall, it's quite an awe-inspiring sight on the launch pad!`

### 12.2 Desktop layout

Desktop target: `1440 × 1024`.

- content container max width: `1275px`
- page title: `03 SPACE LAUNCH 101`
- content row: pagination + text + image
- text/pagination area min width: about `635px`
- image occupies right side
- image frame height: about `600px`

Page title:

- number: `03`, Barlow Condensed Bold, `28px`, `letter-spacing: 4.725px`, opacity `25%`
- label: `SPACE LAUNCH 101`, Barlow Condensed Regular, `28px`, `letter-spacing: 4px`

Pagination:

- three numbered circular controls
- desktop circle size: `80px`
- vertical stack
- gap: `32px`
- active: white background, `--color-blue-900` text
- inactive: transparent background, `1px solid rgba(255,255,255,0.25)`, white text
- number type: Bellefair, `32px`

Text:

- eyebrow: Bellefair, `32px`, opacity `50%`, uppercase
- name: Bellefair, `56px`, uppercase
- body: Barlow, `18px`, line-height `1.8`, color `--color-blue-300`
- stack gap: `24px`

Image:

- desktop uses portrait crop
- positioned on the right
- should not shrink into a tiny image on intermediate desktop widths

### 12.3 Mobile layout

Mobile target: `375 × 880`.

Flow:

1. mobile header
2. page title
3. landscape technology image
4. horizontal pagination
5. explanation text

Measurements:

- page title centered
- technology image appears wide/full-bleed relative to page content
- pagination circle size: `40px`
- pagination gap: `16px`
- eyebrow: `18px`
- name: `24px`
- body: `15px`, line-height `1.8`
- text alignment: center

Important implementation note:

The mobile technology image crop is not a simple proportional resize of the desktop image. The design uses a landscape-oriented crop, internally wider than the mobile frame. Use separate portrait and landscape image assets when available.

### 12.4 Technology accessibility

If technology items are pages/routes:

- pagination numbers should be links
- active item gets `aria-current="page"`
- each control needs an accessible label, e.g. `View launch vehicle`
- image alt text should describe the item, e.g. `alt="Launch vehicle lifting off"`

---

## 13. Background image strategy

Each page family uses its own background imagery:

- Home background
- Destination background
- Crew background
- Technology background

The inspected design uses different crops across mobile, tablet, and desktop. Do not assume one background image with `background-size: cover` will match every frame.

Recommended implementation:

```css
.page-shell {
  min-height: 100svh;
  background-color: var(--color-blue-900);
  background-repeat: no-repeat;
  background-size: cover;
  overflow-x: clip;
}

.page-shell--home {
  background-image: url("/assets/home/background-home-mobile.jpg");
  background-position: center bottom;
}

@media (min-width: 48rem) {
  .page-shell--home {
    background-image: url("/assets/home/background-home-tablet.jpg");
  }
}

@media (min-width: 64rem) {
  .page-shell--home {
    background-image: url("/assets/home/background-home-desktop.jpg");
    background-position: center center;
  }
}
```

Use equivalent modifiers for destination, crew, and technology pages.

---

## 14. Image asset requirements

Required asset categories:

### Logo

- white circular star logo
- desktop/tablet displayed at `48px`
- mobile displayed at `40px`

### Home background

- mobile
- tablet
- desktop

### Destination background

- mobile
- tablet
- desktop

### Destination planet images

- moon
- mars
- europa
- titan

Prefer transparent PNG/WebP images for planets.

### Crew background

- mobile
- tablet
- desktop

### Crew portraits

- Douglas Hurley
- Mark Shuttleworth
- Victor Glover
- Anousheh Ansari

Portraits should retain transparent/isolated background behavior if available.

### Technology background

- mobile
- tablet
- desktop

### Technology images

Each technology item should have:

- portrait image for desktop
- landscape image for mobile/tablet

---

## 15. Component responsibilities

### `PageShell.astro`

Responsibilities:

- choose page background class
- provide full viewport shell
- render header and main content slot
- optionally accept `pageType`: `home | destination | crew | technology`

### `SiteHeader.astro`

Responsibilities:

- render logo
- render desktop/tablet nav
- render mobile menu button
- manage active section from route or prop
- keep semantics correct

### `MainNav.astro`

Responsibilities:

- render primary nav links from data
- render indexes and labels
- apply active styling
- include `aria-current`

### `PageTitle.astro`

Props:

```ts
interface Props {
  index: string;
  children: string;
}
```

Responsibilities:

- render page number and title
- handle responsive alignment
- keep number visually muted

### `HomeHero.astro`

Responsibilities:

- render home eyebrow, heading, body, CTA
- handle responsive layout
- link CTA to `/destination/moon`

### `DestinationLayout.astro`

Responsibilities:

- render page title
- render planet image
- render destination tabs
- render destination name, description, stats
- use data-driven destination content

### `CrewLayout.astro`

Responsibilities:

- render page title
- render role/name/bio
- render crew pagination
- render crew image
- preserve mobile content order from the source design artifacts

### `TechnologyLayout.astro`

Responsibilities:

- render page title
- render technology image with correct portrait/landscape source
- render numbered pagination
- render terminology/name/body
- handle major responsive order shift

---

## 16. Interaction states

### Primary nav links

States:

- default: white text
- hover: white underline or subtle bottom border at reduced opacity
- active: solid white `3px` underline
- focus-visible: visible outline or underline that does not rely only on color

### Destination tabs

States:

- default/inactive: `--color-blue-300`
- hover: white or white underline at reduced opacity
- active: white text + `3px` underline
- focus-visible: visible outline or underline

### Crew pagination dots

States:

- inactive: white at low opacity
- hover/focus: white at medium opacity
- active: white

### Technology pagination numbers

States:

- inactive: transparent, white text, translucent border
- hover/focus: stronger border
- active: white fill, dark text

### Explore CTA

States:

- default: white circle, dark text
- hover/focus-visible: translucent white halo
- active: optional slight scale or unchanged; avoid distracting motion

Respect `prefers-reduced-motion`.

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    scroll-behavior: auto !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## 17. Accessibility requirements

Implementation must include:

- semantic landmark structure: `<header>`, `<nav>`, `<main>`
- skip link to main content
- accessible mobile menu trigger
- keyboard-visible focus styles
- active route communicated with `aria-current`
- meaningful alt text for content images
- empty alt text for decorative images
- sufficient hit areas for touch controls
- route-based pagination links with accessible labels
- no unlabeled dot-only or number-only controls
- no text rendered as images
- no hidden focus traps in mobile navigation

Recommended skip link:

```html
<a class="skip-link" href="#main-content">Skip to content</a>
```

Recommended pagination labels:

```html
<a href="/crew/douglas-hurley" aria-label="View Douglas Hurley" aria-current="page"></a>
<a href="/technology/spaceport" aria-label="View spaceport">2</a>
```

---

## 18. Known design inconsistencies and decisions needed

### 18.1 Selected source-design identifier is not directly usable

The provided node `62857:72` is a zero-size wrapper. Use its child frames for actual implementation references.

### 18.2 Empty footer frame

`62913:2138` is named `Design System - Footer`, but it contains no children. There is no footer design to implement from the inspected file.

Decision: omit the footer unless another design is provided.

### 18.3 Style guide naming appears inconsistent

The Style Guide contains frames named `Colors` that include typography labels and repeated color labels. Use extracted variables and page frames as the implementation source of truth.

### 18.4 Tablet navigation number inconsistency

Home tablet appears to omit `00` for the active Home link while keeping numbers for other nav items.

Recommended decision: make nav numbering consistent across tablet links unless the design owner confirms this is intentional.

### 18.5 tool-generated markup is not production-ready

The generated code uses React + Tailwind-like utility classes and sometimes chooses `<button>` for active links. It should not be copied directly.

Production rules:

- route navigation must be links
- active state must not change element type
- styling must use project CSS, not Tailwind
- avoid design-tool layer names as class names

---

## 19. Implementation risks

### Risk: image crop mismatch

The backgrounds and technology images are highly crop-dependent. Validate with screenshots at 375px, 768px, and 1440px widths.

### Risk: viewport height mismatch

The source design artifacts use fixed frame heights. Browsers have dynamic viewport heights, browser chrome, and device safe areas. Use `100svh`, avoid fixed page heights.

### Risk: nav overcrowding on tablet

The tablet nav uses a dense horizontal layout. If labels overflow at intermediate widths, either hide nav indexes consistently or reduce spacing carefully.

### Risk: technology image implementation

The technology page has the most complex responsive shift. Desktop uses a portrait/right image; mobile uses a landscape image above the text. This should be implemented with `<picture>` or data-provided portrait/landscape assets.

### Risk: copying generated design-tool code

The generated output is useful for measurements, but it is not suitable as final Astro code. It includes implementation noise, artifact class names, and non-semantic element choices.

---

## 20. Acceptance criteria

The implementation is successful when:

- Home, Destination, Crew, and Technology templates match the inspected layouts at mobile, tablet, and desktop sizes.
- Navigation is shared and correctly highlights the current section.
- Destination, Crew, and Technology pages are data-driven rather than duplicated by hand.
- Typography uses Bellefair, Barlow, and Barlow Condensed with the specified hierarchy.
- Colors and spacing come from global tokens.
- Background images use breakpoint-specific crops.
- All interactive controls are keyboard accessible.
- Active sub-navigation controls are announced with `aria-current`.
- Mobile menu button is accessible and not a decorative-only icon.
- No Tailwind dependency is added solely because the design tool generated Tailwind-like classes.
- No footer is implemented unless a footer design is provided.

---

## 21. Suggested implementation order

1. Create global tokens: colors, spacing, fonts, typography helpers.
2. Add static assets and verify background image availability.
3. Build `PageShell` and `SiteHeader`.
4. Implement Home page.
5. Implement data files for destinations, crew, and technology.
6. Implement Destination template and all destination routes.
7. Implement Crew template and all crew routes.
8. Implement Technology template and all technology routes.
9. Add hover/focus states.
10. Add mobile menu behavior if required.
11. Run responsive visual QA at 375px, 768px, and 1440px.
12. Run accessibility QA with keyboard and screen-reader semantics.

---

## 22. Visual QA checklist

Check these viewport widths:

- 375 × 812 or 375 × 880
- 768 × 1024
- 1440 × 1024

For each page family verify:

- background crop matches the source-design intent
- header logo size and placement match
- mobile hamburger position matches
- active nav underline aligns to bottom of nav item
- typography sizes match the intended breakpoint
- content max widths do not stretch too wide
- page title number opacity feels correct
- body copy line-height remains airy
- CTA/button sizes are correct
- destination image size changes correctly
- crew image does not overlap text unexpectedly
- technology image switches from portrait/right to landscape/top
- no horizontal scrolling appears

---

## 23. Summary

The source design artifacts should be implemented as a small design system plus four page templates:

- Home
- Destination detail
- Crew detail
- Technology detail

The strongest design constraints are typography, background cropping, spacing rhythm, and responsive composition. The implementation should prioritize semantic Astro components, data-driven routes, global CSS tokens, and accessible navigation patterns rather than reproducing the design tool's generated React/Tailwind structure.
