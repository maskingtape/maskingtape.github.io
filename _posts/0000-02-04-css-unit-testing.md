---
layout: default
category: articles
title: Unit Testing for CSS
overview: 
related: 
- type: skill
  url: /skills/css-html-development
  title: 4oD Website Relaunch for Channel 4
---

# Example CSS Style Guide - Unit Testing for CSS?

  <p class="auth">Posted by <a href="mailto:dan@thoughtballoon.co.uk">Dan Eastwell</a>
  Tue, 11 Nov 2008 21:00:00 GMT</p>
  <p>A quick example of a <a rel="nofollow" href="http://test.danieleastwell.co.uk/_fRefit08/_format/_templates/">CSS style guide</a> - I've been reading about <a href="http://docs.jquery.com/QUnit">unit testing for jQuery</a> and wonder if an analagous approach could be used on a CSS system.</p>
<p>Probably not, but a style guide featuring every type of box, unit, module and typographic style on the site can quickly allow you to not only see if any changes you make have knock-on or regression errors, but allow you to see what your styles imply.</p>

## An example style guide

<p>What do I mean? Well, if you have a particular form style, a style guide should have all form elements shown, even if they appear nowhere on your site - eventually, they will.</p>
<p>If you have a module style, what will it look like at different widths, and in combination with other similar boxes (even if you're building a fluid layout)? A style guide will help you find out and troubleshoot.</p>
<p>I've written about <a href="/articles/css-analysis">CSS systems analysis</a>, and am happy to find a kindred spirit in Natalie Downe in her article, which covers not only CSS systems analysis, but also the concept of <a href="http://natbat.net/2008/Sep/28/css-systems/">css style guides</a> in any documentation handover.</p>

{% assign related = page.related %}
{% include related.liquid %}