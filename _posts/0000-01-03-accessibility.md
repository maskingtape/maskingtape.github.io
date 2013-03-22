---
layout: default
title: "Accessibility"
category: skills
related: 
- type: project
  url: /projects/4od-relaunch
  title: 4oD Website Relaunch for Channel 4
---

# {{ page.title }}

I aim to make my web sites as accessible as possible. Done correctly accessibility should be invisible to all users.

This is for several reasons, not least to allow accessibility for disabled users, but to ensure a meaningful experience in many situations.

## Access in Less Than Perfect Situations

You can't assume every user has a high resolution screen and a broadband connection. There's a chance that users might be receiving content:

* on a slow connection or with limited data allowance (3G or dial-up)
* with a lower quality or non-colour screen
* without the use of a mouse (especially on devices)
* not necessarily in an office environment
* and using older browsers.

I achieve this using a separation of the content on the page and the styling, writing content first. 

I also use semantic markup - this means, for example, that headings are labelled as such in the code. All pages are written to [W3C standards](http://validator.w3.org/docs/why.html).

## Accessibilty Services

* Advanced Accessibility - implementation techniques, support, testing, user agents (screenreaders, speech controlled), user inexperience/unfamiliarity
* WAI-ARIA 
* Advanced keyboard accessibility (for javascript applications)

{% assign related = page.related %}
{% include related.liquid %}