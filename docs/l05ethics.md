<a name=top><br>
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

## Test Case Priorization

Excessive test:
- Google overdose three bullion
- LN cant ick where tests codm from 

XXX totod: add pointer to zeller's book

## The Truth About Testing

- "Don’t worry if it doesn’t work right.  If everything did, you’d be out of a job."    
  -  Mosher’s Law of Software Engineering
- "One (person)’s crappy software is another man’s full time job."     
  Jessica Gaston

  -## Wy Does testing work

- Most software spent  most of its time within a small number of states
- Druzdel

XXXX

- Bugs are lazy. Clump together. Best predictor of next bug is the last bug.
  GCC clum

It took several decades to find the experience required to build a size/defect relation- ship. In 1971, Fumio Akiyama described the first known “size” law, saying the number of defects D was a function of the number of lines of code; specifically
D = 4.86+0.018⇤loc
Alas, nothing is as simple as that. Lessons come from experience and, as our experience grows, those lessons get refined/replaced. In 1976, Thomas McCabe [290] argued that the number of lines of code was less important than the complexity of that code. He proposed “cyclomatic complexity”, or v(g), as a measure of that complexity and offered the now (in)famous rule that a program is more likely to be defective if:
v(g) > 10
At around the same time, other researchers were arguing that not only is programming an inherently buggy process, its also inherently time-consuming. Based on data from 63 projects, Barry Boehm [37] proposed in 1981 that linear increases in code size leads to exponential increases in development effort:
effort=a⇥KLOCb ⇥Y(Emi ⇥Fi) (1.1) i
Here, a, b are parameters that need tuning for particular projects and Emi are “effort multiplier” that control the impact of some project factor Fi on the effort. For example, if Fi is“analysts capbaility” and it moves from “very low” to “very high”, then accord- ing to Boehm’s 1981 model, Emi moves from 1.46 to 0.71 (i.e. better analysts let you deliver more systems, sooner).

## Testing for Safety crite systems

testing for safety cirtical systems is a different animal. demand u mining isystem. eg. rules for safety critical. small size. on one main loop. if you can find it n 15 seconds go look got it sit safe way
