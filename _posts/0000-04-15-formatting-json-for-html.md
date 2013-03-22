---
layout: default
category: case-studies
title: "Formatting JSON for HTML"
overview: Generating a data object standard for creating surveys to be rendered in HTML
related: 
- type: project
  url: /projects/survey-engine
  title: A survey system for GAIN/IDS/USAID
---

# {{ page.title }}

{{ page.overview }}

## Summary

_When creating a data structure to describe what is to be rendered as HTML (using templates), consider the similarities in function and in structure in your intended HTML output. Ensure the grouping and styling of elements is not described in your data's structure._

## Brief

The brief for the [Nutritious Agrigulture project](/projects/survey-engine) was to take a list of questions then held in an excel spreadsheet and develop a one page survey accessible, with the ability to be stored and sent.

![Screenshot of a questionnaire within excel](/images/4_15_excel.png)

## Creating the details for the json

The survey contained a series of questions, whose outcome determined the next question to be answered or the next section to go to. The vast majority of the questions had a format that mapped directly to HTML form elements (`select`, `checkbox`, `textarea`). Some were vastly more complex, so required further thought.

### Considering the appropriate formats

Given the survey format, we could make a start on the interaction format. The excel version had all steps always visible, but with the greater flexiblity of javascript and CSS it would be trivial to either hide or render on demand the question not currently being answered.

The format chosen (based on a prototype created by [Premasagar](https://github.com/premasagar) for a different project) showed the current question and would render the next step based on the answer to the current question.

Once I had mocked up a [prototype of the interaction behaviour](http://gain-agriculture.dharmafly.com/templates/steps-prototype.html) for client review, I was better placed to establish the data format.

![Prototype of interaction behaviour](/images/4_15_prototype.png)

The data had to:

* Contain the question data
* Indicate the html format required
* Show what the next question or section would be and if this was dependent on an answer

### Allowing the json to have n-levels of depth

A problematic requirement was that each question could contan multiple form elements (e.g. name, organisation, survey name, etc). Another was that questions were contained in sections. What's more each section would be contained within a part. Each of these levels followed an outline numbering format (although not necessarily strictly).

Rather than specifically creating 'parts' or 'sections', we decided to allow any number of steps at any level - this way future questions could have 'sub-sections' for example, or any other way of grouping questions.

At the lowest level, there would be no more steps, so implicitly this would be where the questions lived.

This gave us a data structure of the following format:


    [ // An array of 'steps'
      { // step
        "id" : "0",
        "title" : "section one",
        "type" : "top-level",
        "steps" : [
          { // step
            "id" : "0.1",
            "type" : "mid-level",
            "steps" : [
              {
               "id" : "0.1.1",
               "type" : "question",
               "items" : [
                 { // item
                    "id":"0.1.1.1",
                    "label":"Survey Name",
                    "type":"input"
                 }
               ]
              }
            ]
          },
          { // next step
            "id" : "0.2",
            "type" : "mid-level",
            // ...
          },
          // ... 
        ]
      },
      { // following step
        "id" : "1",
        "type" : "mid-level",
        // ...
      },
      // ...
    ];

    

If the top level is an array of steps and this contains a `steps` array and its children can contain a `steps` array and so on... 

The lowest level contains an `items` array, although in hindsight, that might well have also been a `steps` array with no child `steps` arrays (if you see what I mean!).

The `type` attributes are arbitrary and are not referred to in the javascript - they're used to identify HTML templates so that a 'part' or a 'section' has appropriate styling applied by the CSS.

![Final version of the survey](/images/4_15_final.png)

### Templating

You can see from the data object above that the `items` array now lends itself almost directly to being rendered as HTML. 
    
    "items" : [
     { // item
        "id":"0.1.1.1",
        "label":"Survey Name",
        "type":"input"
     }
    ]

Each item has a label and a type. This can map quite directly to a series of HTML templates such as those used in [mustache](http://mustache.github.com/) or [tim](https://github.com/premasagar/tim), which we used.

Additionally this level of specification (`type` and `label` only) makes the data object simpler for someone non-technical to code (after a little instruction in valid JSON format), or to be automatically generated.

Here's the template for a text field:

    <script id="input" type="text/template">
      <div data-id="{{ id }}" data-required="{{ required }}">
        <label for="{{ id }}">{{ label }}</label>
        <input id="{{ id }}" type="text" value="{{ value }}">
      </div>
    </script>

You can see how presentational and structural elements such as the wrapping `div` can be updated without affecting the data.
    
#### Values for options

Some form field types, such as `select` and `radio`, require more than one input choice. To cater for this, I added in an `options` array.

    "items": [
      {
        "id":"2.1.1",
        "label":"Does the project promote increased availability?",
        "type":"radio",
        "options": [
          {
            "id":"2.1.1.1",
            "answer" : "Yes",
            "next" : "2.4.1"
          },
          {
            "id":"2.1.1.2",
            "answer" : "No",
            "next" : "2.2.1"
          }
        ]
      }
    ]

The format for `select` dropdowns is identical apart from the `type` value. This makes sense to me as even though the HTML for radio buttons and selects are so different, you are still (normally) just choosing one item from a list of mutually exclusive options.
        
## Why not use HTML templates rather than JSON?

In some cases, where the HTML was more complex than a simple list of standard HTML form types, I had to hold up my hands and create a `"type": "html"` . A `src` property mapped this to a microtemplate. 

However, in the case where we had form fields, the intended functions of many HTML form elements are so similar that the JSON describing them could be simple.

The HTML could be as arcane as it needed to be. For example, `textarea`s and `input type="text"`s both allow simple text input (as do `input type="checkbox"`s, albeit limited to boolean yes/no answers). `selects` and `radio` lists allow a choice from options. The HTML for these is wildly different in form, but that's not the concern of the data.

The outline levels in the original spreadsheet (parts and sections) were functionally identical ways of sectioning and grouping parts of data. I did not need to build any distinction between the levels other than to show depth (and to add a `type` property to be used eventually for styling).

## General principles to bear in mind (when you're creating a JSON object for HTML)

* Can it be updated easily (by non-technical staff or automatically)?
* How few attributes can be specified for a new item to still be valid? (preferably 'none' or maybe an id)
* Is it flexible enough to be extended (can you add in new types of items at any level)? 
* Can you add in new properties at any level?
* Can you add in new levels of depth easily?
* Is there anything about the your intended function for the HTML that can be generalised? (as for `input type="text"` and `textarea` - both are text input, so can be treated identically in the data)

{% assign related = page.related %}
{% include related.liquid %}