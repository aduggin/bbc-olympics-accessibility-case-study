# BBC Olympics Accessibility Case study

## Introduction to the product

### Scope of the Project

The most ambitious and comprehensive BBC digital project to date - 4 screen proposition - delivered to PC, tablet, Mobile and Connect TV

Grand vision - to deliver the first truly digital Olympics. Never miss a moment

Website built around the olympics domain - a page for every athlete, team, venue, sport and medal winning event.  Each with an index pages.

* 10, 000 Athlete
* 205 Countries
* 30 Venues
* 36 Sports
* 204 Medal Winning Events

Each of these pages displayed Facts and figures, latest news stories, image galleries, short form video clips, schedule, results and medals tables.

Other Page components including:

* Top Trump style comparison modules
* Twitter module
* Favourites Tray

Other sections and pages

* Interactive Video Player
	* 24 High definition live streams of content
	* 2500 hours of live coverage available on demand to all platforms
* Medals table
* Schedule and Results
* News Articles 

Over 100,000 pages in total
	
### Usage and Stats

We knew the website would be popular and receive a huge amour of traffic - don't think anyone expected the figure we got

	37 million UK browser - 66% UK online adult population
	57m global browser to bbc.co.uk
	111m video requests across all platforms
	
	7.4 million mobile browsers
	1.9m downloads of our Olympics smartphone app
	12m requests for video from mobile devices

## Accessibility at the BBC

The BBC has a duty to deliver big national events on behalf of the **whole population**.
 
Talk about

* Standards and Guidelines - Henny created a single document for all accessibility standards
* BBC Trust

First project I have worked on where accessibility has been made a real priority/requirement from the product owner at the start of the project.

May have had something to do with Australian 2004 olympics website and a belief that the website would be under close scrutiny


## The Aim

* Equivalent access for all
* Consistency in implementation across the site


## The challenges

Lots to build in a relatively short space of time

Immovable deadline

A 17 day event - huge traffic so code freeze during event

Dynamic website - don't get lots of the real data until the actual event

Design upfront with lots of javascript rich interactions

Incorporating features built by other teams

Lots of developers in lots of different teams
	London, Salford and external companies
	many new to BBC
	mixed knowledge of accessibility

BBC Standards and Guidelines not up to date - javascript, html5 and aria

A shortage of practical examples and support information. No single good accessibility resource that shares best practices that is easily digestible by developers and designers.

Many best practices still not really established. Very little shared research and observation - e.g what the best way to build a carousel.  There's a difference between making something technical accessible and intuitive/usable. 

## The Development approach

Thought about accessibility from the start

Spoke to specialists early - Ian and Henny

Digest and circulate BBC standards and Guidelines

Organised training

* Screenreader training - JAWS/NVDA
* Accessibile web applications training - javascript, aria and html5
	* Bespoke - used components that we were going to be building
	* Support forum

Trawl resources for accessibility knowledge and best practice

* blogs
* books
* web aim mailing list
* simply accessible q and a 
Wiki, Blog and Presentations to share round team / organisation

Set up a support network 

* Mentor new developers
* Set up an email list
* learning lunches - chance to review and discuss approaches

Review and feedback accessibility concerns early - to designers, developers and product owners

Agile methodology

* tackle features in priority order
* Push back on new features until core features complete - especially towards end of project

Library of elements and reusable components

* OOCSS - elements and common sub components. don't tie visuals to elements
* components that can be dropped into any page
	* First build the front end - HTML/CSS/JS
	* Then write php to render HTML
	* use static feeds so not dependant on real data
	* feeds feeds for all scenarios / varieties
* reuse leads to consistency, easier to test and maintain and pages that become quicker /easier to put together

Components

* http://www.test.bbc.co.uk/sport/olympics/2012/staticlibrary/are001-athlete-results
* http://www.test.bbc.co.uk/sport/olympics/2012/staticlibrary/h2h001-d-country-head-to-head-during
* http://www.test.bbc.co.uk/sport/ui/docs/top-stories
* http://www.test.bbc.co.uk/sport/ui/docs/pictogram-grid

Let front-end developers concentrate on the front end - php developers concentrate on back end.
		
Progressive Enhancement. Only use aria an an extra if needed.

Characteristics of accessibility
* Perceivable
* Operable
* Understandable
* Robust

Test early and often:

* Developers - browser tests
* Code reviews before merging into release branch 
* Red Bee
* Henny

## Implementation examples

### Page Template

	INSERT SCREEN SHOT
	
Used HTML5 so can validates with aria and data attributes

Skips links

Landmark roles to aid screen reader navigation

* banner
* navigation
* main
* complementary
* search ?
* contentinfo?

Lang attribute

Unique title

Unique h1


### Content Pages

#### Content

Make sure that content is in logical order - rather than thinking about the visual design

Example: [Featured Athletes](http://www.test.bbc.co.uk/sport/olympics/2012/staticlibrary/fea001-featured-athletes)

#### HTML AND ARIA

Add hierarchical heading structure - don't skip and heading levels

	SHOW OUTLINE OF A PAGE

Select most appropriate elements - e.g buttons, links, lists, tables. Ensure page is keyboard navigable and that assistive technologies can communicate content effectively

Don't over engineers or add too much aural clutter

	* heading inside lists
	* buttons inside lists

We didn't use any/many new HTML5 elements (e.g article/section) due to backwards compatibility and didn't use heading section nesting. May have used time element and placeholder attribute

Make sure links make sense out of context - visually hide extra content if needed
	
Don't duplicate links

	SHOW EXAMPLE

Make sure images have alt text when needed - but don't duplicate text

	SHOW EXAMPLE

Make sure tables marked up correctly

Make sure forms marked up correctly (especially for and id) and have buttons

We didn't use title attributes - shouldn't use for core content or duplicate other text already on page

Make sure visual feedback is available without visuals - e.g selected

#### CSS

**Take care not to introduce barriers**

Check for colour contrast

Set background colour swell as background image so can view text immediately

	DEMO MASTHEAD

Make sure that you implement keyboard focus as well as hover - don't use outline:none (check reset.css)

	DEMO SPORT NAV

Make sure fonts resizable and content still readable when font size increased.

	DEMO SPORT NAV

Only use display:none if want to hide from everyone. If hiding text only from visual users the move off screen or clip

	EXAMPLE: Athlete Head to Head
	<p class="blq-hide overview"> <span class="reference-name">Mo Farah</span> vs <span class="comparison-name">Nick Mccormick</span> </p>
	
	.blq-hide {
    	left: -2500px;
    	overflow: hidden;
    	position: absolute;
    	width: 1px;
	}
	
	ARE YOU TAKEN TO NEW CONTENT BY JS?

Only include visible controls in the tab order

	DEMO SPORT NAV

Make sure works with HTTP before implementing any javascript

If an image is decorative and doesn't contain editorial text then background image - NOT SURE IF TO INCLUDE THIS

### Interactive Components


#### Javascript

Where possible make sure everything works before you add javascript - Use progressive Enhancement.

Use aria if it will be useful

	EXAMPLE: Global nag
	aria-haspopup="true"
	aria-hidden="true|false"

Try to make it accessible without ARIA if you can due to limited support - e.g tabs

#### Forms need buttons 

 otherwise unusable by keyboard users.

	EXAMPLE: athlete a-z

##### Layout should work without javascript

	EXAMPLE: carousel

##### expandable content

* needs to be open if no javascript
* add button with javascript
* need to update the text button text to include open/close

	EXAMPLE: http://www.bbc.co.uk/sport/olympics/2012/sports/athletics

##### http before ajax

	EXAMPLE - top medals

http://www.bbc.co.uk/sport/0/olympics/2012/?mini-medal-table-type=athletes&mmt-go=go#medals-widget

##### update virtual buffer

Make inserted content (ajax) available to older screen readers -  

	EXAMPLE: Event Table with example javascript
	
[http://www.bbc.co.uk/sport/olympics/2012/sports/swimming/events](http://www.bbc.co.uk/sport/olympics/2012/sports/swimming/events)

#### keyboard focus 

Manage keyboard focus when inserting new content. Need to decide whether to take user to new content or inform them that new content has appears.

	EXAMPLE: Moving focus as simple as .focus()

#### Provide instructions for how something works

	EXAMPLE: Text moved off screen

#### Keep screen reader users informed about what is going on 

- loading content, new content available
	
	EXAMPLE: ARIA LIVE REGION

#### Keyboard traps

Make sure you can get to all content and that you don't introduce and keyboard traps

#### Keyboard control

if adding any keyboard control make sure it doesn't override any default browser or screen reader keyboard controls

### Medal Table

	ACTION: create video of Medal table
	
	ACTION: ASK ANDY/MATT HOW MANY VISITS THE MEDAL TABLE GOT
	
Our most shared page - over 11K shares

Used Hijax - http before ajax

Built to work without javascript. Good as means you deliver a basic/core version quickly - if you run out of time you still have something that work.  Also if there is an error it will still work. This actually happened during the olympics. A stray coma on international pages meant javascript failed.  However pages still worked.
Also means that you can bookmark and email a page to friends

Most appropriate markup 

* th for countries 
* scope
* caption
* summary


Logical Content order - go to any page without javascript and the content is in logical order.

Identify which content is selected in content layer as well as visual layer.

Keyboard short cuts to be able to jump to next table etc

Alt for medal images

Visible active state for keyboard users

Inform users that content loading - aria live region

Users taken to loaded content

	WRITE UP ANY OTHER ACCESSIBILITY FEATURES IN MEDAL TABLE
	
Using the History API to update the url (so users can bookmark and email)

Design wanted styled scroll bars. Only possible to implement cross browser by using javascript to create fake scroll bars.  Pushed back - said we will only do it in webkit as only browsers with css support
	
	CREATE A SCREENSHOT TO COMPARE


### Add to Favourites

	READ UP ON 'ADD TO FAVOURITES' IN FORUM AND EMAILS
	
	SPEAK TO TIAN ASK ABOUT ACCESSIBILITY OF FAVOURITES
	
dialog

* set focus to dialog when it opens
* make sure there is a close button
* make sure it closes with the ESC key

aria-labelledby and aria-describedby?

### Schedule

Presented in multiple ways - Grid view and list view (simpler layout)

	ASK HENNY IF SHE WANTS TO TALK ABOUT THIS

### Animations

Made sure where at the bottom of the page to minimise distraction to users reading text

Only cycled once ()when area came into view) - had a replay button for those that wanted to.


## Mistakes and solutions

	@ACTION - READ EMAILS WITH HENNY DURING THE OLYMPICS
	
	@ACTION - FIND RED BEE REPORT
	
	@ACTION - TALK TO SAM

* Featured countries - content not in logical order, multiple links. Wrong heading structure
* Aural clutter wrong wrong elements 
	* More from - from headings inside lists - removed lists.
	* [Coverage Promo](http://www.test.bbc.co.uk/sport/ui/docs/coverage-promo) - nested lists
* carousel - used field set, legend and button in links (over engineered).  Added role="presentation"
* Favourite Button - a span changed to a button
* Peeking navigation - on click handler for next and previous on arrow keys. Removed.
* Twitter module - infinite scroll, no way to exit for a keyboard user. Added link to exit.
* Couldn't play video using a keyboard. Added a link to play the video.
* Olympic Powers - had to make lots of fixes! Fixed validation issues, heading structure and added keyboard focus.
* Colour contrast - red bee report


## Stuff that got through / Compromises

Did we do everything perfectly?  Of course not.

* Over engineering semantic mark of early components - athlete facts and 2012 table.
* Team GB country page - different design, different content order
* Medal tables - colour used to distinguish medals
* More from heading links same colour as text
* Auto suggest not screen reader friendly - no supported in query ui - should be now.
* Live tables - didn't have ability to turn off auto update
* Non semantic markup in results sections. .caption etc
* No transcripts for video - was there any? iPlayer?
* editorial info graphics


## Lessons

Think about accessibility early. Much easier to implement accessible from the start rather than refactor at the end.

Turn to experts when you need some advice.

Lack of known best practice - even for simple/common things - e.g
	
* how to use lists and headings
* carousel

Many ways to implement something - don't know the best way or if accessibility has been achieved without testing it - but testing with  a range of people and devices is time consuming and expensive. 

Easy to over engineer things

Compliance != accessible. E.g how many screen reader users what aria is - and that they can use arrow keys etc. We chose not to use aria when we didn't have to - e.g carousel that you tab through (as you would a normal set of links).

Discoverability - if you add keyboard shortcuts how does a user know about them. Can't assume that all disabled users are power users that fully know how to use there device - where that be a browser, a screen reader or a smartphone.

Easy to introduce accessibility barriers - at every step.

Progressive enhancement is key.

Thorough accessibility knowledge not as widespread amongst developers as one would hope. Can't assume that other team members share understanding of accessibility.



Most accessibility issues are due to ignorance not carelessness or spite. Most people simply don't understand the implications of how they design or code something.

Design aesthetics often trump accessibility requirements - e.g medal via colours

Most front end developers are keen to learn a better/accessible way of doing something - this knowledge just needs to be better well documented and findable.

Don't need to compromise aesthetics or functionality to achieve accessibility

Accessibility comes through diligence and attention to detail. Need to have everyone onboard as it's incredible easy for someone to accidentally introduce an accessibility barrier or usability issue.

You can make javascript accessible - and it can actually the improve the usability of a page for assistive technology users - e.g partial page refresh instead of full page refresh.

Aria not as well supported as you would expected - and support not well documented

There will be compromises - things won't be perfect

Feedback early when you sport accessibility issues (esp design)  - be strong enough to refuse to do something if people not listening


## Conclusion

To make a website truly accessible buy-in is required from editorial, design and developer
Developers should implement sites/features using progressive enhancement
You only know if you have achieved accessibility by observing real users.
More research and observation needs to be carried out and shared.

Would help if we have common design and implementation patterns - like iOS components. Every app comes with a degree of accessibility when using default components - and works in the same way for all users.


---



# Notes on Components

## Nav bar

Resizeable

role="banner"

olympic sports > non-us 'sports' page

## Add to favourites

Javascript only

Made team change span to a button

## Event Table

[http://www.bbc.co.uk/sport/olympics/2012/sports/swimming/events](http://www.bbc.co.uk/sport/olympics/2012/sports/swimming/events)

---

# Resources

## Links

* [sportui component Library](http://www.test.bbc.co.uk/sport/ui)
	* [elements](http://www.test.bbc.co.uk/sport/ui/docs/elements)
	* [columns](http://www.test.bbc.co.uk/sport/ui/docs/columns)
* [sos component library](http://www.test.bbc.co.uk/sport/olympics/2012/staticlibrary)
* [TGP Accessibility Forum]()
* [Browser Based Tests](https://confluence.dev.bbc.co.uk/display/accessibility/Browser+based+tests)
* [Building a webpage with accessibility and interoperability in mind: part 1](http://alistairduggin.co.uk/blog/accessibile-interoperable-webpage-1/)
* [Confluence - Alistair Duggin accessibility](https://confluence.dev.bbc.co.uk/display/~alistair.duggin/Home)
	* [Accessibility, Aria and screen readers](https://confluence.dev.bbc.co.uk/display/~alistair.duggin/Accessibility%2C+Aria+and+screen+readers)
	* [Accessibility - bad and good examples](https://confluence.dev.bbc.co.uk/display/~alistair.duggin/Accessibility+-+bad+and+good+examples)
	* [Accessibility Best Practices](https://confluence.dev.bbc.co.uk/display/~alistair.duggin/Accessibility+Best+Practices)
	* [Accessibility Testing](https://confluence.dev.bbc.co.uk/display/~alistair.duggin/Accessibility+Testing)
	* [Accessibility - web components](https://confluence.dev.bbc.co.uk/display/~alistair.duggin/Accessibility+-+web+components)

## Articles
* [BBC INternet Blog - BBC Sport](http://www.bbc.co.uk/blogs/bbcinternet/sport/)
	* [Delivering the Digital Olympics: a programme management perspective](http://www.bbc.co.uk/blogs/internet/posts/olympics_product_development) 5 Nov, Mark
	* [Audio and Video Streaming the Olympics](http://www.bbc.co.uk/blogs/internet/posts/audio_video_stream_olympics_tech) 16 Aug, Marina
	* [More traffic, more videos, more screens: building the BBC's Olympic site](http://www.bbc.co.uk/blogs/internet/posts/building_olympic_website) 16 Aug, Matt
		* [2012 Programme: Architecture Diagram](http://www.bbc.co.uk/blogs/bbcinternet/2012/08/21/2012_Architecture_Overview_Diagram_20120727.pdf)
	* [Olympics: Red Button](http://www.bbc.co.uk/blogs/internet/posts/olympics_red_button_and_connec) 14 Aug, Aaron
	* [The story of the digital Olympics: streams, browsers, most watched, four screens](http://www.bbc.co.uk/blogs/internet/posts/digital_olympics_reach_stream_stats) 13 Aug, Cait
	* [From starting gun to smartphone: delivering the Olympics to your device](http://www.bbc.co.uk/blogs/internet/posts/data_video_flow_olympics) 7 Aug, Cait
	* [Digital Olympics: week one in numbers](http://www.bbc.co.uk/blogs/internet/posts/olympic_statistics_traffic_week) - 3 Aug, Cait
	* [Building the Olympic Data Services](http://www.bbc.co.uk/blogs/internet/posts/olympic_data_xml_latency) 1 Aug, David
	* [Olympic Data Services and the Interactive Video Player](http://www.bbc.co.uk/blogs/internet/posts/olympic_data_services_and_the) 31 July, Oli
	* [Record breaking start to the Olympics for BBC Online](http://www.bbc.co.uk/blogs/internet/posts/online_olympics_traffic) 30 Jul, Cait
	* [BBC Olympic App on Android and iPhone](http://www.bbc.co.uk/blogs/internet/posts/olympic_app_android_iphone) 13 Jul, Lucie
	* [Olympics: User Experience and Design](http://www.bbc.co.uk/blogs/internet/posts/olympics_design)
	* [Launch of Live Interactive Video Player](http://www.bbc.co.uk/blogs/internet/posts/interactive_video_player_launc) 29 June, Alex 
	* [Olympic Favourites](http://www.bbc.co.uk/blogs/internet/posts/olympic_favourites) 29 Jun, Andy
	* [Sports Refresh: Dynamic Semantic Publishing](http://www.bbc.co.uk/blogs/bbcinternet/2012/04/sports_dynamic_semantic.html) 17 April, Jem
	* [Delivering the digital Olympics: 24 live streams via the red button](http://www.bbc.co.uk/blogs/bbcinternet/2012/04/olympics_24_streams.html) 3 April, Phil
	* [The BBC's approach to streaming the digital Olympics](http://www.bbc.co.uk/blogs/bbcinternet/2012/03/the_bbcs_approach_to_streaming.html) 30 March, Richard
	* [Sport Olympic Service Update](http://www.bbc.co.uk/blogs/bbcinternet/2012/03/sport_olympic_service_update.html) 28 March, Andy
	* [BBC Sport: Olympic page launch](http://www.bbc.co.uk/blogs/bbcinternet/2012/02/bbc_sport_olympic_page_launch.html) 8 Feb, Cait

## Videos

* [BBC WiE: Cait O'Riordan and Lucie Mclean on the digital Olympics](http://www.youtube.com/watch?v=zQg_GSb6fUY)
* [BBC Fusion Seminar: London 2012 - Alistair Duggin](http://www.youtube.com/watch?v=c1n_Btq2_5o)
* [BBC Fusion Seminar: London 2012 - Cait O'Riordan](http://www.youtube.com/watch?v=HE9NbqYTz3A)