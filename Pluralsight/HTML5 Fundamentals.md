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

* Native Media Element (Audio/Video Type)
* Media Types (Encoding)
* Speech API

Audio and video elements need their `controls` enabled to display them; you can also use multiple sources (stacked in order of importance) to serve the video to each supported format. The reason `controls` is option is because you may need to control all the settings yourself. Addling the `loop` attribute will cause an automatic looping process. `preload` is available with the inputs `auto`, `metadata`, and `none`. The `poster` attribute can be tethered to the `video` element so you can add an image rather than the first frame of a video.

JavaScript can be used to control the media element controls. By disabling the `controls` option, you can get collect the UI elements via JavaScript. These elements need their event listener functions to process the expected results. I'm not taking notes about each individual case because I can look them up if I decide to do this down the line - the important thing is knowing it's possible.

* video = document.getElementById('vid')
* remainingTime = document.getElementById('remainingTime')
* totalTime = document.getElementById('totalTime')
* playPause = document.getElementById('playPause')
* stop = document.getElementById('stop')
* rewind = document.getElementById('rewind')
* begin = document.getElementById('begin')
* end = document.getElementById('end')
* fastForward = document.getElementById('fastForward')
* volume = document.getElementById('volume')
* mute = document.getElementById('mute')
* scrubber = document.getElementById('scrubber')
* playbackRate = document.getElementById('playbackRate')

Video and audio can be put into an "autoplay" sequence by looking at the "ended" event of the video then loading the next video. Again, this isn't really an HTML5 feature as much as it is a JavaScript recipe, so I'm not taking notes on this individual technique.

## Drawing Shapes, Charts, and More

_Aside: Images are displayed as Raster (Pixeled) vs Vector (Math-based)._

The canvas system is built on top of a grid system that looks a bit like a math-based plot, however the y-axis is reversed (negatives on top, positives on bottom). It's easier to think of this in terms of the CSS axis chart. A canvas element must be invoked to be used via `<canvas id="canvas" width="600" height="400"></canvas>`, then it can be manipulated by the canvas API via JavaScript.  Nothing has actually been created until the path has been filled.

Once a canvas has been called to the DOM, it can be hooked via `canvas = document.querySelector('#canvas');` and given 2d context via `context = canvas.getContext('2d');` to hook the 2d-path.

1. `context.beginPath();` - Be aware of what's happening next.
2. `context.moveTo(75, 50);` - Establish starting position.
3. `context.lineTo(75, 100);` - Establish the second position with a lined edge.
4. `context.lineTo(25, 100);` - Establish the third position with a lined edge.
5. `context.fill()` - This takes the last point of a path and connects it to the first position, then fill it.

Alternative to running `.fill()`, canvas is able to close the path with `context.closePath();` and fill it with custom styles and colors. `.fillStyle = '#555"` for fill colors, `.fill()` will then fill the customized path. Other methods include `.lineWidth`, `.lineJoin`, `strokeStyle`, and `.stroke` to combine into a border (stroke) path.

### Rectangles

Rectangles can be quickly crafted by calling a `.fillStyle` property and then a `.fillRect()` method.

1. `context.fillStyle = 'rgb(500, 0, 0)';`
2. `context.fillRect(50, 50, 100, 100);` where (x, y, width, height).

Note: applying fill first will cause the stroke to take half its body inside and outside the path; applying stroke first will cover it with the fill. Think of this as working in layers - the new layer will sit on top of the existing canvas work.

### Arcs, Text, and Gradients

Radial Gradients:
``` JS
var g1 = context.createRadialGradient(
  160, // X of start
  120, // Y of start
  0,   // Radius of start circle
  320, // X of end
  220, // Y of end
  300);// Radius of end circle
)
g1.addColorStop(0, '#ffffff'); // Values between 0 - 1 to represent keyframe entirety.
g1.addColorStop(1, '#999999');
```

Circle (Using Radial Above):
``` JS
context.lineWidth = 0;
context.strokeStyle = '#000000';
context.fillStyle = g1;
context.beginPath();
context.arc(
  180, // X of start
  180, // Y of start
  160, // Radius
  0,   // Start Angle
  Math.PI * 2, // End Angle, this is a full circle.
  true);       // Direction anticlockwise
)
```

Text:
``` JS
context.fillStyle = '#ffffff';
context.font = '280px Arial';
context.fillText('C', 80, 280); // Text, X, Y.
```

### Scale, Rotation, Translation

To place an image on a canvas:
``` JS
var img = new Image();
img.onload = () => {
  context.drawImage(img, 0, 0) // File, X, Y
}
img.src = "my/img.jpg";
```

Calling `context.scale(.5, .5)` where X and Y scales to the input will let you scale the canvas references.
Calling `context.rotate(0.2)` where the input is a radian.
Calling `context.translate(50, 50)` where X and Y translation pixels.

### Canvas State

Canvas can have its state saved and you can navigate between saved states. States are also stackable, so calling restore will take you to the last snapshot on the stack. Keyword of stack meaning FILO. Calling `context.restore()` will jump back to the previous `context.save()`.

### Animation

He kind of blew right throug this lesson but the idea is that a canvas can create animation by implementing positional changes like `(x+=10)` to increment positional changes and then firing the changes with a `setInterval` function. I'll need to revisit this if I intend to do any sort of realistic animating on canvas.

### Clipping

Clipping involves creating a restricted display area of an image. Basically, think of a clipping mask in Photoshop: you can have areas display or hide based on whether their clipping is active. Invoking `context.clip()` will create a clipping area based on the existing item. Clipping must be invoked before anything is put on the layers above which it was created. Clips can be cleared with calls to `restore()` to load saves made before clips are created. State management is important.

### Miscellaneous

Craig builds a magnification function and a couple of charts here but it would be too much and too specific to take notes on. Just a note, if you're not dynamically changing data within the canvas, there's no reason not to use a static image. In his static chart demo, Craig uses a photo of a blank chart with labels and grids and then plots the line data on top of the image. Simulating data addition can be managed with a new `setInterval` and using an index count. This could potentially be a use case for a generator? Probably not. Much wow, amazing notes. Canvas elements are powerful tools, they can be used for things like taking thumbnail screenshots of actively playing video.

## Drag and Drop

Drag and drop works by defining a drag source and a drop target. Once an element is tagged `draggable="true"`, it may be dragged around. The key to having this feature work is that **you must cancel default behavior** to have drop functionality. The reason behind the implementation is to keep pages secure. You can drag elements around the page all you like, but to drop it into the drop target you must explicitly tell it to accept the draggable action. The *drag source* is the element being moved, the *drop target* is the element you drag the drag source over.

Drag and drop functionality is controlled via JavaScript with event listeners. You create an event listener for the events internally coded on the drag source and drop target. There's a lot of demo content here but I don't think any of it is actually boilerplate for drag and drop functionality, and if it is, I'll look it up as I need it. There were some interesting ideas about dragging text and files into the DOM, where it's processed and displayed in the drop target.

Note: images and links are already set up to be draggable in the browser.

``` Js
var drop = function(e) {
  if (e.preventDefault) {
    e.preventDefault();
  }
  // handle drop here
  return false;
}
```

Drag Source Events:
* dragstart
* drag
* dragend

Drop Target Events:
* dragenter
* dragover
* dragleave
* drop

