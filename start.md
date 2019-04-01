semantic HTML(5) & accesibility - a tl;dr
    h1, h2, ... document outline
    tabindex: some people interact with keyboard only
    label & input
    article
    section
    ...
    role=""
    on using tables for layout (role="presentation")

the box model;
    width,
    padding,
    border,
    margin,
    outline

* { box-sizing: border-box}

POSITIONING how the browser layouts your page.
    display
        inline:
            aligns to baseline
            accept padding & margin (but only pushes other elements horizontal)
            ignores dimensions (width & height)
        inline-block
            aligns to baseline
            same, but accepts dimensions
        block
            break past inline(block) elements
            defaults to full width (within it's parent)
        flex
            create a flex parent - 1 dimension (determine axis with flex-direction)
            affects direct childs (only)
        grid
            create a grid - 2 dimensions
            layout first (defining layout; number of explicit columns, grid areas, ...)
            affects direct childs (only* ... until sub-grid becomes a thing*)
        none
            remove from page
        table, table-row, table-cell -> because you don't know flex exists

    position
        static
            follow flow of document
            default - does not listen to positional properties (left/right/top/bottom/z-index)
        relative
            follow flow of document
            listen to positional properties
            creates new z-index "stacking context" (layer)
                -> how z-index "works" -> bigger number = "closer" on the z-axis (think of it as left/top/... === x and y axis)
                -> now think of stacking contexts as "layers"
                -> each layer has it's own depth/stack, the entire document can be represented as a tree

        absolute
            removes from flow of document; the parent element will behave as if the child isn’t there at all
            listen to positional properties
            relative to the first parent that has it's own "layer/context" (-> why we need to position relative a parent)
                (if none is present, this is the body element!)
            creates new z-index "stacking context" (layer)
        fixed
            removes from flow of document;
            listen to positional properties
            relative to the viewport! more importantly, this value is unaffected by scrolling
            -> creating "floating box" or "modal"
            creates new z-index "stacking context" (layer)

            -> styling modals/overlays
        (sticky)
            -> experimental:
                the element is treated like a relative value
                until the scroll location of the viewport reaches a specified threshold,
                at which point the element takes a fixed position where it is told to stick.
                https://codepen.io/geoffgraham/pen/ybVzeX
            creates new z-index "stacking context" (layer)
        (inherit)
            does not cascade by default - makes it cascade

EXAMPLE/pitfall;
    https://stackblitz.com/edit/position-relative-example?file=style.css
    "why is there space on top? there is no padding there"
    "why do margins collapse"
        -> single direction margin declarations ftw!
        -> https://csswizardry.com/2012/06/single-direction-margin-declarations/
            - Easier to define vertical rhythm in one fell swoop.
            - More confidence in (re)moving components if you know their margins all push in the same direction.
            - Components and elements don’t have to necessarily live in a certain order if their margins aren’t dependent on adjoining sides.
            - Not being concerned with collapsing margins means one less thing to worry about.

CSS units
    relative (web!)
        relative fractions
            % (relative to parent size)
            vw (relative to viewport width)
            vh (relative to viewport height)
            vmin
                portrait:  100 vmin = 100vw
                landscape: 100vmin = 100vh
            vmax
                portrait: 100vmin === 100vh
                landscape: 100vmax === 100vw

                usecase:
                Hero texts are prone to look too small on mobile and too big on large monitors.
                example using 20vmin
                https://codepen.io/dudleystorey/full/ALWrXZ/

        relative font
            em (the problem with em - nested font-size = multipliers)
            rem (same as em, but root = html element)
            ex (height of x-glyph of font -> FONT relative!)
            ch (width of the 0-glyph - FONT relative!)
            fr (grid)

    absolute (print!)
        px (images! perfect usecase)
        cm (yap, that works)
        mm
        pt or points (1/72 of an inch.. imperial system brrr...)
        pc or pica (12 pt... /shrug)
        in (inch, 2.54cm - fun fact: 96px... imperial system brrr...)

https://csswizardry.com/2011/12/measuring-and-sizing-uis-2011-style/
Design is about proportions, not absolutes, and in ignoring actual pixel measurements in favour of relative ones you can ensure that designs are not tethered to numbers, but to proportions.
An element without measurements is inherently fluid, but in the best possible way; it will work wherever you put it

css selectors
    what you CAN do:
        special characters
            *
                blanket selector (any element)
            A, B - Selector list
                any of A or B
            A B - Descendant combinator
                Any element matching B that is a descendant of an element matching A (that is, a child, or a child of a child, etc.).
            A > B - Child combinator
                Any element matching B that is a direct child of an element matching A.
            A + B - Adjacent sibling combinator
                Any element matching B that is the next sibling of an element matching A (that is, the next child of the same parent).
            A ~ B - General sibling combinator
                Any element matching B that is one of the next siblings of an element matching A (that is, one of the next children of the same parent).

        "pseudo" selectors
            before/after
                shadow DOM
            nth-child
                Select Only the Fifth Element
                :nth-child(5)

                Select All But The First Five
                :nth-child(n+6)

                Select Only The First Five
                :nth-child(-n+5)

                Select Every Fourth, Starting At The First
                :nth-child(4n-7)
            state
                :hover
                :active
                :visited
        attribute selectors:
            [lang="fr"]
            [href^="https://www.foreach.be"]
            [href*="foreach"]

    what you CAN'T do
        -> working your way "upwards" ("my parent must...")
            -> you "have to" add classes with logic
                (serverside because javascript relayouts - you don't want stuff to jump)

css specificity
    universal selector(s) * + > ~
        0
    Element
        1
    Class
        10
    ID
        100
    inline
        1000
    important
        infinite

    div#container.m_block.m_block--modifier
        what's wrong about this selector?
        specificity weight?
        how do i override this?
            fighting specificity: nx your class selector(s); .myclass.myclass (no space! (would be a descendant combinator))

    fighting specificity
        - this is why you avoid nested selectors in SASS;
            the deeper, the more complex;
            you have to "calculate" and increase (as little as possible!)
        - exceptions to important:
            - helper classes
            - .

mediaqueries
are used:
    To conditionally apply styles with the CSS @media and @import at-rules.
    To target specific media for the <link>, <source>, and other HTML elements.
    To test and monitor media states using the Window.matchMedia() and MediaQueryList.addListener() JavaScript methods.

    @media not / only (type of media) and (expressions) {
        /* CSS Style elements. */
    }

    media
        all
        print
        screen
        speech

    expressions
        width
        height
        aspect-ratio
        ... a lot (https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries)
    combinators:
        and
        not
        only
        , (comma)

practical example:
    // mobile first (you don't want to override all properties to achieve mobile layout)
    @media screen and (min-width: 480px) {
        body {
            background-color: blue;
        }
    }

webfonts (formats)

SVG
    inline
    external
    in CSS

devtools; debugging tips
    - inspect actual rendered font(s)

    box model (padding vs margin: affecting layout (or not)


colors
    named colors
    hex
    hsl