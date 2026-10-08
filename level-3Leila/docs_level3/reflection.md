# Reflection
Level 3: Complex Layout

## 1. Overview

This webpage has a header, a navigation menu, a left sidebar, a main content area, a right sidebar and a footer. The same HTML is styled twice, once with nested Flexbox containers and the second instance with CSS Grid. A switcher at the top of the page loads either stylesheet, which makes it easy to compare the two on identical content. The font and colors are in a shared css file, to avoid redundancy.

On desktop and iPad landscape, the sidebars take 20% of the width each and the main content takes 60%. On iPad portrait, the main content moves to the top and the sidebars share the row below. On phones, everything stacks in a single column.

## 2. How each technique solved the layout

Flexbox contains two nested containers. The outer one stacks the header, navigation, content and footer, and the inner one places the three columns in a row. The tablet layout was the hardest implementation. The inner container has to wrap, the main content has to take the full width, and the order property has to place the sidebars after it.

In grid, every element is given a name, and each breakpoint redraws the page in a single template. Moving the sidebars below the main content was a matter of editing that template. 

## 3. How the flexbox and grid implementations compare

At a 1440px viewport, the sidebars measured 288px and the main content 864px in both versions. Although similar, Flexbox sets the widths on the elements, while Grid declares them once on the container:

```css
.sidebar { flex: 0 0 20%; }
.main    { flex: 0 0 60%; }
```

```css
grid-template-columns: 20% 60% 20%;
```

The tablet layout shows the difference most clearly. In Flexbox, three properties work together:

```css
.content { flex-wrap: wrap; }
.main    { flex: 0 0 100%; order: 1; }
.sidebar { flex: 1; order: 2; }
```

In Grid, the arrangement is redrawn in the template:

```css
grid-template-areas:
  "header header"
  "nav    nav"
  "main   main"
  "left   right"
  "footer footer";
```

Both versions use mobile-first media queries at 768px and 1024px. The display was checked at phone, iPad and large desktop sizes with no horizontal overflow. The footer stays at the bottom when the content is short, because the body is a flex column and the page container grows to fill it. The page is also limited to 1440px and centered, which keeps the content well spread on large screens:

```css
.page { flex: 1; max-width: 1440px; margin-inline: auto; }
```

The HTML relies on semantic elements such as header, nav, main, aside and footer, with labels. The only extra wrapper is the content container that Flexbox needs for its nested row. To let one HTML file serve both layouts, the Grid stylesheet was set for the wrapper to display: contents, so its children sit directly in the grid:

```css
.content { display: contents; }
```

One accessibility point applies to both techniques. On tablet, the sidebars appear after the main content visually, but the left sidebar still comes first in the HTML. Keyboard and screen reader users would then move through the page in a different order from what sighted users see.

## 4. Trade-offs and when to use each

Flexbox works in one dimension and suits content that decides its own size, such as navigation bars, rows of cards and centered items. Grid works in two dimensions and suits full page layouts with distinct regions.

For this page, Grid was the better choice for the overall structure, since the responsive changes are rearrangements of regions. Flexbox remained the right tool inside it. Both versions use it for the navigation links, which sit in one row and wrap when space runs out.

## 5. Lessons learnt from practicing flaxbox and grid

Grid and Flexbox complement each other. Grid suits the page structure, and Flexbox suits content within it.
Named grid areas are easier to read and change than a combination of flex and order rules.
Reordering with either grid or flexbox changes the visual order but not the source order, so accessibility needs attention.
Mobile first CSS keeps the code short, since each breakpoint only adds what changes.
Shared styles in one file make the differences between the two layouts easier to see and also makes the work organized.
Fluid sizing and a maximum page width cover a wide range of screens better than extra breakpoints.

