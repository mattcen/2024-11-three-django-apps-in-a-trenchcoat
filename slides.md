---
#type: slide
title: "Three Django Apps in a Trenchcoat: Writing an event management website with not a lot of time"
slideOptions:
  theme: white
  transition: none
  hash: true
  hashOneBasedIndex: true
  controls: false
  slideNumber: 'c/t'
  totalTime: 1500
  defaultTiming: 10
  minimumTiming: 5
  autoSlideStoppable: false
  plugins:
  - RevealMarkdown
  - RevealHighlight
  - RevealSearch
  - RevealNotes
  - RevealMath
  - RevealZoom
attributes: '<!-- data-autoslide="0" .slide: data-visibility="hidden" -->'
---

<!-- .slide: data-autoslide="10000" -->

## Three Django Apps in a Trenchcoat

### Writing an event management website with not a lot of time

- Matt Cengia (they/them) -- [blog.mattcen.com](https://blog.mattcen.com)
- Luke Byrnes (he/him) -- [ekulbyrnes.github.io](https://ekulbyrnes.github.io)

<!--
- Email: mattcen@mattcen.com
- Mastodon: [@mattcen@aus.social](https://aus.social/@mattcen)
- Bluesky: [@mattcen.com](https://bsky.app/profile/did:plc:3k4jsgseos5zo7mln3xq7na4)
- Matrix: [@mattcen:mattcen.com](https://matrix.to/#/@mattcen:mattcen.com)
- Website: [blog.mattcen.com](https://blog.mattcen.com)
- Slides: https://github.com/mattcen/2024-11-three-django-apps-in-a-trenchcoat
-->

License: [CC-BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)

Note:

- I'm Matt (they/them)
- Find me by handle, M A T T C E N
- Slides available on GitHub: <https://github.com/mattcen/2024-11-three-django-apps-in-a-trenchcoat>

---

<!-- .slide: data-autoslide="20000" -->

## Acknowledgements

Note:

Luke <!-- .element: style="color: blue" -->

I'm delivering this presentation on the unceded ancestral lands of many Indigenous peoples.
I honour the knowledge, stewardship, and care with which they've tended this land throughout history, and recognise the deep and lasting damage that colonisation has inflicted on them.
I pledge to do my best to respect, learn from, and support these peoples. We can all do better.

---

 <!-- .slide: data-autoslide="20000" -->

## Slides

[![https://github.com/mattcen/2024-11-three-django-apps-in-a-trenchcoat](images/slides_url.svg)](https://mattcen.github.io/2024-11-three-django-apps-in-a-trenchcoat)

---

<!--
- Distill each slide down to a heading of some sort
- Add (placeholders for) images where appropriate
- Elaborate on what we want to say in the speaker notes
- Potentially add code examples and/or screenshots
- Stretch goal: Add enough info to speaker notes such that a reader would be able to get the talk content by just reading the slides
-->
Note:

1. We're Scout leaders - we facilitate young people to explore the world with an ethos of Learning by Doing that is Youth Led, Adult Supported.

---


Note:

a. We don't just do fun things outdoors, but we also provide events like ScoutHack and teach Web Dev (see our lightning talk/Matt's talk).

---

Note:

b. We also run immersive STEM-themed camps. We call it Star Trek: Survival.

----

Note:

i. Instead of using a round-robin or "Track-based" program, we decided to have fun with radios and go agile.

----

Note:

ii. Participants told us their activity preferences, and we yeeted this into our software to make sure everyone did something they asked for to support their badge projects.

----

Note:

iii. 250 Scouts were each given their own radio (a choice so poor we've done it twice now), and they received their marching orders to attend their next activity from "Starfleet Command".

----

Note:

iv. All they had to do now was Check In to activity - do activity - Check Out of activity - Next activity. Food and sleep also occur in designated times and areas.

---

Note:

2. To support such insanely ambitious plans, <del>Luke schmoozied up to Matt</del> we very much relied on custom developed apps to:

---

Note:

a. inform participants of the awesome activities on offer

----

Note:

i. a website for STS

---

Note:

b. register participants in a way that protects data, offers quality UX, provides transparency for guardians

----

Note:

i. a registration system, named after the very first Scouting campsite, Brownsea

---

Note:

c. gamify the distribution of participants across activity sites in a dynamic way that considered preferences for individuals and their activity team

----

Note:

i. a despatch system, RadioActiv8, a play on the words Radio, Active, and the totes hip spelling with a number like all the cool kids do. #toTaLHacKeRbRo

---

Note:

3. To do this we needed three apps in a trenchcoat and a way to rapidly deploy should everything fall over like it did 2 hours after Day 1 started.

---

Note:

a. [ALL] Docker images means that we have a standardized operational environment. Say what you will about micro services being irritating but it does the job effectively.

---

Note:

b. [ALL] One project to <del>rule</del> host them all - using apps in Django. <maybe show some code?>

---

Note:

c. [BRN] Verify and pre-fill:

----

Note:

i. using membership validation to prefill and prompt updating of personal contact information

----

Note:

ii. Less is more - only gather what is needed; heath records have a dedicated confidential information system, so only catering basics are required.

---

Note:

d. [BRN] Provide both guardians and Scout leaders who are responsible for youth access to registration information for individuals.

----

Note:

i. legal guardians can see their child's data

----

Note:

ii. Scout Leaders can see their Youth Member data (to which they *should* already have access through member records).

---

Note:

e. [BRN] Event administration is handled by authorised personnel using the Django Admin backend framework.

----

Note:

i. conveniently, this is already built and was a breeze to customise and to enable bulk field editing.

----

Note:

ii. Exfiltration of data was limited to Super Users for the purposes of providing catering summaries to our Kitchen staff, and our event communications teams as required. Again, less is more.

---

Note:

f. [STS] Delegated access to program information control by using Wagtail CMS for activity content - STS missions.

----

Note:

i. reduces the overhead on git/VCS commit proficiency for maintaining website changes by giving program specialists the ability to edit specific event website content areas, such as the missions.

---

Note:

g. [RA8] Minimize JS by using the impressive capabilities of HTMX.

----

Note:

i. Single programming language for backend Dev avoiding bespoke or customized areas where, ordinarily, JS would feel like the _only_ way to solve a particular problem.

---

Note:

h. [RA8] Leveraging AJAX to update information on a realtime dashboard to give up-to-date information without refreshing

----

Note:

i. Allows for logical decision making without having to consciously think about refreshing to gain the latest information of the status.

---

Note:

i. [RA8] Use a live dashboard to show the states of change to radio operators.

----

Note:

i. Helps despatchers to make operational decisions by showing: Base Capacity, Last reported Location, Last time seen.

---

Note:

j. [RA8] Pre-populate Route/Time estimates between bases

----

Note:

i. Helps make smart decisions - do you send the 5 year olds on a 1km journey uphill 20mins before lunch? No. Older Scouts? Yes.

---

Note:

k. [RA8] Use GeoDjango to add geospatial integration to help with mapping.

----

Note:

i. Speaking of maps...\*show gamified map\*

---

Note:

# Potential questions

- Why not PHP/Laravel, or some other framework/language
- Why not Node/Javascript
  - One programming language is enough
  - Set out to do as much as we can without JS or another language
- Why Docker as opposed to "bare metal"/VM
  - Lift and shift
  - Scalability
  - Ref needing to migrate STS website at the 11th hour
