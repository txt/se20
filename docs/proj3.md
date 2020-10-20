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

# Project 3a

<a href="https://en.wikipedia.org/wiki/Monument_to_the_laboratory_mouse#:~:text=The%20Monument%20to%20the%20laboratory,the%20founding%20of%20the%20city."><img 
src="https://i.pinimg.com/originals/e8/b9/64/e8b96451559e3185d1d524a1df699fb5.jpg" align=right width=200></a>

Be a "lab rat" in someone else's experiments. Two * one hours.

Remember, "lab rats" have rights:
  - Right to privacy : never record details that can personally identify you
  - Right to refuse: as long as you show up to the experimental session,  you get the tokens _even if you refuse to to the experiment and just sit there for an hour_
  - Right to be forgotten: all results have to be tagged with your secret token. On request, you can require that your own data be forgotten.

Tutors will manage the tokens (as per HW3).


# Project 3b

Goal: convince some venture capitalist that your code is worthy of their attention, using qualitative evidence.

Step1: Pick a Proj2 project that is both _interesting_ and _testable_
- Interesting: 
  - does it pass the "wow!" test? 
  - If you could show that it worked, would you care?
- Testable: 
  - Can you show that it works, _better than something else_
  - Does there exist some _opposite_  approach to the idea in the project? 
  - Does that project2 already implemented _X_ and its __opposite_?

Step2: Build the materials necessary to test your work

Step3: Run experiments
- If you need humans, you can assume eight hours of total time (between a bunch of people)
- If your stuff is all algorithms, then strive for 20-30 repeats (^) for both _X_ and its _opposite_, under  different conditions (e.g. different random number seeds)
  - But, say, 30 repeats is impossible if your task is too slow (e.g. some evil deep learning training ask)

Step4: Submit a repo with all your materials, examples,  scripts  used in this work. 
- The top level of that repo needs a _results.md_ file
describing 
your  methods, materials, observations, analysis(+),
conclusions and [threats to validity](https://web.pdx.edu/~stipakb/download/PA555/ResearchDesign.html).  

(+) Extra points for your analysis section including "good stats"; i.e. Statistical nonparametric significance tests and effect size tests
(to check if you are really  measuring  a medium to large significant effect).
 - For more on "goid stats", see my [stats tutorial](https://github.com/txt/ase16/blob/master/doc/stats.md). 
   - That page has a small 1,2,3,4 exercise at the top of page that is worth doing.
   -  But that code has a (small) bug. Better that you use [this version instead](https://gist.github.com/timm/41b3a8790c1adce26d63c5874fbea393)

## Warnings:  Remember the lessons of hw3:
- Ethics matter (3 rights!)
- Pretests matter. 
  - Before you try it out on other people, run a trial yourself to debug the materials
    - Uniformity in data collection matters. 
      - In your pretests, check that if 2 people watching the same behavior record the same events
- Environment matters. To get most our of your "lab rats", have everything set up to start and run fast
- Rate of data collection matters.
  - If your lab rat tasks  take a hour, you'll only get 8 measurements (bad)
  - But if tasks are five minutes long, you'll get 96 measurements
  - And if lab rat tasks take one minutes long, you'll get 480 measurements (really good)
- The write up matters. 
  - Don't just dump csv files into a Markdown file and hand that in. 
  - In your lab report, you need to write a commentary that summarizes your results using informative
  visualizations. 
    - All figures need to be discussed in the text.


