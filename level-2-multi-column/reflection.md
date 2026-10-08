# Reflection: My Experience with Flexbox vs. Grid

For this assignment, I built the Level 2 layout which is a standard webpage with a header, a navigation bar, a main content area taking up 70% of the screen, a 30% sidebar, and a footer at the bottom. On mobile phones, everything stacks vertically. Building this exact same layout twice taught me a lot about how Flexbox and CSS Grid actually work in practice.

**Which was easier to implement?**
CSS Grid was definitely easier to implement for this big-picture page layout. With Grid, I could look at the whole page as a blank canvas and map out exactly where everything should go using `grid-template-areas`. I basically just told the CSS, "put the header on top, put the main content next to the sidebar, and put the footer at the bottom." 

With Flexbox, it was a bit trickier. Because Flexbox naturally only wants to flow in one direction at a time (either as a row or a column), I had to create an extra `.content` wrapper in the HTML just to hold the main area and the sidebar side-by-side, while keeping the rest of the page stacked as a column. 

**Which required less code?**
Grid ended up needing less code and felt a lot cleaner. To make the 70/30 layout split in Grid, I only had to write `grid-template-columns: 7fr 3fr` on the parent container, and the browser did all the math for me. For Flexbox, I had to be much more specific on the child elements, adding `flex-basis: 70%` and `max-width: 70%` to the main section to make sure it didn't accidentally stretch and break the layout.

**Which was more intuitive?**
Grid was way more intuitive for this specific task. Since a full webpage has both rows (like the header and footer) and columns (like the main content and sidebar), Grid is built exactly for that two-dimensional setup. Trying to build a full webpage layout with Flexbox felt like I was forcing a tool to do a job it wasn't really meant to do by relying heavily on `flex-wrap`.

**When would I prefer one over the other?**
Going forward, I will definitely use CSS Grid to build the main "skeleton" or macro-layout of a website. It's incredibly easy to use named areas to move big sections around for different screen sizes. However, I would still prefer Flexbox for the "micro-layouts" inside those big sections. For example, Flexbox is absolutely perfect for lining up the links inside a navigation bar or centering a button inside a card. Ultimately, the best approach seems to be using Grid for the main page structure, and Flexbox to organize the smaller items inside those grid areas.