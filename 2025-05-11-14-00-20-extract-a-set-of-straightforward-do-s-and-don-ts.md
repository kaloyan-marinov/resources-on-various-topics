# Source

   `2018-10-11-hh-mm-jack-diederich-stop-writing-classes.md`
   `./2025-05-11-14-00-10-matthew-macdonald-the-case-against-OOP-is-wildly-overstated.md`



# Notes



   ## Introduction

   Object-oriented programming (OOP) is much less prescriptive than many people believe.
   Object-oriented languages give you a set of tools for creating and using objects.
   But they don's say much about how you should apply those tools to a problem.
   
   That means that
   there is a large gray area
   between OOP tools and the concrete practice of OOP.
   And it is a fact of life that
   the practice of OOP is not an exact science;
   instead, it is more akin to an art form.

   The art of practicing OOP can be summarized as follows:

   (a) giving an honest answer to the "What problem are we trying to solve?" question;

   (b) deciding <u>whether</u> or not OOP <u>has to</u> be used at all;

   (c) deciding <u>how</u> to break down a programming problem into objects.



   ## What is an «object»?

   Many introductory texts blur the line between
   code constructs and real-world objects, by presenting examples with:

   - `Animal` and `Dog` objects;

   - `Car` and `Wheel` objects;
   
   - hopelessly tied-together groups of `Person` and `Family` objects.

   A better description of objects is - like many honest answers - a little vague:

   > An object is a programming construct
   > that lets you pack together data and functionality in a somewhat reusable package.
   > Some objects may be `struct`s by another name.
   > Other objects may simply be bundles of related functions.
   


   ## Do's

   Start with these principles,
   (which are not specific to OOP but)
   which apply to programming in general:

   - <u>**value simplicity and readability above all else**</u>

   - <u>**write tests for your codebas**</u>
   
     Focus not on code coverage but on meaningful assertions.

   - <u>**YAGNI**</u> (You Ain't Gonna Need It)

     Don't build a new code construct
     unless you're sure there will be a concrete use case for it within the next 2 weeks.

   - <u>**continuous refactoring**</u>

     In order to achieve greater simplicity and better readability -
     both in source code, and in test code.

   - DRY (Don't Repeat Yourself)

   - the Law of Demeter 
   
     Restrict what classes must know about each other.

   > Choosing to apply OOP techniques to any given problem
   > is less important than
   > upholding the above-mentioned principles.



   # Don'ts

   This section is specific to OOP.

   - The fact that something sounds like an object <u>**does not**</u> automatically mean that
     it should be an object in your program.

   - Inheritance makes sense in framework design -
     in other words, as a tool for the people who build the tools that you use.

     You <u>**don't**</u> need inheritance
     if you're a fast-moving customer-focused team of agile developers.
   
     - If you want to reuse functionality,
       containment and delegation work perfectly well.
      
     - If you want to standardize different classes,
       that's what interfaces are for.

   - <u>**Do not**</u> glorify «design patterns».
   
     They can easily become
     a way to smuggle in overly complex OOP design
     under a veneer of respectability.
    
   - <u>**Do not**</u> glorify the following concepts:
   
     - separation of concerns
   
     - decoupling (including «loose coupling» and «strong cohesion»)
   
     - encapsulation
   
     - implementation hiding

     - abstractions

     And even if those terms do come up,
     people mean different things when they use them.

     They're not useful for furthering conversation.

     Similarly to inheritance,
     those concepts are not necessary
     if you're a fast-moving customer-focused team of agile developers.



   ## Conclusion

   OOP doesn't prevent you from creating sub-optimal solutions to a problem.

   Bear in mind that
   the set of tools which OOP gives you can be abused.

   An experienced programmer knows that, when choosing between
   a solution that's less object-oriented
   or
   one that's more object-oriented,
   you should pick the simplest approach that solves the problem at hand.
