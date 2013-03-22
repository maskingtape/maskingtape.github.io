---
layout: default
category: articles
title: "CSS Analysis"
related: 
- type: project
  url: /projects/4od-relaunch
  title: 4oD Website Relaunch for Channel 4
- type: case-study
  url: /case-studies/css-files
  title: Modularising CSS files
---

<p class="auth">Originally posted some time in 2005, updated 2013</p>

# Approaching CSS management on large-scale web projects

This article covers the steps that you might take in analysing the designs for a website and the techniques you might use to implement your analysis

## A nice set of documents

At the beginning of a large-scale web design project, if you're lucky, you'll be given a set of designs and a functional specification, describing how the website you are to build will look and what it will do.

If you're really lucky, you'll get a style guide, that will outline in detail how types of elements should look and their relationship to other elements.	For example, main headings are set at 1.5 times the size of sub-headings.
	
Given this set of documents, the CSS developer's job is then to mark up the different page templates so that they conform to the design, with neat semantic HTML and ordered CSS that keeps the coherence the designer intended in the design.

Any Front-End Developer who has worked on a larger site with templates that number in the tens (for enquiry forms, site maps, product pages, overview pages, hub pages, articles and so on) will find that it's quite a task leaping in and 'just getting on with it'.

The developer needs to analyse the proposed site for visual trends and sort the layouts and elements into a semantic outline with a cascade of style inheritance. This has been, in my experience, an informal, heuristic process - often a sole endeavour and rarely with any formal procedure and not necessarily documented: the CSS itself serves as documentation.

On larger projects, the methods used to create a hierarchy, cascade and documentation can follow a formal process.

## CSS Analysis

An analysis of the specifications will:

* reduce the time taken to code, as it will be modular so can be split amongst coders of a lower skill level without fear of them stepping on each others toes or reinventing the wheel on every page.
* reduce time taken fixing bugs. CSS analysis will lead to structured test pages and modular code will reduce the risk of high level changes having cascade effects.
* ease maintenance: better documentation and a greater ability to make changes at a high specificity without affecting other areas.


## Analysing the design 

There are several ways of analysing a design for a large-scale site. You will have your Nice Set of Documents, and you'll be looking to find trends within the design that will allow you to specify how the HTML and CSS will be structured.

The four methods of analysis I use are:

* semantic
* functional
* modular and
* stylistic

As I go, I'll create class names and write them on the specs and designs. I'll also write them _straight into the CSS file_. 

When you come to flesh-out the CSS you (or any other member of the team) can cross-refer the designs to your outline class names.
			
### From a semantic point of view

This analysis will help you structure your HTML documents. Looking at the design in 'outline' view, you should be able to point out all the `h1`s, the `h2`s, the lists etc.

Hopefully, all `h2` elements are styled in a certain way, if not, you'll be able to note that `h2` might look another way in this case, or in these circumstances.

If you are using HTML5, [finding an outline order becomes problematic](http://blog.thoughtballoon.co.uk/post/40841832951/about-html5-document-sectioning).

With the other methods, you'll be able to then structure the semantic elements within the layout of the page.

### From a modular point of view

Your site almost certainly will comprise several modules - an article, a short summary, a product and its description, a navigation, a breadcrumb trail. In all likelihood these will be styled uniformly, and can be easily described.

This form of analysis might form the backbone of the functional specification, or business requirements in a user story (if you're in an Agile environment) and it aims to modularise the system to make for quicker development and easier maintenance, as well as namespacing components. 

Modular analysis comes into play in creating HTML elements that correspond to the modules in the functional, and  possibly technical, specifications. If there are styling differences between modules in differing contexts, a higher level class should identify the context, or an additional class can specify further. (See <a href="http://css.maxdesign.com.au/selectutorial/selectors_class.htm">Maxdesign's Selectutorial</a> for a thorough overview of the topic and [Stubornella's thinking behind 'object oriented' CSS](http://blog.thoughtballoon.co.uk/post/99319876/stubbornella-blog-archive-object-oriented-css)).

### From a functional point of view

All instances of the item you're looking at do the same thing, so will be styled in the same way (make a note of any exceptions). 

This analysis should lead to results that are very close to any functional specification and may borrow thinking from any tech specs. 

You might ask how this form of analysis differs from analysis from a modular point of view? Well, yes, more often than not a functional component of a website is also a modular component: e.g. A search form at the top of every page, or an RSS fed list of blog entries, however, a functional website item can appear in several modules, so its styling needs to be considered accordingly. Examples would be: 

* All form elements
* Error messaging
* Link types (e.g. External links)

It's extremely likely that most form elements will look the same across the site (as this would make for a consistent user experience), but occasionally, they will differ in position, especially when in combination with other form elements: e.g. A label associated with a radio button may well be aligned differently to a textarea label. 

### From a stylistic point of view

This is the part of the analysis that should come directly from the style guide and source design documents (e.g. Photoshop or Fireworks). Hopefully, you'll have little to do converting the style guide into CSS.

Your analysis might cover:

* Fonts
* Colours and themes

* Text after elements (['vertical rhythm'](http://www.markboulton.co.uk/journal/incremental-leading))
* Margins and padding 
* Containing elements, columns, etc

The likely exceptions will probably be when elements are in proximity to other elements and their styling changes, for example the underlining or padding on the first or last element in a list of elements.

Another likely exception would be the styling of headings in different contexts: a heading 3 in a right hand column may well look less important (smaller font size, etc) than one in a main module, but still have the same level in the document hierarchy. Again, have a look at the issue of [document sectioning](http://blog.thoughtballoon.co.uk/post/40841832951/about-html5-document-sectioning)

## Sounds like a lot of work: how's this useful?

You might now suggest that with all the effort of writing your analysis up, you may as well have written the CSS. That's exactly what you'll be doing. I will write down the parts of the analysis in text documents, in CSS comments and with empty rules, with named selectors.

The return on your time investment comes in the future when components are added and unordered lists appear on the page in new and exceptional circumstances: you'll be able to cater for these changes.

On a larger site, the CSS/HTML analysis helps speed up development time, as modules can be handed across to developers (as exceptions can be handled by descendent selectors) before full pages are built, and time is saved in actual CSS development as less experienced coders will be able to take on sub-sections of the site.		
	
In terms of maintenance, you'll be able to come back to the site and understand your decisions, without necessarily having to use developer tools to reverse engineer what you've built.

## Dealing with exceptions

You may find that you are given a design with thematically strong styling: the typography is consistent, the styling devices, backgrounds and colours all follow a theme, but their relationship to functional modular items (e.g. A search box, a list of associated articles) varies across pages. This is obviously poor practice from a point of view of usability (you want the user to get 'used' to using certain items and sub-consciously expecting to see certain items in the same style) but it can and will occur. 

You may also find that the outline page hierarchy of headings and subheadings are styled differently on differing pages - a heading 3 may look like a heading 4 on other pages. You may at this stage want to put this to the designer, but you may well not have that opportunity. If so, the best thing is to have a rather clumsy looking long series of 'edge-case' examples in your CSS.

If, in the future, the next design needs to change all these items' colour, say, they will all be in one place. If, in the future, they are all standardised by their place in the outline page hierarchy, then you only need to comment out in one place.

Spending a few hours analysing designs can save you an immense amount if development, test, implementation and maintenance time in the future.

Ideally, you would want to pore over your supporting documentation, with your designs, flowcharts and wireframes posted up on your office walls and get everything sorted out on paper before commiting to a particular CSS/HTML build methodology, and then document your thought process. 

The task of allocating work to your front-end development team then becomes easier and the build process more straightforward.
It's as true with the front-end as it is anywhere else: a little bit of forethought can save you days overall.

{% assign related = page.related %}
{% include related.liquid %}