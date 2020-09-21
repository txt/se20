<a name=top>
<a href="http://tiny.cc/seng20"><img  width=700
  src="https://raw.githubusercontent.com/txt/se20/master/etc/img/teamBanner.png"></a>
<hr>
<p>
&nbsp;<a href="https://tiny.cc/seng20">home</a> ::
<a href="https://github.com/txt/se20/blob/master/docs/syllabus.md#top">syllabus</a> ::
<a href="https://github.com/txt/se20/blob/master/docs/syllabus.md#timetable">timetable</a> ::
<a href="https://drive.google.com/drive/folders/1ZFn6H8-4kx5uP34bpFgIFonkz9Tw3nYM?usp=sharing">groups</a> ::
<a href="https://moodle-courses2021.wolfware.ncsu.edu/course/view.php?id=3873">moodle</a> ::
<a href="http://seng20.slack.com">chat</a>  ::
<a href="https://github.com/txt/se20/blob/master/LICENSE.md#top">&copy; 2020</a>  
<br>
<hr>

# Testing (the end)

## More on Formal Methods (example)

### "Testing" and Product Lines and Formal Methods

A feature model is a "product line"; i.e. a description of a space 
of products.

Question: what are the _different_ products we can pull from the following?


<img src="https://www.researchgate.net/profile/Paolo_Vavassori3/publication/281701630/figure/fig1/AS:308695956246528@1450610259729/Example-of-a-Feature-Model.png">

Now that was a small feature model. Suppose we are talking about something
really big like a formal model of the LINUX kernel with 4000 variables
and 300,000 contrast. Q: How to reason over that space? A: use a theorem prover.
e.g. _Pycosat_.

## Feature Models and Formal Methods

The following example comes from the excellent documentation
at the
[Python Picostat Github page](https://github.com/ContinuumIO/pycosat/blob/master/README.rst)

Let us consider the following clauses, represented using
the DIMACS `cnf <http://en.wikipedia.org/wiki/Conjunctive_normal_form>`_
format::

   p cnf 5 3
   1 -5 4 0
   -1 5 3 4 0
   -3 -4 0

Here, we have 5 variables and 3 clauses, the first clause being

_x1  or not x5 or x4_

Note that the variable x2` is not used in any of the clauses,
which means that for each solution with x2 = True, we must
also have a solution with x2 = False.  In Python, each clause is
most conveniently represented as a list of integers.  Naturally, it makes
sense to represent each solution also as a list of integers, where the sign
corresponds to the Boolean value (+ for True and - for False) and the
absolute value corresponds to i-th variable::

   >>> import pycosat
   >>> cnf = [[1, -5, 4], [-1, 5, 3, 4], [-3, -4]]
   >>> pycosat.solve(cnf)
   [1, -2, -3, -4, 5]

This solution translates to: x1=x5=True,
x2=x3=x4=False

To find all solutions, use `itersolve`::

   >>> for sol in pycosat.itersolve(cnf):
   ...     print sol
   ...
   [1, -2, -3, -4, 5]
   [1, -2, -3, 4, -5]
   [1, -2, -3, 4, 5]
   ...
   >>> len(list(pycosat.itersolve(cnf)))
   18

In this example, there are a total of 18 possible solutions, which had to
be an even number because x2 was left unspecified in the clauses.

The fact that `itersolve` returns an iterator, makes it very elegant
and efficient for many types of operations.  For example, using
the `itertools` module from the standard library, here is how one
would construct a list of (up to) 3 solutions::

   >>> import itertools
   >>> list(itertools.islice(pycosat.itersolve(cnf), 3))
   [[1, -2, -3, -4, 5], [1, -2, -3, 4, -5], [1, -2, -3, 4, 5]]

### Feature Models and Product Lines

[Software installation as a formal methods problem](http://cseweb.ucsd.edu/~lerner/papers/opium.pdf)

Lets represent software dependancies in a logical framework:

<img src="../etc/img/opium.png">


If we run Picosat over these formulae then:

- Any solution that satisfies all the constraints...
- Is a different way to create a valid install of the program.


Variants:

- min install: 
   - add a cost to the install effort of each part
   - score everything coming out of `itersolve` (sum that cost)
   - pick the easiest thing to install
- optimizing:
   - generate one solution, ask some human what they think
   - if they don't like, negate it add it to the theorems
   - so future solutions will _not_ contain the thing you don;t like

**Important note:** in practice, except for trivally small 
problems, no one writes DIMACS manually. 

- Instead, we write code to generate DIMACS via some code. 
- For example:
  [running code](https://github.com/ContinuumIO/pycosat/blob/master/examples/opium.py).

## Scale-up Issues

### Scaling up SAT Solvers

SAT solvers are great but as software gets really really big, they need help.

- [Scalable product line configuration: A straw to break the camel's back](https://www.semanticscholar.org/paper/Scalable-product-line-configuration%3A-A-straw-to-the-Sayyad-Ingram/3384176ef4196797603ae2ca68ff353bb4233668)
  Abdel Salam Sayyad, Joseph Ingram, H. Ammar, Tim Menzies
  2013 28th IEEE/ACM International Conference on Automated Software Engineering (ASE)
- [Building Very Small Test Suites (with Snap)](https://arxiv.org/pdf/1905.05358.pdf),
  Jianfeng Chen, Xipeng Shen, Tim Menzies, 2020

### Scaling up TDD

- Continuous integration at Google
  - Continuous change to the code base
  - Continuous testing
- January to October 2013
  - Google ran 3 billion unit tests
  - Global network of machines
  - Problems
      - Running out of cpu 
      - less that 0.5% of those tests ever failed
      - Long lags from submission to “passed
- Test case prioritzation
  - Select test if (a)new, or (b)recently failed or (c) not recently executed
  - Found more tests that failed, much earlier
  - Greatly reduced time for programmers to get feedback

<img src="../etc/img/googletdd.png">

- Very many priorization schemes
  - Different according to what information they need

## The Big Question

Why does testing work?

