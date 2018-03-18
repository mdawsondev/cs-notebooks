# HTML5 Fundamentals

[HTML5 Fundamentals](https://app.pluralsight.com/library/courses/html5-fundamentals/table-of-contents) specifically covers the HTML5 aspects of HTML. I decided to go ahead and take notes on this course to refresh myself since I've been spending so much time playing with JavaScript that I've been neglecting my HTML5 skills. 😜

## Introduction

The docs for HTML5 can be found at [HTML5.org](https://platform.html5.org).

The three major standard bodies responsible for HTML development are W3C, WHATWG, and ECMASCRIPT.

The point of a lot of HTML5 elements is not to add new features, but to add semantic readability. For example, `<main>` represents the most important content. `<article>` is a way to group information together and signal to the search engine that the content is important.

Others Noteables:

* `aside`: Used to flag important content but not crucial.
* `section`: Used to group logically grouped data.
* `header`: Used to signal header content.
* `footer`: Used to signal footer content.
* `nav`: Explicially reserved for navigation menus and links.

### Spealized Elements

* `time`: Semantically represent time.
* `figure`/`figcaption`: Meant to give semantic meaning to images.
* `details`/`summary`: A No-JS way of adding interactivity to details.
* `mark`: Intended to highlight matched text for search results.
* `wbr`: Signals where to break long words (wordbreak).
* `output`: Semantic tag to support output results (like calc results).
* `embed`: Host container for plugins, becoming less common.

### Elements with APIs

* `canvas`: Used for drawing on the page.
* `audio`/`video`: For audio or video embedding. 

### Form Elements

* `meter`: Used to visually demonstrate value between a set threshold.
* `progress`: A native progress bar to show progression without JS.
* `math`: Used for MathML elements.
* `datalist`: A list of elements shown as options in an input field.

### JavaScript APIs

* Graphics
  * Canvas
  * Web Animations
* Interaction
  * Battery Status
  * Clipboard API & Events
  * Cross Document MEssaging
  * Device Orientation
  * Fullscreen API
  * Geolocation
  * Media Capture
  * Notifications
  * Touch Events
  * Vibration
* Storage & Files
  * Blob URLs
  * File API
  * File Reader
  * IndexedDB
  * Local Storage
* Real-Time Communication
  * Push API
  * Server-Sent Events
  * Web Sockets
* Web Components
  * Custom Elements
  * Shadow DOM
  * Templates
* Performance Optimization & Analysis
  * High Resolution Time
  * Navigation Timing
  * Page Visibility
  * User Timing
  * Web Workers
* Security & Privacy
  * Content Security Policy
  * Referrer Policy
  * Web Cryptography
* Miscellaneous Features
  * scripts: async & defer
  * contentEditable
  * Drag & Drop
  * History
  * Promises
  * Service Workers

### HTML4 to HTML5

Just some quick notes since I'm pretty familiar with the changes.

* DOCTYPE dropped casting in favor of `html`.
* Scripts and Style dropped `type=""` for internal code.
* `main` should only appear once on a page, housing the main content.
* `nav` represents internal navigation and should not point externally.
* `article` can be used many times, but is good for blocking similars.
* `section` used for logical grouping, `div` is for visual sectioning.
* `a` now capable of wrapping block elements.
* Attributes do not always need to be declared, eg. `<description open>`.

### HTML5 Boilerplate

Discusses [HTML5 Boilerplate](https://html5boilerplate.com); this is optional but lets you jump into projects quicker. Applies items like `normalize.css` and modernizr.

The boilerplate does come with opinionated decisions, but comes with a lot of useful quick-build features. If you head to [Initializr](https://initializr) you can customize your Boilerplate download so you can add or remove various features.

### Fallback Support

Features should be checked via Modernizr and CanIUse. Modernizr is considered a must-have to ensure support.

There are also fallback and polyfill features that can be implemented to support older browsers. **Fallbacks** are typically imported APIs that offer the same functionality for a non-supported feature, while **polyfills** are used to hardcode features into the scripts. The idea is that pollyfills can be removed once the feature becomes more supported without breaking anything.

[HTML5Please](https://html5please.com) can be used to hunt down fallbacks and polyfills to enable simple support.

### Summary

HTML5 is the collection of new elements and new JavaScript APIs, forming a larger web platform foundation. 

## Finding Parts of the Page

## Working with User Input

## Music & Video

## Drawing Shapes, Charts, and More

## Drag and Drop