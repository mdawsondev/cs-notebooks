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

Brief mention of using `getElementsByClassName` but that's been depreciated for general use cases in favor of `querySelector` on the DOM. `querySelectorAll` will pull all nodes associated with the selection. Valid selections work the same as they did in jQuery or targeting via CSS, i.e. `.`, `#`, etc. depending on needs.

Just a reminder, although it appears that selection is returning an array of elements, it's actually returning a `NodeList`. `NodeList` is an object that can be iterated. `forEach` is also mentioned as a node iteration.

When changing elements in the DOM, the DOM will update depending on whether you're working with a live result or static result environment. `querySelector` will return static result while `getElementByClassName` will work with live results.

_Aside: New elements are called via `document.createElement('ELEMENT')`._

## Working with User Input

### New Elements (Overview)

* `input type="color"`: Add color-picker element.
* `datalist`: Appears as predefined options when associated with `input`.
* `input type="datetime"`: Adds a date-picking element.
* `input type="datetime-local"`: Adds a date-picking element for local TZ.
* `input type="email"`: Adds email functionality to mobile KB.
* `input type="url"`: Adds url functionality to mobile KB.
* `input type="tel"`: Adds telephone functionality to mobile KB.
* `input type="month"`: Adds a month/year selector.
* `input type="number"`: Up/down number selection and mobile KB support.
* `input type="range"`: Outputs a slider with start/stop/step control.
* `input type="week"`: Allows selection of single week of given year.
* `input type="time"`: Allows selection of a specific time. Mobile KB.
* `input type="search"`: Similar to text with an 'x' to clear input.

### Native Validation

Don't blindly trust user input. Validation and sanitization is an important way to ensure security and prevent data from breaking.

* `Value Missing` evaluates to `true` if an element has the `required` attribute and the value is empty.
* `Type Mismatch` evaluates `true` when value is not a match to the declared type.
* `Pattern Mismatch` evaluates `true` when value doesn't match given regular expression via `pattern="/RegExp"` on an input.
* `Too Long` evaluates `true` when the value length is longer than the `maxlength="n"` property, where n is an integer.
* `Range Underflow` returns `true` when range type's value is smaller than min attribute (`min="n"`).
* `Range Overflow` returns `true` when range type's value is larger than max attribute (`max="n"`).
* `Step Mismatch` returns `true` when value is not possible given the step value (i.e. modulo).
* `Valid` returns `true` when all other validation rules return `false`. Implies a valid form submission.

This is good for a simple validation via client-side forms, but shouldn't be trusted beyond some basic enforcement rules.

### Demo Notes

These notes were taken from the HTML5 demo and markup sections.

* `autofocus` is an attibute that can instantly set focus to any element without using JS. Only one input element can house `autofocus` at any time.
* `placeholder="Placeholder Words"` allows a ghost-based placeholder text without using a default value.
* `number` inputs only allow up/down functionality, no text input.
* `datalist` lets you fill in a preformed text or custom input.
* `novalidate` allows you to skip validation rules; must be attached to a `form` element.

Repeat on previous notes, `required`, `pattern` are also allowed features.

There were some notes about various browsers supporting different elements (like IE not supporting the `number` type), but this could have changed since the video was made. These things should be checked on CanIUse.

### Psuedo Classes

The new CSS structure with HTML5 allows psuedo classes to target various states of elements without having to implement any JavaScript. CSS can target via `:required` to give hints to the user that items are required. Validity can also be targed via `:invalid` or `:valid`.

### Custom Validation

This stuff was implemented using `data` markup and JavaScript functionality - I don't see it being exlusively HTML5 related so I'm not going to bother taking notes here. The takeaway is just reflecting on various selectors and applying properties to them.

I'm also pretty sure there's a custom validation message feature inside of HTML5 which he doesn't even mention.

## Music & Video

## Drawing Shapes, Charts, and More

## Drag and Drop