# Friday

## Application Architecture Patterns

By Joe Guadagno (Board of Directors - President of the .Net Foundation)

Slides: jjg.me/aboutjjg

About 13 software patterns, about designing the application

Don't re-invent the wheel

### Layered Pattern

    Presentation Tier (Mobile/Web)
    Logic Tier (Place/Ship Order)
    Data Tier (Database, Storage)
    Changes tend to bleed upwards, so changes in data means changes in the logic and/or presentation tier

### Model, View, *

    Model, View, Controller (MVC)
    Model-View-Presenter (MVP) -> Semantics around words
    Model-View-View-Model (MVVM) -> Semantics around words

    Model
    /   \
  View  Controller
    \   /
     User
    Model Updates View
    View See User
    Users uses Controller
    Controller Changes Model

    Big benefit: Controller and the Model have separate of concerns, a Controller owns a Logical Function
    Still has issues with bleeding changes upwards
    Hard to get specialized roles, as they are tied together. Typically Full-Stack Devs, as they have to know all the elements

### Event Driven / Event Sourcing / Pub&Sub

    WinForms is EventDriven

                Account Charge
                /
    Order Placed - Inventory Check
                \
                Inventory Deduct

                Ship Package
                /
    Order Ready - Update Order

    Breakdown elements of code into segments and the Event Caller doesn't care about specifics of a further down stream
    Need another set of software to help (Kafka, MSMQ, Event Bus), as a message broker

### CQRS
    Command & Query Responsibility Segregation

                User Interface
            |                               ^
 Commands   |             Query |           | DTO
            |                   V
    Command Bus                 Query Facade
            |                   |           ^
            |                   |           |
            |                   V           |
    Command Handler             Thin Data Layer
    |           ^               |           ^
    | Aggergate |               |           |
    V           |               V           |
    Domain Model interaction    Event Handler Data
    |           ^                       |
    |           |                       |
    V           |                       |
    Repository    -> Event Bus <- Event Handler
    |           ^
    |   Events  |
    V           |
    Event Store

### CQRS + Event Sourcing

    Same as CQRS, but add a lot of Facades around it
        Multiple clients connect to the network
    Event Bus is much bigger than just CQRS and they have multiple subscribers and Handlers, who connect to the database

    Blackbox style functionality, allows you to reconstruct the data from all the messages 
    Allows ignorance of Data Storage, API or other items
    Good for a lot of transactions coming in BUT not going out
    Querying = Querying the status of what is happening
    Topics subscribe to the events, can break down a lot of downstream effects (posting a queue, so you can post to ALL the social media websites)
    Can turn off/create new subscribers super simple

### Plug-In / Micro-Kernal

                 Account Component
                         |
    Order Component <-> App <-> Inventory Component
                         |
                    Shipping Component

    Add-ons/Plug-Ins for Microsoft Word/Excel, Outlook, etc.
    Has a contract on HOW to hook into it
    Not common, more for installed apps

### SOA / Service Oriented / Microservices

    Capability Pattern
    Widgets call a bunch of individual services, as long as the contract is followed
    Based on Event, where they don't care about implementation specifics
    One common issue is breaking them down too far, meaning you have 1,000+ different ones.
    Focus more on keeping them around Capabilities
    More Micro you make something, the more you have (e.g. build pipelines)
        Makes more specialized roles within the team, so one person knows a specific one better
    
#### Common Microservice Pattern

    Ambassador (Logging, telemtry (AppInsights, NLog, etc))
    Anti-corroption Layer (Sync data to the Legacy System)
    Backends for Frontends (BFF) -> Becomes a central API to organize calling a lot of smaller APIs (MVC Style)
    Bulkhead
    Gateway Aggregation (apart of API Gateway/Load Balancing)
    Gateway offloading (apart of API Gateway/Load Balancing)
    Gateway Routing (apart of API Gateway/Load Balancing)
    Sidecar (Telemetry/metric gathering for the infrastructure)
    Strangler Fig (figures out where to send the query, between new and legacy systems)

### Serverless / Cloud / Not on my PC

    Not really a "pattern", there are give/takes for building in the cloud vs on-prem

### Toolbox

    Because we have a hammer, not everything is a nail

## Building Event Driven User Interfaces

By Sam Ferree

Pure Function -> Deterministic functions, same input, same output
Pure Components are identical

Impure is influenced by state or data from a source off a server

Tiering:
Pure Components
Impure Components
Impure Service/Effects

How to manage state in impure elements?
State in the URL (but may not work for a LOT of state)
Pub/Sub services to a specific type of data

Impure Service gives data to 1+ impure components, data input from one and stream to another
Too many pub/subs components came out
Redux (reduce) way of managing this
    Impure Component -> Action -> Reduce -> Create New State -> Push State up to the other states
Had a lot of problems, data all in one place. Not great for decoupling (slices help)
    Testing components were a pain

Backend:
    "Noun" Service, but done via RPC
    Connections grew exponentially when a new service is added
    Distributed Monolith
    This is a well known/researched topic
    Wrap stuff into microservices based on domain/"verb"
    Solved talking between microservices talking using a Message Bus

Programming is Fractal
    Distributed Systems were simplified by encapsulating state and message passing
    Object Oriented Systems were simplified by encapsulating state and message passing
    Component Based UIs could be simplified by encapsulating state and message passing

Redux/ngRx/RxJS are Immutable and Shared
Event-Driven are Mutable and Local

Event Driven Component

* Subscribe function
* Unsubscribe function (memory leaks :D)
* Publish function

Thinking in Events and Event Handlers

State Machines

Events can trigger state transitions
State transitions can trigger events
Loaded State -> Completed State (based on user input)

For his code
github.com/SamCoSystems/DispatchR

## Async Masterclass

By Stephen Clearly

ValueTask
High performance code that needs to reduce allocations
Classic Use Case: Socket (LEADS style)

ValueTask can also be IValueTaskSource (pooled/recycled source instances, re-usable Task)
tinyurl.com/value-task

Only Consume once
await - 99% case
IsCompleted for fast path

Cannot block
.result .getwaiter().getresult() will compile but may fail at runtime
Even worse, they may work at runtime but block

Producting ValueTasks
AsyncMethodBuilder(typeof(PoolingASyncValueTaskMethodBuilder<>))

IAsyncDisposal
No official patterns on can/should support both
Not supported everywhere (AsyncServiceScope is 6.0+)
    Nito.Disposables if you want helpers

Async Disposal - Why?
Async Streams
    Yield does state machines in the background

    Try/Catch/Finally -> Wraps the state into a try catch (logical dispose)

IAsyncEnumerable -> AsyncDisposable

Observable -> Async, Multiple Values, Push Values
IAsyncEnumerable -> Async, Multiple Values, Pull Values (API Calls, Database Queries)

AsyncLocal
    IHttpRequest uses this under the hood

    Use using to make scopes explicit
    Use immutable types (difference between modifying and setting the value)
        Can potentially share state amongst the usage
    Use sparingly
        Implicit data is too magical e.g. culture
        Similar drawbacks as global variables

    Flowed by ExecutionContext
        Async does a shallow copy at the beginning method, so it doesn't override anything
        Set top level, flows down
    Why?
        Primary Use-Case
            Attaching Contextual Data to log messages
        Middleware calls next, instead of being isolated
        Can add contextual data (such as user id, sematic logging) via middleware for ALL logging
    Pitfall
        Exception logging missing context data
        How does middleware work?
        How does exception logging middleware work?
        Solution: throw context enrichers
            Depends on logging systems (presenter uses gray log, seemingly built by them/him)
            Shows demo of "Seq"
                logging scope (dictionary style)
                Shows that the logging scope data is missing w/o middleware for the Exception
                Enrichers fix that context destruction
                    He wrote a library (nito.Library) to do it default, but Seq has it

    tinyurl.com/toub-async
    tinyurl.com/asynclocal
    
    E.g. AsyncLocal<int>

Channels

Async Producer/Consumer Queues
Replaces hand-grown or TPL Dataflow
Consumer: ReadAllAsync
    Awaits for all things to be added
Producer: WriteAsync + Complete
    Can block (write)
Require them being Bounded for backpressures, otherwise will keep growing and growing

PauseToken

Coordination objects (lock, manual reset event, auto reset event, monitor)
Do some of those "lock" async, but lock is blocking a thread

Instead of cancelling a task, we want to Pause and Unpause it
WaitWhilePausedAsync

Can split into a "Source" (controller) and a "token"

Similar to ManualResetEvent

Event: "a thing that is signalled or unsignalled and enables waiting for it to become signalled
    OS Objects, not C# objects

    (=> signalled) or (=> unsignalled)

Pause -> Reset
Unpause -> Set
WaitWhilePaused -> WaitOnce()

Usually TaskCompletionSource

Set/WaitUntilSet is simple
Reset is complicated, need a new source
    Can add a lock, since we're returing a Task and NOT awaiting the task itself
Will work most of the time
    Can cause deadlocks
        TrySetResult() or any completion result, as they call back on the code with sync
        Have to add TaskCreationOptions.RunContinuationsAsynchronously on the TaskTokenSource
NEVER INVOKE END USER CODE WHILE HOLDING A LOCK
    Deadlocks will happen

    CancellationTokenSource.Cancel, TaskCompletionSource.TrySetResult (and friends) invoke End-User Code!

TCS Dictionary

    Task Completion Source Dictionary

    Common Situation
        Multiple Requests and replies, where replies may not be in request order
        Solution: TCS Dictionary

        Operations: Insert, Remove-And-Complete
        Always complete your Task!

    Higher level than lower code
    
    Good for higher level API Client calls

    Concurrency Dictionary (GUID as Ids)

    TrySet/TrySetException

    Building TCP/IP client/server that uses ValueTask Socket methods, System.IO.Pipelines, Channels and TCS Dictionary all together (14 hours)
    tinyurl.com/async-tcp

AsyncLazy: Simplicity
    Easy solution (Lazy<Task<T>> with GetAwaiter())

    TaskAwaiter<T>

    Complexity:
        How to execute delegate
        Exception cached (same as Lazy)
        Should also reset on demand?

    tinyurl.com/asynclazy-????

AsyncCaching

    NOT the IMemoryProvider
    The Caching is all TASK based, as you are caching the TaskCompletionSource, instead of the result

    tinyurl.com/async-cache

## Creative Problem Solving

TODO: Add
