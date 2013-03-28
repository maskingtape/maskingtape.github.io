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
related_json:
- type: case-study
  url : /case-studies/formatting-json-for-html
  title: Formatting JSON for HTML
related_tdd:
- type: article
  url : /articles/testing-for-jquery-users
  title: Testing for jQuery Users
---

# {{ page.title }}

{{ page.overview }}

{% assign inline = true %}
## Javascript and related techniques
<ul>
<li>coding jQuery plugins</li>
<li>coding javascript as a framework </li>
<li>JSON</li>
<li>coding DOM traversal/manipulation without jQuery etc</li>
<li>Writing APIs/JSON contracts 
  {% assign related = page.related_json %}
  {% include related.liquid %}</li>
<li>Ajax</li>
<li>site performance optimisation (script deferring, injection, XHR, lazy loading, reflow/repaint optimisation)</li>
<li>structuring code for stateful (as opposed to static) user interfaces (applications not pages)</li>
<li>knowledge of patterns for namespacing javascript for web applications</li>
<li>Object-oriented programming, principles and practice</li>
<li>Pub-sub / Event models / event driven interfaces</li>
<li>JSONP, Coss-domain scripting techniques</li>
<li>Hashbang/onHashChange events</li>
<li>Working knowledge of other frameworks such as Prototype, mootools
</li>
</ul>

## Developer practice
<ul>
<li>Test Driven Development / Behavioural driven development 
  {% assign related = page.related_tdd %}
  {% include related.liquid %}</li>
<li>The ability to write code that scales</li>
<li>Pair programming </li>
<li>Write code with a view to the next developer (in naming and organisation)</li>
<li>Ability to refactor existing code effectively (to avoid regressions)</li>
<li>Debug/refactor as I go</li>
</ul>

{% assign inline = false %}
{% assign related = page.related %}
{% include related.liquid %}