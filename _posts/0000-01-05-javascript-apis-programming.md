---
layout: default
category: skills
title: "Javascript and Development"
overview: Javascript, good developer practice and programming techniques
related:
- type: project
  url : /projects/survey-engine
  title: A survey system for GAIN/IDS/USAID
- type: case-study
  url : /case-studies/formatting-json-for-html
  title: Formatting JSON for HTML
---

# {{ page.title }}

{{ page.overview }}

## Javascript and related techniques

* coding jQuery plugins
* coding javascript as a framework 
* JSON
* coding DOM traversal/manipulation without jQuery etc
* Writing APIs/JSON contracts 
  <ul class="related">
  	<li class="related-item case-study"><a href="/case-studies/formatting-json-for-html">Case study - Formatting JSON for HTML</a></li>
  </ul>
* Ajax
* site performance optimisation (script deferring, injection, XHR, lazy loading, reflow/repaint optimisation)
* structuring code for stateful (as opposed to static) user interfaces (applications not pages)
* knowledge of patterns for namespacing javascript for web applications
* Object-oriented programming, principles and practice
* Pub-sub / Event models / event driven interfaces
* JSONP, Coss-domain scripting techniques
* Hashbang/onHashChange events
* Working knowledge of other frameworks such as Prototype, mootools

## Developer practice

* Test Driven Development / Behavioural driven development 
* The ability to write code that scales
* Pair programming 
* Write code with a view to the next developer (in naming and organisation)
* Ability to refactor existing code effectively (to avoid regressions)
* Debug/refactor as I go

{% assign related = page.related %}
{% include related.liquid %}