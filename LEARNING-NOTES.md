# Web Development Learning Notes

A growing reference for HTML, CSS, JavaScript, React, Node.js, PostgreSQL, accessibility, and publishing websites. The examples are general patterns that can be reused in different projects.

## How to use these notes

This is a reference, not something to read or memorize all at once. Choose one topic, try a small example, and inspect the result in browser developer tools.

Quick links:

- [HTML and page setup](#html-document-setup)
- [CSS selectors working together](#how-selectors-work-together)
- [CSS properties: purpose, values, and examples](#css-property-reference)
- [JavaScript basics](#javascript-essentials)
- [Callbacks and arrow functions](#callbacks-and-arrow-functions)
- [filter, map, and find](#filter-map-and-find)
- [OR conditions and filter switches](#conditions-booleans-and-logical-operators)
- [Spread and immutable updates](#spread-syntax-and-immutable-updates)
- [Browser events and the DOM](#browser-javascript-and-the-dom)
- [Current-section navigation](#highlighting-the-current-section)
- [Saving data locally](#json-and-localstorage)
- [React components, props, and state](#react-components-and-jsx)
- [Forms, callbacks, and shared state](#react-forms-and-shared-state)
- [Hooks and saving React state](#react-hooks-and-browser-storage)
- [Automated tests, one concept at a time](#automated-testing)
- [Contrast, keyboard access, and audits](#contrast-keyboard-access-and-audits)
- [APIs, error handling, and caching](#fetching-api-data-and-caching)
- [Node.js, Express, routes, and HTTP](#nodejs-and-express-apis)
- [Connecting React to a backend](#connecting-react-to-an-api)
- [Refs, scrolling, and dependent selections](#react-refs-and-dependent-selections)
- [Tailwind classes and theme tokens](#tailwind-css-and-theme-tokens)
- [Organizing backend code](#organizing-backend-code)
- [PostgreSQL and SQL](#postgresql-and-sql)
- [Connections, Docker, migrations, and seeds](#database-connections-migrations-and-seeds)
- [Dates, availability, and overlapping appointments](#dates-times-and-availability)
- [Hosting and moving a database](#hosting-and-moving-a-database)
- [SEO, robots.txt, and sitemaps](#seo-and-search-engine-discovery)
- [Tools, PERN, and practice roadmap](#development-tools-and-application-stacks)
- [Git and publishing](#git-and-publishing-basics)

When learning something new, add its purpose, a working example, and any mistakes to watch out for.

## HTML, CSS, and JavaScript

| Technology | Responsibility                  | Examples                                           |
| ---------- | ------------------------------- | -------------------------------------------------- |
| HTML       | Content, structure, and meaning | Headings, links, images, forms                     |
| CSS        | Presentation and layout         | Colors, spacing, responsive columns                |
| JavaScript | Programmed behavior             | Fetching data, updating content, application logic |

Many interactions already work without JavaScript: links, form submission, fragment navigation, sticky positioning, and CSS hover effects.

## HTML document setup

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" content="A short description of the page." />
    <title>Page title</title>
    <link rel="stylesheet" href="styles.css" />
    <link rel="icon" type="image/png" href="/images/favicon.png" />
  </head>
  <body>
    <h1>Page heading</h1>
  </body>
</html>
```

| Code                 | Purpose                                                  |
| -------------------- | -------------------------------------------------------- |
| `<!doctype html>`    | Enables modern standards-mode rendering                  |
| `lang="en"`          | Identifies the document language                         |
| `<head>`             | Holds metadata and resource references                   |
| `charset="UTF-8"`    | Supports a wide range of characters                      |
| Viewport meta tag    | Makes the mobile layout viewport follow the device width |
| Description meta tag | Describes the page; search engines may use it in results |
| `<title>`            | Sets the browser tab title                               |
| `rel="stylesheet"`   | Loads CSS                                                |
| `rel="icon"`         | Sets the favicon                                         |
| `<body>`             | Contains the page content                                |

External stylesheets can provide fonts or icon libraries. Loading a font does not automatically apply it: CSS must select it with `font-family`. A `preconnect` resource hint can establish an early connection to an external host. Font connections commonly use `crossorigin` as well.

### Favicons and public assets

A favicon is the small website icon shown in a browser tab. SVG, PNG, and ICO are possible formats; an ICO file is not mandatory when other supported icons are linked correctly.

```html
<link rel="icon" type="image/png" sizes="16x16" href="/favicons/icon-16.png" />
<link rel="icon" type="image/png" sizes="32x32" href="/favicons/icon-32.png" />
```

The `sizes` value should match the image's actual dimensions. A browser can choose an appropriate size for the display.

In a Vite app, a file at `public/favicons/icon-32.png` is served at `/favicons/icon-32.png`. The folder name `public` is not part of that URL. An ordinary static site does not automatically apply Vite's public-directory rules: its paths depend on what the web server serves as the root.

After changing an icon, try a hard refresh if the browser still displays the cached version.

## Semantic HTML

Choose an element for its meaning, then use CSS to control its appearance.

| Element                | Meaning or use                                      |
| ---------------------- | --------------------------------------------------- |
| `<header>`             | Introductory content for a page or section          |
| `<nav>`                | A major group of navigation links                   |
| `<main>`               | The page's main content                             |
| `<section>`            | A thematic group of content, usually with a heading |
| `<article>`            | Self-contained content, such as a news article      |
| `<footer>`             | Supporting information about a page or section      |
| `<h1>`–`<h6>`          | Heading levels describing document hierarchy        |
| `<p>`                  | A paragraph                                         |
| `<ul>`, `<ol>`, `<li>` | Unordered lists, ordered lists, and list items      |
| `<a>`                  | A link to another location                          |
| `<button>`             | An action, such as opening a menu                   |
| `<img>`                | An image                                            |
| `<div>`                | A generic container, often for layout               |
| `<span>`               | A generic container for a small piece of content    |
| `<br>`                 | A meaningful line break, not a spacing tool         |

A heading level is not a font-size setting. Do not choose `<h4>` just because it looks smaller than `<h2>`.

An `<a>` does not need a `<p>` inside it to be semantic. A short navigation label can be written directly inside the link.

## Attributes, classes, and IDs

```html
<section id="services" class="section">
  <h2>Services</h2>
  <a class="text-link card-title" href="#contact">Contact us</a>
</section>
```

- `id` identifies a unique element. IDs can act as link targets.
- `class` provides reusable names for styling or scripting.
- Multiple classes are separated by spaces.
- Classes have no built-in styling; their behavior comes from the CSS that matches them.

The order of class names in HTML does not decide which CSS rule wins.

## Links and paths

| Example                           | Meaning                                             |
| --------------------------------- | --------------------------------------------------- |
| `href="#contact"`                 | Jump to the element with `id="contact"`             |
| `href="contact"`                  | Navigate to a relative path named `contact`         |
| `href="styles.css"`               | Resolve a file relative to the current document URL |
| `src="/images/photo.png"`         | Resolve a file from the website root                |
| `href="/"`                        | Go to the website root                              |
| `href="https://example.com"`      | Navigate to an absolute URL                         |
| `href="mailto:hello@example.com"` | Open an email composer                              |
| `target="_blank"`                 | Open a new browsing context, usually a tab          |

```html
<a href="#contact">Contact</a>
<section id="contact">
  <h2>Contact</h2>
</section>
```

Put fragment IDs on elements that remain rendered across screen sizes. If an element or its ancestor uses `display: none`, it cannot provide a normal visible scroll destination.

Use a local web server when testing paths that start with `/`. A `file://` URL does not behave like a hosted website root.

## CSS rule structure

```css
.badge {
  color: teal;
  padding: 0.25rem 0.5rem;
}
```

- `.badge` is the selector.
- `color` and `padding` are properties.
- `teal` and `0.25rem 0.5rem` are values.
- A property and value form a declaration.
- Declarations are grouped inside braces.
- Comments use `/* ... */` and do not affect styling.

## CSS selector reference

| Selector              | Selects                                                           |
| --------------------- | ----------------------------------------------------------------- |
| `*`                   | Every element                                                     |
| `p`                   | All paragraph elements                                            |
| `.card`               | Elements with the class `card`                                    |
| `#contact`            | The element with that ID                                          |
| `.card p`             | Paragraph descendants anywhere inside a card                      |
| `.card > p`           | Paragraphs that are direct children of a card                     |
| `.card.featured`      | An element that has both classes                                  |
| `.card, .panel`       | Cards and panels independently                                    |
| `a[href]`             | Links with an `href` attribute                                    |
| `.link:hover`         | A link while it is hovered                                        |
| `.link:focus-visible` | A focused link when the browser indicates focus should be visible |
| `.field:focus-within` | A field container when it or a descendant has focus               |
| `.card::before`       | A generated box before the element's content                      |
| `.card::after`        | A generated box after the element's content                       |
| `p::selection`        | Selected text within paragraphs                                   |
| `:root`               | The document root element                                         |

### Spaces, commas, and combined classes

```css
.card .title {
  color: navy;
}
```

A **space** means “a descendant inside.” The title must be inside a card.

```css
.card,
.title {
  color: navy;
}
```

A **comma** separates independent selectors. Every card and every title is selected.

```css
.card.title {
  color: navy;
}
```

With **no space** between the classes, the same element must have both classes.

## How selectors work together

A component usually receives styling from several rules.

```html
<article class="card">
  <a class="text-link card-title" href="/details">
    <h3>Example item</h3>
  </a>
  <p class="date">November 2026</p>
  <div class="badge-list">
    <span class="badge">HTML</span>
    <span class="badge">CSS</span>
  </div>
</article>
```

```css
body {
  color: #334155;
}

.card {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.text-link {
  color: #0f172a;
  text-decoration: none;
}

.text-link:hover {
  color: teal;
}

.card-title h3 {
  font-size: 1.25rem;
  font-weight: 600;
}

.card .date {
  font-size: 0.8rem;
}

.badge-list {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.badge {
  padding: 0.25rem 0.5rem;
  border-radius: 0.5rem;
}
```

| Result          | Rules working together                                                   |
| --------------- | ------------------------------------------------------------------------ |
| Card text color | Inherited `body` color, unless a more direct declaration applies         |
| Card spacing    | `.card` controls space between its direct children                       |
| Title link      | `.text-link` styles the anchor; `.card-title h3` styles its heading      |
| Title hover     | `.text-link:hover` changes the link color, which the heading can inherit |
| Small date      | `.card .date` targets only dates inside cards                            |
| Wrapping badges | `.badge-list` handles layout; `.badge` handles each badge's appearance   |

The parent controls layout between children. The child controls its own appearance. Keep these responsibilities in mind when choosing which rule to edit.

## Cascade and specificity

For ordinary rules in the same author stylesheet, without cascade layers or `!important`:

1. A selector must match, and any media query must be active.
2. Matching declarations for different properties can cooperate.
3. Conflicting declarations are resolved by specificity.
4. If specificity is equal, the later declaration wins.

The full cascade also accounts for origin, importance, and layers. Source order is not the only rule.

| Selector      | IDs | Classes, attributes, pseudo-classes | Elements, pseudo-elements |
| ------------- | --- | ----------------------------------- | ------------------------- |
| `p`           | 0   | 0                                   | 1                         |
| `.date`       | 0   | 1                                   | 0                         |
| `.card p`     | 0   | 1                                   | 1                         |
| `.card .date` | 0   | 2                                   | 0                         |
| `#contact`    | 1   | 0                                   | 0                         |

Compare these columns from left to right. They are not decimal numbers. The universal selector `*` adds no specificity.

```css
.card .date {
  font-size: 0.8rem;
}

.card p {
  font-size: 1rem;
}
```

The date stays `0.8rem`: two class selectors have higher specificity than one class plus one element selector.

### Inheritance

Properties such as `color`, `font-size`, and `font-family` can inherit. Properties such as `padding`, `border`, and `display` normally do not.

```css
body {
  color: #334155;
}

.icon-link {
  color: inherit;
}
```

A declaration matching a child directly takes precedence over a value merely inherited from its parent.

### Useful reset values

| Value     | Meaning                                                                    |
| --------- | -------------------------------------------------------------------------- |
| `inherit` | Use the parent's computed value                                            |
| `initial` | Use the property's initial value                                           |
| `unset`   | Inherit if the property normally inherits; otherwise use its initial value |

For example, `max-width: unset` resets that non-inherited property to `none`.

## Custom properties and colors

```css
:root {
  --color-accent: #5eead4;
  --color-text: #e2e8f0;
  --color-background: #0f172a;
}

body {
  color: var(--color-text);
  background: var(--color-background);
}
```

Custom properties begin with `--` and are read using `var(...)`. They help keep repeated values consistent.

| Example                    | Meaning                                         |
| -------------------------- | ----------------------------------------------- |
| `#0f172a`                  | A hexadecimal RGB color                         |
| `rgb(15, 23, 42)`          | The same color written as RGB channels          |
| `rgba(94, 234, 212, 0.35)` | An RGB color with 35% alpha                     |
| `transparent`              | A fully transparent color                       |
| `opacity: 0.7`             | Fades the entire element, including its content |

A translucent background color affects that background. `opacity` affects the whole rendered element, including descendants.

## CSS property reference

A **selector** chooses elements. A **property** describes what to change. A **value** describes how it should change.

```css
.card {
  background-color: #172238;
}
```

Here, `.card` is the selector, `background-color` is the property, and `#172238` is its value.

This is a reference for common properties, not every CSS property. Start with the group that matches the problem you want to solve:

- [Colors and backgrounds](#colors-and-background-properties)
- [Size and dimensions](#size-and-dimension-properties)
- [Spacing](#spacing-properties)
- [Display and visibility](#display-and-visibility-properties)
- [Text](#text-and-font-properties)
- [Borders and shadows](#border-outline-and-shadow-properties)
- [Flexbox](#flexbox-properties)
- [Grid](#grid-properties)
- [Positioning and layers](#position-and-layer-properties)
- [Images and overflowing content](#image-and-overflow-properties)
- [Interaction and transitions](#interaction-and-transition-properties)

### Colors and background properties

| Property              | Example                              | What it changes                                             |
| --------------------- | ------------------------------------ | ----------------------------------------------------------- |
| `color`               | `color: #e2e8f0`                     | Foreground/text color; descendants can inherit it           |
| `background-color`    | `background-color: #0f172a`          | Only the background color                                   |
| `background-image`    | `background-image: url('photo.jpg')` | Background image or gradient; not the content of an `<img>` |
| `background-position` | `background-position: center`        | Position of the background image                            |
| `background-size`     | `background-size: cover`             | Size of the background image                                |
| `background-repeat`   | `background-repeat: no-repeat`       | Whether the background image tiles                          |
| `background`          | `background: #0f172a`                | Shorthand that sets multiple background properties          |
| `opacity`             | `opacity: 0.7`                       | Transparency of the whole element and its contents          |

#### background versus background-color

Use `background-color` when you want to change only the color:

```css
.banner {
  background-image: url('photo.jpg');
  background-color: navy;
}
```

The image remains. Color is painted behind it and will not show through fully opaque parts.

By contrast, the `background` shorthand resets background properties that you do not specify:

```css
.banner {
  background-image: url('photo.jpg');
  background: navy; /* Also resets background-image to none. */
}
```

You can specify several settings at once:

```css
.banner {
  background: navy url('photo.jpg') center / cover no-repeat;
}
```

This sets a color, image, position, size, and repeat behavior. The `/` separates position from size. See [MDN: background](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/background).

For a translucent background without fading the text:

```css
.panel {
  background-color: rgba(15, 23, 42, 0.8);
}
```

A gradient is a background image:

```css
.banner {
  background-image: linear-gradient(135deg, #0f172a, #164e63);
}
```

### Size and dimension properties

| Property       | Example                  | What it changes                                         |
| -------------- | ------------------------ | ------------------------------------------------------- |
| `width`        | `width: 100%`            | Preferred width, subject to layout constraints          |
| `height`       | `height: 200px`          | Preferred height                                        |
| `min-width`    | `min-width: 0`           | Lower width limit; can allow flex/grid items to shrink  |
| `max-width`    | `max-width: 760px`       | Upper width limit                                       |
| `min-height`   | `min-height: 100vh`      | Minimum height; content may make it taller              |
| `max-height`   | `max-height: 300px`      | Upper height limit; overflow must be handled separately |
| `aspect-ratio` | `aspect-ratio: 16 / 9`   | Preferred width-to-height ratio                         |
| `box-sizing`   | `box-sizing: border-box` | Whether declared dimensions include padding and borders |

A responsive, centered content area:

```css
.container {
  width: 100%;
  max-width: 760px;
  margin: 0 auto;
  padding: 0 1rem;
  box-sizing: border-box;
}
```

The box uses available width up to 760px. A maximum is a limit, not a promise that the element will always be that wide.

`min-height` is often more flexible than a fixed `height` when text can wrap. A percentage height usually needs a suitable definite containing-block height; `height: 100%` does not automatically mean viewport height.

`border-box` includes padding and borders, but never margins. See [MDN: box-sizing](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/box-sizing).

### Spacing properties

| Property                                                         | Example                | What it changes                                                      |
| ---------------------------------------------------------------- | ---------------------- | -------------------------------------------------------------------- |
| `margin`                                                         | `margin: 2rem 0`       | Space outside the border                                             |
| `margin-top`, `margin-bottom`                                    | `margin-top: 1rem`     | Outside spacing on one side                                          |
| `margin-left`, `margin-right`                                    | `margin-left: auto`    | Outside spacing; auto margins can absorb available space             |
| `padding`                                                        | `padding: 1rem 2rem`   | Space inside the border                                              |
| `padding-top`, `padding-right`, `padding-bottom`, `padding-left` | `padding-left: 0.5rem` | Inside spacing on one side                                           |
| `gap`                                                            | `gap: 1rem`            | Gaps between grid/flex items                                         |
| `row-gap`                                                        | `row-gap: 2rem`        | Gaps between grid rows or flex lines/items depending on direction    |
| `column-gap`                                                     | `column-gap: 1rem`     | Gaps between grid columns or flex items/lines depending on direction |

Shorthand order:

```css
.card {
  padding: 1rem; /* All sides. */
  padding: 1rem 2rem; /* Top/bottom, left/right. */
  padding: 1rem 2rem 3rem; /* Top, left/right, bottom. */
  padding: 1rem 2rem 3rem 4rem; /* Top, right, bottom, left. */
}
```

These are alternative examples; if you write all four declarations together, the last one wins.

To separate child items, inspect the parent's `gap`. To move content away from its own border, inspect `padding`. To separate independent boxes, inspect margins. Do not assume all visible empty space is padding.

### Display and visibility properties

| Property/value          | Meaning                                                                                     |
| ----------------------- | ------------------------------------------------------------------------------------------- |
| `display: block`        | A block-level box with normal flow inside                                                   |
| `display: inline`       | Participates in text flow; width/height do not normally size non-replaced inline boxes      |
| `display: inline-block` | An inline-level box that accepts width and height                                           |
| `display: flex`         | A block-level flex container                                                                |
| `display: grid`         | A block-level grid container                                                                |
| `display: none`         | Removes the element and descendants from layout and accessibility APIs                      |
| `visibility: hidden`    | Hides a box while preserving its layout space; normally also hidden from accessibility APIs |
| `opacity: 0`            | Makes content transparent while its layout and interaction can remain                       |

`display` affects both how an element participates in its outer layout and how its children are laid out. See [MDN: display](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/display).

Transparent content is not necessarily disabled or inaccessible. Choose a hiding method based on the actual behavior you need.

### Text and font properties

| Property                | Example                          | What it changes                                                |
| ----------------------- | -------------------------------- | -------------------------------------------------------------- |
| `font-family`           | `font-family: Arial, sans-serif` | Font choices and fallback                                      |
| `font-size`             | `font-size: 1rem`                | Text size                                                      |
| `font-weight`           | `font-weight: 600`               | Text weight, when supported by the font                        |
| `font-style`            | `font-style: italic`             | Italic or normal style                                         |
| `line-height`           | `line-height: 1.6`               | Height of line boxes                                           |
| `letter-spacing`        | `letter-spacing: 0.05em`         | Spacing between characters                                     |
| `text-align`            | `text-align: center`             | Alignment of inline content inside the box                     |
| `text-transform`        | `text-transform: uppercase`      | Displayed letter case                                          |
| `text-decoration`       | `text-decoration: line-through`  | Decoration such as underline or strike-through                 |
| `text-underline-offset` | `text-underline-offset: 0.2em`   | Distance between text and its underline                        |
| `white-space`           | `white-space: nowrap`            | Whitespace handling and wrapping                               |
| `overflow-wrap`         | `overflow-wrap: anywhere`        | Allows long text to break when needed                          |
| `text-overflow`         | `text-overflow: ellipsis`        | Marks clipped inline text, when clipping and sizing are set up |

`text-align: center` centers text, not the element's box itself. Use layout rules or margins to position the box.

A common single-line truncation pattern:

```css
.title {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

The element also needs a constrained width to overflow. In a flex or grid layout, `min-width: 0` on the relevant item may be needed.

### Border, outline, and shadow properties

| Property         | Example                                     | What it changes                                      |
| ---------------- | ------------------------------------------- | ---------------------------------------------------- |
| `border`         | `border: 1px solid #334155`                 | Border width, style, and color together              |
| `border-width`   | `border-width: 2px`                         | Border thickness                                     |
| `border-style`   | `border-style: dashed`                      | Border pattern                                       |
| `border-color`   | `border-color: teal`                        | Border color                                         |
| `border-bottom`  | `border-bottom: 1px solid #334155`          | One border side                                      |
| `border-radius`  | `border-radius: 0.5rem`                     | Rounded corners                                      |
| `outline`        | `outline: 2px solid teal`                   | An outline that does not consume layout space        |
| `outline-offset` | `outline-offset: 4px`                       | Distance between outline and box                     |
| `box-shadow`     | `box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2)` | A visual shadow without reserving extra layout space |

A border needs a visible style such as `solid`; setting only a width or color may not show one. A radius alone does not crop an image to the same corners: use an appropriate clipping rule on the container when needed.

Keep visible keyboard focus:

```css
button:focus-visible {
  outline: 2px solid #5eead4;
  outline-offset: 4px;
}
```

### Flexbox properties

Parent/container properties:

| Property          | Example                          | What it controls                                                |
| ----------------- | -------------------------------- | --------------------------------------------------------------- |
| `display`         | `display: flex`                  | Enables Flexbox                                                 |
| `flex-direction`  | `flex-direction: column`         | Main-axis direction                                             |
| `flex-wrap`       | `flex-wrap: wrap`                | Whether items wrap onto additional lines                        |
| `justify-content` | `justify-content: space-between` | Main-axis distribution                                          |
| `align-items`     | `align-items: center`            | Cross-axis alignment of items                                   |
| `align-content`   | `align-content: start`           | Distribution of flex lines when there is extra cross-axis space |
| `gap`             | `gap: 0.75rem`                   | Spacing between items/lines                                     |

Child/item properties:

| Property      | Example                  | What it controls                                     |
| ------------- | ------------------------ | ---------------------------------------------------- |
| `flex-grow`   | `flex-grow: 1`           | Share of positive free space                         |
| `flex-shrink` | `flex-shrink: 0`         | Whether/how much an item shrinks when space is short |
| `flex-basis`  | `flex-basis: 200px`      | Initial main size before flex distribution           |
| `flex`        | `flex: 1 1 200px`        | Grow, shrink, and basis shorthand                    |
| `align-self`  | `align-self: flex-start` | One item's cross-axis alignment                      |
| `order`       | `order: 2`               | Visual order, without changing source reading order  |

In a typical horizontal writing mode, `row` makes the main axis horizontal and `column` makes it vertical. Therefore `justify-content` is not always horizontal and `align-items` is not always vertical.

A container's `align-items` and a child's `align-self` work together. The child can override its own alignment; it does not change its siblings.

### Grid properties

| Where  | Property                     | Example                         | What it controls                                 |
| ------ | ---------------------------- | ------------------------------- | ------------------------------------------------ |
| Parent | `grid-template-columns`      | `repeat(3, minmax(0, 1fr))`     | Explicit column tracks                           |
| Parent | `grid-template-rows`         | `auto 1fr auto`                 | Explicit row tracks                              |
| Parent | `grid-auto-rows`             | `minmax(100px, auto)`           | Size of automatically created rows               |
| Parent | `grid-template-areas`        | `"header header" "nav content"` | Named regions                                    |
| Parent | `gap`                        | `1rem`                          | Space between tracks                             |
| Parent | `justify-items`              | `start`                         | Items' inline-axis alignment in their grid areas |
| Parent | `align-items`                | `center`                        | Items' block-axis alignment in their grid areas  |
| Parent | `place-items`                | `center`                        | Shorthand for align-items and justify-items      |
| Child  | `grid-column`                | `1 / -1`                        | Column placement or span                         |
| Child  | `grid-row`                   | `span 2`                        | Row placement or span                            |
| Child  | `grid-area`                  | `header`                        | Named area or placement shorthand                |
| Child  | `justify-self`, `align-self` | `justify-self: end`             | One item's alignment                             |

Flexbox is often useful for one-dimensional arrangements. Grid is often useful when coordinating rows and columns. They can be nested and used together.

### Position and layer properties

| Property                         | Example              | What it controls                     |
| -------------------------------- | -------------------- | ------------------------------------ |
| `position`                       | `position: relative` | Positioning mode                     |
| `top`, `right`, `bottom`, `left` | `top: 0`             | Insets for positioned boxes          |
| `inset`                          | `inset: 0`           | Shorthand for all four insets        |
| `z-index`                        | `z-index: 10`        | Stack level within stacking contexts |

```css
.card {
  position: relative;
}

.badge {
  position: absolute;
  top: 0.5rem;
  right: 0.5rem;
}
```

The positioned card supplies the badge's containing block in this layout. The badge leaves normal flow; other content does not automatically reserve space for it.

`top: 0` does not move an ordinary static element. Check its positioning mode first. A large `z-index` cannot escape an ancestor's stacking context.

### Image and overflow properties

| Property                   | Example                       | What it controls                               |
| -------------------------- | ----------------------------- | ---------------------------------------------- |
| `object-fit`               | `object-fit: cover`           | How image/video content fits its element's box |
| `object-position`          | `object-position: center top` | Alignment of that content within its box       |
| `overflow`                 | `overflow: auto`              | Handling content that exceeds a box            |
| `overflow-x`, `overflow-y` | `overflow-y: auto`            | Overflow handling for one axis                 |

`cover` fills the box with possible cropping. `contain` shows the whole image with possible empty space. These differ from `background-size`, which controls background images.

`overflow: hidden` clips overflow; `auto` allows scrolling when needed. Overflow on ancestors can affect sticky positioning, and clipping can hide focus outlines.

### Interaction and transition properties

| Property                     | Example                            | What it controls                                                |
| ---------------------------- | ---------------------------------- | --------------------------------------------------------------- |
| `cursor`                     | `cursor: pointer`                  | Pointer appearance; does not create click behavior              |
| `accent-color`               | `accent-color: teal`               | Accent of supported native controls, such as checkboxes         |
| `appearance`                 | `appearance: none`                 | Native control appearance; custom styling needs care            |
| `user-select`                | `user-select: none`                | Whether users can select text                                   |
| `pointer-events`             | `pointer-events: none`             | Pointer hit testing; does not by itself disable keyboard access |
| `scroll-behavior`            | `scroll-behavior: smooth`          | How relevant programmatic/fragment scrolling behaves            |
| `scroll-margin-top`          | `scroll-margin-top: 5rem`          | Scroll target offset, useful under sticky headers               |
| `transition`                 | `transition: color 200ms ease`     | Animated change between property values                         |
| `transition-property`        | `transition-property: color`       | Which properties transition                                     |
| `transition-duration`        | `transition-duration: 200ms`       | Transition length                                               |
| `transition-timing-function` | `transition-timing-function: ease` | Transition pacing                                               |
| `transform`                  | `transform: translateY(-2px)`      | Visual transformation without normal-flow re-layout             |

A `cursor` style does not replace a real `<button>`. `pointer-events: none` is not a substitute for a button's `disabled` attribute.

Use transitions for deliberate effects and respect reduced-motion preferences. Write transitions on the normal state if you want them when entering and leaving hover/focus.

### Properties versus other CSS tools

Some CSS features are not properties:

| Feature                 | Kind                  | Example                                         |
| ----------------------- | --------------------- | ----------------------------------------------- |
| `.card:hover`           | Selector              | Chooses a hovered card                          |
| `::before`              | Pseudo-element        | A generated box                                 |
| `@media`                | At-rule               | Conditionally applies rules                     |
| `var()`                 | Function              | Reads a custom property                         |
| `calc()`                | Function              | Calculates a value, such as `calc(100% - 2rem)` |
| `min()` / `max()`       | Functions             | Choose the smallest/largest value               |
| `clamp()`               | Function              | Bounds a preferred value between limits         |
| `repeat()` / `minmax()` | Grid sizing functions | Define repeated and bounded tracks              |
| `rem`, `px`, `fr`       | Units                 | Describe dimensions or grid shares              |

```css
.heading {
  font-size: clamp(2rem, 5vw, 4rem);
}
```

The heading prefers `5vw`, but will not become smaller than `2rem` or larger than `4rem` through this declaration.

### A complete small card example

```html
<article class="example-card">
  <h2>A useful idea</h2>
  <p>A short explanation that can wrap onto multiple lines.</p>
  <button type="button">Read more</button>
</article>
```

```css
.example-card {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  width: 100%;
  max-width: 360px;
  padding: 1.5rem;
  border: 1px solid #334155;
  border-radius: 0.75rem;
  background-color: #172238;
  color: #e2e8f0;
}

.example-card h2,
.example-card p {
  margin: 0;
}

.example-card p {
  line-height: 1.6;
}

.example-card button {
  align-self: flex-start;
  padding: 0.5rem 1rem;
  border: 0;
  border-radius: 0.375rem;
  background-color: #5eead4;
  color: #0f172a;
  font: inherit;
}
```

The card controls layout, inside spacing, frame, and default colors. The paragraph controls line spacing. The button adds its own colors and padding and overrides its flex alignment. These rules solve different parts of the same component.

When looking up a property not listed here, use the [MDN CSS property index](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties).

## Box model and spacing

```text
margin → border → padding → content
```

| Property                 | Responsibility                                            |
| ------------------------ | --------------------------------------------------------- |
| `margin`                 | Space outside the border                                  |
| `padding`                | Space inside the border                                   |
| `border`                 | The edge around the padding and content                   |
| `gap`                    | Space between flex or grid items                          |
| `box-sizing: border-box` | Includes padding and borders in declared width and height |

```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
```

This reset removes browser default spacing. Headings and paragraphs still keep other default styles unless those are overridden too.

```css
.card {
  padding: 2rem 1rem;
  margin: 0 auto;
}
```

Two padding values mean top/bottom, then left/right. Four values mean top, right, bottom, left. The same shorthand order applies to margin.

Automatic left and right margins can center a width-limited block. In flex and grid layouts, auto margins can also absorb available space on particular sides.

## Units and dimensions

| Unit or declaration   | Meaning                                                                                                   |
| --------------------- | --------------------------------------------------------------------------------------------------------- |
| `px`                  | CSS pixels                                                                                                |
| `rem`                 | Relative to the root font size                                                                            |
| `em`                  | Relative to the element's font size for most lengths; for `font-size`, relative to the parent's font size |
| `%`                   | A percentage whose reference depends on the property                                                      |
| `fr`                  | A share of available grid space                                                                           |
| `vh`                  | A percentage of viewport height                                                                           |
| `ms`                  | Milliseconds for animation or transition timing                                                           |
| `width: 100%`         | Fill the relevant available width                                                                         |
| `max-width: 600px`    | Limit width; it does not guarantee that width                                                             |
| `height: 100vh`       | A viewport-height box                                                                                     |
| `height: fit-content` | Size according to content within available constraints                                                    |

With a 16px root font size, `1rem` is 16px and `0.5rem` is 8px. Browser/user settings can change the root size.

## Flexbox

Flexbox arranges direct children along a main axis.

```css
.stack {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.icon-row {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}
```

| Property                 | Effect                                                       |
| ------------------------ | ------------------------------------------------------------ |
| `display: flex`          | Makes direct children flex items                             |
| `flex-direction: row`    | Horizontal main axis in a typical left-to-right writing mode |
| `flex-direction: column` | Vertical main axis in a typical horizontal writing mode      |
| `justify-content`        | Distributes items or space along the main axis               |
| `align-items`            | Aligns items on the cross axis                               |
| `gap`                    | Separates items                                              |
| `flex-wrap: wrap`        | Allows items to continue on another line                     |
| `flex: 1`                | Allows an item to grow and shrink with a zero basis          |

`justify-content: space-between` distributes available space between items. `align-items: center` centers across the cross axis. Their physical direction changes with the layout's axes.

A wrapping badge list commonly combines a flex parent with individually styled badge children.

## CSS Grid

Grid manages rows and columns.

```css
.layout {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 2rem;
}
```

- `repeat(2, ...)` creates two repeated tracks.
- `1fr` gives each column a share of the available space.
- `minmax(0, 1fr)` allows the track to shrink below its default content-based minimum.
- Content can still overflow a track if its own sizing does not allow it to shrink.

```css
.card {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 1rem;
}

.card-content {
  grid-column: span 3;
}
```

The first item can occupy one column and the content span three. A declaration such as `span 3 / span 3` does not mean six columns; in this automatic-placement situation, the item still spans three tracks.

```css
.full-width {
  grid-column: 1 / -1;
}
```

This spans from the first to the last explicit grid line.

`display: grid; place-items: center` is also useful for centering a single icon or image on both grid axes.

## Responsive design and media queries

Start with base styles, then adapt when the available space changes.

```css
.layout {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
}

@media (min-width: 640px) {
  .layout {
    gap: 2rem;
  }
}

@media (min-width: 1024px) {
  .layout {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}
```

At 1024px, both media queries are active. The resulting layout has two columns and a `2rem` gap. A later media query does not replace all earlier rules; it only contributes declarations.

The names “mobile,” “tablet,” and “desktop” are convenient labels. Width queries measure viewport width rather than identifying the physical device. Choose breakpoints where the content needs a different layout.

### Visual order

`order` changes the visual placement of flex and grid items. It does not change their HTML reading order or necessarily their keyboard focus order. Prefer a sensible HTML order first.

### Showing and hiding elements

`display: none` removes an element and its descendants from layout and the accessibility tree. It differs from visual hiding intended to keep text available to screen readers.

## Positioning and stacking

| Value                | Behavior                                                                                       |
| -------------------- | ---------------------------------------------------------------------------------------------- |
| `position: static`   | Normal default positioning                                                                     |
| `position: relative` | Keeps normal-flow space and can establish a containing block for positioned descendants        |
| `position: absolute` | Leaves normal flow and uses a containing block for positioning                                 |
| `position: fixed`    | Usually positioned relative to the viewport; certain ancestors can change the containing block |
| `position: sticky`   | Remains in flow but sticks within scroll/container constraints                                 |

```css
.section-heading {
  position: sticky;
  top: 0;
}
```

Sticky positioning needs an inset such as `top: 0`. Its behavior depends on its container, available scroll space, and ancestor overflow. It is not the same as permanently fixing an element to the viewport.

`inset: 0` sets all four offsets to zero. `top`, `right`, `bottom`, and `left` can also be set individually.

`z-index` controls stacking within stacking contexts. A larger number does not automatically place an element above every other element on the page.

### A background behind a heading

```css
.section-heading {
  position: sticky;
  top: 0;
  padding: 1rem 0;
}

.section-heading::before {
  content: '';
  position: absolute;
  inset: 0;
  background: rgba(15, 23, 42, 0.9);
}

.section-heading h2 {
  position: relative;
  z-index: 1;
}
```

The parent handles sticking, the pseudo-element paints a background, and the heading is positioned above it. These selectors cooperate to create one component.

## Images, frames, and thumbnails

```css
.thumbnail {
  aspect-ratio: 16 / 9;
  overflow: hidden;
  border: 1px solid rgba(94, 234, 212, 0.35);
  border-radius: 0.5rem;
}

.thumbnail img {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```

| Property              | Role                                                                 |
| --------------------- | -------------------------------------------------------------------- |
| `aspect-ratio`        | Sets a preferred width-to-height ratio                               |
| `object-fit: cover`   | Fills the image box while preserving proportions and cropping excess |
| `object-fit: contain` | Fits the whole image, potentially leaving empty space                |
| `overflow: hidden`    | Clips content outside the container                                  |
| `border`              | Adds a visible frame                                                 |
| `border-radius`       | Rounds corners                                                       |

The container controls the shape and frame. The image controls how its content fills that box. The outer layout also matters: a thumbnail in one narrow grid column cannot become wide just because it has `max-width: 200px`.

For a circle, combine a square box, such as `aspect-ratio: 1`, with `border-radius: 50%`.

## Typography

| Property                    | Role                                                                    |
| --------------------------- | ----------------------------------------------------------------------- |
| `font-family`               | Font choices and fallbacks                                              |
| `font-size`                 | Text size                                                               |
| `font-weight`               | Weight, such as 400 regular, 500 medium, or 600 semibold when supported |
| `line-height`               | Height of line boxes                                                    |
| `text-transform: uppercase` | Changes displayed capitalization without rewriting the HTML text        |
| `text-decoration`           | Underlines and other text decorations                                   |

A unitless `line-height`, such as `1.5`, scales with the element's font size. A fixed value such as `1.5rem` stays tied to the root size.

A line box contains more than just visible letter shapes. Two elements can have equal `gap` values but appear differently spaced because of font size, line height, or wrapping.

### Applying an external font

```css
:root {
  --font-family: 'Roboto', sans-serif;
}

body {
  font-family: var(--font-family);
}

button,
input {
  font: inherit;
}
```

The HTML font link loads the font; the CSS variable stores the font list; `font-family` applies it. `font: inherit` lets form controls use their parent's font settings too. The fallback `sans-serif` is used if the named font is unavailable.

Examples supplied by font websites may contain placeholders such as `<weight>` or `<uniquifier>`. Replace those placeholders if using the example. Extra variable-font settings are not always needed for a basic font-family declaration.

A missing semicolon can accidentally join two declarations and make both invalid:

```css
/* Correct: the semicolon separates these declarations. */
body {
  font-family: var(--font-family);
  background-color: #16171d;
}
```

## Hover, focus, transitions, and selection

```css
.text-link {
  color: navy;
  transition: color 200ms;
}

.text-link:hover,
.text-link:focus-visible {
  color: teal;
}
```

Declare transitions on the normal state to get timing when entering and leaving that state. Naming the property makes the intended animation clear.

`transition-duration: 200ms` alone leaves the transition property at its default, `all`, so several eligible property changes may animate.

Keyboard users need visible focus. Hover styling alone does not provide an equivalent keyboard interaction.

```css
::selection {
  color: #0f172a;
  background: #5eead4;
}
```

This styles selected text. A selector such as `p::selection` limits the rule to selected text inside paragraphs.

### Generated underlines

```css
.archive-link {
  position: relative;
  text-decoration: none;
}

.archive-link::after {
  content: '';
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  height: 1px;
  background: transparent;
  transition: background-color 200ms;
}

.archive-link:hover::after,
.archive-link:focus-visible::after {
  background: currentColor;
}
```

The link supplies the positioning reference. `::after` creates the line. The hover and focus rules change its color. `content: ""` creates the generated box without adding visible text.

## Smooth scrolling and reduced motion

```css
html {
  scroll-behavior: smooth;
}

@media (prefers-reduced-motion: reduce) {
  html {
    scroll-behavior: auto;
  }
}
```

Smooth scrolling can affect fragment navigation. Respect users who request reduced motion, and review other transitions or animations separately.

A back-to-top link can target an ID near the start of the page; JavaScript is not required.

## Accessibility

### Accessible names for icon-only links

```html
<a href="https://example.com/profile" aria-label="Visit my profile">
  <i class="fa-solid fa-user" aria-hidden="true"></i>
</a>
```

The link has a meaningful name. The decorative icon is hidden from accessibility APIs. The `<i>` tag does not inherently create an icon; the icon library's CSS provides its appearance.

Use normal visible text when possible. Do not add `aria-label` to every element: naming support depends on the element and its role.

### Visually hidden text

```html
<div class="item-stat">
  <i class="fa-solid fa-star" aria-hidden="true"></i>
  <p>0<span class="sr-only"> stars</span></p>
</div>
```

```css
.item-stat {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip-path: inset(50%);
  white-space: nowrap;
  border: 0;
}
```

The visible content is a star and a number. The text also provides “0 stars” for assistive technology. The layout class, icon attribute, text, and utility class each have a separate job.

Do not put `aria-hidden="true"` on the whole container if the number conveys information. Descendants would also be hidden. Do not use `display: none` for text that screen readers should still access.

### Images and alternatives

Use `alt` to express an image's purpose in context. A useful screenshot description is more informative than `alt="thumbnail"`. Purely decorative images can use an empty alternative, `alt=""`.

### Other checks

- Use logical heading levels and meaningful link text.
- Keep keyboard focus visible.
- Check text contrast against its actual background.
- Keep the reading order sensible across responsive layouts.
- Test zoom and narrow viewports.
- Use links for navigation and buttons for actions.

## Contrast, keyboard access, and audits

### Color contrast and transparency

WCAG AA requires at least **4.5:1** for normal text and **3:1** for large text. Large text means at least 24 CSS pixels for normal weight, or approximately 18.67 CSS pixels when bold. Relevant non-text information, such as a custom focus indicator, generally needs **3:1** against adjacent colors.

Check the actual rendered colors. `opacity` affects the whole element, including its text. A readable text color can become too faint when opacity is reduced. Transparent backgrounds must be combined with the colors behind them before calculating contrast.

```css
.date {
  color: #94a3b8;
  /* Avoid reducing opacity without recalculating text contrast. */
}
```

Do not confuse text-to-background contrast with link recognition. A link can have enough background contrast while being difficult to distinguish from the surrounding text. An underline is a clear non-color cue. If using weight or another persistent cue instead, verify that the difference remains obvious with the real font and fallback fonts. A hover-only change cannot help someone who has not found the link yet.

Reference: [WCAG contrast](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html) and [use of color](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html).

### Focus is different from hover and active

| Selector                | When it applies                                                              |
| ----------------------- | ---------------------------------------------------------------------------- |
| `:hover`                | A pointing device is over the element                                        |
| `:active`               | The element is being activated, such as while a mouse button is held         |
| `:focus-visible`        | The focused element needs a visible focus indicator according to the browser |
| `[aria-pressed='true']` | The HTML attribute says a toggle button is pressed                           |

```css
a:focus-visible,
button:focus-visible {
  outline: 2px solid #5eead4;
  outline-offset: 4px;
}

button:active {
  transform: translateY(1px);
}
```

Removing an underline does not mean removing the focus outline. `outline` also differs from `border`: it does not take space in normal layout.

### Skip links and accessible headings

```html
<a class="skip-link" href="#main-content">Skip to content</a>
<header><!-- Navigation and introduction --></header>
<main id="main-content" tabindex="-1">
  <h1>Page content</h1>
</main>
```

`tabindex="-1"` makes the target focusable without adding it to the normal Tab order. The skip link lets keyboard users bypass repeated content. Hide the link visually until it receives focus, then position it clearly above the page content. Test the native link behavior in a browser, not just a simulated DOM.

Use heading levels for structure rather than appearance. A job title or subtitle does not automatically need to be a heading. A heading with `display: none` is also removed from the accessibility tree; use a visually hidden technique if the heading should remain available to screen readers.

### Labels, current location, and toggle state

```jsx
<button
  type="button"
  aria-pressed={showOpenOnly}
  onClick={() => setShowOpenOnly(!showOpenOnly)}
>
  Show open items
</button>
```

`aria-pressed` communicates a toggle button's state; it does not change state or add styling by itself. `aria-current="location"` can identify the current section link. Do not use the two attributes interchangeably.

Repeated action links benefit from specific names:

```jsx
<button aria-label={`Delete item: ${props.title}`} onClick={props.onDelete}>
  Delete
</button>
```

The backticks create a template literal. `${props.title}` inserts the title. Keep the visible label in the accessible name so speech and screen reader users can relate it to the interface.

### What a complete audit still needs

- Review source structure, labels, contrast, assets, and fragment links.
- Use Tab, Shift+Tab, Enter, and Space where appropriate.
- Check narrow screens, short screens, zoom, and increased text spacing.
- Check that sticky content does not obscure focused controls.
- Test a real screen reader and reduced-motion/high-contrast settings.
- Verify live links, external fonts and icons, and linked documents such as PDFs.

A successful build, passing unit tests, valid PDF syntax, or a clean automated scan does not establish full WCAG compliance. A tagged PDF can still have incorrect reading order or metadata. Record what was actually tested and what remains unverified.

Reference: [WCAG 2.2 quick reference](https://www.w3.org/WAI/WCAG22/quickref/).

## Organizing a stylesheet

A practical order is:

- Variables and shared values.
- Base styles and resets.
- Page layout.
- Shared components and utility classes.
- Page sections or specialized components.
- Interaction states.
- Responsive overrides.

Use descriptive comments, such as `/* Navigation */`, near the relevant rules. Keep related selectors close together. Consistency matters more than choosing one universal order.

For more visible section boundaries, use the same comment style throughout:

```css
/* ========================================
   Form controls
   ======================================== */
```

Use meaningful section names rather than numbers, which become difficult to maintain when moving sections.

Repeated selectors are sometimes intentional, especially in media queries. Identical duplicate declarations add noise; conflicting duplicates require checking the cascade before removal.

## Debugging CSS

| Symptom                                 | First checks                                                        |
| --------------------------------------- | ------------------------------------------------------------------- |
| Style does not apply                    | Selector spelling, HTML class, stylesheet path, syntax              |
| Value is crossed out in developer tools | Specificity, source order, active media queries                     |
| Text size is unexpected                 | Browser defaults, matching declarations, inheritance                |
| Space looks like padding                | Inspect margin, padding, gap, line height, and nesting separately   |
| Grid item is too small                  | Available track width, spans, content sizing, maximum width         |
| Sticky element does not stick           | Insets, container height, scrolling ancestor, overflow              |
| Anchor works only at one width          | Hidden targets, missing IDs, overlays                               |
| Link cannot be clicked                  | Overlapping positioned elements, stacking, incorrect HTML           |
| Layout breaks after adding a card       | Unclosed tags and incorrect parent/child nesting                    |
| Local image fails online                | Path, case sensitivity, committed files, deploy contents            |
| Changes are not visible                 | Saved file, correct folder/server, browser cache, deployment status |

Developer tools can show the box model, computed styles, matched rules, flex/grid overlays, and which declarations are overridden. Use those before changing unrelated properties.

A formatter can catch some syntax problems and keep code consistent. It cannot prove that the design, links, or accessibility work correctly.

## JavaScript essentials

JavaScript variables hold values. Functions group reusable steps, and arrays and objects organize data.

```javascript
const task = {
  id: 1,
  title: 'Learn JavaScript',
  completed: false,
};

console.log(task.title); // 'Learn JavaScript'
task.completed = true;
```

| Concept        | Example                                          | Meaning                                          |
| -------------- | ------------------------------------------------ | ------------------------------------------------ |
| String         | `'Learn JavaScript'`                             | Text                                             |
| Number         | `42`                                             | A numeric value                                  |
| Boolean        | `true`, `false`                                  | True or false                                    |
| Array          | `[1, 2, 3]`                                      | An ordered collection                            |
| Object         | `{ title: 'Learn', completed: false }`           | Named properties                                 |
| `undefined`    | A missing return value or unsuccessful `.find()` | No value has been provided                       |
| `null`         | An intentionally empty value                     | Also returned by some APIs when nothing is found |
| `typeof value` | `typeof 42`                                      | Inspect a value's type                           |

Use **camelCase** for variables and functions: `taskList`, `findTaskById`. React component names use **PascalCase**: `TaskItem`.

### const and let

Use `const` when a variable will not be reassigned. Use `let` when it will.

```javascript
const title = 'Learn React';
let count = 0;
count++;
```

`const` does not make objects or arrays immutable:

```javascript
const titles = ['Learn JavaScript'];
titles.push('Learn React'); // Allowed: changes the array's contents.
// titles = [];           // Not allowed: reassigns the variable.
```

`const` helps prevent accidental reassignment; it is not a security feature. Always declare variables rather than relying on accidental globals.

### Converting strings to numbers

```javascript
Number('43.8'); // 43.8
Number('43px'); // NaN
parseInt('43px', 10); // 43
parseInt('43.8', 10); // 43, not 44
```

`Number()` converts the whole value. `parseInt()` reads an integer prefix from a string; `10` means decimal. It does not round. An empty string becomes `0` with `Number()` but `NaN` with `parseInt()`.

### Functions, parameters, and return

```javascript
function calculateArea(width, height) {
  return width * height;
}

const area = calculateArea(3, 4); // 12
```

`width` and `height` are parameters. `3` and `4` are arguments supplied by the caller.

`return` sends a value back and ends the current function call. Code after an unconditional `return` cannot execute. A function that reaches its end without returning a value returns `undefined`.

```javascript
function findTitle(task) {
  if (!task) {
    return undefined;
  }
  return task.title;
}
```

Writing `saveTasks` refers to a function. Writing `saveTasks()` calls it. A function passed as an event callback should usually be passed without calling it immediately.

### Scope and closures

A variable declared inside a function is not directly accessible outside it. A nested function can keep access to that variable:

```javascript
function createCounter() {
  let count = 0;
  return function () {
    count++;
    return count;
  };
}

const increment = createCounter();
increment(); // 1
increment(); // 2
```

That retained access is a **closure**. Logging `count` outside `createCounter` would fail because it is outside the variable's scope.

## Conditions, booleans, and logical operators

| Operator            | Meaning                | Example                                  |
| ------------------- | ---------------------- | ---------------------------------------- |
| `=`                 | Assign a value         | `completed = true`                       |
| `===`               | Strict equality        | `task.id === id`                         |
| `!==`               | Strict inequality      | `task.id !== id`                         |
| `!`                 | Logical NOT            | `!true` is `false`                       |
| `&&`                | Logical AND            | With booleans, both must be true         |
| `\|\|`              | Logical OR             | With booleans, at least one must be true |
| `condition ? a : b` | Conditional expression | Choose `a` when true, otherwise `b`      |

Objects are truthy. `undefined`, `null`, `false`, `0`, `NaN`, and the empty string are falsy. An empty array and the string `'false'` are truthy.

### OR means either condition is enough

For boolean inputs:

| Left side | Right side | `left \|\| right` |
| --------- | ---------- | ----------------- |
| `true`    | `true`     | `true`            |
| `true`    | `false`    | `true`            |
| `false`   | `true`     | `true`            |
| `false`   | `false`    | `false`           |

Think: “Take an umbrella if it rains **OR** snows.” Rain is enough; snow is enough. Neither means the condition is false.

JavaScript's `||` actually returns an operand, rather than always converting it to a boolean. In the examples here, both operands are booleans, so the result is a boolean. It also short-circuits: if the left side is truthy, the right side is not evaluated.

### A filter switch, step by step

```javascript
!showOnlyIncomplete || task.completed === false;
```

Read this as: **“The filter is off OR this task is unfinished.”**

| Filter | Task       | Left side: filter off? | Right side: unfinished? | Keep task? |
| ------ | ---------- | ---------------------- | ----------------------- | ---------- |
| Off    | Completed  | `true`                 | `false`                 | Yes        |
| Off    | Unfinished | `true`                 | `true`                  | Yes        |
| On     | Completed  | `false`                | `false`                 | No         |
| On     | Unfinished | `false`                | `true`                  | Yes        |

The equivalent longer callback is:

```javascript
(task) => {
  if (showOnlyIncomplete === false) {
    return true;
  }
  return task.completed === false;
};
```

When the filter is off, `return true` runs and ends the callback. The task's completion status does not need to be checked. Either form is valid; choose the one you can explain.

## Callbacks and arrow functions

A **callback** is a function passed to other code, which calls it when needed. Callbacks are not necessarily asynchronous.

```javascript
const doubled = [1, 2, 3].map(function (number) {
  return number * 2;
});
```

The function passed to `.map()` is the callback. `.map()` calls it for each existing array element.

The arrow version is:

```javascript
const doubled = [1, 2, 3].map((number) => number * 2);
```

| Arrow form                           | Return behavior                                  |
| ------------------------------------ | ------------------------------------------------ |
| `(number) => number * 2`             | Automatically returns the expression             |
| `(number) => { return number * 2; }` | A block requires an explicit return              |
| `(number) => ({ value: number })`    | Parentheses make an object literal an expression |

```javascript
const result = [1, 2].map((number) => {
  number * 2;
});
// [undefined, undefined]: the callback did not return anything.
```

Arrow functions also handle `this` differently from ordinary functions. For these simple array callbacks, focus first on parameters and return values.

## filter, map, and find

| Method      | Question                         | Result                                   |
| ----------- | -------------------------------- | ---------------------------------------- |
| `.filter()` | Which elements should stay?      | A new array containing matching elements |
| `.map()`    | What should each element become? | A new array containing callback results  |
| `.find()`   | Which is the first match?        | One matching element, or `undefined`     |

These methods do not directly modify the source array. A callback can still mutate objects if you write code that does so. Array copies are shallow: nested objects are not automatically cloned.

### filter selects elements

```javascript
const numbers = [2, 7, 4, 9];
const selected = numbers.filter((number) => number > 5);
// [7, 9]
```

For each element, a truthy callback result means keep it; a falsy result means leave it out. A false result does not preserve the original element unchanged: it removes that element from the result.

```javascript
[2, 7, 4].filter(() => true); // [2, 7, 4]
[2, 7, 4].filter(() => false); // []
```

See the [MDN filter reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter).

### map transforms values

```javascript
const numbers = [2, 7, 4];
const doubled = numbers.map((number) => number * 2);
// [4, 14, 8]
```

For ordinary dense arrays, the result has one output element for every input element. Returning `false` does not remove an element:

```javascript
[2, 7, 4].map((number) => number > 5);
// [false, true, false]
```

See the [MDN map reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map).

### Combining filter and map

```javascript
const result = [2, 7, 4, 9]
  .filter((number) => number > 5)
  .map((number) => number * 2);
// First: [7, 9]. Then: [14, 18].
```

Each method operates on the array returned by the previous step.

```javascript
const tasks = [
  { id: 1, title: 'Read a chapter', completed: false },
  { id: 2, title: 'Write notes', completed: true },
];

const titles = tasks
  .filter((task) => task.completed === false)
  .map((task) => task.title);
// ['Read a chapter']
```

### find returns one element

```javascript
const task = tasks.find((task) => task.id === 2);
const missing = tasks.find((task) => task.id === 99); // undefined
```

Check that a match exists before reading or changing its properties.

### Other array and string methods

| Method or property    | Meaning                                                         |
| --------------------- | --------------------------------------------------------------- |
| `.length`             | Number of array elements or string length                       |
| `.push(value)`        | Appends to the existing array; returns the new length           |
| `.slice(start, end)`  | Copies a range; `end` is excluded; does not modify the original |
| `.sort(compare)`      | Sorts the existing array                                        |
| `.indexOf(value)`     | Finds an index or returns `-1`                                  |
| `.concat(other)`      | Combines values into a new array                                |
| `.trim()`             | Returns a string without leading or trailing whitespace         |
| `Object.keys(object)` | Returns an array of the object's own enumerable string keys     |

Call methods with parentheses: `items.slice(1, -1)`. `items.slice[...]` is property access, not a method call.

`.length` has no parentheses because it is a property whose value you read. `filter()` is a method you call; it returns an array, and that array has its own `.length`.

```javascript
const openCount = items.filter((item) => item.completed === false).length;
```

For numeric ascending order, use `(a, b) => a.price - b.price`. Reverse the subtraction for descending order.

### every and parsed data

`.every()` returns `true` only if every visited element passes the callback's check. It returns `true` for an empty array too.

```javascript
[2, 4, 6].every((number) => number > 0); // true
[2, -4, 6].every((number) => number > 0); // false
```

`Array.isArray(value)` only checks the container. `[null, 'hello', 42]` is an array, but it may not contain the objects your application needs.

## Spread syntax and immutable updates

Spread syntax `...` copies array elements or object properties into a new container.

```javascript
const numbers = [1, 2, 3];
const extended = [...numbers, 4];
// numbers: [1, 2, 3]; extended: [1, 2, 3, 4]
```

```javascript
const original = { id: 1, title: 'Learn', completed: false };
const updated = { ...original, completed: true };
```

Later properties override earlier ones. `{ completed: true, ...original }` would restore the original `completed` value instead.

These are **shallow copies**. A nested object or array is still shared until that nested value is copied too.

### Add without push

```javascript
function addItem(items, newItem) {
  return [...items, newItem];
}
```

The caller must use the returned array:

```javascript
items = addItem(items, newItem);
```

Calling `addItem(items, newItem)` without storing its result leaves `items` pointing to the original array.

### Remove with filter

```javascript
function removeItem(items, id) {
  return items.filter((item) => item.id !== id);
}
```

### Update one object with map and spread

```javascript
function toggleItem(items, id) {
  return items.map((item) => {
    if (item.id === id) {
      return { ...item, completed: !item.completed };
    }
    return item;
  });
}
```

The matching item is copied. Other items retain their references. Forgetting `return item` produces `undefined` entries for nonmatching items; serializing those array entries to JSON turns them into `null`.

## Browser JavaScript and the DOM

The **DOM** is the browser's object representation of the HTML document.

```html
<ul id="item-list"></ul>
<script src="app.js" defer></script>
```

```javascript
const listElement = document.querySelector('#item-list');
const itemElement = document.createElement('li');
itemElement.textContent = 'Read a chapter';
listElement.appendChild(itemElement);
```

| API                                | Purpose                                                         |
| ---------------------------------- | --------------------------------------------------------------- |
| `document.querySelector(selector)` | Find the first matching element, or return `null`               |
| `document.createElement(tag)`      | Create an element                                               |
| `.textContent`                     | Read or write text; assigning it replaces the existing children |
| `.appendChild(element)`            | Append a child node                                             |
| `.setAttribute(name, value)`       | Set an HTML attribute                                           |
| `input.value`                      | Read or write the input's current value                         |
| `checkbox.checked`                 | Read or write a checkbox's boolean state                        |
| `.focus()`                         | Move keyboard focus to an element                               |
| `form.reset()`                     | Restore form controls to their defaults                         |

`'#item-list'` selects an ID. `'item-list'` selects a tag with that name. Always check spelling when a selection unexpectedly returns `null`.

Use `textContent` for user-entered text rather than treating it as HTML.

### Events and handlers

```javascript
button.addEventListener('click', () => {
  console.log('Clicked');
});
```

The callback is the **event handler**: code that runs when the event occurs. It does not need a separate function name.

- `click`: activating a button.
- `change`: changing a checkbox's value.
- `submit`: submitting a form, including through Enter.

```javascript
form.addEventListener('submit', (event) => {
  event.preventDefault();
  const title = input.value.trim();
  if (!title) return;
  // Update data, save it, render the interface, then clear the form.
});
```

`preventDefault()` stops the browser's normal submission behavior. `required` rejects an empty input, but whitespace-only text still needs trimming and validation.

### Rendering in plain JavaScript

A typical render function clears old content before creating new elements. Otherwise repeated calls append duplicates.

Separate task operations from rendering. A useful flow is:

```text
User event → update data → save data → render current view
```

Store the selected filter separately from the data, then reuse one function to decide what to render. Replacing DOM nodes can remove keyboard focus; restore it when appropriate.

### Browser versus Node.js

Browser code can use `document`. A normal Node.js process cannot: it has no HTML document. Run a DOM-based app through a browser and inspect its browser console. Use Node.js for independent JavaScript scripts and server code.

`node --check app.js` checks syntax without executing browser APIs. It does not prove that browser behavior works.

### Highlighting the current section

In-page links provide navigation with ordinary HTML. JavaScript can additionally mark which section the visitor is reading.

```html
<nav aria-label="On this page">
  <a href="#introduction">Introduction</a>
  <a href="#examples">Examples</a>
</nav>
<main>
  <section id="introduction"><h2>Introduction</h2></section>
  <section id="examples"><h2>Examples</h2></section>
</main>
```

```javascript
const links = [...document.querySelectorAll('nav a[href^="#"]')];
const sections = links.map((link) =>
  document.getElementById(link.hash.slice(1)),
);

function updateCurrentSection() {
  let current = sections[0];

  for (const section of sections) {
    if (section.getBoundingClientRect().top <= 160) {
      current = section;
    }
  }

  for (const link of links) {
    if (link.hash === `#${current.id}`) {
      link.setAttribute('aria-current', 'location');
    } else {
      link.removeAttribute('aria-current');
    }
  }
}

window.addEventListener('scroll', updateCurrentSection, { passive: true });
window.addEventListener('resize', updateCurrentSection);
updateCurrentSection();
```

Run this script after the example markup exists, such as with `defer`. This small example assumes at least one navigation link and a valid section for every fragment ID.

`getBoundingClientRect().top` measures the section's top relative to the viewport. The last section whose heading passed the chosen boundary becomes current. The initial call sets the state before scrolling. No JavaScript scroll action is needed for ordinary links.

```css
nav a::before {
  content: '';
  display: inline-block;
  width: 2rem;
  height: 2px;
  background: currentColor;
}

nav a[aria-current='location']::before {
  width: 4rem;
}
```

The attribute selector connects the script's state to the CSS. A longer line provides a cue beyond color. Review the cascade: a general class selector can override a less specific navigation rule even if that rule appears later.

For a longer page, batch scroll updates with `requestAnimationFrame` so only one update is queued per frame. Consider restored scroll positions, hash changes, and late-loading content. Test the real layout; simulated section coordinates only test the selection logic.

## JSON and localStorage

```javascript
localStorage.setItem('items', JSON.stringify(items));
```

`localStorage` stores strings. `JSON.stringify()` converts serializable data into JSON text.

```javascript
const savedItems = localStorage.getItem('items');
if (savedItems !== null) {
  items = JSON.parse(savedItems);
}
```

`getItem()` returns the stored string or `null`. `JSON.parse()` converts JSON text back into JavaScript data and can throw if the text is invalid.

Important habits:

- Save after adding, deleting, or changing data.
- Load before the first render.
- Do not confuse a function such as `saveItems` with a variable such as `savedItems`.
- Validate parsed data; valid JSON is not necessarily the expected array shape.
- Use `try...catch` when reading or writing storage may fail.
- Recalculate a numeric ID counter from loaded IDs rather than resetting it to a fixed value.
- Preserve an empty saved array; an empty list is valid data.

Browser storage belongs to a website origin and browser profile. A local preview and a deployed website have separate storage. It does not synchronize between devices and should not be treated as a secure place for secrets.

### Handling parsing and storage failures

```javascript
function loadItems() {
  try {
    const savedItems = localStorage.getItem('saved-items');

    if (savedItems !== null) {
      const parsedItems = JSON.parse(savedItems);
      const isValid =
        Array.isArray(parsedItems) &&
        parsedItems.every(
          (item) =>
            item !== null &&
            typeof item === 'object' &&
            (typeof item.id === 'string' || typeof item.id === 'number') &&
            typeof item.title === 'string' &&
            typeof item.completed === 'boolean',
        );

      if (isValid) return parsedItems;
    }
  } catch (error) {
    console.error('Could not read saved items:', error);
  }

  return [];
}
```

`try` runs the code normally. If it throws, `catch` receives the error. If no error occurs, `catch` is skipped. Valid JSON with an unexpected shape does not necessarily throw, so validation is a separate step.

Put `getItem()` inside `try` too: reading storage itself can fail. Saving needs its own error handling. Logging an error does not save the data; explain storage failures to users when that matters for the application.

This example checks basic field types. Other requirements, such as nonempty titles, finite numeric IDs, and unique IDs, require additional validation. `null` must be checked separately because `typeof null` is `'object'`.

## React components and JSX

React builds interfaces from reusable **components**. A basic component is a function that returns JSX:

```jsx
function Greeting() {
  return <p>Hello!</p>;
}

function App() {
  return (
    <main>
      <h1>A small app</h1>
      <Greeting />
    </main>
  );
}

export default App;
```

- Component names begin with a capital letter.
- JSX looks like HTML but is JavaScript syntax processed by the build tools.
- `{expression}` inserts a JavaScript value into JSX.
- `export default` makes a value available as the module's default export.
- Use `className` rather than `class` in React JSX.

React manages the rendered DOM based on component output. Avoid manually creating and appending the same elements React owns.

### Props pass information into components

```jsx
function Item(props) {
  return (
    <li>
      {props.title}
      {props.completed ? ' — Done' : ' — To do'}
    </li>
  );
}

<Item title="Read a chapter" completed={false} />;
```

Props are values supplied by a parent. Do not mutate them. `completed={false}` passes a boolean; `completed="false"` passes a truthy string. See [React: passing props](https://react.dev/learn/passing-props-to-a-component).

### Lists use map and stable keys

```jsx
<ul>
  {items
    .filter((item) => item.completed === false)
    .map((item) => (
      <Item key={item.id} title={item.title} completed={item.completed} />
    ))}
</ul>
```

`filter()` selects data; `map()` turns each selected object into a React element. `key` helps React identify items among siblings when a list changes. Use a stable ID rather than generating a random key on each render. `key` is special and is not received as `props.key`; pass a separate `id` prop if needed.

### State remembers values between renders

```jsx
import { useState } from 'react';

function App() {
  const [showOnlyIncomplete, setShowOnlyIncomplete] = useState(true);

  return (
    <button type="button" onClick={() => setShowOnlyIncomplete(false)}>
      Show all
    </button>
  );
}
```

`useState` provides the current state value and a setter. Calling the setter requests a new render when the state changes. Call Hooks at the top level of a component or custom Hook, not inside a loop or condition. See [React: useState](https://react.dev/reference/react/useState).

Pass the event handler rather than calling it during rendering:

```jsx
// Run when clicked:
<button onClick={() => setShowOnlyIncomplete(false)}>Show all</button>
```

State setters do not change the state variable in the already-running render. Use new arrays and objects when updating state instead of mutating existing state.

### Components inside a list

```jsx
function ListItem(props) {
  return <li>{props.title}</li>;
}

<ul>
  {items.map((item) => (
    <ListItem key={item.id} title={item.title} />
  ))}
</ul>;
```

For three objects, `map()` produces three `ListItem` elements. React renders the `<li>` returned by each component. The browser receives a list containing three `<li>` elements, not custom `<ListItem>` HTML tags.

### Separate component files

```jsx
// components/ListItem.jsx
function ListItem(props) {
  return <li>{props.title}</li>;
}

export default ListItem;
```

Import the component where it is used:

```jsx
import ListItem from './components/ListItem.jsx';
```

The path is relative to the importing file. Move the component function and export together; remove the duplicate definition from the original file. Moving a component does not automatically move its parent's state.

## React forms and shared state

### Values flow down; callbacks report actions

Keep shared state in the closest parent that needs to coordinate it. A child receives values and functions through props.

```jsx
<ListItem title={item.title} onDelete={() => deleteItem(item.id)} />
```

Inside the child:

```jsx
<button type="button" onClick={props.onDelete}>
  Delete
</button>
```

The parent owns the array and knows how to update it. The child owns the markup for one displayed item. Clicking calls the function supplied by the parent.

`onDelete={() => deleteItem(item.id)}` passes a function for later. `onDelete={deleteItem(item.id)}` calls `deleteItem` immediately during rendering and passes its return value. A function declaration belongs in JavaScript code, not among a component's JSX props.

### Controlled inputs and submitting with Enter

```jsx
function EntryForm(props) {
  return (
    <form onSubmit={props.onSubmit}>
      <label htmlFor="entry-title">New entry</label>
      <input
        id="entry-title"
        type="text"
        value={props.title}
        onChange={(event) => props.onTitleChange(event.target.value)}
      />
      <button type="submit">Add entry</button>
    </form>
  );
}

export default EntryForm;
```

The parent can connect its state like this:

```jsx
const [title, setTitle] = useState('');

function addEntry(event) {
  event.preventDefault();
  const trimmedTitle = title.trim();
  if (trimmedTitle === '') return;

  const entry = {
    id: crypto.randomUUID(),
    title: trimmedTitle,
    completed: false,
  };

  setEntries((previousEntries) => [...previousEntries, entry]);
  setTitle('');
}

// Inside the parent's returned JSX:
<EntryForm title={title} onTitleChange={setTitle} onSubmit={addEntry} />;
```

The snippet assumes the parent also has `entries` state. `crypto.randomUUID()` generates the ID when the entry is created, not on every render. It is available in secure browser contexts, including HTTPS and localhost.

The flow is: type -> `onChange` -> callback -> parent state -> new props -> input display. On submission, `preventDefault()` prevents the normal form navigation. Both the submit button and Enter can submit the form. Keep the input and submit button inside the form; ordinary filter or delete buttons should use `type="button"`.

The prop name `onTitleChange` is chosen by us. `setTitle` is the function passed as its value. Calling `props.onTitleChange('Hello')` therefore calls the parent's `setTitle('Hello')`.

### Derived values and conditional rendering

```jsx
const visibleEntries = entries.filter(
  (entry) => !showOpenOnly || entry.completed === false,
);
const remainingCount = entries.filter(
  (entry) => entry.completed === false,
).length;

// Inside returned JSX:
<p>Remaining: {remainingCount}</p>;
```

Calculate these values from existing state instead of storing extra copies that can become inconsistent. React recalculates them when the component renders.

```jsx
{
  visibleEntries.length === 0 && <p>No entries to show.</p>;
}
```

The comparison produces a boolean. With `&&`, the paragraph is evaluated only when the comparison is true; React does not display the false boolean. Replacing `&&` with `||` reverses when the paragraph is evaluated in this particular expression. Prefer an explicit comparison over `visibleEntries.length && ...`, because React can render the number `0`.

### Conditional classes and matching CSS selectors

```jsx
<span className={props.completed ? 'entry-title is-completed' : 'entry-title'}>
  {props.title}
</span>
```

```css
.entry-title {
  flex: 1;
  min-width: 0;
  overflow-wrap: anywhere;
}

.entry-title.is-completed {
  text-decoration: line-through;
}
```

The base class is always present. A completed entry gains the second class. The selector with no space matches one element with both classes; `.entry-title .is-completed` would instead look for a descendant.

For controls, `input[type='text']` selects text fields rather than checkboxes. `button[aria-pressed='true']` styles the state set by JSX; CSS does not toggle the attribute itself.

Reference: [React: sharing state](https://react.dev/learn/sharing-state-between-components).

## React hooks and browser storage

A Hook is a React function such as `useState` or `useEffect` that provides React functionality. Call Hooks at the top level of a component or custom Hook, not in conditions, loops, or event handlers.

```jsx
import { useEffect, useState } from 'react';

function App() {
  const [items, setItems] = useState(loadItems);

  useEffect(() => {
    try {
      localStorage.setItem('saved-items', JSON.stringify(items));
    } catch (error) {
      console.error('Could not save items:', error);
    }
  }, [items]);

  return <p>Saved items: {items.length}</p>;
}
```

This example uses the `loadItems` helper from the storage section and runs in a browser. The setter is available for future item actions.

- `useState(loadItems)` passes an initializer function rather than calling it on every render.
- `useEffect` synchronizes React state with an external system, here browser storage.
- `[items]` makes this effect run after the initial commit and subsequent commits where `items` changed.
- Read saved state before the first saving effect; otherwise default data can overwrite existing saved data.
- Preserve an empty saved list as valid data.

An effect with `[]` runs after mounting, not after every change to a particular state value. Omitting the dependency array runs it after every commit. Do not use an effect for a count that can be calculated while rendering.

In development, StrictMode can call an initializer twice and run an extra effect setup/cleanup cycle to expose problems. This can explain repeated startup console messages. Initializers should not write storage or perform other side effects.

Reference: [React: useEffect](https://react.dev/reference/react/useEffect).

## Automated testing

This section is a reference. Begin with one tiny test; you do not need to memorize every import or tool before using tests.

### Formatting, linting, building, and testing

| Tool or check         | What it does                                                        |
| --------------------- | ------------------------------------------------------------------- |
| Prettier              | Formats code consistently                                           |
| Oxlint                | Reports configured code problems and suspicious patterns            |
| Vite build            | Builds the app for production; does not prove interactions work     |
| Vitest                | Runs automated tests and reports their results                      |
| React Testing Library | Renders components and finds elements by how users encounter them   |
| user-event            | Simulates user interactions such as typing and clicking             |
| jest-dom              | Adds DOM assertions such as `toBeInTheDocument()`                   |
| jsdom                 | Simulates DOM APIs in Node.js; does not perform real browser layout |

### A first test

```javascript
import { expect, test } from 'vitest';

test('adds two numbers', () => {
  expect(2 + 3).toBe(5);
});
```

`test` names and defines the test. `expect` starts an assertion. `.toBe(5)` calls a matcher. Changing `5` to `6` makes the test fail: the expected result differs from the received result. Missing the matcher's parentheses means it is not called.

### Preparing React tests with Vite

Install development dependencies from the project folder:

```bash
npm install -D vitest jsdom @testing-library/react @testing-library/dom @testing-library/jest-dom @testing-library/user-event
```

Add to the existing Vite configuration without removing its React plugin:

```javascript
test: {
  environment: 'jsdom',
}
```

Add a script inside `package.json`'s `scripts` object:

```json
"test": "vitest"
```

These two snippets are additions inside existing objects, not complete standalone files. Keep the required commas between properties.

### Reading test imports

```jsx
import { afterEach, expect, test } from 'vitest';
import { cleanup, render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import '@testing-library/jest-dom/vitest';
```

Braces import named exports. `userEvent` is a default import. The jest-dom import has no assigned variable: it runs setup code that adds matchers to Vitest's assertions.

```jsx
function Greeting() {
  return <h1>Hello</h1>;
}

afterEach(() => {
  cleanup();
  localStorage.clear();
});

test('shows the heading', () => {
  render(<Greeting />);
  expect(
    screen.getByRole('heading', { name: 'Hello', level: 1 }),
  ).toBeInTheDocument();
});
```

Use this example with the imports above in a `.test.jsx` file. `render` mounts the component in the simulated document. `screen.getByRole` finds an element by its role and accessible name. Literal string names are case-sensitive: `'New entry'` differs from `'New Entry'`.

`afterEach` runs after each test. Explicit `cleanup()` removes mounted components when automatic cleanup is not configured. Clearing localStorage here affects the test environment, not your everyday browser profile. Clear storage before a test too if other setup can seed it; restore spies and mocks after using them.

### Typing, clicking, and waiting

For the `EntryForm` component shown earlier, an interaction test can check the callback:

```jsx
import { vi } from 'vitest';
import EntryForm from './components/EntryForm.jsx';

test('submits the entry form', async () => {
  const user = userEvent.setup();
  const onSubmit = vi.fn((event) => event.preventDefault());

  render(
    <EntryForm
      title="Read a chapter"
      onTitleChange={vi.fn()}
      onSubmit={onSubmit}
    />,
  );

  await user.click(screen.getByRole('button', { name: 'Add entry' }));
  expect(onSubmit).toHaveBeenCalledOnce();
});
```

This snippet also needs the shared imports and cleanup above. It tests submission, not updating an entire list. `vi.fn()` records calls; it does not implement the parent's state logic. To test typing and adding an entry together, render the parent that owns that state.

`await user.type(input, 'Read a chapter')` waits for simulated typing. `await user.click(button)` waits for the click interaction. A test that uses `await` needs an `async` callback. Type the input before clicking submit if the application rejects empty values.

### Commands and common failures

```bash
npm test
npm test -- --run
```

The first command watches for changes. The second runs once and exits. Stop watch mode with `q` or Ctrl+C.

- **No test suite found:** the file has no registered test, perhaps only imports.
- **Unable to find an element:** check the actual label, role, visibility, and whether the action that creates it happened.
- **Multiple matching elements:** make the query more specific or use `within` to search a particular container.
- **Expected versus received differs:** inspect the assertion and application behavior before changing the expected value.

Test adding, rejecting blank input, toggling, deleting the correct item, filtering, empty states, and persistence. Test network and storage failures where they affect important behavior. Mocked responses verify your handling logic, not the availability of the real service. Keep real-browser checks for layout, zoom, and actual keyboard behavior.

References: [Vitest environments](https://vitest.dev/guide/environment.html) and [React Testing Library API](https://testing-library.com/docs/react-testing-library/api/).

## Fetching API data and caching

An API request can supply data that a page should not hard-code, such as a public repository's star count.

```javascript
async function loadStarCount(repository, countElement) {
  try {
    const response = await fetch(`https://api.github.com/repos/${repository}`, {
      headers: { Accept: 'application/vnd.github+json' },
      signal: AbortSignal.timeout(8000),
    });

    if (!response.ok) throw new Error('Request failed');

    const data = await response.json();
    const count = data.stargazers_count;
    if (!Number.isSafeInteger(count) || count < 0) {
      throw new Error('Invalid count');
    }

    countElement.textContent = String(count);
  } catch {
    countElement.textContent = '—';
  }
}
```

The function expects a public `owner/repository` name and an existing DOM element. It does not send an API token. Never put private API credentials in browser code.

- `async` makes the function return a Promise; `await` waits for asynchronous work inside it.
- `fetch` can resolve even for HTTP error responses, so check `response.ok`.
- `response.json()` parses the body asynchronously; validate the returned shape.
- `AbortSignal.timeout(8000)` limits the request to about eight seconds in supporting browsers.
- `0` is valid data. An unavailable count is not the same as zero.
- `textContent` inserts text rather than interpreting external data as HTML.

`data-*` attributes can connect markup to script:

```html
<a
  data-repository="octocat/Hello-World"
  href="https://github.com/octocat/Hello-World/stargazers"
>
  <span data-count>—</span>
</a>
```

```javascript
const link = document.querySelector('[data-repository]');
loadStarCount(link.dataset.repository, link.querySelector('[data-count]'));
```

The normal link still works without JavaScript. JavaScript enhances it with a count.

### Cache data without hiding failures

`sessionStorage` normally lasts for the tab's page session and survives reloads; `localStorage` can remain after the browser is closed. Both store strings and can be unavailable.

Save cached data with a timestamp, for example `{ count: 0, savedAt: Date.now() }`. Validate the parsed values, then compare `Date.now() - savedAt` with a chosen lifetime. A 15-minute cache reduces repeated requests but means a displayed count can be up to 15 minutes old. Handle missing, expired, malformed, and inaccessible caches.

For public unauthenticated GitHub REST requests, the primary limit is normally 60 requests per hour per originating IP. Multiple visitors can share an IP. Caching reduces requests but does not remove the limit. A timeout, HTTP error, or unavailable count should not break the rest of the page.

References: [GitHub repository API](https://docs.github.com/en/rest/repos/repos#get-a-repository) and [rate limits](https://docs.github.com/en/rest/using-the-rest-api/rate-limits-for-the-rest-api).

## Node.js and Express APIs

### Browser, server, and database

- React runs the interface in the browser.
- Node.js runs JavaScript outside the browser, including a backend server.
- Express helps the backend match routes and send responses.
- A database stores data beyond the lifetime of a server process.

A server array is not a database. It can remember changes between HTTP requests while the same process runs, but those changes disappear on restart. Different server instances have separate arrays. localStorage belongs to a browser, not the Express server.

### Starting an Express project

```bash
npm init -y
npm install express
```

Use `"type": "module"` in package.json when writing `import` and `export` in `.js` files.

```javascript
import express from 'express';

const app = express();
app.use(express.json());

app.get('/message', (req, res) => {
  res.json({ message: 'Hello from the server' });
});

const port = Number(process.env.PORT || 3000);
app.listen(port, '0.0.0.0', () => {
  console.log(`Server listening on port ${port}`);
});
```

`app.listen` starts listening for requests. Express does not automatically define a `/` route. `Cannot GET /` can mean the server works but that particular route does not exist.

`req` is the incoming request; `res` is used to send the response. `app.use(express.json())` must run before routes that read JSON request bodies.

### HTTP methods and status codes

| Method | Example        | Purpose                 |
| ------ | -------------- | ----------------------- |
| GET    | `/entries`     | Read the list           |
| GET    | `/entries/:id` | Read one entry          |
| POST   | `/entries`     | Create an entry         |
| PATCH  | `/entries/:id` | Change part of an entry |
| DELETE | `/entries/:id` | Remove an entry         |

| Status | Meaning in a small API                    |
| ------ | ----------------------------------------- |
| 200    | Successful response with data             |
| 201    | A resource was created                    |
| 204    | Success without a response body           |
| 400    | Invalid request data                      |
| 404    | Route or resource not found               |
| 413    | Request body exceeds the configured limit |
| 500    | Unexpected server failure                 |

`res.json(value)` serializes JavaScript data as JSON. `res.status(201).json(entry)` sends JSON with a different status. `res.status(204).send()` has no body, so the client must not call `.json()` on it.

### Route parameters, IDs, and finding data

```javascript
app.get('/entries/:id', (req, res) => {
  const entry = entries.find((entry) => entry.id === req.params.id);
  if (!entry) {
    return res.status(404).json({ error: 'Entry not found' });
  }
  res.json(entry);
});
```

This snippet assumes `app` and an `entries` array already exist. `:id` captures the matching URL segment. In Express, route parameter values are strings. Numeric IDs need deliberate conversion before a strict comparison; UUID strings can be compared directly. Keep ID types consistent rather than adding conversions randomly.

`crypto.randomUUID()` calls the function and returns a UUID string. Without parentheses, `crypto.randomUUID` refers to the function itself. Generate IDs when creating records, not every time an existing record is read. Seed records generated at startup get new IDs after each restart unless stored permanently.

Use `find()` when you need the object and `findIndex()` when you need its array position. Index zero is the first position; `-1` means not found.

```javascript
const index = entries.findIndex((entry) => entry.id === id);
if (index === -1) {
  return res.status(404).json({ error: 'Entry not found' });
}
entries.splice(index, 1);
res.status(204).send();
```

The second argument to `splice(index, 1)` is the number of elements to remove. Check `-1` first: `splice(-1, 1)` removes the last element rather than doing nothing.

### Validate before modifying server data

```javascript
const title = req.body?.title;
if (typeof title !== 'string') {
  return res.status(400).json({ error: 'Title must be a string' });
}
const trimmedTitle = title.trim();
if (trimmedTitle === '') {
  return res.status(400).json({ error: 'Title cannot be empty' });
}
```

These are statements inside a route handler. Optional chaining `?.` safely returns undefined when the body is absent. Check the type before calling string methods. Trim spaces before checking for an empty value. Use `return` with an error response to stop the handler from continuing and sending a second response.

For a completion flag, use `typeof completed === 'boolean'`. Both true and false are valid. `if (!completed)` incorrectly rejects false. The string `"true"` is not the boolean true.

An Express array can be changed with `push`, `splice`, or an object assignment while practicing in-memory data. React state is different: produce a new array or object and call its setter so React can render the change.

### Watching files and reading terminal output

```bash
node --watch index.js
```

Node restarts when watched files change. A package script such as `"dev": "node --watch index.js"` lets you use `npm run dev`. That script is project-specific: in a frontend it may start Vite, and in a backend it may start Node.

An open terminal does not guarantee a running server. Read its latest output. Browser console logs come from browser JavaScript; backend logs appear in the server terminal.

Every watched restart resets in-memory records. If an ID worked before a file save but now gives 404, read the list again and check whether the server regenerated it.

### Sending requests with curl

```bash
curl -i -X POST http://localhost:3000/entries \
  -H 'Content-Type: application/json' \
  -d '{"title":"Read a chapter"}'
```

`-X` chooses the HTTP method, `-H` adds a header, `-d` supplies the body, and `-i` includes response headers/status. The server response appears in the terminal. A browser address bar makes GET requests; entering a URL does not send a POST or PATCH request.

Test successful and invalid requests. A response with 400 and a validation message is expected when deliberately sending bad data. A syntax check cannot detect every runtime problem, such as using an undeclared variable or calling `.find()` on the wrong value.

## Connecting React to an API

### Development proxy and two running servers

```javascript
// Add inside the existing Vite configuration object.
server: {
  proxy: {
    '/entries': 'http://localhost:3000',
  },
}
```

The snippet is an object-property example, not a complete standalone file. Vite forwards matching local development requests to Express. Keep both servers running: the frontend handles the interface and the backend answers API requests.

Open the frontend root URL, usually `http://localhost:5173/`, to run React. Opening `http://localhost:5173/entries` instead shows the proxied JSON response. React's effects and logs will not run on that JSON page.

### GET, POST, PATCH, and DELETE from the browser

```javascript
const response = await fetch('/entries');
if (!response.ok) throw new Error('Could not load entries');
const entries = await response.json();
```

Use this inside an async function or module context. Fetch a JSON list, validate its shape, then place it in state with `setEntries(entries)`. The setter requests a render; it does not synchronously change the state variable in the already-running function.

```javascript
const response = await fetch('/entries', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ title }),
});
```

POST sends the title to the server. Read the server's successful response and use its ID and other fields rather than creating another client-side ID for the same record.

For PATCH, request `/entries/${id}` and send the field being changed, for example `{ completed: true }`. For DELETE, send the method without a JSON body when the route does not require one. Do not parse the empty body of a 204 response.

Update the visible list only after the operation succeeds. This keeps the screen consistent when a request fails. Read the updated object returned by PATCH instead of guessing what the server accepted.

### Loading, errors, and request cleanup

```jsx
const [isLoading, setIsLoading] = useState(true);
const [error, setError] = useState('');

// In returned JSX:
{
  isLoading && <p role="status">Loading entries...</p>;
}
{
  error && <p role="alert">{error}</p>;
}
{
  !isLoading && !error && visibleEntries.length === 0 && (
    <p>No entries to show</p>
  );
}
```

The empty message should not compete with loading or error feedback. A request should use try/catch/finally: try the request, catch the failure, and stop the loading state in finally. Put fetch itself inside try, not just the code after it. Clear an old error when starting a new attempt.

An AbortController can cancel a request when the component unmounts. Ignore results from aborted requests so they cannot overwrite newer state. React StrictMode intentionally performs an extra effect setup/cleanup cycle in development; duplicate startup requests are a cue to write correct cleanup, not to remove StrictMode.

### Updating state after await

```jsx
setEntries((currentEntries) => [...currentEntries, newEntry]);
setEntries((currentEntries) =>
  currentEntries.filter((entry) => entry.id !== id),
);
```

An async function retains the state from the render in which it started. Other actions can complete while it waits. A functional setter receives the current state when React processes the update, reducing the risk of overwriting another change.

Disable relevant controls while saving so double-clicks and repeated Enter presses do not send duplicate writes. A ref can hold an immediate in-flight flag between renders; changing a ref does not itself redraw the interface. Use state as well when the interface needs to show that saving is in progress.

### Testing the API connection

Mock fetch responses when testing React so the suite can run without a live backend. Include delayed responses, HTTP failures, rejected network requests, malformed JSON/data, empty lists, duplicate submissions, and empty 204 bodies.

Backend tests should exercise route validation and middleware separately. In-process request streams can check Express behavior without opening a TCP socket. Passing those tests does not prove CORS, HTTPS, DNS, live hosting, or actual browser requests work; check those after deployment.

### Hosting frontend and backend separately

A Vite development proxy is not a deployed server. A hosted static frontend needs a real backend URL or a hosting-platform proxy. A variable such as `VITE_API_URL` is embedded in the public client bundle, so it must never hold a private credential.

An Express host may supply its port through process.env.PORT and require binding to 0.0.0.0. Supply a start script, a health route, and the allowed frontend origins. Configure those origins deliberately. CORS is a browser rule, not login or authorization: non-browser clients can still call a public API.

A free host may sleep and restart. Temporary memory then disappears, and the first request can be slow. A shared demo should explain that behavior. Database persistence and accounts are separate later features, not properties that appear automatically when an API goes online.

## React refs and dependent selections

State holds information used to render the interface. A ref can hold a reference to a DOM element without causing a render when its value changes.

```jsx
import { useEffect, useRef } from 'react';

function DetailsSection({ selectedTime }) {
  const detailsRef = useRef(null);

  useEffect(() => {
    if (!selectedTime) return;

    detailsRef.current?.scrollIntoView({
      behavior: window.matchMedia('(prefers-reduced-motion: reduce)').matches
        ? 'auto'
        : 'smooth',
      block: 'start',
    });
  }, [selectedTime]);

  return selectedTime ? (
    <section ref={detailsRef}>
      <h2>Your details</h2>
    </section>
  ) : null;
}
```

React assigns the element to `detailsRef.current` when it commits the rendered element. The effect then scrolls to it. Calling the scroll immediately after setting state may run before the new element exists. Scrolling does not move keyboard focus; consider focus separately when a workflow needs it.

Selections can depend on earlier choices: service → date → time → contact details. When the service or date changes, clear the selected time and fetch the matching availability. Display loading, error, and empty states. Ignore stale responses using effect cleanup, or cancel them with an `AbortController`, so an older request cannot replace newer results.

During submission, use a pending state, disable repeated submission, and show the server's result. The server must still validate the request: a disabled button is only a browser convenience.

Reference: [React: useRef](https://react.dev/reference/react/useRef).

## Tailwind CSS and theme tokens

Tailwind uses utility classes to apply CSS in markup. The browser still receives ordinary CSS; Flexbox, Grid, spacing, and responsive design still work by the same rules.

| Class                     | Meaning                                             |
| ------------------------- | --------------------------------------------------- |
| `flex items-center`       | Flex layout with cross-axis alignment               |
| `grid grid-cols-2 gap-3`  | Two grid columns with a gap                         |
| `p-4`                     | Padding on every side                               |
| `px-4 py-2`               | Horizontal and vertical padding                     |
| `mt-6`                    | Margin at the top                                   |
| `w-full`                  | Full available width                                |
| `md:grid-cols-3`          | Three columns from the configured medium breakpoint |
| `hover:bg-primary`        | Background utility applied during hover             |
| `focus-visible:outline-2` | Outline width applied during visible keyboard focus |

Numbers such as `4` use the theme's spacing scale; they do not mean four pixels. A visible focus indicator also needs an appropriate outline style, color, and contrast.

Theme tokens describe a color's purpose, such as `background`, `foreground`, `primary`, or `muted`. This makes a palette easier to update consistently. Component libraries may pair background and foreground tokens to describe text on that background.

```css
@import 'tailwindcss';

:root {
  --brand: #b7aaa0;
}

@theme inline {
  --color-primary: var(--brand);
}
```

This Tailwind CSS v4 example makes `bg-primary` and `text-primary` available. It defines a color; it does not prove that every use has sufficient contrast.

A component generator such as shadcn adds component source files to your project. Read and adapt the components you use. An accessible foundation still needs meaningful labels, visible focus, and sensible application behavior.

References: [Tailwind utilities](https://tailwindcss.com/docs/styling-with-utility-classes), [theme variables](https://tailwindcss.com/docs/theme).

## Organizing backend code

Split code when responsibilities become difficult to follow. A small feature does not need a new file for every line.

| Location       | Responsibility                                       |
| -------------- | ---------------------------------------------------- |
| `app.js`       | Express middleware and route registration            |
| `server.js`    | Starting the process, listening, and shutdown        |
| `routes/`      | Connecting a URL and HTTP method to a handler        |
| `controllers/` | Reading the request and sending the response         |
| `validators/`  | Checking the shape and meaning of input              |
| `models/`      | Reading and writing database data                    |
| `services/`    | Application rules, such as availability calculations |
| `utils/`       | Small reusable helpers                               |
| `db/`          | Connection pool, migrations, and database scripts    |

A typical request travels through route → controller → validation and application rules → database query → response. These names are conventions; understand each file's job rather than memorizing one directory tree.

### Validate and normalize on the server

`trim()` removes surrounding whitespace from strings. Check the value's type before calling string methods. Use normalization deliberately: a name can be trimmed, but a password should not silently change.

Validate IDs against real records. Read the price and duration from the database instead of trusting values sent by the browser. A booking can store a snapshot of those values so later price changes do not alter the original agreement.

For international phone numbers, use a maintained phone parsing library with the appropriate default country. Simple length checks cannot cover all numbering plans. A number that passes format validation has not been proven to belong to the customer; that requires verification, such as a code sent to the number.

Use `400` for invalid input, `404` for a missing resource, `409` for a booking conflict, and `503` for temporary maintenance when appropriate. Return useful public messages without database credentials or internal stack traces.

## PostgreSQL and SQL

A relational database stores rows in tables. Relationships connect rows through keys.

| SQL feature                | Purpose                                                |
| -------------------------- | ------------------------------------------------------ |
| `PRIMARY KEY`              | Identifies a row uniquely and cannot be null           |
| `REFERENCES`               | Requires a related row to exist                        |
| `NOT NULL`                 | Requires a value; does not reject an empty string      |
| `CHECK`                    | Enforces a condition, such as a positive duration      |
| `integer`                  | Whole numbers, useful for minutes and money in cents   |
| `uuid`                     | An identifier type; a UUID is not an access permission |
| `date`                     | A calendar date                                        |
| `time without time zone`   | A time of day without a date or zone                   |
| `timestamp with time zone` | An instant, suitable for creation times                |

```sql
CREATE TABLE services (
  id text PRIMARY KEY,
  name text NOT NULL,
  duration_minutes integer NOT NULL CHECK (duration_minutes > 0),
  price_cents integer NOT NULL CHECK (price_cents >= 0)
);

INSERT INTO services (id, name, duration_minutes, price_cents)
VALUES ('consultation', 'Consultation', 30, 2500);

SELECT id, name, duration_minutes, price_cents
FROM services
ORDER BY name;
```

`2500` represents 25.00 in a currency with 100 cents per unit. Format the value for display at the interface boundary.

### Parameterized queries in Node.js

```javascript
import pg from 'pg';

const pool = new pg.Pool({
  connectionString: process.env.DATABASE_URL,
});

async function findServiceById(id) {
  const result = await pool.query(
    `SELECT id, name, duration_minutes, price_cents
     FROM services
     WHERE id = $1`,
    [id],
  );

  return result.rows[0] ?? null;
}
```

This assumes an ES module project with `pg` installed and a database URL supplied to the process. Create one shared pool per application process rather than a pool for each request.

`$1` receives the first value from `[id]`. Keep user input in the values array instead of interpolating it into SQL. Parameters represent values; they cannot replace table or column names. Parameterization prevents SQL injection through those values, while validation and authorization remain separate responsibilities.

`result.rows` is an array. `rows[0]` reads its first row; `?? null` provides an explicit missing result. `INSERT ... RETURNING id` can return the identifier generated by the database.

### Inspecting data with psql

Inside `psql`, `\dt` lists tables, `\d services` describes a table, `\x` toggles expanded output, and `\q` exits. If output opens in a pager, press `q` to leave the pager. `-P pager=off` disables it for a command.

```sql
SELECT service_id, appointment_date::text AS booking_date
FROM bookings
ORDER BY created_at DESC
LIMIT 1;
```

Use column names and expanded output when terminal columns wrap. `::text` converts the date to text for inspection; `AS booking_date` changes the result label, not the stored column.

References: [PostgreSQL constraints](https://www.postgresql.org/docs/current/ddl-constraints.html), [node-postgres queries](https://node-postgres.com/features/queries).

## Database connections, migrations, and seeds

### Local PostgreSQL with Docker

Docker Compose can run PostgreSQL in a container while Node.js runs on your computer. The host and container ports can differ:

```yaml
ports:
  - '127.0.0.1:5433:5432'
```

Node.js on the host connects to `localhost:5433`. PostgreSQL inside the container listens on `5432`. Another container on the same Compose network normally uses the database service name and container port. Connecting to the wrong local PostgreSQL instance can cause a misleading “role does not exist” error.

```bash
docker compose up -d database
docker compose ps -a
docker compose logs database
docker compose exec database pg_isready -U app_user -d app_database
```

These examples assume the Compose service is named `database`; use the actual service, user, and database names. A container with status `Created` has not successfully started. `pg_isready` checks server readiness; an application query is still needed to confirm its credentials and permissions.

A volume preserves database files across container replacement. Follow the image's instructions for the volume mount path, which can differ between PostgreSQL versions. Changing initialization environment variables does not rename users in an existing database volume. Do not delete the volume as a routine connection fix.

### Environment variables

Store local credentials in an ignored `.env` file and commit an `.env.example` containing placeholders. Never place a database password in a public `VITE_` variable, README, screenshot, or Git commit.

```bash
node --env-file=../.env src/db/checkConnection.js
```

The environment-file path is relative to the terminal's current directory. This example assumes the script exists and uses a Node.js version supporting `--env-file`. A successful `SELECT 1 AS connected` confirms that this process can execute a query; it does not prove migrations or application permissions are correct.

### Migrations and seeds have different jobs

A migration changes the schema: tables, columns, indexes, or constraints. A seed supplies initial reference data, such as services. Customer bookings are application data, not disposable seed data.

Keep ordered migration files in Git, for example `001_create_services.sql` and `002_create_bookings.sql`. A runner records applied filenames in a migration table and uses transactions where supported. Do not edit an already applied migration to make a new change; add another migration.

An idempotent seed can use `ON CONFLICT (id) DO NOTHING` to skip existing IDs. This does not update an existing price, and repeated execution must not erase customer records.

For multiple queries in one transaction, check out a client with `pool.connect()` and use that same client for `BEGIN`, the queries, and `COMMIT` or `ROLLBACK`. Release it in `finally`. Separate calls to `pool.query()` may use different connections and cannot be assumed to share a transaction.

Reference: [node-postgres transactions](https://node-postgres.com/features/transactions).

## Dates, times, and availability

### Calendar dates and instants are different

An appointment date such as `2030-06-12` is a calendar date. A creation timestamp represents an instant. In an ISO timestamp, `Z` means UTC, not the user's local timezone.

Parsing means turning a representation into a value that code can work with. Parsing is not the same as validating: JavaScript can normalize an impossible day into the next month. For a strict date, check `YYYY-MM-DD`, parse in a deliberate timezone, and compare the resulting year, month, and day with the input.

Compute “today” in the business's timezone, such as `Europe/Amsterdam`. `toISOString().slice(0, 10)` uses UTC and can disagree with the local date around midnight. Keep a local appointment date as a date value rather than converting it unnecessarily to an instant.

### Convert time to minutes for comparisons

```javascript
function timeToMinutes(time) {
  const [hours, minutes] = time.split(':').map(Number);
  return hours * 60 + minutes;
}

function minutesToTime(totalMinutes) {
  const hours = Math.floor(totalMinutes / 60);
  const minutes = totalMinutes % 60;
  return `${String(hours).padStart(2, '0')}:${String(minutes).padStart(2, '0')}`;
}
```

These helpers assume validated same-day times and minute values within that day. Validate incoming `HH:mm` values before using them. An appointment at 10:00 lasting 30 minutes occupies minutes 600 through 630.

Generate candidate starts with an interval such as 15 minutes. Keep a start only when its end is no later than closing time. Compare bookings for the relevant date and resource, such as the selected staff member.

```javascript
function overlaps(start, end, existingStart, existingEnd) {
  return start < existingEnd && end > existingStart;
}

const appointments = [{ start: 600, end: 630 }];
const candidateStarts = [600, 615, 630, 645];
const duration = 30;

const availableStarts = candidateStarts.filter(
  (start) =>
    !appointments.some((appointment) =>
      overlaps(start, start + duration, appointment.start, appointment.end),
    ),
);
// [630, 645]
```

`some()` asks whether at least one booking conflicts. `!` changes that into “no booking conflicts.” `filter()` keeps those starts. Strict `<` and `>` allow a new booking to begin exactly when another ends.

Opening hours, closed days, staff schedules, breaks, and elapsed times today are separate rules. A basic overlap filter does not implement them automatically.

### Prevent overlapping writes in the database

Two customers can submit the same available time together. Both requests can pass a JavaScript availability check before either has inserted a booking. The database needs a rule that also rejects conflicting concurrent writes.

PostgreSQL range types can describe `[start, end)` intervals: include the start, exclude the end. An exclusion constraint using the overlap operator `&&` can reject intersecting ranges. Scope the rule by staff member or resource when multiple simultaneous appointments are allowed. A global constraint would otherwise restrict the entire business to one appointment at a time.

An exclusion violation has PostgreSQL code `23P01`. Check the expected constraint and return a `409 Conflict`, then let the interface refresh availability. Do not silently book another time.

Reference: [PostgreSQL range types and exclusion constraints](https://www.postgresql.org/docs/current/rangetypes.html).

## Hosting and moving a database

### The application server and database can have different hosts

Render can run an Express process while Neon provides PostgreSQL. The server connects using a private environment variable such as `DATABASE_URL`. The browser calls the API and must never receive that database credential.

A single Express deployment can also serve the built Vite frontend. In development, Vite proxies `/api` to Express; in production, Express can serve `dist/` and API routes from the same origin. Register API routes before a frontend fallback so missing API URLs return JSON errors instead of HTML.

Use the host's `PORT` and required network binding. Add a health endpoint, inspect startup logs, and verify the application after deployment. A successful GitHub push alone does not prove that the new version is live.

Providers may offer pooled and direct PostgreSQL URLs. Choose according to the driver, migration tool, and workload; migration tools can need direct or session-compatible connections. Preserve the provider's TLS verification settings. Do not work around certificate errors by disabling verification.

### Move data without losing it

A schema migration and a database transfer are different operations. A transfer moves existing rows to another database.

- Prepare the destination schema and test the transfer procedure on a separate database or branch.
- Pause writes before the final copy, or use a migration method that explicitly handles continuing writes.
- Copy related records in an order that respects foreign keys, preserving IDs and timestamps.
- Verify actual field values as well as row counts. Equal counts can still hide different data.
- Use transactions, rollback on failure, and a completion record so an accidental repeat cannot duplicate the transfer.
- Switch the application's connection setting, redeploy, test reads and writes, and resume service.
- Retain a usable backup or old database until the migration is verified. Track expiration dates for temporary databases.

Timestamp comparisons need care: JavaScript `Date` uses millisecond precision, while PostgreSQL can store microseconds. A transfer that must preserve exact timestamps should avoid losing precision through a JavaScript conversion.

Free hosting can suspend idle compute or impose usage limits. Database compute hours are not always wall-clock hours: `0.25 compute units × 4 active hours = 1 CU-hour`. Check current provider documentation rather than assuming a fixed free allowance forever.

## SEO and search engine discovery

SEO helps search engines discover and understand a website. It cannot guarantee indexing, a ranking, or a particular search-result appearance.

### Page information

Use a descriptive title, a useful meta description, meaningful visible text, and logical headings. Keep important page content available in HTML when possible. Write image alternatives for the image's purpose and set dimensions to reduce layout movement.

```html
<title>Alex Morgan | Web Developer</title>
<meta
  name="description"
  content="Explore Alex Morgan's web development projects and experience."
/>
<link rel="canonical" href="https://example.com/" />
```

A canonical link identifies the preferred URL when the same content is available at different addresses. Search engines can still choose another canonical. Open Graph metadata supplies information for shared-link previews; it is not a promise of a higher ranking. JSON-LD can describe public facts about a person or website and should match the visible content.

### robots.txt and sitemap.xml

`robots.txt`, with an **s**, belongs at the website root. It gives crawlers instructions and can point to a sitemap:

```text
User-agent: *
Allow: /

Sitemap: https://example.com/sitemap.xml
```

This permits crawling. A missing `robots.txt` does not automatically block crawling. Blocking crawling is different from requesting that a page stay out of search results; use the appropriate indexing controls for the latter.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://example.com/</loc>
  </url>
</urlset>
```

List canonical pages in a sitemap. Sections such as `/#about` are anchors within the homepage, not additional pages. In a plain HTML site served from the repository root, put these files beside `index.html`. In Vite, files placed in `public/` are copied to the build root. Check the deployed URLs rather than assuming every project uses the same public path.

### Google Search Console

Verify ownership of the correct property. Domain verification commonly uses a TXT record at the DNS provider; retain the verification record afterward. Ownership verification does not index the website.

After the hosting deployment succeeds, open the deployed sitemap and robots file. Submit the sitemap in Search Console, inspect the homepage, and request indexing. If a sitemap cannot be read, inspect the detailed error and use a live URL test to check whether Google can fetch it. Do not assume that waiting will fix a missing file or server error.

Reports can take time to update. Repeatedly requesting indexing does not make crawling faster. A valid sitemap helps discovery but does not guarantee inclusion in search results.

References: [Google SEO starter guide](https://developers.google.com/search/docs/fundamentals/seo-starter-guide), [sitemap troubleshooting](https://support.google.com/webmasters/answer/7451001), [requesting indexing](https://developers.google.com/search/docs/crawling-indexing/ask-google-to-recrawl).

## Development tools and application stacks

| Tool or term | Role                                                                   |
| ------------ | ---------------------------------------------------------------------- |
| npm          | Installs project dependencies and runs package scripts                 |
| Vite         | Provides a development server and production build tooling             |
| React        | Builds the interface from components                                   |
| React Native | Uses React to build native applications                                |
| Next.js      | A React framework with routing, server features, and rendering options |
| Express      | A backend framework running on Node.js                                 |
| Node.js      | Runs JavaScript outside the browser, including on servers              |
| PostgreSQL   | A relational database queried with SQL                                 |
| MongoDB      | A document database                                                    |
| Tailwind CSS | Utility classes for styling                                            |
| Bootstrap    | Styling, components, and layout tools                                  |

Common Vite project commands:

```bash
npm install
npm run dev
npm run build
npm run preview
```

`dev` starts the development server. `build` creates production output, normally in `dist/`. `preview` serves that built output locally for checking; it is not the production hosting service. Keep the development-server terminal running while developing.

### Project files and generated output

| File or folder      | Responsibility                                                 |
| ------------------- | -------------------------------------------------------------- |
| `index.html`        | Vite's HTML entry point, in the project root rather than `src` |
| `src/`              | Application source code and styles                             |
| `public/`           | Files served directly, such as favicons                        |
| `package.json`      | Scripts and declared dependencies                              |
| `package-lock.json` | Resolved dependency versions; normally commit it               |
| `node_modules/`     | Installed packages; do not commit it                           |
| `dist/`             | Generated production output; do not edit it manually           |
| `vite.config.js`    | Build, plugin, and test configuration                          |

Starter logos, images, and CSS can be removed once nothing references them. Keep tooling and dependency files that the application still uses. A new build recreates `dist`; deleting it does not delete your source code.

### Markdown documentation

A useful README explains what the project does, its live URL, features, technologies, setup commands, tests, build/deployment steps, and relevant limitations. Learning projects can also describe what was practiced without claiming professional experience with every tool.

Use `#` for the project title, `##` for sections, `-` for list items, and fenced code blocks for commands. Keep blank lines around headings, lists, and code blocks. Describe real behavior; for example, browser storage is not a shared database.

### PERN and MERN

- **PERN:** PostgreSQL, Express, React, Node.js.
- **MERN:** MongoDB, Express, React, Node.js.

The database choice differs. Learning SQL and PostgreSQL does not invalidate earlier JavaScript work. Browser `localStorage` is useful for local practice; a database behind an API is the later step for shared, persistent server-side data.

### Practice roadmap

These are learning projects, not a list of technologies to master immediately:

| Stage                 | Practice project                                         | Main learning goal                                                          |
| --------------------- | -------------------------------------------------------- | --------------------------------------------------------------------------- |
| Foundation            | A task manager, first in plain JavaScript and then React | Understand data, events, components, and state                              |
| Full-stack practice   | A barber booking app                                     | Availability, appointments, relational data, and preventing double bookings |
| More independent work | A ride-booking app                                       | Maps, user roles, and real-time status; begin with simulated drivers        |

Express and PostgreSQL come after the initial React work. Payments, real GPS tracking, and more advanced infrastructure are later extensions. First build and understand a small reliable version.

## Learning habits

This document is a reference, not a reading assignment. Look up one topic when you need it.

- Try a small problem yourself before asking for a complete answer.
- Ask for a hint or explanation, then explain the code in your own words.
- Rebuild a small example later without copying it.
- Keep practice exercises separate from the active application.
- Treat AI-generated code as code to understand, review, and test.
- Use short sessions and breaks when concentration drops.

Understanding one small example is more useful than rushing through several new tools.

## Git and publishing basics

| Term or command                       | Purpose                                                  |
| ------------------------------------- | -------------------------------------------------------- |
| Repository                            | A project and its version history                        |
| Commit                                | A recorded snapshot of staged changes                    |
| Remote                                | A named connection to another repository                 |
| Branch                                | A line of development                                    |
| `git status`                          | Show working tree and staging status                     |
| `git diff`                            | Review unstaged tracked-file changes                     |
| `git add file.html styles.css`        | Stage selected changes                                   |
| `git commit -m "Describe the change"` | Save a commit locally                                    |
| `git push`                            | Send local commits to the configured remote branch       |
| `.gitignore`                          | Patterns for files that should normally remain untracked |

Saving a file, committing it, pushing it, and deploying it are separate steps. A commit does not upload itself.

A hosting service connected to a Git repository can deploy automatically after a push to the configured production branch. Check deployment status instead of assuming a successful push means publication has finished.

A plain HTML/CSS site usually needs no build command. Its publish directory must contain the entry HTML file and referenced assets. DNS configuration is separate from deploying updated files.

For a typical Vite deployment, use `npm run build` as the build command and `dist` as the publish directory. Confirm that the connected repository and production branch are correct.

### Review, commit, and push

```bash
git status
git diff
git add README.md
git commit -m "Update documentation"
git push
```

Replace the staged filenames with the changes you intend to publish. Untracked files do not appear in ordinary `git diff`; inspect them too. A remote-tracking branch such as `origin/main` records the last known remote state, not a live connection to GitHub.

If a coding tool reports `Could not resolve host`, check whether the same command works in your own terminal. A sandbox can block all networking and produce a DNS-looking error even when the computer's connection works. Check permissions and connection evidence before editing system DNS settings. Report a failed push honestly instead of assuming the site has been updated.

## Reusable learning workflow

1. Identify the HTML element and its parents.
2. Find every selector that matches it.
3. Check inherited styles and active media queries.
4. Identify the exact property responsible for the behavior.
5. Make one focused change.
6. Test mouse, keyboard, and different viewport sizes.
7. Review the diff before committing and publishing.

## Adding new learning notes

Use this template when extending the document:

```markdown
## Topic name

### Purpose

What problem does this solve?

### Example

Add a small working HTML, CSS, or JavaScript example.

### How the parts work together

Describe matching selectors, parent/child relationships, and dependencies.

### Common mistakes

Record the symptom, cause, and fix.

### Practice

Describe a small exercise to try independently.
```
