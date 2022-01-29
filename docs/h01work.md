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

# Howework: 1: Write a "good" Github Repo

Your repo is your resume. But what is a  good looking repo?

## Write a repo 

With the structure shown below. Ensure that  everyone in the group do at least one commit to the repo

Note:
- There is a lot to do here in a  week . 
- You'll probably only get bits of this going in 1 week. But keep at it. Remember that homeworks can be submitted many
times with no penalties
- Suggestion: Divide up the structure between your group and everyone do different parts.
But make sure everyone knows what each part is.

Submit your a URL to your repo to Moodle.

## Structure

```txt
.gitignore
.travis.yml
CITATION.md : fill on once you've got your ZENODO DOI going
CODE-OF-CONDUCT.md
CONTRIBUTING.md
LICENSE.md
README.md
setup.py
requirements.txt
data/
  README.md
test/
  README.md
code/
  __init__.py
```

If you don't know what any of the above do, then google them (they are quite standard). ALso, read the following: 

- README.md
   - add the travis badge "build:passing"  to your README.md. See [Instructions]https://docs.travis-ci.com/user/customizing-the-build)
   - add the Zenodo DOI badge to your README.md. See [Instructions](https://genr.eu/wp/cite/)
- [.gitignore](https://github.com/github/gitignore)
- LICENSE.md
   - see [here](https://github.blog/2015-03-09-open-source-license-usage-on-github-com/)
   - and [Choose a License](https://choosealicense.com/licenses/)
- [CODE_OF_CONDUCT.md]( https://docs.github.com/en/github/building-a-strong-community/adding-a-code-of-conduct-to-your-project)
- [CONTRIBUTING.md](https://github.com/atom/atom/blob/master/CONTRIBUTING.md)
  - This contrib file is too verbose. Discuss with your group which 10-20 items you'd actually endorse from your project.
- [requirements.txt](https://www.idkrtm.com/what-is-the-python-requirements-txt/)
- [setup.py, __init__.py](https://github.com/bmcfee/spatialtree)
  - Test your package (`python3 setup.py install`)
- [.travis.yml](https://docs.travis-ci.com/user/customizing-the-build)

Regarding the last point, keep it real simple.
In Python, write the smallest example of [pytest](https://docs.pytest.org/en/stable/)
 running a file containing some `test_` functions.

```python
# content of __init__.py
def inc(x):
    return x + 1

def test_answer():
    assert inc(3) == 5
```

Hook that code into Travis so that everytime you commit your repo, your tests re-run.
