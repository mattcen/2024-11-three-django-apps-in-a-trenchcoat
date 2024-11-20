---
title: "Three Django Apps in a Trenchcoat: Writing an event management website with not a lot of time"
---

Luke and I are both members of the STEM[^STEM] team of Scouts Victoria, and thus
part of WOSM[^WOSM]; a "Youth Lead, Adult Supported" organisation focused on empowering
 kids and young adults to pursue fun and educational activities they want to do,
and facilitates their safe participation in anything from rock climbing, to air
activities, to laser tag, to website development. We've come a long way from
camping in the bush and tying knots, and we are hellbent on continuing to engage
young people in making their Scouting world, and by extension, the wider
community, equipped with better resources.

[^STEM]: Science, Technology, Engineering, Maths

[^WOSM]: World Organization of the Scout Movement

We're both technologists; I'm a Linux systems administrator and software
developer, and Luke is a Security Architect with interests in web development
and security education. We are also both Amateur Radio Operators.

As an organisation run by volunteers, we don't always have the resources to work
as efficiently as we'd like. Some of our IT systems are dated (think PHP sites
from the early 2000s) and due to limited resources, haven't always grown as
the organisation's needs have changed. Our organisation is unique in its structure,
and isn't well served by off-the-shelf products.

Luke and I have often thought that as a youth led organisation, if we can empower youth to have direct input and
contributions into these systems, we would be in a position to perpetuate volunteer development and growth of our
tools that conserves our paid adults to focus on supporting the business operations of the organisation, and leave
the program development to the volunteers who run program.

We embarked on this journey with the first of the three apps in a trenchcoat:
Luke, as our State Leader of Communication Technologies, wanted to replicate the exciting experience
of Amateur Radio Contesting. Much like like fishing, the joy of contesting is found in making contact with
another radio station, exchanging callsigns, location, and a custom serial identifier, before
searching for another contact - the station with the most contacts wins the contest, so speed and effiency are rewarded.
Contests had already proved interesting and exciting to our Youth members, so why not
simulate the experience as a next-generation wide game[^WideGame]? In its simplest form, scouts would use two-way radios to
receive instructions and relay information while running around a park.

[^WideGame]:
    wide game (n) (plural wide games): Any of various games played by
    groups in a large area, such as a field or woodland.

The principle of RadioActiv8[^RA8Name] is quite straightfoward: We set out bases around
a neighbourhood park or scout camp, each with a two-way radio, and a sheet of
\
paper with some "intelligence" (a mapping of questions to answers). At the start
of the game, each patrol[^Patrol] would be sent to one these bases. Once they
arrive, they radio to HQ, identifying their patrol and current location, and we
ask them a question, which they answer using the intelligence sheet. Once they
answer, we send them off to another randomly chosen base. The game's end
condition (and whether it is competitive) is up to the facilitator's discretion.
The Proof-of-Concept used a sheet of paper to track the game state[^GameState]
of patrols, recorded by Luke while we gave contacts the next base to attend.

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

Obviously this approach doesn't scale well, and can get overwhelming quickly for
a poor operator to manage. Increasing scale with multiple radio operators at HQ
trying to write on the same sheet of paper was hilarious, but not optimal with a
high number of patrols and bases, so we sought a better solution.

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

And thus, Brownsea[^Brownsea] was born - not as an example of enshittification,
but as a platform on which we could manage events for multiple <del>ages and
sections</del> audiences.
Better UX opportunities were available to pursue, so we set to request contact
information from the existing membership database while only pulling what we
needed - the less PII[^PII] we collect and store, the better. This results in a
sign up and receive an invoice process taking, literally, 30 seconds:

[^Brownsea]:
    Named after the first Scout camp held by Lord Robert Baden-Powell
    on Brownsea Island in England in 1907

[^PII]: Personally Identifiable Information

<video controls src="images/Brownsea-rego.mp4" width="1280"></video>

This system integrates with <del>a pair of</del> <!--obfuscation of detail-->
authenticated API endpoints of Extranet[^Extranet], which do the following:

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
Scouts, and Star Trek's Starfleet organisation - with the exception of space flight,
the virtue Venn Diagram is practically a circle. With Star Trek's comprehensive
back-catalogue and world building, it's a rich universe to draw ideas from for
theming Scouting activities.

[^Trekkie]: Star Trek fan

To that end, we devliered two [_Star Trek: Survival_'s](https://startreksurvival.tech/), "an
_immersive_ adventure experience for all Scouting Members".

This was an incredibly ambitious idea. Scouts Victoria has several major events
that are state-wide, and many smaller events targeting scouts of all ages.

A typical Scouting event is age-group specific, which makes targeting program
activities easy to facilitate within a targeted age. However, Scouts Australia
has redesigned its program since we were youth members, and now facilitates a
"One Program" concept of program delivery, meaning that program areas should be
executed in a fashion that scales according to capability, rather than age. Just
because a program is designed for older teenage Venturer Scouts, doesn't mean it
can't be done by Joey Scouts (and sometimes done better!). There are exceptions;
Cub Scouts don't drive like Rover Scouts, but the program can be adjusted to suit
the needs of the inidividual - what could be more inclusive?

Then comes the STEM program area. Anyone who has done anything with Tech and young
people will appreciate the level of logistical planning that is required to support
a tech program, and the amount of effort that goes into supporting young people
is no small task either. Add into the effects of scale, and you're asking for trouble.
Executing a major state-wide event with no age restriction is rarely done when
the program focuses on Outdoor Adventure, let alone the chaos of technology activities.

The idea was that we'd take over one of Scouts Victoria's largest scout camps,
(Mafeking Rover Park, about 2 hours north-east of Melbourne), ask various Scouts
Victoria Activity Teams (initially with a STEM focus, but eventually more
broadly) to each run activities, and use RadioActiv8 to run the entire event by
semi-randomly sending patrols to activities based on pre-selected patrol
preferences, walking distance, and activity capacity.

The first step was to create a _Star Trek: Survival_ website, which we also
created in Django. The Program team compiled a list of 18 individual activities
for the 2022 event, with 18 additional activities added to the 2024 event.

Each activity was published online, and included an immersive Trek-themed
narrative a list of "I can..." skill-based statements that facilitate Scouts
Australia's award scheme components, ready for peer-review and presentation back
in their Scout Groups post-event.

Then into STS[^STS] website, we added the Brownsea and RadioActiv8 Django
applications, and mapped these into the STS website's various models.

[^STS]: _Star Trek: Survival_

As always, we sought a straightforward, user-friendly workflow for both members
and organisers - an oxymoronic representation of the Be Prepared motto for any
Scouting planning process.

The idea was:

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

As part of our Youth Leading, Adults Supporting approach, we wanted our youngest
scouts to be able to contribute to running STS, so here are some Joeys in
Starfleet Command, dispatching patrols to their various other bases.
Content warning: Cute youth members.

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
