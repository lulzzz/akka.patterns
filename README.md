# akka.patterns
A sandbox of akka patterns

## From Effective Akka (https://www.amazon.com/Effective-Akka-Jamie-Allen/dp/1449360076)

Workers Actors

    worker actors are meant for parallelization or separation of dangerous tasks into
    actors built specifically for that purpose, and the data upon which they will act is always
    provided to them. 

Domain Actors

    Domain actors, introduced in the previous section, represent a live
    cache where the existence of the actors and the state they encapsulate are a view of the
    current state of the application.
    
Extra Pattern 

    One of the most difficult tasks in asynchronous programming is trying to capture con‐
    text so that the state of the world at the time the task was started can be accurately
    represented at the time the task finishes. However, creating anonymous instances of
    Akka actors is a very simple and lightweight solution for capturing the context at the
    time the message was handled to be utilized when the tasks are successfully completed.
    
Cameo Pattern

    Those are good reasons for pulling the type you’re creating with the Extra Pattern into
    a pre-defined type of actor, where you create an instance of that type for every message
    handled.
    
Also See: https://www.javacodegeeks.com/2014/01/three-flavours-of-request-response-pattern-in-akka.html

Petabridge also have a post about this pattern, but have called it https://petabridge.com/blog/top-akkadotnet-design-patterns/

    The Character Actor Pattern is used when an application has some risky but critical operation to execute,
    but needs to protect critical state contained in other actors and ensure that there are no negative side effects.
    It’s often cheaper, faster, and more reliable to simply delegate these risky operations to a purpose-built,
    but trivially disposable actor whose only job is to carry out the operation successfully or die trying.
    These brave, disposable actors are Character Actors.

Superviser-Only Pattern

    introducing a layer of supervision between the
    [one hierarchy] and [another hierarchy of] children, as we see [below] [...] I can tailor
    supervision to be specific to failure that can occur with accounts and that which may
    occur with [a hierarchy].
    
                            +---------------+
                  +---------+   Actor       +-------+
                  |         +---------------+       |
                  |                                 |
         +--------+------+                      +---+---------------+
       +-+  Supervisor 1 +--+                 +-+ Supervisor 2      +--+
       | +---------------+  |                 | +-------------------+  |
       |                    |                 |                        |
    +--+------+     +-------+--+         +----+-----+         +--------+--+
    | child 1 |     | child 2  |         | child 3  |         | child 4   |
    +---------+     +----------+         +----------+         +-----------+
    
also see http://getakka.net/docs/concepts/supervision

    At this point it is vital to understand that supervision is about forming a recursive fault
    handling structure. If you try to do too much at one level, it will become hard to reason about,
    hence the recommended way in this case is to add a level of supervision.

Sentinel Pattern

    I call these kinds of actors
    “sentinels,” as they guard the system from falling out of synchrony with a known
    expectation of what state should exist in the system.

## Best Practices

https://petabridge.com/blog/how-to-stop-an-actor-akkadotnet/

Use Immutable Messages with Immutable Data

    The reasons for this are the same as stabilizing a variable before using it in a future—you
    don’t know when the other actor will actually handle the message or what the value of the
    variable will be at that time. The same goes for when you want to send an immutable value
    that contains mutable attributes.
    Erlang does this for you with copy on write (COW) semantics, but we don’t get that for free
    in the JVM. Assuming your application has the heap space, take advantage of it.
    Hopefully, these copies will be short-lived allocations that never leave the Eden space of
    your garbage collection generations, and the penalty for having duplicated the value will be minimal.
    
also see: http://hackerboss.com/i-have-seen-the-future-and-it-is-copy-on-write/

## Stashing Patterns

http://getakka.net/docs/working-with-actors/Stashing%20Messages TODO
