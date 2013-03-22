---
layout: default
category: projects
title: "4oD Website Relaunch for Channel 4"
dates: "February 2010 - October 2011"
thumb: 4od_sml.jpg
related: 
- type: article
  url: /articles/modular-css
  title: Modular CSS
- type: article
  url: /articles/css-analysis
  title: CSS Analysis
- type: case-study
  url: /case-studies/css-files
  title: Modularising CSS files
---

# {{ page.title }}

{{ page.dates }}

For the [4oD relaunch](http://www.techradar.com/news/internet/channel-4-gets-personal-with-4od-relaunch-1000806) I worked as a Front End senior developer closely with the external designers and the internal engineers. The site got a complete rebuild and redesign, and included new personalisation features.

<img src="/images/4od_big.jpg" width="490" alt="screenshot of the 4od site, showing open custom dropdown">

## Process

This was a great project to be involved in. Designed by the Ostmodern agency and developed by an in-house team (comprising four front end developers), we quickly prototyped a fairly high fidelity version of the initial mock-ups. These were very helpful in working out interaction and user experience with the designers.

The work was completed in an Agile environment, and functionality was iteratively integrated into the framework - it was essential that the code, especially the CSS was modular and flexible enough to cope with placement in any context and with varied page load orders and any number of unknown third party scripts.

My process was to conduct a workshop with the front end team looking over the designs and grouping the modules that are likely to be used across the site straight into a new stylesheet.

By the end of the first afternoon, we had an outline for the whole site and the modules were then fleshed out and deployed across the site sections.


## Work covered

* HTML, CSS (modular) and JavaScript (OO, DRY, unit test covered with jsTestDriver) quality and consistency in 4oD and Programmes website areas in Java/spring environment
  <ul class="related">
    <li class="related-item skill"><a href="/skills/css-html-development">Skill - CSS / HTML Development</a></li>
  </ul> 
* Accessibility of all 4oD pages and widgets (screen-readers, voice, keyboards). AA standard.
  <ul class="related">
    <li class="related-item skill"><a href="/skills/accessibility">Accessibility</a></li>
  </ul> 
* Cross-browser consistency and progressive enhancement	
* Front-end advocacy during the 4oD redesign period in stakeholder meetings
* Cross-site consistency 
* Work with internal and [external designers and UX](http://www.ostmodern.co.uk/4od/)
* Tasks and bug management for front-end team in Agile environment with Continuous Integration
* Created Object Oriented jQuery plugins in MVC format
* Introduced HTML5 to 4oD site. Made use of APIs and attributes 
* Managed the modular CSS structure

{% assign related = page.related %}
{% include related.liquid %}