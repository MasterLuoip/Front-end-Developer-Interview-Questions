---
title: CSS Questions
layout: layouts/page.njk
permalink: /questions/css-questions/index.html
---

- What is CSS selector specificity and how does it work?

  ***

  If there are two or more conflicting CSS rules that point to the same element, the browser follows some rules to determine which one is most specific and therefore wins out.

  Think of specificity as a score/rank that determines which style declarations are ultimately applied to an element.

  The universal selector (\*) has low specificity, while ID selectors are highly specific!

  !important > inline > id > classes, attributes, pseudo-classes > elements, pseudo-elements

  ***

- What's the difference between "resetting" and "normalizing" CSS? Which would you choose, and why?

  ***

  Resetting: Every css elements should have the same/inital styles.
  Normalizing: Every css elements can have their own styles.

  differences:

  1. Normalize.css preserves useful defaults rather than "unstyling" everything.
  2. Normalize.css corrects some common bugs that are out of scope for reset.css.
  3. Normalize.css doesn't clutter your dev tools. A common irritation when using reset.css is the large inheritance chain that is displayed in browser CSS debugging tools.
  4. Normalize.css is more modular.
  5. Normalize.css has better documentation.

  ***

- Describe Floats and how they work.

  ***

  The float Property
  The float property is used for positioning and formatting content e.g. let an image float left to the text in a container.

  The float property can have one of the following values:

  left - The element floats to the left of its container
  right - The element floats to the right of its container
  none - The element does not float (will be displayed just where it occurs in the text). This is default
  inherit - The element inherits the float value of its parent
  In its simplest use, the float property can be used to wrap text around images.

  If a parent element contains nothing but floated elements, its height will be collapsed to nothing. It can be fixed by clearing the float after the floated elements in the container but before the close of the container.

  ***

- Describe z-index and how stacking context is formed.

  ***

  Needs relative,absolute,fixed

  The z-index property in CSS controls the vertical stacking order of elements that overlap. z-index only effects elements that have a position value which is not static.
  Without any z-index value, elements stack in the order that they appear in the DOM (the lowest one down at the same hierarchy level appears on top). Elements with non-static positioning (and their children) will always appear on top of elements with default static positioning, regardless of HTML hierarchy.

  A stacking context is an element that contains a set of layers. Within a local stacking context, the z-index values of its children are set relative to that element rather than to the document root. Layers outside of that context — i.e. sibling elements of a local stacking context — can't sit between layers within it. If an element B sits on top of element A, a child element of element A, element C, can never be higher than element B even if element C has a higher z-index than element B.

  ***

- Describe BFC (Block Formatting Context) and how it works.

  ***

  A block formatting context is a part of a visual CSS rendering of a web page. It's the region in which the layout of block boxes occurs and in which floats interact with other elements.

  It solves the problem like float element intercate with sibling element. Parent element would not show.

  Side effect: margin collasping.

  ***

- What are the various clearing techniques and which is appropriate for what context?

  ***

  clearing css float:

  1. The floating container method.

     Perhaps, the easiest way to clear floats is to float the container element itself. But unfortunately this method only works in a limited number of circumstances, as floating the parent element may have undesirable effects on the layout.

  2. The overflow method. `overflow: hidden`

     it will automatically adjust its height and take the floated children into account. It has some styled issue.

  3. The empty div method.

     ```css
     div.clear-float { clear:both; font-size:0; height:0; }
     <div class="clear-float"></div>
     ```

     Drawback: will slow SEO

  4. The pseudo element method.

     use the CSS3 pseudo-class ":after" to generate on-the-fly content after the containing element and use it to clear floats. An important thing to do with this approach is to hide the generated content so it doesn't use up any screen space. However, this being a CSS3 feature, the obvious drawback is that this is not supported by older browsers.

  ***

- How would you approach fixing browser-specific styling issues?

  ***

  1. Identify issue browser, create a separate css sheet for it when it is used. This technique requires server-side rendering.

  2. Use style library like boostrate that already handles these issues for you.

  3. Use autoprefixer to automatically add vendor prefixes to your code.

  4. Use Reset CSS or Normalize.css

  ***

- How do you serve your pages for feature-constrained browsers?

  - What techniques/processes do you use?

    ***

    **Graceful Degradation**: Graceful degradation is a design philosophy that centers around trying to build a modern web site/application that will work in the newest browsers, but falls back to an experience that while not as good still delivers essential content and functionality in older browsers.(like polly fill in javascript)

    **Progressive enhancement** — The practice of building an application for a base level of user experience, but adding functional enhancements when a browser supports it.

    **Autoprefixer for automatic vendor prefix insertion.**

    ***

- What are the different ways to visually hide content (and make it available only for screen readers)?

  ***

  **visibility**: hidden. However the element is still in the flow of the page, and still takes up space.

  **width: 0; height: 0**: Make the element not take up any space on the screen at all, resulting in not showing it.

  **position**; absolute; left: -99999px. Position it outside of the screen. (This has least caveat)

  ***

- Have you ever used a grid system, and if so, what do you prefer?

  ***

  Vuetify and Material UI, I had been working before have grid system.

  The CSS Grid Layout Module offers a grid-based layout system, with rows and columns, making it easier to design web pages without having to use floats and positioning.

  ***

- Have you used or implemented media queries or mobile specific layouts/CSS?
  ***
  Yes, Different element layout in different size of screen.
  ***
- Are you familiar with styling SVG?
  ***
  Elements in an SVG document can be styled using CSS. Most visual characteristics and some aspects of element geometry are controlled using CSS properties. For example, the fill property controls the paint used to fill the inside of a shape, and the width and height properties are used to control the size of a ‘rect’ element.
  ***
- Can you give an example of an `@media` property other than `screen`?

  ***

  all Default. Used for all media type devices

  print Used for printers (different color of print and display)

  screen Used for computer screens, tablets, smart-phones etc.

  speech Used for screenreaders that "reads" the page out loud

  ***

- What are some of the "gotchas" for writing efficient CSS?

  ***

  1. Vertical centering is hard: you can use flex box now, but not **vertical-align property**!. You may be wondering what the vertical-align property does. The answer is “jack squat, except on an HTML table.” Never heard of HTML tables? That’s because they’re not cool. If you use them you can expect to be ostracized from the development community forever. Why? Because, much like the Spice Girls, they were way too popular in the 90’s and everyone got sick of them.

  2. 100% of width has too many conditions. First of all, this doesn’t work for inline elements (like <span> and <i>) and certain table elements. Second of all, it doesn’t work if its parent’s width isn’t explicitly specified — so good luck making it work inside an element that’s all funky-dory with flexbox. And lastly, margin properties are applied on top of the calculated width, so if your element has a margin on the left side, it’s gonna jut out like Aunt Marge’s pregnant belly.

  from: https://medium.com/@isaaclyman/8-css-gotchas-to-start-your-morning-off-right-c5daade0731d

  ***

- What are the advantages/disadvantages of using CSS preprocessors?

  ***

  Advantages:

  1. css is made more maintainable
  2. Easy to write nested selectors
  3. Variable, functions and can be shared across different files
  4. Mixins to generate repeated CSS.
  5. Splite code into different files (requires a HTTP request to download each CSS file)

  Disadvantages:

  1. Requires tools for preprocessing. Re-compilation time can be slow.

  2. In Less, variable names are prefixed with @, which can be confused with native CSS keywords like @media, @import and @font-face rule.

  3. Debugger can be very hard.

  ***

  - Describe what you like and dislike about the CSS preprocessors you have used.
    ***
    Same as above.
    ***

- How would you implement a web design comp that uses non-standard fonts?
  ***
  Use @font-face and define font-family for different font-weights.
  ***
- Explain how a browser determines what elements match a CSS selector.

  ***

  This part is related to the above about writing efficient CSS. Browsers match selectors from rightmost (key selector) to left. Browsers filter out elements in the DOM according to the key selector, and traverse up its parent elements to determine matches. The shorter the length of the selector chain, the faster the browser can determine if that element matches the selector.

  For example with this selector p span, browsers firstly find all the `<span>`elements, and traverse up its parent all the way up to the root to find the `<p>` element. For a particular `<span>`, as soon as it finds a `<p>`, it knows that the `<span>` matches and can stop its matching.

  ***

- Describe pseudo-elements and discuss what they are used for.

  ***

  A css pseudo-elemnts is a keyword added to the end of selector that lets you style a specific part of the selected elements. They can be used to for decoration (:first-line, :first-letter) or adding elements to markup (combined with content: ...) without having to modify the markup (:before, :after).

  - :first-line and :first-letter can be used to decorate text.

  - Used in the .clearfix hack as shown above to add a zero-space element with clear: both.

  - Triangular arrows in tooltips use :before and :after. Encourages separation of concerns because the triangle is considered part of styling and not really the DOM, but not really possible to draw a triangle with just CSS styles.

  ***

- Explain your understanding of the box model and how you would tell the browser in CSS to render your layout in different box models.

  ***

  All HTML elements can be considered as boxes.

  The CSS box model is essentially a box that wraps around every HTML element. It consists of: margins, borders, padding, and the actual content.

  Whether or not borders and/or margins overlap, or collapse.

  The box model has the following rules:

  1. The dimensions of a block element are calculated by width, height, padding, borders, and margins.
  2. If no height is specified, a block element will be as high as the content it contains, plus padding (unless there are floats, for which see below).
  3. If no width is specified, a non-floated block element will expand to fit the width of its parent minus padding.
  4. The height of an element is calculated by the content's height.
  5. The width of an element is calculated by the content's width.
     By default, paddings and borders are not part of the width and height of an element.

  ***

- What does `* { box-sizing: border-box; }` do? What are its advantages?

  ***

  `content-box` gives you the default CSS box-sizing behavior. If you set an element's width to 100 pixels, then the element's content box will be 100 pixels wide, and the width of any border or padding will be added to the final rendered width, making the element wider than 100px.

  `border-box` tells the browser to account for any border and padding (margin excluded) in the values you specify for an element's width and height. If you set an element's width to 100 pixels, that 100 pixels will include any border or padding you added, and the content box will shrink to absorb that extra width. This typically makes it much easier to size elements.

  Advantage:
  when you have mutiple box that you some have boards but other don't, and you want to have the same width.

  ***

- What is the CSS `display` property and can you give a few examples of its use?
  The display CSS property sets whether an element is treated as a block or inline element and the layout used for its children, such as flow layout, grid or flex.

  Formally, the display property sets an element's inner and outer display types. The outer type sets an element's participation in flow layout; the inner type sets the layout of children. Some values of display are fully defined in their own individual specifications; for example the detail of what happens when display: flex is declared is defined in the CSS Flexible Box Model specification. See the table at the end of this document for all of the individual specifications.

  ```css
  /* legacy values */
  display: block;
  display: inline;
  display: inline-block;
  display: flex;
  display: inline-flex;
  display: grid;
  display: inline-grid;
  display: flow-root;

  /* box generation */
  display: none;
  display: contents;

  /* two-value syntax */
  display: block flow;
  display: inline flow;
  display: inline flow-root;
  display: block flex;
  display: inline-flex;
  display: block grid;
  display: inline grid;
  display: block flow-root;

  /* other values */
  display: table;
  display: table-row; /* all table elements have an equivalent CSS display value */
  display: list-item;

  /* Global values */
  display: inherit;
  display: initial;
  display: unset;
  ```

- What's the difference between inline and inline-block?
  Displays an element as an inline element (like <span>). Any height and width properties will have no effect

  Displays an element as an inline-level block container. The element itself is formatted as an inline element, but you can apply height and width values

- What's the difference between the "nth-of-type()" and "nth-child()" selectors?
- What's the difference between a relative, fixed, absolute and statically positioned element?
- What existing CSS frameworks have you used locally, or in production? How would you change/improve them?
- Have you used CSS Grid?
- Can you explain the difference between coding a web site to be responsive versus using a mobile-first strategy?
- Have you ever worked with retina graphics? If so, when and what techniques did you use?
- Is there any reason you'd want to use `translate()` instead of _absolute positioning_, or vice-versa? And why?
- How is clearfix css property useful?
- Can you explain the difference between px, em and rem as they relate to font sizing?
- Can you give an example of a pseudo class? Can you provide an example use case for a pseudo class?
- What is the difference between a block level element and an inline element. Can you provide examples of each type of element?
