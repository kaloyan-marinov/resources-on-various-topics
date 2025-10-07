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
   concluce (wrongfully) that this indicates a terrible rot at the core of the programming world

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
   