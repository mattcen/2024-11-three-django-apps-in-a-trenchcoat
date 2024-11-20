---
title: "Three Django Apps in a Trenchcoat: Writing an event management website with not a lot of time"
---

Luke and I are both members of the STEM[^STEM] team of Scouts Victoria, and thus
part of WOSM[^WOSM]; a "youth leading, adults supporting" organisation, meaning
that, far above and beyond camping in the bush and tying knots, empowers kids
and young adults to decide what fun and educational activities they want to do,
and facilitates their safe participation in anything from rock climbing, to air
activities, to laser tag, to website development.

[^STEM]: Science, Technology, Engineering, Maths

[^WOSM]: World Organization of the Scout Movement

We're also both technologists; I'm a Linux systems administrator and software
developer, and Luke is an IT generalist with interests in website development
and information security.

As an organisation run by volunteers, we don't always have the resources to work
as efficiently as we'd like. Some of our IT systems are dated (think PHP sites
from the early 2000s) and due to insufficient resources, haven't always grown as
the organisation's needs have changed. Luke and I have often thought that as a
youth led organisation, if we can empower youth to have direct input and
contributions into these systems, we wouldn't need to rely as heavily on
(potentially paid) adults to maintain them. We embarked on this journey when
Luke, as our State Leader of Communication Technologies, wanted to run a next
generation wide game[^WideGame], in which scouts would use two-way radios to
receive instructions and relay information while running around a park.

[^WideGame]:
    wide game (n) (plural wide games): Any of various games played by
    groups in a large area, such as a field or woodland.

The principle of RadioActiv8[^RA8Name] is quite simple: We set out bases around
a neighbourhood park or scout camp, each with a two-way radio, and a sheet of
paper with some "intelligence" (a mapping of questions to answers). At the start
of the game, each patrol[^Patrol] would be sent to one these bases. Once they
arrive, they radio to HQ, identifying their patrol and current location, and we
ask them a question, which they answer using the intelligence sheet. Once they
answer, we send them off to another randomly chosen base. The game's end
condition (and whether it is competitive) is up to the facilitator's discretion.
Initially the game state[^GameState] was tracked on a sheet of paper by the
folks at HQ:

[^RA8Name]:
    Wordplay on the use of two-way radios, the active component of
    moving between bases, "activate", and "radioactive". Abbreviated to RA8

[^Patrol]: A group of 4-7 scouts

[^GameState]:
    the current and previous locations of each patrol, and which
    questions they'd answered

![RA8 0.1 paper implementation. A sheet of lined paper with 4 named bases, each
represented by coloured dot stickers. Under each base is a list of intelligence
answers, most of which are crossed out with circled patrol names beside them,
indicating who answered what.](images/ra8-0.1.jpg)

Obviously this approach doesn't scale well, and can get overwhelming quickly
with multiple radio operators at HQ trying to write on the same sheet of paper,
and a high number of patrols and bases, so we sought a better solution.

What we needed, was a CRUD[^CRUD] app, and having recently begun experimenting
with Django, I was _definitely_ feeling like a perfectionist with
deadlines[^DjangoSlogan], so reached for it immediately.

[^CRUD]: [Create, Read, Update,
Delete](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete)

[^DjangoSlogan]:
    Django's slogan is "The web framework for perfectionists with
    deadlines." as per their [website header](https://www.djangoproject.com/)

After a month or so, we had an app so simple, that Joeys[^Joey] could sit in the
hotseat at our HQ:

[^Joey]: 5--7-year-old scouts

![FIXME: The iteration of the RadioActiv8 main page](images/RadioActiv8%20-%20Play.png)

This form is laid out in a logical order. When a patrol first contacts HQ, we
want their patrol name or number. Once we have that, the system can suggest,
based on previous data, where that patrol is expected to be, pre-fill their
current location, offer an intelligence question if relevant, and suggest a
destination based on various heuristics. The operator can confirm whether the
intelligence was answered correctly, and then if the patrol is checking out of
the base, they can confirm the destination is sensible, and send the patrol on
their way.

After successfully running RadioActiv8 as one of several dozen activities at a
state-wide scout event, and getting great feedback, we were keen to find other
uses for this platform.

---

Because having just one project on the go is boring for two folks with ADHD, and
on the back of building RadioActiv8, yet another tech platform that needed
maintenance, we were keen to empower scouts to help out with this, so Luke
created ScoutHack[^ScoutHack].

[^ScoutHack]:
    A weekend long hackathon/tutorial hybrid in which we teach youth 11-years
    and up basic HTML, CSS, and a little Python in the form of a Flask app. See
    Matt's talk [Developing Labs for Teaching Kids
    Webdev](https://www.youtube.com/watch?v=VXFuL5PcPKI) for more information

In Australia, Scouts is split up into [5
sections](https://scoutsvictoria.com.au/age-sections-adults/)[^Sections]:

[^Sections]:
    - Joey Scouts 5--8 Years
    - Cub Scouts 8--11 Years
    - Scouts 11--14 Years
    - Venturers 14--18 Years
    - Rovers 18--25 Years

As we were preparing for ScoutHack, we rediscovered that the main Scouts
Victoria event management system, which ties into our membership database, only
allows any given event to be available to one of these sections. This meant that
we'd need to create up to 4 different events in the system for the same dates,
each targeting different sections. This sounded like a pain, and while we could
have dealt with it, we really wanted to lead the way by finding a better way,
usable by both us, and other members of the organisation.

And thus, Brownsea[^Brownsea] was born: a platform on which we could list events
for multiple ages and sections, request the bare minimum of information
necessary (the less PII[^PII] we collect and store, the better), and have people
sign up and receive an invoice in literally 30 seconds:

[^Brownsea]:
    Named after the first Scout camp heled by Lord Robert Baden-Powell
    on Brownsea Island in England in 1907

[^PII]: Personally Identifiable Information

<video controls src="images/Brownsea-rego.mp4" width="1280"></video>

This system integrates with a pair of authenticated API endpoints of
Extranet[^Extranet], which do the following:

[^Extranet]: Scouts Victoria's membership database

1. Given a surname[^names], date of birth, and membership number, confirm if
   they match an active Scouts Victoria membership record
2. Given a membership number, return minimal information about that member:

   - Name
   - Email address
   - Phone number
   - Age (years, as an integer)
   - List of roles within the organisation, including name of scout group(s)

[^names]: Yes, I hate that we split up names into given/surnames too.

Our goal was not only to store minimal information, but to streamline the
sign-up experience by avoiding _requesting_ information that we could get from
the existing membership database, but allowing members to override
system-provided information if desired. This also incentivises members to keep
their membership record up to date (something that sometimes falls by the
wayside).

Brownsea has made it trivial for members to sign up to ScoutHack, and receive a
Xero invoice both in the interface, and via email (the system doesn't accept
credit card payments currently).

But we wanted to go bigger.

I'm not Trekkie[^Trekkie], but Luke, who is, saw a values alignment between
Scouts, and Star Trek's United Federation of Planets, and with Star Trek's
comprehensive back-catalogue and world building, it's a rich universe to draw
ideas from for theming scouting activities.

[^Trekkie]: Star Trek fan

I give you [_Star Trek: Survival_](https://startreksurvival.tech/), "an
_immersive_ adventure experience for all Scouting Members".

This was an incredibly ambitious idea. Scouts Victoria has several major events
that are state-wide, and many smaller events targeting scouts of all ages, but
to combine the two and have a major state-wide event with no age restriction was
rarely done, and would need a lot of planning and a streamlined logistical
execution.

The idea was that we'd take over one of Scouts Victoria's largest scout camps,
(Mafeking Rover Park, about 2 hours north-east of Melbourne), ask various Scouts
Victoria Activity Teams (initially with a STEM focus, but eventually more
broadly) to each run activities, and use RadioActiv8 to run the entire event by
semi-randomly sending patrols to activities based on pre-selected patrol
preferences, walking distance, and activity capacity.

The first step was to create a _Star Trek: Survival_ website, which we also
created in Django. We then began to come up with a list of activities we wanted,
as well as appropriate Star Trek-themed backstory for each of them, and a list
of which parts of Scouts Australia's award scheme could be signed off upon
activity completion.

Then into STS[^STS] website, we added the Brownsea and RadioActiv8 Django
applications, and mapped these into the STS website's various models.

[^STS]: _Star Trek: Survival_

As always, we sought a straightforward, user-friendly workflow for both members
and organisers. The idea was:

1. Member uses Brownsea to sign up using their Scouts Victoria membership information
2. As part of sign-up, the member can select which activities interest them
3. As the event nears, organisers creates patrols of members in the same group
   or district, taking each member's activity preferences into account where
   possible
4. These scout groups' leaders can sign in (again using their Scouts Vic
   membership details) to check which of their members have registered, and
   which patrols they've been allocated to.
5. When the event begins, every member is signed in using Brownsea's admin
   portal, given a 2-way radio to keep, and sets up cap with their patrol.
6. Each patrol is sent off to one of the activities on their priority list.
7. On arrival, the patrol checks in by radioing their identity and location to
   the RadioActiv8 team at Starfleet Command (which is also one of the
   activities), does the activity, and checks out the same way.
8. This continues throughout the weekend, and each patrol gets to complete
   _most_ of their preferred activities.
9. After the weekend, each member can access a web page listing which award
   scheme components they have achieved, based on which activities they
   actually got to throughout the event.

Both Brownsea and RadioActiv8 required additional features to facilitate STS.
Some of these features were generically useful for most events, but a small
subset were specific to STS, so I carefully kept those on a separate branch.

One of Django's huge advantages in an endeavour like this is its admin app. I
was able to give event administrators access to the admin without writing them a
custom portal up-front, and in general it was Good Enough™ for their needs.

Also, as previously mentioned, as part of our Youth Leading, Adults Supporting
approach, we wanted our youngest scouts to be able to contribute to running STS,
so here are some Joeys in Starfleet Command, dispatching patrols to their
various other bases.

![3 Joeys sitting at a table in front of a two-way radio, and a computer with 2
monitors, being mentored by a Venturer on how to operate the
equipment](images/1000001380.jpg)

As part of RadioActiv8, there are some comprehensive dashboards showing base
capacity, last known location of each patrol, and when we've last heard from
them. Still on my to-do list is an interactive map showing everyone's locations,
but in lieu of that, and to keep things fun, we printed out an A0 table-top
gaming-style map of the entire campsite and its activities, with which Starfleet
Command personnel could visually track the location of each patrol:

![an A0 map of coloured hexagons on a table, with magnetic markers for each
patrol. There are 2 Venturers standing around the table updating the map's
locations](images/ima_6316733.jpeg)

---

From a technical perspective, we wanted to do our best to adhere to current
industry best practices for the tools we used. Django is obviously a
well-understood and battle-tested framework. As much as possible, we run all of
our Django apps as 12-factor apps in Docker containers to make them easy to
deploy anywhere and migrate where necessary. Because our goal is for these apps
to be maintainable by youth members who may be very novice programmers, we want
to reduce what they have to learn. As a result, we're doing what we can to
standardise on HTMX for the interactive parts of RadioActiv8, so that people
don't need to know JavaScript or another front-end framework.


---

---

# OK here we go

This talk is about building web apps voluntarily for a non-profit organisation
to solve organisational and logistical challenges.

We'll start with a little backstory about us and the organisation, and touch on
the problems we're trying to solve.

Then we'll describe the evolving solutions we've developed, initially at a high
level, but getting into a bit of the technical detail, time permitting.

---

Luke and I are both members of the STEM[^STEM] team of Scouts Victoria, a "youth
leading, adults supporting" organisation, meaning that, far above and beyond the
stereotype of camping in the bush and tying knots, we empower kids and young
adults to decide what fun and educational activities they want to do, and
facilitate their safe participation in anything from rock climbing, to air
activities, to laser tag, to website development.

[^STEM]: Science, Technology, Engineering, Maths

We're also both technologists; I'm a Linux systems administrator and software
developer, and Luke is an IT generalist with interests in website development
and information security.

---

FIXME: How much do we talk about the logistical and organisational problems of
the organisation as a whole, vs the specific chanllenges we face as a result?

Our ultimate goal is to deliver program requested by youth members in a way that
gives them as much input as possible, while removing any friction to
participating in, or organising activities and events, in a way that is
child-safe and protects people's privacy.

We wanted to be able to manage ScoutsVic member registrations for upcoming
events, but (a) need to verify registrants *are* members of ScoutsVic, and (b)
want to offer different "tickets" to the same event to different ages and scout
sections[^Sections]. No existing systems met this need without also collecting
unnecessary amounts of PII[^PII], which we wanted to avoid the responsibility of
storing safely.

[^PII]: Personally Identifiable Information

FIXME: What *problem* does RA8 solve? Sure it facilitates a wide-game, but is
that it? I know it was designed with the likes of ScoutHike in mind, so perhaps
the greater problem is "how do we keep track of youth members across a large
area, and send them to different activities without them having to wait around
for activities to be available etc.?"
