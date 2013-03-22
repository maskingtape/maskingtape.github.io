---
layout: default
category: case-studies
title: "Building Responsive Sites"
overview: Techniques for tailoring content to device size for a project documentation site
related: 
- type: project
  url: /projects/satya
  title: A documentation system for Dharmafly
- type: skill
  url: /skills/css-html-development
  title: CSS / HTML Development
- type: case-study
  url: /case-studies/css-and-svg/
  title: Using SVG with CSS
---

# {{ page.title }}

{{ page.overview }}

## Summary

Dharmafly required an approach to documenting its project websites. These needed to be built to cover a number of colour themes and to be built from text only project documentation at a single click.

The sites should look good to developers using the ways of browsing the web developers use - modern browsers and modern devices.

## Approach

The requirements and intended audience for the websites meant that the site was built from a mobile first point of view. In practice, this means doing very little, as the web is [responsive by default](http://blog.andyhume.net/responsive-by-default/).

The key thing that is required is a device width

    <meta name="viewport" content="width=device-width,initial-scale=0.75">
    
Using the `viewport` meta allows devices such as the iPhone to distinguish between a standard site, that the device will scale down to fit within the smaller width of the device, and a site that intends to have its content fit into the device's width. This article covers [Safari's device scaling](http://developer.apple.com/library/ios/#documentation/AppleApplications/Reference/SafariWebContent/UsingtheViewport/UsingtheViewport.html)

If all sites were designed without fixed widths, this meta element would not be required and the device designers would not need to perform scaling on fixed width sites.

<figure class="marginalia marginalia-left">
<figcaption>View of this site on an iPhone first without and then with <code>width=device-width</code> specified in the meta viewport element </figcaption>
<img src="/images/4_16_device_width.png" alt="">
</figure>

I adjusted the initial scale to be slightly lower than `1`, due to the generous nature of the padding on the containing elements, this allowed for a broader [measure](http://en.wikipedia.org/wiki/Measure_(typography)) on the copy.

<figure class="marginalia marginalia-right">
<figcaption>View of a documentation site on an iPhone with <code>initial-scale=0.75</code> specified in the meta viewport element</figcaption>
<img src="/images/satya-iphone-big.png" alt="" class="image-default">
</figure>

## Floating navigations

Within a smaller device, the header as designed for the desktop would take up the vast majority of the user's screen. 

There were also two possible navigations. One would show the pages in the site, ususally 'overview' and 'reference', and the other would show, for example a list of functions to be documented for the project. The length or width of this could be considerable.

The initial approach was to have the left hand navigation 'disappear' at smaller widths, to be replaced by an icon. Clicking the icon would slide reveal the navigation. This is a fairly [standard pattern](http://codepen.io/sturobson/full/rAoBh).

This was implemented successfully, and is still present within larger width devices (go to [http://jquerypromises.com/](http://jquerypromises.com/) and reduce your screen width.)


The issue came with the permanently present navigation. As the page scrolls, navigation is set `position:fixed` as is the subnav. This is no issue for the main navigation, as it is centered using CSS. The subnav must tag along to the left hand edge of the main content on resize, so must be calculated using javascript.

<figure class="marginalia marginalia-left">
<figcaption>At a smaller device width, the icon is shown - clicking slides the content right, and fades in the subnav</figcaption>
<img src="/images/4_16_subnav.png" alt="" class="image-default">
</figure>

Due to the problematic [support for position fixed within iOS](http://remysharp.com/2012/05/24/issues-with-position-fixed-scrolling-on-ios/), let alone [with animated opacity](http://stackoverflow.com/questions/11507683/webkit-css-force-hardware-acceleration-for-2d-transforms-without-using-3d-css-p), we decided upon a completely different pattern. In a narrow width environment, the subnav is mapped to a hidden `select` dropdown element, and shown on click of the nav icon

<figure class="marginalia marginalia-right">
<figcaption>Subnav shown as select dropdown on a narrow width device</figcaption>
<img src="/images/4_16_dropdown.png" alt="" class="image-default">
</figure>

## Finessing the style

You might be wondering why I've not mentioned [media queries](http://www.w3.org/TR/css3-mediaqueries/) yet. 

Given that the site has a liquid layout and a viewport meta element defined, setting different styles at breakpoints is for little more than finessing the style. For example - the twitter links are represented by icons covered by an [SVG colour layer](/case-studies/css-and-svg/). 

They're just a list in the copy at smaller widths,

    aside li,
    .buttons .badge {
      float: left;
      margin-right: 1em;
      position:relative;
    }
    
![icons shown as a list in a narrow width browser](/images/4_16_stem_narrow.png)
    
but at larger widths, they grow out of the main content on an SVG 'stem'
 
    @media (min-width:52em) {
      aside {
        position: absolute;
        top: 3em;
        right: -10em;
        margin: 0;
        z-index: 5;
      }
      aside li {
        float: none;
        margin-right: 0;
      
    }

![icons shown on a decorative stem in a wider width browser](/images/4_16_stem_wide.png)

## Other techniques

These are just a couple of patterns and a couple of techniques for working around them. There are many other design patterns for [rearranging elements for device widths](http://bradfrost.github.com/this-is-responsive/patterns.html), and [techniques for adapting the layout](http://dbushell.com/2013/03/19/on-responsive-layout-and-grids/). 

Additionally, there are adaptive techniques for changing the content such as [changing the image `src` based on device width](http://nicolasgallagher.com/responsive-images-using-css3/).

I don't have one fixed approach to responsive web development, in this instance device width and an alternative design pattern were the required implementation.

{% assign related = page.related %}
{% include related.liquid %}