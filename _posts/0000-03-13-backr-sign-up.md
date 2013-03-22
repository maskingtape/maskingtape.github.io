---
layout: default
category: projects
title: "Application: a registration system for Backr.net"
dates: "June 2012"
thumb: backr_sml.png
related: 
- type: case-study
  url: /case-studies/css-and-svg
  title: CSS and SVG
---

# {{ page.title }}

{{ page.dates }}

A single page sign up app, allowing users to choose a career path and pass this info on to Backr to set up mentoring. Now replaced with the live Backr.net site, see a [demo version of the site here](http://test2.thoughtballoon.co.uk/backr/).

<img src="/images/backr_big.png" width="490" alt="screenshot of the backr site showing a selected career network with joined circles containing related career information">

## Process

This site was built to enhnance an standard sign up form and to give a flavour of the final site, which allows young people to connect with experienced professionals for mentoring.

The solution was to construct the data for a single form over several 'pages'. The pages were compiled from a configuration object and templates with javascript - without, the user still gets the sign up form.

Users could fill in their desired career path, then be given a list of related careers displayed as a network. As these related careers were updatable and changed per use, the solution was to dynamically build the network using [underscore.js](http://underscorejs.org/) to draw the network elements using a mixture of SVG (rendered with [pablo](pablojs.com) and CSS generated content). 

## Work covered

* CSS techniques to draw generated content (squares, circles, triangles)
* Data import using YQL
* Parsing large data structures using underscore.js
* Dynamic SVG rendering

{% assign related = page.related %}
{% include related.liquid %}
