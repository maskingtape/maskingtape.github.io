---
layout: default
category: projects
title: "Survey Engine - A survey system for GAIN/IDS/USAID"
dates: "Jan - Feb 2013"
thumb: gain_sml.png
related:
- type: case-study
  url: /case-studies/formatting-json-for-html
  title: "Formatting JSON for HTML"
---

# {{ page.title }}


{{ page.dates }}

## Process

The project covered coverting an existing Excel spreadsheet into a single page survey - a worksheet enabling fieldworkers to review their work in agricultural projects and get recommendations.

[![Survey front page](/images/gain_big.png)](http://nutritiousagriculture-tool1.gainhealth.org/)

The original spreadsheet contained hundreds of questions, and was very weighty. Megabytes of data had to be sent to each fieldworker, who were usually working with limited bandwidth. The new app had to have the same quantity of questions, but be much lighter and additionally operate on older machines.

My role was to lead development on a small team. The solution was to create a general engine that would cater for standard question types and allow the hundreds of questions to remain separate in a JSON object. I had the task of working out a suitable data format so that non-technical staff were able to copy across the questions from the spreadsheet. This stripped the data down to about 300kb.

The engine had loaded this object, stepping through the questions, rendering the next question and storing the previous answer. Additionally users could store many copies, create and update new copies as they could do with the spreadsheet version. Upon completion, the survey could be sent back to GAIN, the survey owners to improve future research.

## Work covered

* Support for legacy browsers
* Microtemplating 
* Establishing a JSON format
* Javascript engine development
* pub-sub pattern implementation
* HTML5 APIs - localStorage
* UI module creation
* Print stylesheet creation
* BDD testing and integration testing

{% assign related = page.related %}
{% include related.liquid %}