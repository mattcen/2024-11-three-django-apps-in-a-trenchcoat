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

Matt Cengia
(they/them)

[blog.mattcen.com](https://blog.mattcen.com)

<!--
- Email: mattcen@mattcen.com
- Mastodon: [@mattcen@aus.social](https://aus.social/@mattcen)
- Matrix: [@mattcen:mattcen.com](https://matrix.to/#/@mattcen:mattcen.com)
- Website: [blog.mattcen.com](https://blog.mattcen.com)
- Slides: https://github.com/mattcen/2024-11-three-django-apps-in-a-trenchcoat
-->

License: [CC-BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)

Note:

- I'm Matt (they/them)
- Find me by handle, M A T T C E N
- Post about talk using #PyConAU and #3AppsInATrenchcoat
- Slides available on GitHub: <https://github.com/mattcen/2024-11-three-django-apps-in-a-trenchcoat>

---

<!-- .slide: data-autoslide="20000" -->

## Slides

[![https://github.com/mattcen/2024-11-three-django-apps-in-a-trenchcoat](images/repo_url.svg)](https://github.com/mattcen/2024-11-three-django-apps-in-a-trenchcoat)

---

<!-- .slide: data-autoslide="20000" -->

## Acknowledgements

Note:

I'm delivering this presentation on the unceded ancenstral lands of many Indigenous peoples.
I honour the knowledge, stewardship, and care with which they've tended this land throughout history, and recognise the deep and lasting damage that colonisation has inflicted on them.
I pledge to do my best to respect, learn from, and support these peoples. We can all do better.

----

# "Let's make a tech and radio outdoor wide game!"

## "It'll be fun!", he said

Note:

> wide game (n) (plural wide games):
>
>     Any of various games played by groups in a large area, such as a field or woodland.

Luke wanted to create a wide game which uses 2-way to communicate with a home base. Each radio would be at a base out in the field, and patrols of scouts would be sent to one of those bases.

Upon reaching a base, they would use the radio to contact HQ for further instructions. Each base would have a sheet of "intelligence" questions, one of which would be requested by the operator at HQ. Once the scouts answered the intelligence question, HQ would send them to another base.

![RadioActiv8 site map]()

---

## Getting RadioActiv8 off the ground

----

# "We should build an event registration platform!"

## "Uh, sure?"

---

## The gathering of Brownsea

----

# "So I wanna run the biggest STEM scout camp in the state…"

## "And I want to make use of these other two apps *and* build a new one!"

---

## Creating Star Trek: Survival

### And getting youth to run it

----

# Lessons learned
