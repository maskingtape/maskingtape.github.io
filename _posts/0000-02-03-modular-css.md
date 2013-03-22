---
layout: default
category: articles
title: Modular CSS
related: 
- type: project
  url: /projects/4od-relaunch
  title: 4oD Website Relaunch for Channel 4
- type: article
  url: /articles/css-analysis
  title: Article - CSS Analysis
---

# {{ page.title }}

<p class="auth">Posted by <a href="mailto:dan@thoughtballoon.co.uk">Dan Eastwell</a> 20/03/2007, 20:17:00 GMT</p>

## Target Audience

* HTML/CSS Developers who are getting to the stage where they are building sites with dynamically loaded content with very many templates, rather than one-off static builds
* Project Managers who need to know what's technically involved in managing a build with more than one HTML/CSS developer, or on a project that's likely to have a scalable or modular front-end

## Summary

We've got to the stage where, in most cases, a Front-end Developer is recognised being a trade in its own right, and that accessible, semantic and cross-browser compliant sites are the norm. 

Most projects are normally well spec'ed out. Even in  Agile projects a specification of some kind usually exists. 

Designs are normally worked from wireframes of some description to Photoshop or Fireworks templates, to be passed to the interface developers.

The stage that may well be done informally is the analysis of all these documents to create a 'CSS architecture', a project plan for this work and a review of the integration of the generated CSS and HTML into any back end development.

The larger a project and the more complex it is the more there is a need for this form of analysis.

The more likely a site is to scale, and the greater the flexibility and modularity needed from the components within the site, the greater is the need, and the greater a need for some form of documentation of this process.

[This article](/articles/css-analysis) examines the relatively easy steps needed to analyse a set of design documents, and how to create a framework for CSS design that will allow for work to be split between developers and the dependencies it may create for any back-end development work, as well as the logical problems it will solve in order to reduce the burden on back-end developers.


{% assign related = page.related %}

{% include related.liquid %}