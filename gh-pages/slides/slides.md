![floats](img/image.png)

---

### CSS 4 devs - the basics
- situating CSS
- semantic HTML
- Positioning
- CSS units
- CSS selectors
- CSS specificity
- mediaqueries, webfonts, SVG
- devtools

---

### situating CSS - what is

What is CSS
- declarative approach
- CSSOM

---

### situating CSS - how it works

- how the browser renders:
- layout, paint composite
- (csstriggers.com)

---

###  Semantics (HTML5) & Accessibility (ARIA)
####  WAAROM

- Crawlers

- Screenreaders: Inclusive websites with ARIA

https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques

---

###  Semantics & Accessibility
####  WAAROM

- how you navigate with a screen reader
    - document title = tells the user where they are (did the page change)
    - navigate by (structured) headings
    - navigate by links -> why "read more" links are bad (15 times "read more")
    - navigate by article (aria-labeled-by="") ...
    - navigate images (why alt text is not just for SEO; describe what's happening!)

---

###  Semantics & Accessibility
####  WAAROM

- tables for layout are *horrible* - complicates navigation a LOT for blind users

- if you still insist on doing it, at least use 

```<table role="presentation">```

---

###  Semantics & Accessibility
####  WAAROM

How A Screen Reader User Surfs The Web:
https://www.youtube.com/watch?v=OUDV1gqs9GA

---

###  Semantics & Accessibility
####  HOE

- HTML(5) Tags gebruiken 
    - (div !== button, use header, footer, aside, sections, article, ...)
- Structuur uitdenken voor headings: H1->H6 !== size, but content structure

---

###  Semantics & Accessibility
####  HOE - tips & tricks

- tabindex
- role="tab" -> no markup to replace this
- aria-pressed -> for toggles, but also play/paused
- aria-expanded -> another state that helps convey what's going on
- aria-labeled-by -> tying pieces of content together

---

###  Semantics & Accessibility
####  HOE - tips & tricks

- like seasoning; don't overdo it - HTML gives you accessibility for free

---

###  Semantics & Accessibility
####  HOE - example

example of good aria: https://tink.uk/ (website by leony watson)

---

### Semantics & Accessibility
#### VOORBEELD

![semantics](img/semantics.png)

---

###  Semantics & Accessibility
#  VRAGEN ?

---

### BOX MODEL
####  WAT
- The CSS box model is essentially a **box that wraps around every HTML element**. 
- Consists of: margins, outline, borders, padding, and the actual content.

---

### BOX MODEL
####  WAAROM
- we use border-box
- We want our elements width to be one on one the width you define

---

### BOX MODEL
####  HOE

```
*, 
*:before, 
*:after { 
    box-sizing: border-box;
}```

---

### BOX MODEL
####  VOORBEELD

https://stackblitz.com/edit/content-box-vs-border-box?file=index.js

---

### BOX MODEL
#  VRAGEN ?

---

### POSITIONING
- Display Properties
- Hiding Elements
- Positioning
- Flexbox
- Grid

---

### DISPLAY PROPERTIES
####  WAT
![display](img/display.png)
- The display property specifies the display behavior (the type of rendering box) of an element.

---

### DISPLAY PROPERTIES
####  WAAROM
- Every HTML element has a default display value depending on what type of element it is. The default display value for most elements is block or inline.

---

### DISPLAY PROPERTIES
####  HOE
- **inline**: accepts padding and margin, ignores dimension
- **inline-block**: accepts padding and margins, accepts dimensions
- **block**: breaks past inline(block) elements, full width within parent

---

### DISPLAY PROPERTIES
#  VRAGEN ?

---

### HIDING ELEMENTS
####  WAT
- 3 Properties that can hide an element
- Choose wisely

---

### HIDING ELEMENTS
####  WAAROM
![display](img/hidden.png)

---

### HIDING ELEMENTS
####  HOE
- `.element { display: none; }`
- `.element { visibility: hidden; }`
- `.element { opacity: 0; }`

---

### Floats
- float
    - left
    - right
    - use on display: block element;

- original usecase: images in text (wrapping of text)
- "hack": position all the things
- the need for clearfixing (border)

---

### Floats
examples:
https://stackblitz.com/edit/clear-examples?file=index.js

---

### Flexbox
####  WAT
- Flexbox or CSS Flexible Box Layout Module is a layout mode used almost exclusively in responsive websites, that provides for a better arrangement of all of the page elements that behave in a predictable mode.

---

### Flexbox
####  WAAROM
- 1 Dimension positioning (determine axis with flex-direction)
- Content first (we don't care what surrounds us)

---

### Flexbox
####  HOE
![flex](img/flex.png)

---

### CSS grid

- grid
    - create a grid - 2 dimensions
    - layout first (defining layout; number of explicit columns, grid areas, ...)
    - affects direct childs (only) (*) subgrid

https://gridbyexample.com/examples/

---

###  position
- static
    - follow flow of document
    - default - does not listen to positional properties (left/right/top/bottom/z-index)

---

###  position
- relative
    - follow flow of document
    - listen to positional properties
    - creates new z-index "stacking context" (layer)

    https://stackblitz.com/edit/z-index-demo?file=style.css

---

###  position
- absolute
    - removes from flow of document; the parent element will behave as if the child isn’t there at all
    - listen to positional properties
    - relative to the first parent that has it's own "layer/context" (-> why we need to position relative a parent)
        - (if none is present, this is the body element!)
    - creates new z-index "stacking context" (layer)

---

###  position
- fixed
    - removes from flow of document;
    - listen to positional properties
    - relative to the viewport! more importantly, this value is unaffected by scrolling
    - creating "floating box" or "modal"
    - creates new z-index "stacking context" (layer)
    - styling modals/overlays (position sticky is a thing but support...)

---

### position - example

https://stackblitz.com/edit/position-relative-example?file=style.css
why is there space on top? there is no padding there

(correct version with position absolute:)
https://stackblitz.com/edit/position-relative-example-fixed?file=style.css

---

### margins
(margins collapse)
-> single direction margin declarations, always!

-> https://csswizardry.com/2012/06/single-direction-margin-declarations/
- Easier to define vertical rhythm in one fell swoop.
- More confidence in (re)moving components if you know their margins all push in the same direction - order doesn't matter

---

### CSS units

relative (web!)
- relative fractions
    - % (relative to parent size)
    - vw (relative to viewport width)
    - vh (relative to viewport height)
fr (grid)

---

### CSS units

- relative font
    - em (the problem with em - nested font-size = multipliers)
    - rem (same as em, but root = html element)
- usable in any property: width, padding, ...

---

### CSS units

- absolute (print!)
    - px (images! perfect usecase)

    - cm (yap, that works)
    - mm
    - pt or points (1/72 of an inch.. imperial system brrr...)
    - pc or pica (12 pt... /shrug)
    - in (inch, 2.54cm - fun fact: 96px... imperial system brrr...)

---

### Proportions not absolutes
https://csswizardry.com/2011/12/measuring-and-sizing-uis-2011-style/

Design is about proportions, not absolutes, and in ignoring actual pixel measurements in favour of relative ones you can ensure that designs are not tethered to numbers, but to proportions.

An element without measurements is inherently fluid, but in the best possible way; it will work wherever you put it.

---

### css selectors
https://codepen.io/nana8/full/aXQgoj

---

### css specificity
![important](img/specificity.jpg)

---

### css specificity
![wars](img/css-specificity-wars.png)

---

### css specificity
`div#container.m_block.m_block--modifier`

- what's wrong about this selector?
- specificity weight?
- how do i override this?
    fighting specificity: 

    multiply your class selector(s); .myclass.myclass 


---

### css specificity

fighting specificity
- this is why you avoid nested selectors in SASS;
    - the deeper, the more complex;
    - you have to "calculate" and increase (as little as possible!)
- exceptions to important:
    - helper classes

---

### mediaqueries
are used:
- To conditionally apply styles with the CSS @media and @import at-rules.
- To target specific media for the `<link>`, `<source>`, and other HTML elements.

```
@media not / only (type of media) and (expressions) {
    /* CSS Style elements. */
}
```

---

### mediaqueries

- media type
    - all
    - print
    - screen

- expressions
    - width
    - height
    - aspect-ratio

more: (https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries)

---

### mediaqueries

combinators:
- and
- not
- only
- , (comma)

---

### mediaqueries
```
.myClass {
    // mobile first (you don't want to override all properties to achieve mobile layout)
    ...
}

@media only screen and (min-width: 200px and max-width: 500px){
    .myClass {
        /* Tablet only */
        ...

// "Shortcut" with sass mixin:
.myClass {
    // mobile first
    ...
    @include respond-to('tablet') {
        // some rules
    }
    @include respond-to('desktop') {
        // some rules
```

---

### mediaqueries in javascript

- To test and monitor media states using the `Window.matchMedia()` and `MediaQueryList.addListener()` JavaScript methods.

https://stackblitz.com/edit/matchmedia-addlistener-demo?file=index.js

---

### webfonts (formats)
- @font-face -> define your fonts
    - per font-family combination of font-weight & font-style -> which file

---

### webfonts (formats) - code example
```
@font-face {
    name: 'Roboto',
    files: url(static/Robot.woff2, ...)
    weight: 100; style: normal;
}
@font-face {
    name: 'Roboto',
    files: url(static/RobotoItalic.woff2, ...)
    weight: 100; style: italic;
}

.myClass {
    font-family: "Roboto", Arial, Helvetica, sans-serif; // fallback "stack"
    font-weight: 100;  font-style: italic;
}
```

---

### webfonts (formats) - font resources

- fontsquirrel
    - many formats needed for different browsers

- google fonts
    - cdn with generated css & files
- adobe fonts
    - likewise

---

### fonts

<video controls width="1200">

    <source src="/video/fonts_step1.mov"
            type="video/mp4">

    Sorry, your browser doesn't support embedded videos.
</video>

---

### fonts

<video controls width="1200">

    <source src="/video/fonts_step2.mov"
            type="video/mp4">

    Sorry, your browser doesn't support embedded videos.
</video>

---

# SVG
- inline
- external
- in CSS

---

### Frontend architecture

- Style
- Applying (5) software principles to CSS

---

### Style

declare your properties in order of impact first:

- positioning 
    - (position, z-index, overflow, ...)
- box model 
    - (padding, margin, border, outline, ...)
- presentation 
    - (font, colors, ...)

http://csscomb.com/

---

### DRY

Don’t repeat yourself

---

### DRY

“Every piece of knowledge must have a single,
unambiguous, authoritative representation
within a system“

---

### DRY

“DRY is not about no repeating anything but is about not repeating yourself “


---

### DRY

```
.u-margin-top { margin-top: 12px; }

.u-margin-right { margin-right: 12px; }

.u-margin-bottom { margin-bottom: 12px; }

.u-margin-left { margin-left: 12px; }
```

---

### DRY

sass variable

```
$unit : 12px;
.u-margin-top { margin-top: $unit; }
.u-margin-right { margin-right: $unit; }
.u-margin-bottom { margin-bottom: $unit; }
.u-margin-left { margin-left: $unit; }
```

---

### DRY


css custom properties ("built-in" variables)
```
:root {
    --unit: 12px;
}
.u-margin-top { margin-top:  var(--unit); }
.u-margin-right { margin-right: var(--unit); }
.u-margin-bottom { margin-bottom: var(--unit); }
.u-margin-left { margin-left: $var(--unit); }
```

---

### DRY

```
.page-title {
    font-family: “Custom Font”, sans-serif;
    font-weight: 700;
}
.btn {
    font-family: “Custom Font”, sans-serif;
    font-weight: 700;
}
.pagination {
    font-family: “Custom Font”, sans-serif;
    font-weight: 700;
}
```

---

### DRY

sass mixins
```
@mixin custom-font() {
    font-family: “Custom Font”, sans-serif;
    font-weight: 700;
}
.page-title {
    @include custom-font();
}
.btn {
    @include custom-font();
}
.pagination {
    @include custom-font();
}
```

---

### DRY

Gives the exact same
output, but at least we
haven’t duplicated
anything manually

---

### DRY

do not "DRY" this - it's purely coincidental:

Repetition is better than the wrong abstraction.

```
.btn {
    color : white;
    font-weight : bold;
}

.calendar__title {
    font-size : 14px;
    font-weight : bold;
}

.message {
    font-weight : bold;
}
```

---

### DRY

- Every discrete piece of information should exist only once.
- You shouldn’t need to make the same change several times.
- Repetition is extra overhead : more to maintain, more to go wrong

---

### The single Responsibility Principle

---

### The single Responsibility Principle

Everything should do one job, one job only and
should do that job very very well.

---

### The single Responsibility Principle

```
<button class=”my-button”></button>

.my-button {
    display: inline-block;
    padding: 2em;
    background-color: green;
    color: white;
}
```

---

### The single Responsibility Principle

```
<button class=”btn btn--large
btn-positive”> … </button>

.btn {
    display: inline-block;
}

.btn--large {
    padding: 2em;
}

.btn--positive {
    background-color: green;
    color: white;
}
```

---

### The single Responsibility Principle

Provide everyone with the ingredients.
Let them make the meals

---

### Separation of Concerns

---

### Separation of Concerns

Each thing responsible for itself and
nothing more

---

### Separation of Concerns

Using HTML to provide cosmetics.

```
<font color="red">

<div style=”color : red; “>...</div>
```

---

### Separation of Concerns

Targetting the wrong attributes or classes to apply styles.

```
[role="navigation"] > ul > li { ... }
.js-mybutton { ... }
```

---

### Separation of Concerns

Doing it right.

```
<nav class="site-nav js-site-nav" role="navigation">
    <ul class="site-nav__list">
        <li class="site-nav__item">
            <a class="site-nav__link" data-cy="cypress-anchor">...</a>
        </li>
    ….
    </ul>
</nav> 
```

---

### Separation of Concerns

- semantic concern
- accessibility concern
- behaviors concern
- stylistic concern
- testing concern
- ...

---

### Separation of Concerns

Only bind CSS onto CSS-based classes.

Don’t write DOM-like selectors.

Don’t bind CSS onto data-* attributes.

Don’t bind JS onto CSS classes. 

---

### Immutability

---

### Immutability

"...an immutable object is an object whose
state cannot be modified after it is created."

---

### Immutability

doing it wrong.
```
.col-6 {
    width: 50%;
}

@media screen and (max-width: 480px) {
    .col-6 {
            width: 100%;
        }
} 
```

---

### Immutability

doing it wrong.
```
.btn {
    font-size: 1em;
}

.promo .btn {
    font-size: 1.2em;
}
```

---

### Immutability

doing it right.
```
.btn {
    font-size: 1em;
}

.btn--large {
    font-size: 1.2em;
}
```

---

### Immutability

Don’t have several states of the
same thing.

Use Modifiers (btn--large) or Responsive
Suffixes (hidden@mobile)

---

### The Open/Closed Principle

“Software entities (classes, modules, functions, etc.)
should be open for extension, but closed for
modification.”

---


### The Open/Closed Principle

```
.btn {
    padding: 1em 2em;
}

.btn--large {
    …
    padding: 1.5em 2.5em;
}
```

---

### The Open/Closed Principle

Safe way to make changes.
Safe way of working with legacy.

---

# Loose coupling
that is, to say, avoid tight coupling.

example; theming.

Copy pastes across themes !== bad case of DRY

- be careful of implementing "inheritance" when the base can ever change (trust me, it always does if it's styling)
- unpredictability should be avoided

---

#  (questions?)

Approach CSS as you would programming.

Structure brings great maintainability as a result.

---

# BEM

- block
- element
- modifier

````
.faq-example

.faq-example__title
.faq-example__content

.faq-example--small

.is-expanded
```

---

### BEM
#### pitfalls

- an element can be several nodes deep into the element (and that's fine).

---

### BEM
#### pitfalls

- `.header__navigation__navigation-item`; 
    - never more than one level "deep" with underscores
    -  creates tight coupling (navigation is always in header) and couples styling to markup
    - modularise instead, and start a new block where it makes sense: 
    ```.header, .header__logo, 
    .navigation, .navigation__item```

---

### BEM
#### pitfalls

- a modifier is not state
- a modifier is a variant.
- (use is- or has- classes instead to indicate this distinction)

---


### itcss
![itcss](img/itcss.png)

https://www.xfive.co/blog/itcss-scalable-maintainable-css-architecture/
https://github.com/ahmadajmi/itcss

---

structuring folders (at foreach):

- base
    - settings, ...
- layout
    - "system"
- modules
    - 90% of scss
- non-modular
    - plugins, external css, hacks


---

### bonus
####  element queries

- mediaqueries !== element queries
- for a re-usable component, it's parent's dimensions are more important thatn the viewport dimensions

---

### bonus
####  element queries

- polyfill: https://github.com/eqcss/eqcss
- example: nettopension widget (small & large design, gets rendered as such based on where you place it)

https://www.smashingmagazine.com/2016/07/how-i-ended-up-with-element-queries-and-how-you-can-use-them-today/

---

### bonus; 
#### "slicing" 

slicing a project from design deliverables to maintainable markup & (s)css

- design: 

https://projects.invisionapp.com/d/main#/console/15810598/328132895/preview
- repo: 

http://stash.foreach.be/users/jsv/repos/css4devs-example/browse

---