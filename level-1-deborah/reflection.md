# Level 1 Reflection: Basic Layout (Header, Main, Footer)

## What I built
A simple page with a header, a main area and a footer, built three ways with the same HTML:
Flexbox (`css/flexbox.css`), CSS Grid (`css/grid.css`) and plain CSS (`css/style1.css`).
The header and footer have fixed heights (80px and 60px), `main` fills the rest of the screen,
and the footer stays at the bottom even when there is little content.
On screens up to 768px wide, the header, footer and padding get smaller.

## My experience with Flexbox
- **How it worked:** I made the `body` a flex container with `display: flex` and
  `flex-direction: column` so the three sections stack top to bottom. Then I added
  `min-height: 100vh` so the page fills the screen, and `flex: 1` on `main` so it takes all the
  leftover space. That pushes the footer to the bottom.
- **What felt easy:** `flex: 1` is a short way to say "take the remaining space". I didn't
  have to calculate any heights.
- **What felt less obvious:** Flexbox only controls one direction. The header and footer heights
  are set on each element, and `main` grows through a different property. The layout is spread
  over several rules instead of being described in one place.
- **Mobile:** I only had to change `height` and `padding` in the media query. `main` kept filling
  the space on its own.

## Flexbox vs Grid vs plain CSS
| | Flexbox | Grid | Plain CSS |
|---|---|---|---|
| Key idea | `flex: 1` on `main` | `grid-template-rows: 80px 1fr 60px` | `min-height: calc(100vh - 140px)` |
| Code amount | Medium | Least | Medium |
| Mobile change | Edit 3 rules | Edit 1 line (plus padding) | Edit 3 rules and the `calc()` |
| Main drawback | Sizes are spread across rules | `grid-template-areas` is extra to learn | Heights must be updated by hand |

- **Less code:** Grid. One line sets all three row sizes, and the mobile version changes only that line.
- **More intuitive:** Grid for this layout, because it describes the whole page structure in one
  place. Flexbox felt natural too, but I had to think about the container and the items separately.
- **Plain CSS:** It works, but the `140px` and `100px` in `calc()` are copied from the header and
  footer heights. If those change and I forget the `calc()`, the layout breaks. Flexbox and Grid
  do this work automatically.

## Key takeaways
- Flexbox is great for laying things out in one direction, such as a column or a row.
- Grid is better when I want to define the structure of the whole page at once.
- Both give the same result here, but they get there with different ideas: Flexbox shares out
  space, Grid divides it into rows and columns.
- `box-sizing: border-box` made padding and fixed heights much easier to work with.
