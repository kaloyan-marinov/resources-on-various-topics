# Source

    (
        yt
        >>
        Python Italia
        >>
        Pro tips for writing great unit tests - Raymond Hettinger
    )



# Transcript

   ...

   # Test coverage

   I'd like to pass in a note of caution:
   it is very common, when people start using coverage,
   to look at the percentage of coverage
   and
   start trying to grow that number as if [having a bigger number is better].
        
   Is it possible to have bugs in your code and still have 100% test coverage?
   Yes.
   
   Is it probable?
   Yes. In fact, it's the case.
   
   100% means nothing.
   
   To get to 100,
   you have to test a lot of things that rarely could happen,
   possibly will never happen -
   like being out of memory, which is quite difficult to simulate.
   
   If you try to make the number bigger,
   generally it's a waste of time.
   
   There are lots of ways to improve code quality:
   you could have spent some of that extra time: 
   (a) doing a code reviews, or
   (b) improving your documentation, or
   (c) user testing.

   I love coverage -
   just don't get in the business of trying to make the percentage bigger.
   The percentage is not a measure of quality.
