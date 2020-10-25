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

# Programming Languages and ABstraction

All these following use the same idea... abstraction

- Language features that simplify programming complex systems
  - Iterators
  - Error handling
- Hardware independent operating systems
- Languages implemented via virtual machines (LISP, Smalltalk, Java, JavaScript, Erlan,...)
- Languages implemented via transpiles
- "Jump technologies" 
  - Virtual machines
  - Containers
  - Serverless computing

Note that while the applications are different, and occur at very different scales,
the essential idea of _abstraction_ is used  throughout

- Between the programmer and the hardware there are layers of abstraction
- Programmers talk to the abstraction
- Automated tools make abstraction to the hardware



## Queuing Theory 
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
- If repeated rescheduling are too slow, then there is much waste of computer rescues.

## Abstraction

Abstraction in computer science had to be invented.
- Barbara Liskov won at $250K prize for her work on  abstraction in programming languages.
  - [Her award lecture](https://amturing.acm.org/vp/liskov_1108679.cfm)
    is amazing
    - at minute  1:09 to 1:11 the whole world disappears and her and Guy Steele debate
      iterator design and the rest of us can just listen

Why abstraction? well?

- If you underlying data structures are complex, you want some way to talk to them
  without having to know everything about them
- If you hardware is different, 
  -  you want to write code in  hardware independent manner
     - so code can run all over the place
  - Add an abstraction layer between
    - operating systems below and
    - the application above
    - Once you get "it" going for one OS on one machine
      - It runs wherever that OS runs
    - e g. UNIX
- If computing environments are dynamic, we want to bounce our
computation around the hardware to take full advantage of unused
resources.
 - And when we bounce a "program", we want to bounce with it:
     - all the current
   variable settings, 
     - contents of RAM, 
     - activation records of current
   functions, 
     - return addresses for when those functions return, 
     - network
   connections, 
     - hooks to GUIs and databases, etc etc. 
 - Think of the _layers_ pattern, on steroids
     - Where you grab whole layers and move them to another piece hardware
 - Under the hood, again, this is abstraction.

This tactic has been applied, successfully, dozens of times in the history of computing

- Language features that simplify programming complex systems
  - Iterators
  - Error handling
- Hardware independent operating systems
- Languages implemented via virtual machines (LISP, Smalltalk, Java, JavaScript, Erlan,...)
- Languages implemented via transpiles
- "Jump technologies" 
  - Virtual machines
  - Containers
  - Serverless computing

## Error handling

Throw a ball into a stadium, wait for what returns while holding a catchers mitt.
Only catch things you know how to handle

```python
def atom(token: str) -> Atom:
    "Numbers become numbers; every other token is a symbol."
    try: return int(token)
    except ValueError:
        try: return float(token)
        except ValueError:
            return Symbol(token)
```

## Iterators
When you code recursive data structures, give programmers
so way to way around that code.

e.g. What does this return?

```python
for x in [10,[[11,12,13],15], 20,30,[40,50,"tim"]]:
   print(x)
```

```python
def items(x):
  if isinstance(x,(str,list,tuple)):
   for y in x:
     for z in items(y):
       yield z
  else:
    yield x
```
Another example (in awk):

```awk
while(csv(lst,file))
  doSOmething(lst)
```

```awk
function csv(a,file,     i,j,b4, ok,line,x,y) {
  file  = file ? file : "-"     # [1] read from standard input or file       
  ok = getline < file
  if (ok <0) {                  # [2] complain if missing file
     print "missing "file > "/dev/stderr"; exit 1 }
  if (ok==0) { close(file);return 0 }                                    
  line = b4 $0                         
  gsub(/([ \t]*|#.*$)/, "", line) # [3] kill white space and comments      
  if (!line)       return csv(a,file, line) # [4] skip blanks lines
  if (line ~ /,$/) return csv(a,file, line) # [5] contact incomplete rows with next
  split(line, a, ",")                       # [6] split line into cells on comma
  for(i in a) {
    x=a[i]
    y=a[i]+0
    a[i] = x==y ? y : x                     # [7] coerce number strings, if any
  }
  return 1
}
```

## UNIX

If iterators and error handlers are "little abstractions", then operating systems are
"big abstractions".

<img align=right width=500 src="https://upload.wikimedia.org/wikipedia/commons/4/49/Baby_Bells.svg">

- Pre-unix: operating systems were hardware-specific
- The breakup of the Bell System was mandated on January 8, 1982
  - So after laying down all that copper
    - Bell Corporation was not allowed to use it all. 
    - And they actually set up commercial competitors!
- They needed someway for different organizations to work together
  - The ultimate "why can't we all get along"
- Step1: a hardware independent systems language "C"
- Step2: an operating system written in "C"
- Step3: design patterns to allow for interactions
  - Uniform file representation (everything is "ASCII test", no special binary formats for each fie).
  - Enter the _pipe_ pattern

Examples
- `nroff` is a text formatter (old version of latex)
- `lp` is the line printer
- `col` handles escale sequences that layes up text in 2 columns
- `tbl` is an nroff pre-processor that expresses tables in terms of lower-level nroff commands
- `eqn` is an nroff pre-processor that expresses equations in terms of lower-level nroff commands

```bash
nroff files | col | lp

tbl file-1 file-2 . . . | eqn | nroff -ms
````

Think of pipes as `produce`, `translate`, `filter`, `consume`:

```bash
find /usr/bin/ |                #produce 
sed 's:.*/::'  |                #translate: strip directory part
grep -i '^z'   |                #filter   : select items starting with z
xargs -d '\n' aFinalConsumer    #consume 
```



## LISP
- 1955: LISP: a minimal virtual machine. Code these (small set of primitives) on any hardware
  you like then, on top of all that, code written in LISP runs everywhere
  - Well, not really. 
    - Turns out, code does more than "computes". 
    - It also "connects" (to GUIs, databases, networks)
    - It also "explores"; i.e. Cognitive support for humans  exploring the world with software 

## Smalltalk

<img align=right width=500
 src="https://lh3.googleusercontent.com/-ezZ4lM0y5rE/WezC7wsnC2I/AAAAAAABFgc/3NuHmtD8q20B11eRKpL141huA2nC5JnpQCHMYBhgL/w606/smalltalk-desktop.jpg">

- 1974 Smalltalk VM
  - Its the source man
  - [Smalltalk-80 in a TV show](https://www.youtube.com/watch?v=AuXCc7WSczM)
  - [Smalltalk article 1980](http://dreammachin.es/Kay_SciAm_77.pdf)
  - Later on, was used to design the Java VM 
    - Q: Why does JAVA have single parent inheritance? 
    - A: Cause of Smalltalk

## Virtual Machines and Contains

<img src="https://imesh.github.io/images/contvsvm.png">

- Another useful example is UNIX
  - designed to evolve vendor lock in
   
- ECMA
  - In September 1995, a Netscape programmer named Brandan Eich developed a new scripting language in just 10 days. 
    - Clinet-side intra-interpreter language
      - a Virual machine in every borwser
    - Why so fast? Cause its theoretical foundations were well defined... in LISP.
  - It was originally named Mocha, but quickly became known as LiveScript and, later, JavaScript.

- ERLANG, ELIXR


- Transpilers
  - Why write a new language? Why not just convert your source code into some other language
    - e.g. CoffeeScript into JavaScript

<img src="../etc/img/cs.png">

- Serverless
  - e.g. AWS Lambda (btw, why is it called "lambda"? See below).
  - Why even have an operating system, just start with your current application and only ship the little bits
    needed for the application
  - Good news:
    - Cheaper
    - Smaller memory (so more scalable)
    - Productivity: less to configure, less messing with threading.
      Just explore  the unit of code to the outside world are simple event driven functions.
  - Bad news:
    - Debugging. If you ship a barebones unit of functionality, you may not get
      the debugging tools needed to understand a drash.
    - Security: more tiny components, less protection frpm other OS facilites (which
      not execist in your tiny comptuational slice)
    - Vendor lock-in : 
          - But in the serveless world, no OS abstraction between comptuation and support
        environment
        - So not "write once, run everywhre" 
    - Configuration: can't make _any_ assumptions about background utilities from
      "the operating system" cause their ain't one
      - You have to do it all.

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
  - "In 1960, John McCarthy published a remarkable paper in which he did for programming something like what Euclid did for geometry. He showed how, given a handful of simple operators and a notation for functions, you can build a whole programming language. He called this language Lisp, for "List Processing," because one of his key ideas was to use a simple data structure called a list for both code and data."
  - "It's worth understanding what McCarthy discovered, not just as a landmark in the history of computers, but as a model for what programming is tending to become in our own time. It seems to me that there have been two really clean, consistent models of programming so far: the C model and the Lisp model. These two seem points of high ground, with swampy lowlands between them. As computers have grown more powerful, the new languages being developed have been moving steadily toward the Lisp model. A popular recipe for new programming languages in the past 20 years has been to take the C model of computing and add to it, piecemeal, parts taken from the Lisp model, like runtime typing and garbage collection."
- [Do not read](https://web.archive.org/web/20131004232653/http://www-formal.stanford.edu/jmc/recursive.pdf)
  MacCarthy, 1960, "Recursive Functions of Symbolic Expressions and Their Computation by Machine, Part I"
- Here's a [Better](https://sep.yimg.com/ty/cdn/paulgraham/jmc.ps?t=1595850613&) read

XXX isp failed. vendor babel. 1970s


```lisp
; The Lisp defined in McCarthy's 1960 paper, translated into CL.
; Assumes only quote, atom, eq, cons, car, cdr, cond.
; Bug reports to lispcode@paulgraham.com.

(defun null. (x)
  (eq x '()))

(defun and. (x y)
  (cond (x (cond (y 't) ('t '())))
        ('t '())))

(defun not. (x)
  (cond (x '())
        ('t 't)))

(defun append. (x y)
  (cond ((null. x) y)
        ('t (cons (car x) (append. (cdr x) y)))))

(defun list. (x y)
  (cons x (cons y '())))

(defun pair. (x y)
  (cond ((and. (null. x) (null. y)) '())
        ((and. (not. (atom x)) (not. (atom y)))
         (cons (list. (car x) (car y))
               (pair. (cdr x) (cdr y))))))

(defun assoc. (x y)
  (cond ((eq (caar y) x) (cadar y))
        ('t (assoc. x (cdr y)))))

(defun eval. (e a)
  (cond
    ((atom e) (assoc. e a))
    ((atom (car e))
     (cond
       ((eq (car e) 'quote) (cadr e))
       ((eq (car e) 'atom)  (atom   (eval. (cadr e) a)))
       ((eq (car e) 'eq)    (eq     (eval. (cadr e) a)
                                    (eval. (caddr e) a)))
       ((eq (car e) 'car)   (car    (eval. (cadr e) a)))
       ((eq (car e) 'cdr)   (cdr    (eval. (cadr e) a)))
       ((eq (car e) 'cons)  (cons   (eval. (cadr e) a)
                                    (eval. (caddr e) a)))
       ((eq (car e) 'cond)  (evcon. (cdr e) a))
       ('t (eval. (cons (assoc. (car e) a)
                        (cdr e))
                  a))))
    ((eq (caar e) 'label)
     (eval. (cons (caddar e) (cdr e))
            (cons (list. (cadar e) (car e)) a)))
    ((eq (caar e) 'lambda)
     (eval. (caddar e)
            (append. (pair. (cadar e) (evlis. (cdr e) a))
                     a)))))

(defun evcon. (c a)
  (cond ((eval. (caar c) a)
         (eval. (cadar c) a))
        ('t (evcon. (cdr c) a))))

(defun evlis. (m a)
  (cond ((null. m) '())
        ('t (cons (eval.  (car m) a)
                  (evlis. (cdr m) a)))))
```

- Here's a [much, much better](https://norvig.com/lispy.html)
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

```lisp
is.py> (define circle-area (lambda (r) (* pi (* r r))))
lis.py> (circle-area 3)
28.274333877
lis.py> (define fact (lambda (n) 
              (if (<= n 1) 
            1 
      (* n 
         (fact (- n 1))))))
lis.py> (fact 10)
3628800
lis.py> (fact 100)
9332621544394415268169923885626670049071596826438162146859296389521759999322991
5608941463976156518286253697920827223758251185210916864000000000000000000000000
lis.py> (circle-area (fact 10))
4.1369087198e+13
lis.py> (define first car)
lis.py> (define rest cdr)
lis.py> (define count (lambda (item L) 
            (if L 
                (+ (equal? item (first L)) 
                   (count  item (rest L))) 
                0)))
lis.py> (count 0 (list 0 1 2 3 0 0))
3
lis.py> (count (quote the) (quote (the more the merrier the bigger the better)))
4
lis.py> (define twice (lambda (x) (* 2 x)))
lis.py> (twice 5)
10
lis.py> (define repeat (lambda (f) 
                          (lambda (x) 
                              (f (f x)))))
lis.py> ((repeat twice) 10)
40
lis.py> ((repeat (repeat twice)) 10)
160
lis.py> ((repeat (repeat (repeat twice))) 10)
2560
lis.py> ((repeat (repeat (repeat (repeat twice)))) 10)
655360
lis.py> (pow 2 16)
65536.0
lis.py> (define fib (lambda (n) 
               (if (< n 2)
                   1 
                  (+ (fib (- n 1)) 
                     (fib (- n 2))))))
lis.py> (define range (lambda (a b) 
                           (if (= a b) 
                               (quote ()) 
                               (cons a 
                                     (range (+ a 1) 
                                            b)))))
lis.py> (range 0 10)
(0 1 2 3 4 5 6 7 8 9)
lis.py> (map fib (range 0 10))
(1 1 2 3 5 8 13 21 34 55)
lis.py> (map fib (range 0 20))
(1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597 2584 4181 6765)
```  

<img s
rc="https://camo.githubusercontent.com/c84bd9db4bc8d854c4a3e66bcf64ec81bbf8a27c/68747470733a2f2f696d67732e786b63642e636f6d2f636f6d6963732f6c6973702e6a7067">


interesting ideas. multip methods. glue for all

used i julia 


other things we got first from lsp:
garbage colection, runtime typing, read eval print

It seems to me that there have been two really clean, consistent models of programming so far: the C model and the Lisp model. These two seem points of high ground, with swampy lowlands between them. As computers have grown more powerful, the new languages being developed have been moving steadily toward the Lisp model. A popular recipe for new programming languages in the past 20 years has been to take the C model of computing and add to it, piecemeal, parts taken from the Lisp model, like runtime typing and garbage collection.
