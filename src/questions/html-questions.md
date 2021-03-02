---
title: HTML Questions
layout: layouts/page.njk
permalink: /questions/html-questions/index.html
---

- What does a `doctype` do?

  ***

  Doctype stands for Document Type Declaration. It informs the web browser about the type and version of HTML used in building the web document. This helps the browser to handle and load it properly.

  The `<!DOCTYPE html>` declaration must be placed in the beginning of every HTML document: it informs the browser about the document type.

  ***

- How do you serve a page with content in multiple languages?

  ***

  Use html attribute `lang` to set language.

  Always use a language attribute on the html tag to declare the default language of the text in the page. When the page contains content in another language, add a language attribute to an element surrounding that content.

  ***

- What kind of things must you be wary of when designing or developing for multilingual sites?

  ***

  Always use the lang and the dir attributes in all your HTML.
  dir is the direction
  Machine translation

  ***

- What are `data-` attributes good for?

  ***

  It is used to store custom data private to the page or application

  The `data-` gives us the ability to embed custom data attributes on the all html pages.

  The stored data can be used in page's javascript to create a more engaging user experience. used in tests get elements.

  ***

- Consider HTML5 as an open web platform. What are the building blocks of HTML5?

  ***

  1. Semantics - Allows you to describe more precisely what your content is.
  2. Connectivity - Allows you to connect serve in new and innovation ways. using javascript to access javascript
  3. Offline and storage - Allows data to be stored in client side locally and operate offline more efficiently
  4. Multimedia - Making video and audio
  5. 2D/3D graphics and effects.
  6. Performance and integretion - Providing greeter performance optimazation and better usage of computer hardware
  7. Devices access
  8. Styling

  ***

- Describe the difference between a `cookie`, `sessionStorage` and `localStorage`.
  ***
  ![img](https://res.cloudinary.com/practicaldev/image/fetch/s--l0dXxSlh--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/eyov7ylvzgm3o7t5j27w.png)
  https://dev.to/rohanshakya/javascript-local-storage-vs-session-storage-vs-cookies-95n
  ***
- Describe the difference between `<script>`, `<script async>` and `<script defer>`.

  ***

  The HTML `<script>` element is used to embed executable code or data; this is typically used to embed or refer to JavaScript code.

  `<script>`: Will prevent html render, will download script first.z

  `async`: For classic scripts, if the async attribute is present, then the classic script will be fetched in parallel to parsing and evaluated as soon as it is available.

  For module scripts, if the async attribute is present then the scripts and all their dependencies will be executed in the defer queue, therefore they will get fetched in parallel to parsing and evaluated as soon as they are available.

  `defer`:

  This Boolean attribute is set to indicate to a browser that the script is meant to be executed after the document has been parsed, but before firing DOMContentLoaded.

  Scripts with the defer attribute will prevent the DOMContentLoaded event from firing until the script has loaded and finished evaluating.

---

- Why is it generally a good idea to position CSS `<link>`s between `<head></head>` and JS `<script>`s just before `</body>`? Do you know any exceptions?

  ***

  CSS needs to be ready, when the page is render. The css files are placed in the "head" so that they load and the page is seen as it should be.

  HTML is loaded line by line and runs it will call the files and execute it’s contents as the line is loaded. JavaScript is known to delay or block some pages from loading because of this.

  It became a best practice to add JavaScript or refer to external JavaScript files at the bottom of the page, the files are only loaded after all the page content loads.

  Currently there is an alternative most recent browsers implemented called async.

  ***

- What is progressive rendering?

  ***

  Progressive Rendering (aka Progressive Server Side Rendering) is a technique in which once you render the critical content on the server, you start streaming it to the client without waiting for non-critical content. You then stream the non-critical content later once it’s rendered on the server. The browser starts to progressively render (paint) the HTML on the page as soon as a chunk for critical content is received. Non-critical content is then later rendered (paint) on the page when the browser receives it from the server.

  for more: https://medium.com/the-thinkmill/progressive-rendering-the-key-to-faster-web-ebfbbece41a4

  ***

- Why you would use a `srcset` attribute in an image tag? Explain the process the browser uses when evaluating the content of this attribute.

  ***

  The HTMLImageElement property srcset is a string which identifies one or more image candidate strings, separated using commas (,) each specifying image resources to use under given circumstances. Each image candidate string contains an image URL and an optional width or pixel density descriptor that indicates the conditions under which that candidate should be used instead of the image specified by the src property.

  ```html
  <div class="box">
    <img
      src="/files/16797/clock-demo-200px.png"
      alt="Clock"
      srcset="
        /files/16864/clock-demo-200px.png 1x,
        /files/16797/clock-demo-400px.png 2x
      "
    />
  </div>
  ```

  ***

- Have you used different HTML templating languages before?
  ***
  jsx and vue, compile to Virtual DOM
  ***
- What is the difference between `canvas` and `svg`?

  ***

  SVG is a language for describing 2D graphics in XML.

  Canvas draws 2D graphics, on the fly (with a JavaScript).

  SVG is XML based, which means that every element is available within the SVG DOM. You can attach JavaScript event handlers for an element.

  In SVG, each drawn shape is remembered as an object. If attributes of an SVG object are changed, the browser can automatically re-render the shape.

  Canvas is rendered pixel by pixel. In canvas, once the graphic is drawn, it is forgotten by the browser. If its position should be changed, the entire scene needs to be redrawn, including any objects that might have been covered by the graphic.

  ***

  for more: https://www.w3schools.com/html/html5_svg.asp

- What are empty elements in HTML ?
  ***
  Element cannot have any child nodes. Using a closing tag on an empty element is usually invalid

```html
<area />
<base />
<br />
<col />
<embed />
<hr />
<img />
<input />
<link />
<meta />
<param />
<source />
<track />
<wbr />
```

---
