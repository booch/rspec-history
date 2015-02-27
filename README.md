RSpec History
=============

This is currently just an experiment.
(So no tests for a while, until the experiment is ruled a success.)

The idea is to keep a history of all test runs, and record information about each test.
We'd like to record the following information:

* How many times the test suite has been run
* Average runtime of the full test suite
* How many times each test has passed
* How many times each test has failed
* How many times each test has errored out
* How many times each test has been skipped
* Average runtime of each test
* Date of last failure/error for each test

With this information, we'd be able to gain more insights about our tests and code:

* Which tests are brittle?
* Which tests are taking the most time to run over the long run?

Longer term, we could use this information to be smarter (and data-driven) with regards to subsets of tests within the suite that we run.
For example, we could skip tests that haven't failed in a long time.
Or we could run a random set of tests, weighted by the inverse of the amount of time since last failure.
We could do those with a set time limit, a percentage of tests, or a percentage of passes versus failures.
But all that's a bit off in the future; the first part is just to gather the data.
(And the stuff that uses the data will likely be in a separate RSpec plugin.)


Other Thoughts
--------------

It'd probably be a good idea to throw away all the error and test counts the first time a test passes.
This is so as to not penalize a test for failing while the code for it is still being written.

We'd keep track of the tests by name.
I don't believe that there will likely be any name collisions using that method.
I know that tests will sometimes get renamed.
We'd likely just remove the test that no longer exists, and add the test that does exist, starting its stats over.
The other possibility would be to do some sort of heuristic involving line numbers and similarity of text.
But that would be error prone, and probably not worth the effort.

I'm not sure if there's a good way to tell if a given test has changed.
We could do a MD5 sum of the test's code.
But I'm not sure what the "right" thing to do would be in such a situation.


Inspiration
-----------

This idea came to me when I first heard about [Aaron Patterson's work][1] on using code coverage for individual tests to determine what code would affect a given test.

[1]: http://tenderlovemaking.com/2015/02/13/predicting-test-failues.html
