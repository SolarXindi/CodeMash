# Precompiler Day 2 - Wednesday, 2024

## Morning - Event Storming Unleased: Building Bridges for Effective Communication

### Summary

TODO: Add

### Notes

### What is Event Storming?

Collaborative workshop-based experience to gain shared understanding of a complex business system.
When inheriting a system, if they original people are still around, get info from them.
Overkill for basic CRUD based systems, but an eCommerence shop calling an ERP system is a right fit

#### What is an Event?

What happened yesterday, a month or a year ago? Event = Something that happened in the past.
Past Tense is very intentional

#### Orange Sticky Note

Creator of Event Storming technique, used about 50,000 orange sticky notes and increased all the way to 100,000 stick notes used

#### Merge the People, split the software

Bring together everyone (QA, Developers, Stakeholders, Project Managers, Business Owner, and others who know the process).
People with questions and people with answers

Split the Software can describe taking an existing system and making it modular/microservice

#### What is Storming?

Putting sticky notes up on the board, in a mass chaos style.
Don't worry about anyone else, can do private mode in Miro

#### Types

Big Picture Event Storming
Goal: Generate shared understanding
Used for discovery
Past Tense for eventing
30-50 people?
No one knows the whole story
Ask questions about the unknown
Should be a safe space to ask anything (relevant)

Processing Modeling
Goal: Address the hotspots (pain points or unknown points)
Used for exploring a process
Typically limited to a single end-to-end process
20-30 people?
Having a coordinating/dedicated person to avoid Rabbit Holes

System Design
Goal: Evaluate a system and propose a solution
Design a solution
Be aware of alternatives
Hide unnecessary complexity from the users
People: Senior Devs, architects
Focus: Firewall, patterns, infrastructure, etc.

People Experience
Goal: Understand customer/user/persona interactions and experiences
Built on Processing Modeling
Understanding user experience and designing parts of the system to help with user pain points

Refactoring
Given an existing solution, use Event Storming to identify what is available for potential refactoring points
Built on System Design
Pain Points for devs, aka flexibility, maintainability, extensibility, etc.

Startups

* Fewer silos, if any
* People wearing multiple hats
* People who are more likely to admit they don't know
* May find company gaps where no one knows or know who should know
* May be easier to schedule people

Corporations:

* Consultant/outside facilitator may find it easier to get the key stakeholders together
* Discovering key impediments, solving key problems
* People vs Process vs Code problems (or a combination of all of them)

#### Step 1 - Chaotic Exploration

Starts with a (orange) sticky note, analysis paralysis is normal
May need to guess at the Domain
Color may not matter too much in Big Picture (but more important in System Design)

#### Step 2 - Deduplicate

#### Step 3 - People and Systems

App talks to a different system or don't know who use your systems
Anything external to the App (team/company as well) is noted here
People = Personas (accounting), roles (security levels) or even a specific person (maintains a process or system)

Add more roles to existing sticky notes?
Are there systems you want to add sticky notes to?
    Point of Sale system, Inventory Management portion

#### Step 4 - Identify Areas to Explore

Domain = Area to Explore (a specific, big or silo'd business area)
Event Storming based on the Domain
Figure out what else to explore, which is Process Modelling

Back of House, Front of House, Management are all examples of Areas to Explore

#### Event Storming Grammar (Colors)

Green = Read Model
Small yellow = User
Blue = Command
Light yellow = Aggegate
Orange = Domain Event
Policy = Purple
Red = External System

    B LY O P B
G SY
      R

Domain Event = What Happened / Past Tense
Command = Imperative, mainly issued by a user or an event and triggers an event
User = may be generic or specific
Policy = "Whenever", under what condition and may include a related role
    If the role is used (User)
External System = Not always third party, is at least outside the app
Hot Spots = Red/Purple (sometimes black or speech bubbles). What are pain points or what are the unknowns?
Aggregate = Used to group objects for purpose of data changes
Read Model = Data needed for a user to make a decision, do not get wrapped up in reusability.
    Understand the decision
    Define necessary data
    Make it happen
    Lives in a bounded context, where the decision is happening

#### First Exercise

Big Picture Eventing Storming
Won't be using Command or Aggregate sticky notes

Theme: Scenes at a Restaurant
Inherited family restaurant, don't know what we are getting involved ourselves in
Hosts, chefs, waiters and patrons are the user groups

**Did exercies and Step #1, so chaos and then de-duped**

This gets the ball rolling and can focus on a specific portion of the Domain (back of house vs front of house)
Do more sessions on other portions of the Domain

How do major life / world events impact the process
    Do another Event Storming, but can narrow the focus down to individual aspects

Categorize events before OR after de-duping

### Transitioning between Event Storming Sessions

#### Flow

How do the Event Storming sessions flow into each other?

Big Picture into Processing Modeling into Experience Modeling
Big Picture into System Design
Big Picture into Refactoring Modeling

#### Transitioning

Process uncovered during discovery

Deep dive into a process

#### Processing Modeling

Aggregate is for System Design/Domain Driven Design/Refactoring, NOT for Processing Modeling
All other note types are available

Collaborative processing modelling
Limited scope - single end-to-end process
Smaller # of people
Use the cooperative game principle - the problem is the opponent and everyone in hte room must work together to defeat it
May need to up technical or specialty jargon to get everyone on same page
If someone critically cannot attend, mark that as a pain point
    Executives are busy to schedule? Separate Event Storming sessions (with even smaller group OR with executive representatives)

Domain Driven Design - Ubitiquous Language, breakdown language into a common and understandable verbiage

Game Goals for Processing Modeling

* All process paths are **completed** (focus on happy path first)
* Every possible **Hotspot** is addressed
* All the stakeholders involved in the process are **reasonable happy**
* The **color grammar** is preserved with no holes and gaps
  * Get details, the flows, the happy paths and bad paths
  * Least important and want to be "good enough", as there is only so much time you can reasonable spend here

##### Grammar

* Events - Orange Sticky Notes
  * Triggered by a user interaction
  * Triggered by an external system
  * Triggered by time (temporal)
  * Triggered as a cascading reaction
* Command/Actions - Blue sticky notes
  * Also interactions or user decisions
  * Commonly triggers more events
* People - Small Yellow sticky notes
  * Can be used for roles, actors, personas, or concrete examples of people
* External Systems - Pink sticky notes
  * e.g. Inventory system, ERP system, Reservation system, Staff Scheduling system
* Hotspots - Red, Purple, or Black sticky notes or Comment Bubbles
  * Something that calls attention and stands out
    * E.g. "How are the specials of the week determined", "What payment methods are supported?", or "What if this step fails?"
* Policies - Lilac sticky notes
  * Capture **reactive logic** to porcesses
  * Business Decisions
  * Organization reaction to given events
  * "Whenever"
* E.g. Policy "Whenever the meal is complete" - Command "Calculate the Check - Event "Line items summed" - Command "Calculate Tax" - Event "Tax calculated
* Read Models - Green sticky notes
  * Information needed to make a decision
  * E.g. allergic to food, so need list of ingridents OR budget issues, need price before buying a shed
* Wireframes/Sketches
  * Visual Aids are welcome
  * If they add value, be explicit
* Team Dynamics
  * **The Pragmatic**: will know which path delievers more value and why
  * **The Driller**: will come up with alternatives and "What if...?" scenarios
  * **The Empathic**: will care about emotions & feelings

Events are written in past tense, answers what happened

Revelations in Talking with Participants

* I just started working here recently, I finally understand what they do here!
* This is where everything is broken
  * Is it Code, a process that doesn't make sense, etc.
* This never really works
  * Have they stated it before? Have they given feedback? If not, talk and provide a way.
  * Try to get repro steps
* It takes forever to complete this step
  * Debug an issue to help out?

De-duping also means putting it into a Timeline, so we know how it flows

Step 4, identifiy pain points and figure out possibly resolutions

#### Second Exercise

Process Modeling
Customers' reservation process
Chefs' inventory management
Staffing / Scheduling Management

Put down a bunch of events, add user roles and then start thinking critical of how it flows.
Organize into a timeline and then identify the pain points / gaps in knowledge

### Additional Event Storming Guidance

Aggregate items into groups, then can make a bounded context (which could be microservices), this is apart of the System Design portion

### Additional Resources

PowerPoint has resources for after the fact
EventStorming by Alberto Brandolini
The EventStorming Handbook by Paul Rayner
EventStorming.com
50,000 Stickies Later (video, 2016/2017) by Alberto Brandolini
100,000 Stickies Later (video, 2019) by Alberto Brandolini

<https://bit.ly/contact-np>

## Afternoon - Thinking Architecturally

### Afternoon Summary

Rich Hickey once said programmers know the benefits of everything and the trade offs of nothing...an approach that can lead a project down a path of frustrated developers and unhappy customers. As architects though, we must consider the trade offs of every new library, language, pattern or approach and quickly make decisions often with incomplete information. How should we think about the inevitable technology choices we have to make on a project? How do we balance competing agendas? How do we keep our team happy and excited without chasing every new thing that someone finds on the inner webs?

As architects it is our responsibility to effectively guide our teams on the technology journey. In this talk I will outline the importance of trade offs, how we can analyze new technologies and how we can effectively capture the inevitable architectural decisions we will make. I will also explore the value of fitness functions as a way of ensuring the decisions we make are actually reflected in the code base.

### Afternoon Notes

Thinking Architecturally by O'Reily, written by presenter - 60/70 pages
Responsible Microservices as well

#### As an Architect

Many competing agendas
Dale Carnegie - How to influence people (book)
Technology changes. Constantly.

#### Quality Attributes / Big Picture

Non-functional requirements, issue with language when talking with people
The "ilities"
Customers care about functionality

E.g.

* Maintainability
* Scalability (sometimes over engineered)
* Reliability
* Security
* Deployability
* Simplicity
* Usability
* Compataiblity
* Fault tolerance
* Modularity

What matters most to an individual?
"It depends"

Every decision has trade-offs (especially life)

Inverse relation, max one, you min another
e.g. Security/Usability

Customers may recognize some quality attributes over others
Fairly easy to convince others of certain attributes
Others are harder to convince
e.g. Maintainability and simplicity

Be able to explain WHY we need to upgrade, get decision makers to buy-in
Learn how to influence people, what techniques?
Make it their decision
Outline the benefits
Find common ground (should suck less)
Avoid aggression
Listen.
Have a conversation, as it is hard to convince people

Hammer (force people to do it) or the Ninja (make it their decision)

Find the Influencers and influence them
Way you shape the message
Reputation speaks for you, when you are not there
Ask what you reputation. Be ready for the answer, you can work to change it.
Find common ground
Respect and help each other
Use trusted source (even if you don't like it)
Recruit credible allies
Customers don't care about jargon, speak their language.

Shape the message according to the customer

#### Self-Driving Car Example

Phone Home
Send payload (including VIN)
Demand is very high
Expect millions of cars within 3 years
Marketing is full of great ideas
24/7 system
Web UI/Mobile App
Status of Car / maintenace issues?
Secure
Summon the car to location
Push notifications

Data:
Fleet generates data
Anonymized
Ensure only authorized user
Audit access
Push updates
Push recal//update information to customers

What stands out?

* Demand is "extremely high"
  * What is "extremely high"
* Millions of cars? Currently, expected, how many cars are built per day/year?
  * Market Speed
* Available 24/7
  * Very expensive, very face
* How to identify owner?
* How is it secured?
* Location Data (summon car)
  * This can be toxic, we don't want to keep that data
* Fleet generates data, what is "a lot"
* What is authorized user access (company facing)
* Audit access, what is the requirement?

Key: Auditability, Availability, Security and Usability

Ranking: Depends on the user
    (customer is Usability, Availablity, Security, and Reliability)
    (service center is Security, Auditability, Efficiency, and Usability)

Discussions are the best part, with peers and it evolves

#### Group Activity (Kata)

We could do internal Katas ("effortful study") with the team, to help teach others how to architect

<https://fundamentalsofsoftwarearchitecture.com/katas/list.html>

A concert ticketing site with big acts and high volume needs an elastic solution to sell tickets.

Users: thousand of concurrent users, bursts of up to 10,000/second when tickets go on sale
Requirements:
allow concurrent ticket buying
do not sell a seat more than once!
shoppers can see an overview of remaining seats
Additional Context:
consider an implementation in both Space Based and Microservices architecture style
identify the tradeoffs for each solution

Key Features:
Scalability
Availability
Reliability
Security (do not sell a seat more than once)
Visbility
Usability / Compatibality

Artist/Management (Visibility, Availability, Reliability)
Venue (Same as Artist)
Company (Scalability, Availability, Reliability, Security)
Customer (Usability, Reliability, Visibility, Security)

Space-based architecture would have the benefits:
    Horizontally scaling the services needed for user interaction while avoiding the need to scale the data sources
    Allows for central data sources, independent of the Processing Unit, to keep sources central / separate scaling
Cons:
    Unfamiliar pattern that would require research and time
    Finding a product within code language that supports this pattern

Microservices would have the benefits:
    Allows for encapsulation of the entire Ticket Reservation portion of the website
Cons:
    Is unaware of other attributes of the system that may also scale
    Requires multiple Microservices to scale at the same time due to load
    Careful slicing required to make the Domain Bounded Context the most reliable

#### Principles

Limited amount of (mental) capital (what hill do you want to die on)
    This testing tool over this other one, doesn't matter. They're testing

Establish principles, can't be everywhere at once or be involved in every decision.
Principles, guard rails or etc to setup for decisions not involved w/

Create the environment within which our projects can thrive

How do we know if they are being followed?

Short-feed back loops are ideal

Fitness Functions
    Second law of thermodynamics ("teenager bedroom", couldn't find anything)
    Universal law is disorder, software not immune
    Keep the team making good decisions, but change is constant
    Change Assumptions?
    What if architecture is designed to change?
        Guided incremental change?
    Components are deployed/features are enabled via toggles
        Deployment vs Release are different
        Hypothesis driven development
    A TODO List for Devs by Architects
        As long as these tests pass, you're good
        Lightweight, low ceremony, governance
            Shortens the feedback loop
        Is a mutation (closer or further from goals)
        Identify those key items that as a "ilities"
        Since it can be measured, doesn't mean we should
        Service Level Objectives (not an agreement/contract!)
    Set of tests to validate the architecture to meet our needs (pipeline, but will always be manual)
        E.g.
            Performance (can automate test)
            How many "paths" (cyclomatic complexity") are there? Shall not exceed a certain amount
        Consumer Driven Contracts
            Sprint Cloud Contract (schema)
            Can setup tests based around contracts and ensure that it is all functional
        App Faults, Timeouts, Ticking over pricing tiers for cloud providers, etc.
        Use Cost Ceilings, to cap incurrence of a cost
    Chaos Engineering
        Stress test systems to find weaknesses
            e.g. taking out wires from a server randomly
    Have a unified starting point, company wide (e.g. use one-based image)
    Some architects write, some are done by the dev team

#### What fitness functions would you recommend for the Group Kata (not implementation)

Load test up to 12,500 users/second (per deploy)
Test concurrently buying (per deploy)
Test unable to purchase the SAME ticket  (per deploy)
Test scalability (per release/further claim)
Test Visibility of tickets being claimed (UI and total #s) (per deploy)

#### 

Normal vs warning vs alert

Atomic vs Holistic
    Some attributes can be tested in isolate (Atomic)
    Some cannot and needs to be merged with others (Holistic)

Triggered vs Continual
    Fitness Function triggered by something (Triggered)
    Conitnual are constant

Static vs Dynamic
    Metric based tests
    Range of outcomes of are reasonable

Automated vs Manual
    Automation is good
    Apart of deployment pipelines
    Legal department sign-offs, gates in pipelines

Temporal
    Fail on X date, to remind people to check
    Fail on updating of a package version

Never know everything up front
Can classify fitness function
    Key / critical decisions
        Should be a small, less than 10
    Relevant, not critical to architecture
    Non-relevant, note them

[Interrupted by Aaron]

Review old decisions and make sure that they are marked appropriately
Explain WHY you're picking a specific technology, so people know WHY
    Show credible reasons to explain it specifically

ADR => Storybook of the project
Architectural Decison Record (ADR)
