# Web Development Learning Notes

A growing reference for HTML, CSS, JavaScript, React, accessibility, and publishing websites. The examples are general patterns that can be reused in different projects.

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
- [Saving data locally](#json-and-localstorage)
- [React components, props, and state](#react-components-and-jsx)
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
  background-image: url("photo.jpg");
  background-color: navy;
}
```

The image remains. Color is painted behind it and will not show through fully opaque parts.

By contrast, the `background` shorthand resets background properties that you do not specify:

```css
.banner {
  background-image: url("photo.jpg");
  background: navy; /* Also resets background-image to none. */
}
```

You can specify several settings at once:

```css
.banner {
  background: navy url("photo.jpg") center / cover no-repeat;
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
  content: "";
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
  content: "";
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
  title: "Learn JavaScript",
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
const title = "Learn React";
let count = 0;
count++;
```

`const` does not make objects or arrays immutable:

```javascript
const titles = ["Learn JavaScript"];
titles.push("Learn React"); // Allowed: changes the array's contents.
// titles = [];           // Not allowed: reassigns the variable.
```

`const` helps prevent accidental reassignment; it is not a security feature. Always declare variables rather than relying on accidental globals.

### Converting strings to numbers

```javascript
Number("43.8"); // 43.8
Number("43px"); // NaN
parseInt("43px", 10); // 43
parseInt("43.8", 10); // 43, not 44
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
  { id: 1, title: "Read a chapter", completed: false },
  { id: 2, title: "Write notes", completed: true },
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

For numeric ascending order, use `(a, b) => a.price - b.price`. Reverse the subtraction for descending order.

## Spread syntax and immutable updates

Spread syntax `...` copies array elements or object properties into a new container.

```javascript
const numbers = [1, 2, 3];
const extended = [...numbers, 4];
// numbers: [1, 2, 3]; extended: [1, 2, 3, 4]
```

```javascript
const original = { id: 1, title: "Learn", completed: false };
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
const listElement = document.querySelector("#item-list");
const itemElement = document.createElement("li");
itemElement.textContent = "Read a chapter";
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
button.addEventListener("click", () => {
  console.log("Clicked");
});
```

The callback is the **event handler**: code that runs when the event occurs. It does not need a separate function name.

- `click`: activating a button.
- `change`: changing a checkbox's value.
- `submit`: submitting a form, including through Enter.

```javascript
form.addEventListener("submit", (event) => {
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

## JSON and localStorage

```javascript
localStorage.setItem("items", JSON.stringify(items));
```

`localStorage` stores strings. `JSON.stringify()` converts serializable data into JSON text.

```javascript
const savedItems = localStorage.getItem("items");
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
      {props.completed ? " — Done" : " — To do"}
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
import { useState } from "react";

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
