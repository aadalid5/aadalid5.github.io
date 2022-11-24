---
parent: Guides
title: Mobile First
layout: home
---

# Mobile First

*This concept requires on an understanding of the basics of responsive design. [CSS Tricks](https://css-tricks.com/?s=responsive%20design) is a great resource for all things CSS.*

We should be building UIs
["mobile-first"](https://www.browserstack.com/guide/how-to-implement-mobile-first-design).
What this means is to build UIs, such as a component, for the smallest
screen size we support. Below are the breakpoints we currently support in
this project:

    $medium: 768px;
    $large: 1025px;
    $x-large: 1351px;

All CSS should be written, by default, for the mobile design of the site
first. Media queries should only be used for going up in screen size, not
down, meaning they would progressively override the styles applied at the
previous breakpoint as the screen gets wider. An example of this is as
follows:

    .container {
        width: 100%;
        background-color: #f00;
    }
    
    // $medium is the variable for the 768px breakpoint.
    @media only screen and (min-width:$medium) {
        .container {
            background-color: #0f0;
        }
    }
    
    // $large is the variable for the 1024px breakpoint.
    @media only screen and (min-width:$large) {
        .container {
            background-color: #00f;
        }
    }
    
    // $x-large is the variable for the 1351px breakpoint.
    @media only screen and (min-width:$x-large) {
        .container {
            background-color: #f0f;
        }
    }


With the above code, the background color of `.container` will be red in
the smallest viewports, green in viewports wider than 768 pixels, blue in
viewports larger than 1024 pixels, and purple in all viewports larger
than 1,351 pixels.

**However...**

Since we're using [SASS](https://sass-lang.com/documentation) in this
project, we have access to convenient syntax shorthands, such as
[mixins](https://sass-lang.com/documentation/at-rules/mixin). Below is an
example of the previous media query example refactored to use a mixin:


    .container {
        width: 100%;
        background-color: #f00;
    }
    
    // $medium is the variable for the 768px breakpoint.
    @include screen-min-width($medium) {
        .container {
            background-color: #0f0;
        }
    }
    
    // $large is the variable for the 1024px breakpoint.
    @include screen-min-width($large) {
        .container {
            background-color: #00f;
        }
    }
    
    // $x-large is the variable for the 1351px breakpoint.
    @include screen-min-width($x-large) {
        .container {
            background-color: #f0f;
        }
    }


If mobile mockups were not provided, contact Marta Kusztra, Director of
UX and Product Design for HBRG.