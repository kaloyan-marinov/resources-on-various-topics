# Source

    (
    medium.com
    >>
    The Case Against OOP is Wildy Overstated
    [by Matthew MacDonald]
    )



# Notes



   ## Introduction

   object-oriented programming (OOP) ... certainly has some enemies

   What all these rants have in common is that they
   point out (rightfully) some of the pitfalls in modern software development
   and then
   conclude (wrongfully) that this indicates a terrible rot at the core of the programming world

   Yes, object-oriented programming doesn't look so great
   if you conflate it with
   sloppy design practices and fuzzy architectural thinking.
   But are these crimes really an unavoidable part of OOP?

   ...



   ## The Original Sin

   The problem starts with one brittle assumption made by
   some OOP supporters
   and
   almost all of its critics -
   that OOP is meant to model the real world.
   This is the original sin of OOP,
   a corrosive idea that's responsible for countless bloated codebases.

   ... Many introductory texts blur the line between
   code constructs and real-world objects, by presenting examples with
   `Car` and `Wheel` objects,
   or hopelessly tied-together groups of `Person` and `Family` objects.
   ...

   This sort of design isn't wrong for everyone.
   But there are plenty of unhappy people handcuffed to
   [a large number of classes that are] far more complicated than they need.
   Did OOP encourage this?
   Maybe, but
   the real curprit is the idea-gone-wild that
   every idenitifable thing deserves its own object representation.

   > Nothing good happens when we forget that
   > our designs should be led by the needs of our code,
   > not the completeness of our object models.

   A better description of objects is - like many honest answers - a little vague ...:

   > An object is a programming construct
   > that lets you pack together data and functionality in a somewhat reusable package.
   > Some objects may be `struct`s by another name.
   > Other objects may simply be libraries of related functionality.
   > Deciding how to break down a programming problem into objects
   > is part of
   > the art of OOP.

   And, from the always-insightful Eloquent JavaScript:

   > The fact that something sounds like an object does not automatically mean that
   > it should be an object in your program.
   > Reflexively writing classes for every concept in your application
   > tends to leave you with ...
   > [a codebase that is] often hard to understand and thus easy to break.

   An experienced programmer knows that, when choosing between
   a solution that's less object-oriented
   or
   one that's more object-oriented,
   you should pick the simplest approach that meets the needs of your project.




   ## Design is Difficult

   If OOP is difficult to do right,
   that's at least partly because
   software design is hard to do right,
   no matter what tools you use.

   In fact, OOP is much less prescriptive in design than many people believe.
   Object-oriented languages give you a set of tools for using objects ...
   But they don's say much about how you should apply these objects to a problem.
   This is a great and deliberate ambiguity.

   The gap between theory and practice has fueled the interest in design patterns...
   Unfortunately, design patterns can easily become
   a way to smuggle in overly complex OOP design
   under a veneer of respectability.

   How do you avoid this trap?
   Focus on the rock-solid principles of good programming ...

   - DRY (Don't Repeat Yourself)
   - YAGNI (don't build it if You Ain't Gonna Need It)
   - the Law of Demeter (restrict what classes must know about each other)
   - continuous refactoring
   - valuing simplicity and readability above all else

   Start with these ... principles ...
   and
   let your design take shape in that environment.



   ## The Expectation Mismatch of Inheritance

   Some of the sharpest attacks launched on OOP target inheritance.
   Critics point out the very real «fragile base class problem»,
   where a codebase becomes frozen in time
   thanks to subtle dependencies between child classes and their parents.

   The solution to
   the «fragile base class problem»
   and
   other inheritance hangovers is surprisingly simple -
   don't use it.
   All the cautionary tales you've heard are true.

   When inheritance makes sense is in framework design -
   in other words, as a tool for the people who build the tools that you use.
   The .NET and Java class libraries would be a far poorer and less organized place
   without a rigorous inheritance hierarchy tying things together.
   But creating and maintaining this type of framework is a massive architectural task.
   It's not the kind of thing you want to undertake
   if you're a fast-moving customer-focused team of agile developers.
   And here's a dirty secret -
   you probably won't get it right unless you do it wrong a few times first.

   In other words, inheritance is
   a great feature when you use it indirectly,
   but rat poison squared when use it to extend your own classes.
   And you don't need it.
   If you want to reuse functionality,
   containment and delegation work perfectly well.
   And if you want to standardize different classes,
   that's what interfaces are for.

   ... OOP ... doesn't prevent you from appyling the wrong solution to a problem.
   It gives you a set of tools that can be enjoyed or abused.
   The rest is up to you.

   There's one criticism leveled against OOP that's probably true.
   OOP may not be dead, but its moment of total world domination is fading...
   pure OOP is shifting to make room for so-called multi-paradigm languages like Go and Rust -
   languages that have a slimmer set of object-oriented features and avoid some of the traditional OOP baggage.
   Sometime in the next decade we'll know these languages have truly arrived,
   when we see them featured in their own developer take-downs.
   ...
