---
layout: default
category: case-studies
title: "Using SVG with CSS"
overview: 
thumb: 4_13_sml.png
related: 
- type: project
  url: /projects/satya
  title: A Documentation system for Dharmafly
- type: skill
  url: /skills/emerging-technologies
  title: Use of Emerging Web Technologies
---
  
# {{ page.title }}

Images are great, but have their limits. There's a certain amount of time involved and software required to update images. It would be useful to be able to update images directly in a text file. 

Images are often used for decorative graphic devices on websites (such as icons, complex decoration). In terms of accessibility it's trivial to [add an empty alt attribute](http://alistapart.com/blog/post/on-alt-text), but even that [technique is contentious](http://www.webaxe.org/leave-accessibility-to-experts-please/).

SVG within CSS provides an easily updatable text version of any vector-based decorative imagery. This was the technique used on a [documentation template system](/projects/satya) to allow colour updating across themes for graphical elements.

## Main decorative elements

![SVG elements applied to a page and rotated, reflected](/images/svg-items.png)

The main decorative element seen above was exported from illustrator, then cleaned up witin [google's SVG editor](http://svg-edit.googlecode.com/svn/trunk/editor/svg-editor.html). These were used for each theme were used multiple times: rotated, duplicated, lightened and flipped and scaled. 

However, the multiple uses did not require three seperate HTML elements with separate requests, nor any editing, the changes were completed using CSS `transform` on an SVG element set as a background image:

    background-image: url(./svg/node_sundae.svg);
    transform: rotate(61deg); 
    /* and proprietory prefixes */

With an image this would have been equally possible, however the SVG will perform much better with scaling, being based on vectors rather than bitmaps. Additionally, the colour of the element can be set server-side within the SVG file, in the same way as is possible within HTML.

There is no redundant HTML element required in the code, as a generated CSS element is used to hang the SVG elements off.

Admittedly, this still feels like something of a hack - we should be able to [include the SVG file directly](http://css-tricks.com/using-svg/), and then access the SVG nodes within the DOM using CSS, however we have to include the SVG within the document and it can't be reused or cached as an 'asset'.

Adding less complex decorative elements
----------------------------------

The graphic element shown above is relatively complicated, its SVG weighs in at a few kb, so it's advantageous to cache it. Less complex elements like the underlines (a line and a disc) come out at a few lines of SVG, so it seems of more benefit to avoid the HTTP request in fetching the SVG or image as a file.

My immediate thought was to use a [data URI](https://developer.mozilla.org/en-US/docs/data_URIs). Would it be possible to place an SVG element within a CSS `background-image` `url` value?

Chrome supports unencoded data URIs as `url`s for `background-image` CSS properties as follows

    'data:image/svg+xml;utf-8,<svg width="33" height="34" xmlns="http://www.w3.org/2000/svg"><line y2="31.5" x2="30.5" y1="2.5" x1="2.5" stroke-width="5" stroke="#000000" fill="none"/></svg>'
    
Unencoded data URIs are not supported by Firefox, so initially the data-uri was encoded using base64. Base64 is not human-readable, of course. Readibility was one of the reasons for choosing SVG over images to allow easy updating. 

As shown in this article, [SVG data URIs can be escaped](http://stackoverflow.com/questions/11703541/using-a-data-encoded-svg-as-a-css-filter) providing a (partially) readable version of the SVG. 

    'data:image/svg+xml;%3Csvg%20width%3D%2233%22%20height%3D%2234%22%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%3E%3Cline%20y2%3D%2231.5%22%20x2%3D%2230.5%22%20y1%3D%222.5%22%20x1%3D%222.5%22%20stroke-width%3D%225%22%20stroke%3D%22%23000000%22%20fill%3D%22none%22/%3E%3C/svg%3E'

Escaped URIs can be unescaped easily in the browser console, but unlike base64 don't require unescaping in order to be edited.

Colour changes with Liquid or SASS
----------------------------------------

The key benefit of using SVG background images within the site CSS, was to allow colour changes with a site theme. 

[Jekyll](https://github.com/mojombo/jekyll/)/[Liquid](http://liquidmarkup.org/) was used to create the documentation websites as outlined in this [article on the documentation project](/projects/satya). The site uses Jekyll to declare colour variables in a theme file that are then added to any site's CSS as Liquid tags. 

For example in the theme file you have `link_colour: "#2f4430"`, which is evaluated in the main CSS file via the template tag. The same is possibly using SASS or any other preprocessor:   
  
    a {
      color: {{ "{{ page.link_colour " }}}};
      text-decoration:underline;
    }

    
This means that creating differing coloured graphical elements is possible with SVG data URIs in a way that is not possible with static images (line breaks added for readability).

<pre><code>
background-image: url('data:image/svg+xml,%3Csvg
%20width%3D%22403%22%20height%3D%228%22%20xmlns
%3D%22http%3A//www.w3.org/2000/svg%22%3E%3Cline
%20stroke%3D%22%23<span style="color:red">{{ "{{ page.subnav_color " }}}}</span>
%22%20stroke-width%3D%222%22%20x1%3D%224%22%20y1%3D
%224%22%20x2%3D%22400%22%20y2%3D%224%22%20/%3E%3C
circle%20fill%3D%22%23<span style="color:red">{{ "{{ page.subnav_color " }}}}</span>
%22%20cx%3D%224%22%20cy%3D%224%22%20r%3D%224%22
%20/%3E%3C/svg%3E');
</code></pre>

Not where I'd ideally liked to have been, but the graphica elements are now added to the page without an HTTP request, and can be colour themed per template, without recourse to image editing software.


SVG grayscale filter and overlay
-------------------------------

What might formerly have been done in Photoshop and exported as an image can now be completed using SVG. 

![Steps to reproduce image style from Photoshop](/images/ColourOpacity.png).

Firstly an SVG filter was created to set the background image greyscale,

    filter:url(data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%3E%3Cfilter%20id%3D%22desaturate%22%3E%3CfeColorMatrix%20type%3D%22saturate%22%20values%3D%220%22/%3E%3C/filter%3E%3C/svg%3E#desaturate);

unescaped:

    <svg xmlns="http://www.w3.org/2000/svg">
      <filter id="desaturate">
        <feColorMatrix type="saturate" values="0"/>
      </filter>
    </svg>
 
(and natively in webkit:)

    -webkit-filter: grayscale(1);

then the semi-transparent colour overlay is applied as an SVG circle, with `rgba` background and a solid stroke. The overlay should transition out on hover.

Full [demo here](http://jsfiddle.net/daneastwell/wVmc4/5/).

<!--  Add placeholder, click to view with js
<iframe style="width: 100%; height: 300px;" src="http://jsfiddle.net/daneastwell/wVmc4/5/embedded/result,html,css" allowfullscreen="allowfullscreen" frameborder="0">&nbsp;</iframe>
-->

The only asset required from photoshop was a single sprite file - for each them the colour overlay is added via SVG.

Examples project themes be viewed in the sidebar on: [jQuery.promises](http://jquerypromises.com/), [jsonpatch](http://jsonpatchjs.com/) and [Pablo](http://pablojs.com).

{% assign related = page.related %}
{% include related.liquid %}