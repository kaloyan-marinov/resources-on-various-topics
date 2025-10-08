# Source

   `2018-10-11-hh-mm-jack-diederich-stop-writing-classes.md`
   `./2025-05-11-14-00-10-matthew-macdonald-the-case-against-OOP-is-wildly-overstated.md`



# Notes



   ## Introduction

   Object-oriented programming (OOP) is much less prescriptive in design than many people believe.
   Object-oriented languages give you a set of tools for using objects ...
   But they don's say much about how you should apply these objects to a problem.
   This is a ... deliberate ambiguity.

   Furthermore,
   the practice of OOP is not an exact science;
   instead, it is more akin to an art form.

   The art of practicing OOP can be summarized as follows:

   (a) deciding <u>whether</u> or not OOP <u>has to</u> be used at all;

   (b) deciding <u>how</u> to break down a programming problem into objects.



   ## What is an object?

   Many introductory texts blur the line between
   code constructs and real-world objects, by presenting examples with:

   - `Animal` and `Dog` objects;

   - `Car` and `Wheel` objects;
   
   - hopelessly tied-together groups of `Person` and `Family` objects.

   A better description of objects is - like many honest answers - a little vague ...:

   > An object is a programming construct
   > that lets you pack together data and functionality in a somewhat reusable package.
   > Some objects may be `struct`s by another name.
   > Other objects may simply be bundles of related functions.
   


   ## Do's

   Start with these principles:

   - valuing simplicity and readability above all else

   - [write tests for your codebase, focusing not on code coverage but on meaningful assertions]

   - YAGNI (don't build it if You Ain't Gonna Need It)

   - continuous refactoring

   - DRY (Don't Repeat Yourself)

   - the Law of Demeter (restrict what classes must know about each other)



   # Don'ts

   - The fact that something sounds like an object does not automatically mean that
     it should be an object in your program.

   - inheritance makes sense is in framework design -
     in other words, as a tool for the people who build the tools that you use.

     you don't need inheritance
     if you're a fast-moving customer-focused team of agile developers.
   
     - If you want to reuse functionality,
       containment and delegation work perfectly well.
      
     - If you want to standardize different classes,
       that's what interfaces are for.

   - design patterns can easily become
     a way to smuggle in overly complex OOP design
     under a veneer of respectability
    
   - do not glorify the following terms:
   
     - separation of concerns
   
     - decoupling
   
     - encapsulation
   
     - implementation hiding

     And even if those terms do come up,
     people mean different things when they use them.

     They're not useful for furthering conversation.

     Similarly to inheritance,
     those concepts are not necessary
     if you're a fast-moving customer-focused team of agile developers.



   ## Conclusion

   OOP ... doesn't prevent you from designing sub-optimal solutions to a problem.

   OOP gives you a set of tools that can be used or abused.

   An experienced programmer knows that, when choosing between
   a solution that's less object-oriented
   or
   one that's more object-oriented,
   you should pick the simplest approach that solves the problem at hand.
