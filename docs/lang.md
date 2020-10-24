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

# Programming Languages

Before we start... this is going to seem a digression, but just stay with me here

N tellers/ checkout people. How many lines? One? N?

<img src="https://csbcorrespondent.com/sites/default/files/WSJ%20Teller%20Graphic_050418%20v.4.jpg" width=500>

Answer: see [7 insights into Queue Theory](http://www.treewhimsy.com/TECPB/Articles/SevenInsights.pdf)

[According to the RIOT paper](https://arxiv.org/pdf/1708.08127.pdf)
Computers
execute in highly dynamic environment.

- For example, Schad et al. [11] found that the
runtime of a widely used benchmarks suite can vary by up
to 33% even when run on supposedly identical instances
within the same cloud environment. 
- Not only CPU, but
also bandwidth can be highly variable within the cloud.
  - Schad et al. report that network bandwidth between the
same type of EC2 instances can vary from 410KB/s to
890KB/s. 
- Hence, even after a workflow is planned and
deployed, it is important to monitor instances and repeat
the scheduling process during deployment when necessary.
- If repeated reschedulings are too slow, then there is much waste of computer rescues.

## History of computers

When one person did work on a computer then..

Year|#Computers|$computers|#os|community|#locations|notes
----|----------|----------|---|---------|----------|-----
1945|1         |$$$$$$    |0  |tiny     |1         |"coding" means wiring
1950|1         |$$$$$$    |1  |small    |1         |some recognition that "coding" means reusing old parts
1955|1         |$$$$      |1  |larger   |growing   |LISP: a minimal "virtual machine" for symbolic computation
1957|1         |$$$$      |N  |larger   |growing   |FORTRAN:  multi-machine scientific programming language
1959|1         |$$$$      |N  |larger   |growing   |COBOL: a multi-machine business-oriented language

Virtual machines are an engineering 
- [Paul Graham](http://www.paulgraham.com/rootsoflisp.html)
  In 1960, John McCarthy published a remarkable paper in which he did for programming something like what Euclid did for geometry. He showed how, given a handful of simple operators and a notation for functions, you can build a whole programming language. He called this language Lisp, for "List Processing," because one of his key ideas was to use a simple data structure called a list for both code and data.
- [Don't read](https://web.archive.org/web/20131004232653/http://www-formal.stanford.edu/jmc/recursive.pdf)
  MacCarthy, 1960, "Recursive Functions of Symbolic Expressions and Their Computation by Machine, Part I"
- [Better](https://sep.yimg.com/ty/cdn/paulgraham/jmc.ps?t=1595850613&)
- [Much, much better](https://norvig.com/lispy.html)
  - Sooo much fun
- Lisp = computation = rewrite terms
    - there are atoms (symbols, numbers or nil or `t`, aka "true")
    - and there are lists (which contain atoms of lists)
    - 'a ==> a
    - `(eq x y)` is the same or both nil
      - `(car '(a b c))` ==> `a` ; i.e. pull the head
      - `(cdr '(a b c))` ==> `(b c)` ; i.e. pull the rest
    - `(cons 'x '(y z))` ==> `(x y z)` ; i.e. assemble something
    - `(cond (if1 do1) (if2 do2) ..)`  ; i.e. branch the reasoning
  - "Functions" and _lambda bodies_ `((lambda (p1 p2 p3..) e)  a1 a2 a3...)`
    - set `p1 p2 p3...` to the values of the arguments `a1 a2 a3...`
    - then evaluate  `e`.
    - Note that lambda bodies are just lists (so we can build them up and pull them down with `car` `cdr` `cons` just
      like anything ese
    - When we "define a function", we add a "lambda body" to the  "environment"
  - "Environments" and lists of pairs of symbol binding
    - `'((a 1) (b 2) ...)`
    - When enter a lambda body, we add parameter arguments to the _left_ hand side:
      -  `((p1 a1) (p2 a2) (p3 a3) (a 1) (b 2) ...)`
      - Look up local values left to right, local recursive vars shadow parent vars
        - So now we can recursion.

      
