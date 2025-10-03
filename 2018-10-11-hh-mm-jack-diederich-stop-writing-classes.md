# Source

    (
    yt
    >>
    Next Day Video
    >>
    Stop Writing Classes
    [by Jack Diederich, a Python core developer]
    )



# Transcript

I don't mean to disappoint,
but I'm actually going to agree with everything that Raymond [Hettinger] just said

<div style="margin-left: 20px;">
   [
   That refers to the preceding talk, which was given by Raymond Hettinger.
   The talk can be gleaned from [the schedule of PyCon US 2012](
        https://us.pycon.org/2012/schedule/
   );
   for convenience,
   that talk is titled "The Art of Subclassing"
   and
   can be seen at https://www.youtube.com/watch?v=miGolgp9xq8 .
   ]
</div>



   ## [recall the Zen of Python]

   ```
   Simple is better than complex.
   Flat is better than nested.
   Readability counts.
   If the implementation is hard to explain, it's a bad idea.
   If the implementation is easy to explain, it may be a good idea.
   ```

   All of these points say:
   don't do hard things, do easy things.



   ## Overview of this presentation

   [what the preceding talk by Raymond Hettinger was about]

   - classes can be very complicated

   - he laid out some principles
       how you should figure out
       what you shouldn't be doing



   [what this talk is about]

       (a)
       don't do hard things in the 1st place,
       do easy things

           all the places where people go wrong
           and
           how you can just not do that at all

           you end up doing that anyway
           - even when you're trying to avoid it -
           so this talk [is also going to explain]
           how to notice when you've gone down the wrong path
           [and, from there, how to]

       (b)
       revert complications later



   ## this is what I tell the guys at work all the time:

   I hate code and I want as little of it as possible in our product.
   
   We ship features, we do not ship code.
   
   We don't have customers because we have lots of code;
   
   we have customers because we have lots of features.



   ## this is the biggest overuse of classes you see out in the wild:

   ```python
   class Greeting(object):

       def __init__(self, greeting='hello'):
           self.greeting = greeting

       def greet(self, name):
           return f"{self.greeting}, {name}!"


   greeting = Greeting('Hello')
   print(greeting.greet('Bob'))
   ```

   This is _not_ a class!
   It looks like a class...
   [but] the signature of "this shouldn't be a class" is that
   it has 2 methods, one of which is `__init__`.

   Anyitime you start aliasing your classes
   to just instantiate them once, use them once, and then throw them away,
   in your brain you should be thinking,
   "Oh, I can refactor that - it can be simpler! Much simpler!"



   ## [Impressive words, which mean different things to different people, are not useful for furthering conversation]

   [
   if you have a Computer Science degree,
   it is highly likely that
   you were taught that classes give us the following lovely things:
   ]
       
   - separation of concerns
   
   - decoupling
   
   - encapsulation
   
   - implementation hiding
   
   I haven't used those words in 15 years
   (since I graduated).

   Anytime you hear someone using one of those words,
   they're trying to pull a fast one on you.

   It just doesn't come up.

   And even if [those terms do] come up,
   people mean different things when they use them.
   [They're] not useful for furthering conversation.
   


   ## Lots of you use 3rd-party APIs in your day-to-day job.

   Anytime you have to use someone else's code,
   the first thing you have to do is read it.



   ## [An example of] The overuse of classes...

   Lots of time people think you might need something later -
   you don't.

   Or you can just do it later; if it comes up, you know, do it.
   
   ```python
   class MuffinHash(dict):
       pass
   
   
   d = MuffinMail.MuffinHash.MuffinHash(foo=3)
   ```



   ## Namespaces are there to help
   
   To echo what Raymond [Hettinger] said, ...
   namespaces are not for creating taxonomies, ...
   namespaces are for preventing name collisions.
   
   If you have a deep hierarchy,
   you are not doing anyone any favors...
   
   The [Python] Standard Library has a very flat namespace.



   ## exceptions are overused

   Anytime you type a class,
   you should be thinking,
   "What am I doing this for?"



   ## [Guidelines for naming exceptions appropriately]

   For example:

   - bad:

     `EmptyBeerNotFoundError`

   - better:

     `EmptyBeer`

     `BeerError`

     `BeerNotFound`

   - best:

     You can just use [Python] Standard Library exceptions.
     People understand them.
     Unless you want to catch a very specific condition,
     `LookupError` is just as good as anything else.

   If you get an email with a traceback in it,
   you're going to have to go read it anyway
   and
   it doesn't really matter what the exception was named.

   Another reason you don't have to complicate the names of your exceptions is [as follows]:
   anyone who's reading your code [understands] that
   the thing right after either a `raise` or an `except` [has got to] be an exception!
   (So, adding the word `Exception` to the name of the class doesn't help.)



   ## [Start by using exceptions from the Python Standard Library; define your own exceptions only when you have to.]

   [The Python] Standard Library has got some rusty corners
   but it's a pretty good example of how you should do things.

   - 200k SLOC [= 200k lines of code]

   - 200 top-level modules

   - averages 10 files per package

   - it only defines 165 Exceptions

   So once again:
   any time you think you need to write an exception,
   you probably don't
   (because the Python Standard Library gets along quite fine with just 165).



   ## Sometimes you do want a class
    
   Classes are great for things that classes are great for.
   
   [Namely,] when you have
   a bundle of mutable data
   and
   a bunch of related functions that you want to use with that data,
   then yes - classes are the right thing to do.
   
   You don't have to do this much in your day-to-day,
   because if you're pulling something from the [Python] Standard Library,
   someone else has already done it for you.
   
   There is one case in the [Python] Standard Library where this isn't true,
   which is the `heapq` module:
   there's about 10 methods in the `heapq` module
   and
   they all act on the same heap,
   so their first argument is always ... the same thing,
   which ... implies:
   yes, this actually is a class.



   ## Classes encourage atrocities

   Oauth2 implementation

   htttps://code.google.com/p/google-api-python-client/source/browse

   ```python
   class Flow(object):
       """Base class for all Flow objects."""
       pass
   ```

   ```python
   class Error(Exception):
       pass
   ```



   ## Conway's game of life

   [see the source video for an example of how to avoid classes altogether]



   ## Conclusion

   (1) If you see a class with 2 methods..., it's not a class.

   (2) Don't make new exceptions when you don't need to. And you don't need to.

   (3) Refactor relentlessly.



# Q & A



   ## Raymond Hettinger:

   What do you think the social forces are that drive people to write "the ... Muffin-style code"?

   Jack Diederich:
   
   ...
   It's ex-Java people,
   it's what they teach in CS curriculum.
   It took years to beat it out of me.



   ## [audience member B]: ...

   Jack Diederich:

   Yes,
   it's a form of premature optimization.



   ## [audience member C]:

   ... `class MuffinHash(dict)` ...
   they might have come back later on and said, um,
   "make it a `namedtuple`"
   or
   "make it an `OrderedDict`"
   or
   "it must be dict such that we can iterate over it deterministically"
   or
   ...

   Jack Diederich:

   there's 2 things

   one:
   you shouldn't ... have planned for the future like that in the first place, preferably

   two:
   but if you think you had good reasons for it
   and
   then you notice later that they weren't good reasons,
   you can go back & refactor it out



   ## [audience member D]:

   is subclassing the built-in exceptions still overkill
   or
   is that more acceptable?
   ...
   from the angle [that] ...
   if you just catch all `KeyError`s,
   you're gonna catch errors you don't intend to catch.

   Jack Diederich:
   I don't use custom Exceptions until I need to ...

   [indeed, the described scenario can be problematic, but still:]
   define your own exceptions only when you have to



   ## [audience member E]:

   I've seen a lot of the pattern of
   "classes as mere containers for constants" -
   they don't actually do anything;
   they just hold a bunch of constants.
   How do you feel about those?

   Jack Diederich:
   ... it's sometimes useful to use classes as tiny namespaces -
   [e.g.] when you don't want to add a module ...

   it's even useful to hold functions in ...

   so if you want a small namespace with some constants in it
   and
   maybe a small bag of functions,
   then classes are fine
