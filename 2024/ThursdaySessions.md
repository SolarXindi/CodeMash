# Thursday

## Software Test Automation ​and System Design

By Kate Jordan

Usual testing pyramid (unit, integration, end-to-end)

Why resist tests?
Higher dev cost when initially writing more code
Any test that you write must be maintained going forward
Tests against a system not designed for testing is challenging and can be expensive

Why test?
Automated testing (especially full system) is much faster
Provides rapid feedback loop to engineers when making changes
    Allows for more targeted feedback, especially when QA finds the bug and you are unsure of WHERE the issue is
Improves system stability when making code changes
Provides documentation on how system works
Leads to better system design and more maintainable code
Allows you to continue to grow your codebase w/o having to add large # of manual testers

### Unit Tests

Test happy paths (combinations) and exception testing
Complicated testing portion, use SOLID Design Principles
    Dependency Inversion (using interfaces instead of concrete classes)

Broader Design Applications
    Interfaces makes it easier to bring in new concrete examples


### Integration Tests

Seed data to database, run tests
Can use Docker to keep data isolated

#### Design Patterns

Microservices
    Smaller service with granular API routes
    One database per service
    De-coupled comm between APIs using events
Messaging Solutions (e.g. Kafka)
    If something doesn't have to happen right away, use a message to queue up and handle them later

### End-To-End Tests

User-based tests
Focus on critical paths

### Comments after

Keep doing what we're doing, but see what we can do to get more integration tests, especially in a dockerized setting

## Not Your Mother's or Father's C#

By Bredan Enrikc

### Outdated Info

Requires Visual Studio and Windows to develop
Only runs on Windows
Needs IIS to host it
Just curly braces and indentation halfway across the screen
Just like Java (was, not anymore)
Monolithic business app

### Curly Braces and Indentation

Usings don't need curly braces

### C# was missing basics

No generics (awesome now)
No Lambdas (even using strongly typed)
Tuple Type is a joke (4 years ago has the good one)
Async/Await (other languages adopted the syntax)

### Recent new features

Every November, new version of c# and dotnet (tied together)

Primary Constructors (C# 12)
    public readonly class Rectangle(int length, int width){ public int Area=> length*width; }
    Basically a Record Type, but a class!
Record Types (C# 9)
    public record Session1(string Title, DateTime SessionTime, String SpeakerName);
    Automatically add the constructor parameters as properties
    Not only saves code, but also adds
        Equality Checks (as long as properties match, it is an equality match)
        Don't have to compare properties between classes manually (person.FirstName == person2.FirstName)
    Don't have to use Primary Constructor, can use standard way of building out the properites
    Also works with Structs
    .ToString() puts it as Json Data structure instead of "Person Object"
    You can new instance from existing records
    "with" keyword, take the existing record and apply a change "with {prop = value}"
Constructor Interfaces (C# 10)
    Session session = new("this, DateTime.Today", "Brendan");
    Be a bit careful, especially with weird typing issues
Init-Only Setter (C# 9)
    //Set in Constructor or Init
    public string BirthName {get; init; }
String Interpolation
    Best feature
    C# 10 added a constant String Interpolation
Verbatim Strings (before C# 11)
    The @ sign
    Now have Raw String Literals (triple quotes)
        Allows you to use quotes INSIDE of the string
    Also have Interpolated Verbatims Strings
Pattern Matching
    Before casting an object as a separate object
    Is Expression
        if (shape is Rectangle rec) return rec.Length * rec.Width;
        Declares a new object "rec" if it is a rectangle
    Can pattern match against a CONSTANT
    Can pattern match against a TYPE
    Can pattern match against property patterns
        Nested Property Pattern is in C# 10
    List Patterns
        Can check against lists or arrays, with "..." wild card ("A", ..., "B")//Check start and end
            "A" or "B", ... (boolean pattern in C# 9)
    Span<char>
        name is "Brendan"
        name is ['B', ...] //starts with B (list pattern)
Required Modifier (C# 11)
    [SetsRequiredMembers]//Required to complete Compile Check. If you DO set it and don't set it, it is ignores it and could be issue
    public User(int id, string name) => (Id, Name) = (id, name)

    public required int Id{get;set;}
    public required string Name{get;set;}
File Access Modifier (C# 11)
    file enum RelatedEnum //Can only be used in this file
Collection Expressions
    int[] first = [1, 2, 3]
    int[] second = [4, 5, 6]
    int[] all = [... first, ... second, 7, 8, 9]
Top Level Statements
    Removing of the main.cs file, just using Console.WriteLine("Hello World");
    Why? Demo Apps
Static Usings
    using System
    using static System.Console
    WriteLine("Hello World") //Notice no Console.
    Why? Demo Apps
Tuples
    (bool success, int number) SafePArse(string s) => (int.TryParse(s, out int n), n);
    var r = SafeParse("123");

    Tuple Deconstruction
    var (number, success) = SafeParse("123")

    Declare/Assign (C# 10), missing of the two styles
        int x = 0;
        (x, int y) = point;
Alias Any Type (C# 12)
    using MyUser = (int id, string name);

    (int id, string name) myUser = (1, brendan)
    string message = "Hello and welcome!";
    SendMessage(message, myUser);

    //Changed to
    MyUser myUser = (1, brendan)
Global Usings
    GlobalUsings.cs
        global using static System.Console //Don't use this in reality, an example
Using Statements (no curly brace)
    'nuff said
Null Reference Exception
    Tons of stuff to help avoiding Null References
    Null-Coalescing (A ?? B)
    Null Conditionals (A?.B) and this does Null Propogation
    Null-Coalescing Assignment (public Thing THing => _thing ??= new Thing())
    Null Annotation Contexts (Nullable Reference Types)
        <nullable>enable</nullable>
Reverse Indexing
    ^1 (end of list)
Range Indexing
    var middle = numbers[3..7];
    var firstFew = numbers[..3];
    var lastBunch = numbers[4..];

    var lastFew = numbers[^3..];
File-scoped Namespaces
    Reduces curly braces on namespace

### Future Items

Only current one is Params Collection
    public bool Something(params int[] numbers)
    { //Do Something }

    Something(1,2,3);

    public bool Something(params string letters)
    Something ('a', 'b', 'c');
    Something("abc");

## Async/Await from the Ground Up

By Stephen Cleary

Concurrency in C# Cookbook (by presenter)

### Terminology

#### What is Async
Threads
Multi-tasking
Parallel Processing

Asynchronus/Asynchrony
Concurrency
Reactive

            Concurrent

    Async                       Multithreaded
                                    Parallel

Multithreading is one set of async (Paralle is kind of a subset)

Asynchronus code is doing more than one thing at the same W/O more threads
Code -> Overlap (code to talk to OS) -> OS -> Device Driver (via IO Request Packet)
Calls back a Async Process Code into the user stack
No thread is being blocked (polling), using Interrupt Service Request

Synchronus Code
Over is now "Thread"
Kernal mode is the same between async and sync (for Windows). All IO is async in the Kernal

Benefits:
Client: Responsiviness, UI Thread free, Better UX and required by many app stores
Server: Scalability, minimize threads used to serve requests, 10x-100x scalability (same box), faster response with more traffic

Async allows await (method only)
Transform the method into a state machine, similar to the yield keyword

Await takes a single argument
Awaitable: Taks/ValueTask (Future/Promise)

Await "yielding execution"
If task is complete, continues synchronously
If Task is not completed, continues asynchronously
    Pauses the method and registeres it with the task
    Then returns

Await "resuming execution"
Pausing/Resuming
    Where to resume? UI, thread pool, etc.
By default, async captures a sync context (if null, on task scheduler, it that is null then the Thread Pool). UI Thread has its own sync context

### Async as a Language Feature

Archaeology
Events -> Callbacks -> Futures -> Async/Await

#### Futures

Future completes exactly once, either with a value or exception
Supports continuations (callbacks)
Task<T> in C#
A future can be anything
File download, database write, timeout, join of other futures, or mutual exclusion
Can build an async lock

Task, Task<T>, ValueTask, ValueTask<T>
Operations have a distinct beginning and ending
By the time you get a task, it's already started

Three end states:
Successful (Task<T> has result)
Faulted (Task/Task<T> has an exception)
Canceled

Tasks <> Threads

Task = Reference Type
ValueTask = Value Type (can only be used once)

#### Tasks

Promise vs Delegate Tasks

Promise Task:
Primarly used in async code
Represents an event or signal

Delegate Tasks
Primarly used by Parallel code
Has code (delegate) to run; is scheduled, etc.

### Conceptionalizing Async

Await = Async Wait
Task<T> is a future value of T
async wraps future values into Task<T>
await "unwraps" it

hint: Async is a monad in functional languages

Callbacks
    At runtime the code stack inverts
    How Garbage Collector doesn't get confused

.Wait() on a Task will **block** the thread

### Refactor PIC away from Parallel.ForEach??? Specifically BLIS calls

## Automating your smarthome without the cloud

Agenda:
Why anti-cloud
Z-Wave vs Zigbee vs Wifi vs Matter
Home Assistant
Bright ideas for bulbs, switches, etc.
How to use the cloud

### Why Anti-Cloud

Stuff breaks when cloud services go down
e.g. Nest Cam is solely depedent
    Ring was taken down by an AWS outage
    Google down, Nest Thermostat was solely down because of that
Vendor Out of business (Insteon), completely out of luck
Lackluster attention to security
    Ring doorbell leaked wifi login
    Wyze data leak
Limited functionality / interoperability
Poor performance
    Syntax issues, connection issues between cloud and network

### What is a "truly smart home" is

Automation is better than control
    Walking down to a room, have 5 lights in the way. How to turn on? Voice better, but speaker range
    Motion Sensorsto control said light groups
    Smart automations beat dumb automations
        Lack of larger context
        Unable to disable them if wanted
    Make smart automations that are context aware
    Don't care about what happens to others
    Works for other people, not just a singular person
    
### How to get to the promised land -> Hubs

Bring the Brain/Hub into the home
    Hubitat
    SmartThings (Cloud-based)
    Home Assistant
    Apple HomeKit (Apple but can be local)
    HomeSeer

#### Communications
Zigbee, Z-Wave, Matter and WiFi

WiFi are not standardized. Designed to support vendors. Usually depend on the Cloud.

Matter is brand new, Zigbee and Z-Wave have been around for awhile

Zigbee/Z-Wave are Mesh Networks (devices talk to each other)

Zigbee -> No limit of hops between devices
Up to 65,000 devices
2.4Ghz, fast but WiFi can interfere
Loose certification process, interop issues

Z-Wave -> Max 4 hops between devices
Up to 232 devices
No Wifi interference
50-100 feet between devices
Robust certification, reliable interop

Matter:
Launched in Nov 2022 (announced in 2019)
Designed for multi-vendor interop
Adding another protocol to a vendor encased garden
Uses Wifi, Thread (low power devices in mesh) by Google (2.4Ghz), and BlueTooth Low Energy (for "easy" setup)

Presumptions by presenter:
Z-Wave will stick around
Zigbee may die in-case for Matter

Hubitat
    $120 box with OS installed, Z-Wave and Zigbee already installed
HomeSeer
    $150-999
    Both hardware and software
    HS4 run on Windows or Linux
Home Assistant
    I already know, use it

Choose hardware, install software, configure devices, make magic happen

### Choose Hardware

Lots of different options

### Install Software

OS, Container, Core and Supervised

### Configure Devices

Need to get USB sticks for Zigbee/Z-Wave
Z-Wave, add Z-Wave JS
WiFi takes a lot of power, Z-Wave is more low energy

ZooZ (motion/temp sensor, battery powered)
Smart Plug to determine power draw
RPi Zero and $5 Ultrasonic Distance Sensor
    Reads sensor to determine state
    Uses MQTT (lightweight sub/pub) for collecting sensor data
Home Assistant can use MQTT, but needs to have a Data Broker
Can modifer sensor data in the configuration.yaml

DIY can be fun/easy!

### Automation beats Control

Triggers/Conditions/Actions

Can create toggles (boolean), which can be assigned to a room

Can control local network devices
Can tell it only record video of a garage if the garage door is open and motion is detected

### More Bright Ideas

Flic.io (battery powered button, with adhesive)
This can toggle items
Can configure it to call a WebHook in Home Assistant

### Data

InfluxDB and Grafana
Graph Data over time
    Air Quality
    Network issues

### Remote Access

Nabu Casa to pay $6.50 per month
or do it yourself

### Examples

Ceiling Light + Fan switch from Inovelli
NSPanel Pro -> Displays a Home Assistant Dashboard
    Changes per day and sensor
Portable Scene controller from Remotec
SwitchBot controlling an old pedastal
    Presses button
RPi w/ motion sensors using CAT5 cables
    RPi Zero, with 3 infrared sensors -> Connected via CAT5 Cables
ESP8266 Microcontroller to monitor Dryer
    Senses electric current in around a cable

bit.ly/LocalSmarthomeFTW

## Aerospace Engineer for Computer Scienctists

By Illyana Smith

Crossover

Write requirement, write validation/testing steps
Gilded Rose Kata (TDD oriented)
Fewer points of failure (KISS)

First manned flight (US) was built as an antipattern / spaghetti code
IIS was built with good (after the initial research) practices and modularized
IIS has Separation of Concerns (rooms)
IIS also does depency injection

## Alerts Don't Suck. YOUR Alerts Suck.

By Leon Adato

Oyster Talk(TM)

Site Reliability Engineering has their own defintion
What is the value of an alert?

Inbox Rules indicate that you are ignoring an alert, so what value are those?
A hill I will die on: FYI Alert is trash

Three important rules:

* Alerts are not monitoring x3

High CPU does not matter, 98% but everything runs means it is correctly sized

Monitoring vs Observability
Should be Monitoring **and** Observability

Monitoring:

* Known Unknowns
* All cardinalities welcome
* (Mostly) manual correlation (connection between parts of the infrastructure)
* Domain specific signals

Observability:

* Un-nkown Unkowns
* High Cardinality
* Correlation baked-in
* Golden Signals (latency, traffic, errors, and saturation)

High Cardinality is depraved from a lot set of disparity systems

### Alerts have to matter

A simple algorithm

IFF(Huamn && do something && now && about $problem) == true

If not about a human, automate it.
If is it not right now, put it in a report it.
if it isn't a problem, dashboard it.
If not doing something about it, throw it away.

Taking away resources from the system when it could be doing something else.

#### Issues with CPU Alert

Correlate the high CPU with other factors, abandonment rate of users, more jobs than expected are in the queue.
What are you going to do about it?

### Value of monitoring/alerting

Take timeframe into account, don't let human bias influence it.
Fixed thresholds, but better to use a relative off a baseline
    Normal for the last Thursday before Tax season starts
Use a combination of fixed ceiling and relative baseline, so that if it exceeds baseline but NOT exceeding the fixed. Don't alert

### Automation

Respond to an event (disk getting close to full), automate the response
Still allows for humans to deal with it, if the automation fails

Talk to the person who deals with a ticket, about what they do. Can you automate it?

Example:
    IIS App is slow
        Clear the Application Pool (automation)
        (wait)
            Reset the IIS Service
            (wait)
                Rebuild from an image/remotion it/virutalization reset
                (wait)
                    Move to a new region/site/whatever
                    (wait) Send a ticket, with the feedback from all the above

Can respond faster to more critical tickets if they are not bombard by issues that can be fixed by automation

### Lession 4 - Skilled Interviewing

Hunting for the great "useful alert", who is initially a project manager or something like. They want to push to production, so they'll lie.
Find the person receiving the ticket a month in the future.

How do **YOU** know when something went wrong?
How do you know when it's "all better"?
    e.g. Diskspace: 90% vs 89%, what is "all better". Stay below 75% for 20 minutes
    Never auto-close tickets, but do agree with reversal
Is there a knowledge article for it (yet)?
    Don't do an alert for it until then, as you don't know enough about the alert
Can you make it happen on purpose?
    Spelling errors, measurement errors (C vs F)
    If you cannot make it trigger, inverse it and verify that you are getting GOOD responses

### The work never ends

Go back every so often and ask the ticket receviers on how it is going for them.
    Even if everything is all good, they make ask for other assistance/help.

Remove interruption and toil from daily lives
