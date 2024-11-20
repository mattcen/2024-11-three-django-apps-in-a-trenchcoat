---
title: "Three Django Apps in a Trenchcoat: Writing an event management website with not a lot of time"
lang: en
---

Content Summary:

1. Introduction & Motivation
  a. Introduce speakers
  b. Introduce organisational goals
  c. Organisation limitations
  d. Supporting a Legion of Devs with Python

2. Brownsea
  a. ScoutHack Origins


3. RadioActiv8
  a. What is RA8 - Where did I come from
  b.
  c.


# Introduction & Motivation

## 1.a. Introduce Speakers

mattcen is a Linux systems administrator and software developer;
Luke is a security analyst and systems architect with interests in web
development and security education. We are also both Amateur Radio Operators.
FIXME: Phrasing: "We are also both…" "Luke and I are both…" -- tie these
together better

Luke and I are both members of the STEM[^STEM] team of Scouts Victoria; a "Youth Lead, Adult Supported" organisation focused on
empowering young people to pursue fun and adventurous activities they want to do,
and facilitating their safe participation in camping, climbing, sailing, cycling,
and our specialties, radio communications and website development.

[^STEM]: Science, Technology, Engineering, Maths

[^WOSM]: World Organization of the Scout Movement

## 1.b. Introduce organisational goals

Scouting has come a long way from camping in the bush and tying knots, and as
Leaders, we are hellbent on continuing to engage young people in providing
better resources to both Scouting and the wider community.

## 1.c. Organisation Limitations

As an organisation run by volunteers, we don't
always have the resources to work as efficiently as we'd like. Some of our IT
systems are dated (think PHP sites from the early 2000s) and due to limited
resources, haven't always grown as the organisation's needs have changed. Our
organisation is unique in its structure, and isn't well-served by off-the-shelf
products.

## 1.d. Supporting a Legion of Devs using Python

Luke and I have often considered the value of raising a "Legion of Devs" to
perpetuate volunteer development and growth of Scouting information tools.
Python with its supportive framework is a natural colleague to this challenge,
with Python being a friendly and familiar language to young coders through
school and tech programs already well established. Python, along with its
frameworks, is an obvious solution due to its ubiquitous presence in early
coding education spaces.

# 2. Brownsea

<!--
[!FIXME - This is verbose. Remove from talk, but keep this as a note.]
Building a Legion of Devs is ambitious, and starting that process
at age 10 is insanity. We have learnt that teaching young people to code can
never be started too early - how this is achieved is much more important. While
there is a plethora of excellent coding resources that teach kids to build games
or spin turtles on their local machines, we found that sharing information is
not only a skill for life, but one of the most rewarding tech experiences for
young people to see the fruit of their labour. Given the ubiquity of information
accessible to young people via websites, it seems obvious that web development
is the best place to start building skills with a tangible outcome.
-->

## 2.a. About ScoutHack

So we created ScoutHack[^ScoutHack], a WebDev course that walks Scouts aged ten
to adult through HTML, CSS, and Python Flask. Check out our [Lightning Talk from
Everything Open 2023](https://www.youtube.com/watch?v=GGgHsA8WifE&t=1460) for a
little more about that adventure, or mattcen's talk, [Developing Labs for
Teaching Kids Webdev](https://www.youtube.com/watch?v=VXFuL5PcPKI) for a deeper
dive. Today we're discussing the registration app built to support event
registrations - our second app in our trenchcoat!

## 2.b. Registration System needs

However, registration for a Scouting event poses some administrative burdens we
felt empowered to overcome.

FIXME tidy up phrasing:

FIXME: Option 1: Firstly, minimise the need for an event administrator to export
(and thus duplicate/exfiltrate) registration data in order to augment it with
information such as catering or grouping.

FIXME: Option 2: Firstly, minimize the need for data exfiltration and
duplication as a solution to support event functions like catering and grouping.

Secondly, avoid paying a third party provider that only does half of what we
need.

Thirdly, use a system that understands the unique structure of the
organisation.

In summary, our need is to:

1. allow registered members to sign up for an event
2. prefill the minimum essential PII from our membership database
3. auto-generate an invoice from our accounting system
4. summarise dietary needs at a glance
5. and as a proficient user, have the whole process take about 60 seconds.

## 2.c. Registration System capabilities

Welcome to Brownsea[^Brownsea]! This system integrates with authenticated API
endpoints of Extranet[^Extranet], which do the following:

[^Brownsea]:
    Named after the first Scout camp held by Lord Robert Baden-Powell
    on Brownsea Island in England in 1907

[^Extranet]: Scouts Victoria's membership database

1. Given a surname[^names], date of birth, and membership number, confirm if
   they match an active Scouts Victoria membership record
2. Given a membership number, return minimal information about that member:

   - Name
   - Email address
   - Phone number
   - Age (years, as an integer)
   - List of roles within the organisation, including name of Scout Group(s).

[^names]: Yes, I hate that we split up names into given/surnames too.

We now have a viable system for any event administrator to manage the event
details for our organisation.

## 2.d. Limiting data storage needs

Our goal is to store minimal PII[^PII] and streamline the sign-up experience by
avoiding _requesting_ information that we could get from the existing membership
database, and still allowing members to override system-provided information if
desired.

[^PII]: Personally Identifiable Information

We achieved this by only allowing registration using valid member-database
authorization credentials, forcing members to update their membership records if
there are data inaccuracies or mismatches, and allowing authorized registrants
could override the data presented by the membership registration database if
they needed to use other contact details for the purpose of the event.

## 2.e. Ease and speed of use

Brownsea has made it trivial for members to sign up to ScoutHack, and
immediately receive a Xero invoice both in the interface and via email (the
system doesn't accept credit card payments currently). This results in a sign up
and receive an invoice process taking, literally, 30 seconds:

<video controls src="images/Brownsea-rego.mp4" width="720"></video>

Now we have members registered to participate, it's time for some program.
Let's play with some radios!

FIXME: Wait wait, we don't have them sorted into Patrols; we don't even know
what a Patrol *is* at this stage!

# 3. CQ, CQ, CQ: RadioActiv8

### 3.a. Introduce RA8

As our State Leader of Communication Technologies, Luke wanted to replicate the
exciting experience of Amateur Radio Contesting as an activity for Scouts.

### 3.b. Introduce Radio Contesting

A metaphor of fishing (with a rod, not a mail server), the joy of contesting is
found in making contact with another radio station, exchanging callsigns,
location, and a custom serial identifier, before searching for another contact -
the station with the most contacts wins the contest, so speed and efficiency are
rewarded.

### 3.c. Contesting into youth program

Contests had already proved interesting and exciting to our Youth members, so
why not simulate the experience as a next-generation wide game[^WideGame]? In
its simplest form, scouts would use two-way radios to receive instructions and
relay information while running around a park.

[^WideGame]:
    wide game (n) (plural wide games): Any of various games played by
    groups in a large area, such as a field or woodland.

### 3.d. RadioActiv8 concept

FIXME: Rephrase "grid" and "matrix" etc
The principle of RadioActiv8[^RA8Name] is quite straightforward: Bases are set
out across a neighbourhood park or Scout Camp. Each base has a two-way radio,
and a sign with the name of the base and an intelligence grid featuring an
answer matrix.

[^RA8Name]:
    Wordplay on the use of two-way radios, the active component of
    moving between bases, "activate", and "radioactive". Abbreviated to RA8

### 3.e. RadioActiv8 gameplay

At the start of the game, each patrol[^Patrol] is sent to
a base. Once they arrive, they radio to HQ and identify themselves and
current location. The HQ station responds with a question which the patrol must
answer using the intelligence answer matrix. On receipt of an answer HQ
provides the patrol a new destination. The game's end condition (and whether it is
competitive) is up to the facilitator's discretion. The proof-of-concept used a
sheet of paper to track the game state[^GameState] of patrols, recorded by Luke
while we gave contacts the next base to attend.

[^Patrol]: A group of 4-7 scouts

[^GameState]:
    the current and previous locations of each patrol, and which
    questions they'd answered

![RA8 0.1 paper implementation. A sheet of lined paper with 4 named bases, each
represented by coloured dot stickers. Under each base is a list of intelligence
answers, most of which are crossed out with circled patrol names beside them,
indicating who answered what.](images/ra8-0.1.jpg)

### 3.f. RadioActiv8 - does it scale?

Obviously this approach doesn't scale well, and can get overwhelming quickly for
an inexperienced operator to manage. Increasing scale necessitated multiple
radio operators at HQ trying to write on the same sheet of paper with hilarious
and chaotic results, but was not optimal with a high number of patrols and
bases, so we sought a better solution.

FIXME: We introduce Django and CRUD below, but should move some of this up to
the Brownsea section

### 3.g. Digitizing RadioActiv8

What we needed was a CRUD[^CRUD] app, and having recently begun experimenting
with Django, mattcen was _definitely_ feeling like a perfectionist with
deadlines[^DjangoSlogan], so reached for it immediately.

[^CRUD]: [Create, Read, Update,
Delete](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete)

[^DjangoSlogan]:
    Django's slogan is "The web framework for perfectionists with
    deadlines." as per their [website header](https://www.djangoproject.com/)

### 3.h. RadioActiv8 is Youth Led!

[!FIXME clean up this wording. #phrasing, boom]
After a few trial sessions, we refined the app so effectively that the complex
contest concepts became a simple process to follow. This was so effective that
the entire game could be independently managed by older Scouts with minor
support from us.

![FIXME: The iteration of the RadioActiv8 main page](images/RadioActiv8%20-%20Play.png)

### 3.i. RadioActiv8 Interface

This form is laid out in a logical order. When a patrol first contacts HQ, we
want their patrol name or number. Once we have that, the system can suggest,
based on previous data, where that patrol is expected to be, pre-fill their
current location, offer an intelligence question if relevant, and suggest a
destination based on various heuristics. The operator can confirm whether the
intelligence was answered correctly, and then if the patrol is checking out of
the base, they can confirm the destination is sensible, and send the patrol on
their way.

### 3.j. Expanding capability (Yes, it scales)

After successfully running RadioActiv8 as one of several dozen activities at a
state-wide scout event, and getting great feedback, we were keen to find other
uses for this platform. For example, each base only has intelligence on a card,
but what if the base was an activity base that had a task to complete?

RadioActiv8 would work really well for distributing Youth members to different
activities, and so we began putting together ideas as to how this application
would work to facilitate management of a Scouting event, rather than just being
an activity for its own sake.

---

--- We are here ---

### 4. Star Trek: Survival (2022, 2024)

The best way to teach a young person (or anyone, really) is to make it fun <ins>and engaging</ins>. The
more fun the activity, the less obstruction to focus and learning. Immersion of
experience, much like chocolate on vegetables, is a great way to discover new
skills and explore self-capability without feeling the burden of pressure to
learn.

To that end, we have devlivered not one, but two [_Star Trek:
Survival_'s](https://startreksurvival.tech/), "an _immersive_ adventure
experience for all Scouting Members". This website forms the third app in our
trenchcoat.

We have supported many STEM-based activities at conventional Scouting events,
but now that we have a versatile registration system and a dynamic and gamified
distribution utility, we decided to combine these activities into an immersive
program experience.

The idea was that we'd take over one of Scouts Victoria's largest Scout camps,
invite various Activity Teams to each run activity, and use RadioActiv8 to run
the entire event by sending patrols to activities based on pre-selected patrol
preferences, walking distance, activity capacity, and availability.

The first step was to create a _Star Trek: Survival_ website. The Program team
compiled a list of 18 individual activities for the 2022 event, with 18
additional activities added to the 2024 event.

Each activity was published online, and included an immersive Trek-themed
narrative, and a list of "I can..." skill-based statements that facilitate Scouts
Australia's award scheme components, ready for peer-review and presentation back
to their Scout Groups post-event.

![FIXME Get an "I Can" statement list from STS mission ]

Then into the STS[^STS] website, we added the Brownsea and RadioActiv8 Django
applications, and mapped these into the STS website's various models.

[^STS]: _Star Trek: Survival_

As always, we sought a straightforward, user-friendly workflow for both members
and organisers -- for the most part, this was achieved as a minimum viable
product with room to grow.

<del>The idea was:</del>
The combined workflow follows: [!FIXME: phrasing this sentence.]

1. Member uses Brownsea to sign up using their Scouts Victoria membership information
2. As part of sign-up, the member can select which activities interest them
3. As the event nears, organisers creates patrols of members in the same group
   or district, taking each member's activity preferences into account where
   possible
4. These scout groups' leaders can sign in (again using their Scouts Vic
   membership details) to check which of their members have registered, and
   which patrols they've been allocated to.
5. When the event begins, every member is checked in using Brownsea's admin
   portal, given a 2-way radio to keep, and sets up camp with their patrol.
6. When activities begin, each patrol is sent off to one of the activities on
   their priority list.
7. On arrival at their activity, the patrol checks in by radioing their
   identity and location to the RadioActiv8 team at Starfleet Command (which is
   also one of the activities), does the activity, and checks out the same way.
8. This continues throughout the weekend, and each patrol gets to complete
   _most_ of their preferred activities.
9. After the weekend, each member can access a web page listing which award
   scheme components they have achieved, based on which activities they
   actually got to throughout the event.

Both Brownsea and RadioActiv8 required additional features to facilitate STS.
Some of these features were generically useful for most events, but a small
subset were specific to STS and carefully kept on a separate branch.

One of Django's huge advantages in an endeavour like this is its admin app. I
was able to give event administrators access to the admin without writing them a
custom portal up-front, and in general it was Good Enough™ for their needs.

#### Post-event tech review

From a technical perspective, we wanted to do our best to adhere to current
industry best practices for the tools we used. Django is obviously a
well-understood and battle-tested framework. As much as possible, we run all of
our Django apps as 12-factor apps in Docker containers to make them easy to
deploy anywhere and migrate where necessary. As our goal is for these apps
to be maintainable by youth members who may be very novice programmers, we want
to reduce what they have to learn. As a result, we're doing what we can to
standardise on HTMX for the interactive parts of RadioActiv8, so that people
don't need to know JavaScript or another front-end framework.

# 5.a Evidence of success

Under our Youth Lead, Adult Supported approach and assisted by the process
driven layout of the RadioActiv8, we are able to have our youngest scouts to be
able to contribute to running STS, so here are some Joey Scouts in Starfleet
Command, dispatching patrols of peers and seniors to their various other bases.
Content warning: Cute youth members.

![3 Joeys sitting at a table in front of a two-way radio, and a computer with 2
monitors, being mentored by a Venturer on how to operate the
equipment](images/1000001380.jpg)

To guide our dispatch team to make operational decisions, RadioActiv8 uses
comprehensive dashboards that include the base capacity, last known location of
each patrol, and when we last heard from them. We're yet to develop an
interactive map showing everyone's locations but is on the to-do list. To
overcome this for our visual and kinesthetic learners, our colleague designed an
 A0 table-top gaming-style map of the entire campsite and its activities, with
 which Starfleet Command personnel could use to visually track the
location of each patrol:

![an A0 map of coloured hexagons on a table, with magnetic markers for each
patrol. There are 2 Venturers standing around the table updating the map's
locations](images/ima_6316733.jpeg)

Using RadioActiv8, Brownsea, and the STS website in an integrated fashion helped
us to minimize the administrative functions of supporting the delivery of the
Scouting program, and gave Scouts Victoria the capability to allow simultaneous
participation and delivery of the Scouting program.

As a result, we have literally made it possible for the operations of an event
to be Youth Led, and Adult Supported. With thanks to the capabilities of Python
and Django, we can continue to do perpetuate our success and upskill our members
in ways that were only a dream just a few years ago.

--- EOF ---

---

---

# OK [here we go](https://www.youtube.com/watch?v=-l5G5BT8-fQ)

## Outline

This talk is about building web apps voluntarily for a non-profit organisation
to solve organisational and logistical challenges.

We'll start with a little backstory about us and the organisation, and touch on
the problems we're trying to solve.

Then we'll describe the evolving solutions we've developed, initially at a high
level, but getting into a bit of the technical detail, time permitting.

---

## Who are we

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

## Our goals in scouting

FIXME: How much do we talk about the logistical and organisational problems of
the organisation as a whole, vs the specific challenges we face as a result?

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

---

## Building sustainable software

- Empower youth to contribute by using friendly tools and languages, and
proactively teaching these tools as valuable skills

TODO: Humming poll on who is familiar with Django to decide how much detail to
cover.

---


## Keeping track of youth member location

RA8 facilitates keeping track of youth members over a large area at an event,
and scales up to a several-hundred person event.

In addition to this being a valuable safety measure at events that span a large
campsite or a forest, we can use this to run a wide game over this sort of area
in which we send youth to different bases around the site.

TODO: Elaborate on how RadioActiv8 works and were we started with it.

![RA8 0.1 paper implementation. A sheet of lined paper with 4 named bases, each
represented by coloured dot stickers. Under each base is a list of intelligence
answers, most of which are crossed out with circled patrol names beside them,
indicating who answered what.](images/ra8-0.1.jpg)

![FIXME: The iteration of the RadioActiv8 main page](images/RadioActiv8%20-%20Play.png)

TODO: Show RA8 dashboard listing base capacity and patrol locations

---

## Registering youth member participants to an event

- Services like Eventbrite or Trybooking are great, but require storing youth
PII with a third party, which may (but shouldn't) include medical info
- These services also don't allow us to validate ScoutsVic membership
- We wanted to request as little info as possible, to reduce both attack surface
and friction for registrants.

Brownsea collects:

- Scouts Victoria Membership Number
- Date of Birth
- Surname
- Dietary requirements
- Any other notes the participant enters

Brownsea stores:

- Scouts Victoria Membership Number
- Full name
- Phone number
- Email address
- Age (to nearest year)
- List of roles (and associated scout groups) within the organisation
- Dietary requirements
- Notes

----

### Registrant event sign-up workflow

- Authenticate with surname/birthdate/membership number
- Select an eligible event from a list
- Select an eligible ticket from a list
- Confirm personal and contact details, and enter dietary requirements
- Select "register"
- Receive invoice via link and in email

----

### Demo of registration

<video controls src="images/Brownsea-rego.mp4" width="720"></video>

---

### Event admin

- Organisers can see registrations appear in the Django admin
- Invoices get generated into Xero, and their payment status could be reflected
in the admin too (though isn't currently)
