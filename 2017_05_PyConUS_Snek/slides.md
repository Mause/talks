## &nbsp; <!-- .slide: class="center" -->
# Snek in the Browser <!-- .slide: class="center" -->
## PyCon US May 2017
 <img src="pictures/footer.svg" />

Note: 

Breathe. You got dis.
---

 <div style='width: 50%; margin: 0 auto;'><p align='center'><img height='400px' src='pictures/wave.svg'></p></div> <!-- .slide: class="center" -->

Note: 
Hi! I'm Katie, and this is Snek in the Browser. We're going to be diving into some
content in this talk that might be a bit daunting at first, but trust me, we'll get there.

And like any good talk, we should start with some definitions


Let's kick off with the most important definition of all


---
# What is 'snek'? <!-- .slide: class="center" -->

Note: 

What is 'snek'? According to the most reliable source of information on the internet, Tumblr..
---

 <img src="pictures/snek.png" />

Note: 

A snek is comprised of a dangernoodle, with a snoot for booping. snek is very cute

---

 <div style='margin: 0 auto;'><p align='center'><img src='pictures/python-logo.png'></p></div>  <!-- .slide: class="center" -->

Note: 

more conventionally, snek is also pronounced "snake", of which Python is an instance.

More more importantly,

---

# What is Python? <!-- .slide: class="center" -->

Note: 

What _is_ Python?

Now, this might be tricky one. Python itself isn't a language. It's a language specification

What you're used to when you type `python` into a terminal and get a nice little interactive
program to play with is, probably, CPython. i

---

# What is CPython? <!-- .slide: class="center" -->

Note: 


What is CPython?

This is the most common implementation of the Python language specification

---
<pre class="cli"><code>$ cat snek.py
</code></pre> 
Note: 
Say you have a file called snek.py

---
<pre class="cli"><code>$ cat snek.py
print("hey snek <img src="s.png" class="e">")
</code></pre> 


Note: 

Say you have a file called snek.py

And all it does is print "hey snek"

---
<pre class="cli"><code>$ python snek.py
</code></pre> 

Note: we can execute this file by asking python to run it.
---
<pre class="cli"><code>$ python snek.py
hey snek <img class="e" src="s.png">
</code></pre> 

Note: 


And then we get our snek

But we have more ways to execute this code

---
<pre class="cli"><code>$ python
Python 3.5.1
>>> 
</code></pre> 

Note: we could also use the interactive python interface

---
<pre class="cli"><code>$ python
Python 3.5.1
>>> import snek
</code></pre> 

Note: 
and ask it to import the snek file for us

---
<pre class="cli"><code>$ python
Python 3.5.1
>>> import snek
hey snek <img src="s.png" class="e">
</code></pre> 

Note: 

which gives us snek
---

<pre class="cli"><code>$ cd &#95;&#95;pycache&#95;&#95;
$ cat snek.cpython-35.pyc
</code></pre> 
Note: after we do that, we see a new folder that's turned up in our file system

it has a file in it that's got the extension pyc instead of just py
---

<pre class="cli"><code>$ cd &#95;&#95;pycache&#95;&#95;
$ cat snek.cpython-35.pyc

hey snek <img src="s.png" class="e">N)�print�rr�/tmp/snek.py
</code></pre> 
Note: but it looks to be full of a little bit of jibberish
However, it's not gibberish to the python intepreter. It knows how to read this compiled content


---


<pre class="cli"><code>$ python
Python 3.5.1
>>> snek = "print('hey snek <img src="s.png" class="e">')"
</code></pre> 

Note: 
If we run python, storing our python code in a string
---


<pre class="cli"><code>$ python
Python 3.5.1
>>> snek = "print('hey snek <img src="s.png" class="e">')"
>>> import dis
>>> dis.dis(snek)
</code></pre> 

Note: but then import a module called 'dis'

and ask it to dis this snek

---
<pre class="cli" style="margin-left: -20px"><code>
&nbsp; 1&nbsp;0 LOAD_NAME &nbsp; &nbsp; &nbsp; 0 (print)
&nbsp; &nbsp; 3 LOAD_CONST&nbsp; &nbsp; &nbsp; 0 ('hey snek <img src="s.png" class="e">')
&nbsp; &nbsp; 6 CALL_FUNCTION &nbsp; 1
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; (1 positional, 0 keyword pair)
&nbsp; &nbsp; 9 RETURN_VALUE
</code></pre> 
Note: 

and you get this.

The module 'dis' that we used, that's short for "disassembler"

And what you're seeing here, is raw Cpython bytecode

Bytecode is an intemediate intepretation that is then run against the Python Virtual machine.

It looks a bit like Assembly, or basic, and it is similar. The Python Virtual Machine is stack based, so these languages may look similar.


We can pretty much read these instructions and work out the execution steps that will happen
---
<pre class="cli" style="margin-left: -20px"><code>
&nbsp; &nbsp; print('hey snek <img src="s.png" class="e">')
<p align="center">&#45;&#45;&#45;</p>&nbsp; 1&nbsp;0 LOAD_NAME &nbsp; &nbsp; &nbsp; 0 (print)
&nbsp; &nbsp; 3 LOAD_CONST&nbsp; &nbsp; &nbsp; 0 ('hey snek <img src="s.png" class="e">')
&nbsp; &nbsp; 6 CALL_FUNCTION &nbsp; 1
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; (1 positional, 0 keyword pair)
&nbsp; &nbsp; 9 RETURN_VALUE
</code></pre> 

Note: 
I'm going to put the original code up the top so we can see what's going on

---
<pre class="cli" style="margin-left: -20px"><code>
&nbsp; &nbsp; print('hey snek <img src="s.png" class="e">')
<p align="center">&#45;&#45;&#45;</p>&nbsp; <h>1</h>&nbsp;0 LOAD_NAME &nbsp; &nbsp; &nbsp; 0 (print)
&nbsp; &nbsp; 3 LOAD_CONST&nbsp; &nbsp; &nbsp; 0 ('hey snek <img src="s.png" class="e">')
&nbsp; &nbsp; 6 CALL_FUNCTION &nbsp; 1
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; (1 positional, 0 keyword pair)
&nbsp; &nbsp; 9 RETURN_VALUE
</code></pre> 

Note: 

We start on line one. Well, we only have one line

---
<pre class="cli" style="margin-left: -20px"><code>
&nbsp; &nbsp; <h>print</h>('hey snek <img src="s.png" class="e">')
<p align="center">&#45;&#45;&#45;</p>&nbsp; 1&nbsp;0 <h>LOAD_NAME</h> &nbsp; &nbsp; &nbsp; 0 (<h>print</h>)
&nbsp; &nbsp; 3 LOAD_CONST&nbsp; &nbsp; &nbsp; 0 ('hey snek <img src="s.png" class="e">')
&nbsp; &nbsp; 6 CALL_FUNCTION &nbsp; 1
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; (1 positional, 0 keyword pair)
&nbsp; &nbsp; 9 RETURN_VALUE
</code></pre> 

Note: 

We load up the code assoiated with the name print onto our stack
---
<pre class="cli" style="margin-left: -20px"><code>
&nbsp; &nbsp; print(<h>'hey snek <img src="s.png" class="e">'</h>)
<p align="center">&#45;&#45;&#45;</p>&nbsp; 1&nbsp;0 LOAD_NAME &nbsp; &nbsp; &nbsp; 0 (print)
&nbsp; &nbsp; 3 <h>LOAD_CONST</h>&nbsp; &nbsp; &nbsp; 0 (<h>'hey snek <img src="s.png" class="e">'</h>)
&nbsp; &nbsp; 6 CALL_FUNCTION &nbsp; 1
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; (1 positional, 0 keyword pair)
&nbsp; &nbsp; 9 RETURN_VALUE
</code></pre> 

Note: 
Then we load the constact string onto the stack

---
<pre class="cli" style="margin-left: -20px"><code>
&nbsp; &nbsp; print('hey snek <img src="s.png" class="e">')
<p align="center">&#45;&#45;&#45;</p>&nbsp; 1&nbsp;0 LOAD_NAME &nbsp; &nbsp; &nbsp; 0 (print)
&nbsp; &nbsp; 3 LOAD_CONST&nbsp; &nbsp; &nbsp; 0 ('hey snek <img src="s.png" class="e">')
&nbsp; &nbsp; 6 <h>CALL_FUNCTION</h> &nbsp; 1
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; (1 positional, 0 keyword pair)
&nbsp; &nbsp; 9 RETURN_VALUE
</code></pre> 

Note: Then we call the function.
We have one positional argument, because we provided just the string to print, and no keyword pairs
---
<pre class="cli" style="margin-left: -20px"><code>
&nbsp; &nbsp; print('hey snek <img src="s.png" class="e">')
<p align="center">&#45;&#45;&#45;</p>&nbsp; 1&nbsp;0 LOAD_NAME &nbsp; &nbsp; &nbsp; 0 (print)
&nbsp; &nbsp; 3 LOAD_CONST&nbsp; &nbsp; &nbsp; 0 ('hey snek <img src="s.png" class="e">')
&nbsp; &nbsp; 6 CALL_FUNCTION &nbsp; 1
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; (1 positional, 0 keyword pair)
&nbsp; &nbsp; 9 <h>RETURN_VALUE</h>
</code></pre> 

Note: 

We then return

We can also walk through a more complex example

---

<pre class="cli"><code>
$ cat pybee.py
s = "<img src="s.png" class="e">"
b = "<img src="b.png" class="e">"
print(s + b)
</code></pre> 

Note: here, we define the variables s and b, then print their concatenation

---
<pre class="cli" style="margin-left: -20px"><code>$ python
&gt;&gt;&gt; import dis
&gt;&gt;&gt; with open("pybee.py") as f:
...&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dis.dis(f.read()) 
Note: we can then disassemble our code file

---
<pre class="cli" style="margin-left: -20px">
&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;0&nbsp;LOAD_CONST&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;('<img src="s.png" class="e">')
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3&nbsp;STORE_NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;(s)<br> 
&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;6&nbsp;LOAD_CONST&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;('<img src="b.png" class="e">')
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9&nbsp;STORE_NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;(b)<br> 
&nbsp;&nbsp;3&nbsp;&nbsp;12&nbsp;LOAD_NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2&nbsp;(print) 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;15&nbsp;LOAD_NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;(s) 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;18&nbsp;LOAD_NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;(b) 
&nbsp;&nbsp;...<br> 
---
<pre class="cli" style="margin-left: -20px"><code>
&nbsp;&nbsp;... 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;21&nbsp;BINARY_ADD 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;22&nbsp;CALL_FUNCTION&nbsp;&nbsp;1&nbsp; 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(1&nbsp;positional,&nbsp;0&nbsp;keyword&nbsp;pair) 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;25&nbsp;POP_TOP 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;26&nbsp;LOAD_CONST&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2&nbsp;(None) 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;29&nbsp;RETURN_VALUE 


---

## 500 Lines or Less: A Python Interpreter Written in Python <!-- .slide: class="center" -->
### Allison Kaptur, asosbook.org

Note: if you're interested more in how this works, This amazing piece by Allian Kaptur in the Architecture of Open Source applications is worth the read.

---

# That's snek <!-- .slide: class="center" -->

Note: So that's the 'snek'. A language that we know and love, that's really just a nice wrapper around building blocks

---

# But who is browser? <!-- .slide: class="center" -->

Note: 

But what about the browser?

---

 <div style='margin: 0 auto;'><p align='center'><img src='pictures/browser_logos.png'></p></div>  <!-- .slide: class="center" -->

Note: when I say browser, I mean one of the many application use use to
surf the information superhighway, also known as the internet. You may
have heard of it.

---

 <div style='margin: 0 auto;'><p align='center'><img src='pictures/browser_window.png'></p></div>  <!-- .slide: class="center" -->

Note: This is a browser window. We have an address bar, which shows where we are. We have a window, which shows some content.

---

 <div style='margin: 0 auto;'><p align='center'><img src='pictures/html_logo.png'></p></div>  <!-- .slide: class="center" -->
Note: this is made using HTML.

HTML, or Hypertext Markup Language, is what gives the information super highway it's look and feel

---

<pre class="cli"><code>&lt;html>
&nbsp; &lt;title>Hello World&lt;/title>
&nbsp; &lt;body>
&nbsp; &nbsp; &lt;h1>Hello World&lt;/h1>
&nbsp; &nbsp; &lt;p>
&nbsp; &nbsp; &nbsp; Welcome to the information
&nbsp; &nbsp; &nbsp; super highway
&nbsp; &nbsp; &lt;/p>
&nbsp; &lt;/body>
&lt;/html> 
</code></pre> 
Note: using a combination of markup tags we can make a structure on a page that is then rendered in a browser

---

 <img src="pictures/css_logo.png" />

Note: We can also use CSS -- Cascading Style Sheets -- to take our browser from it's drab, but functional state


---

 <div style='margin: 0 auto;'><p align='center'><img src='pictures/browser_window_css.png'></p></div>  <!-- .slide: class="center" -->

Note: into something that looks a little bit nicer

---
<pre class="cli"><code>&lt;html>
&nbsp; &lt;head>
&nbsp; &nbsp; &lt;link href="style.css"
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; rel="stylesheet">
&nbsp; &lt;/head>
&nbsp; ...
&lt;/html> 
Note: 
This is done by importing a stylesheet into the page

---
<pre class="cli"><code>$ cat style.css
body {
&nbsp; font-family: "Arial";
} 
h1 {
&nbsp; color: #452768;
&nbsp; font-size: 24px;
} 
</code></pre> 
Note: And that stylesheet tells certain parts of the page how to display.
---

 <img src="pictures/form-window.png" />

Note: We can extend our HTML to include a form, that will allow us to surf the internets

Well, not actually. What we're doing here is enabling us to send information from the client front-end to the server bakend, which is the basis of the infotainment supertollway

---

<pre class="cli" ><code>&lt;form>
&nbsp; &lt;label>Username: &lt;/label>
&nbsp; &lt;input type="text"
&nbsp; &nbsp; &nbsp; &nbsp;&nbsp; id="username">
&nbsp;&lt;button>Surf!&lt;/button> 
&lt;/form> 
</code></pre> 

Note: This is what that little bit we've added looks like. There's a label, a form input element, and a button
---

 <div style='margin: 0 auto;'><p align='center'><img src='pictures/server.png'></p></div>  <!-- .slide: class="center" -->

Note: So we want to validate our form

We want to ensure the username is valid

The actual validation rules here we'll use aren't best practice, but I'm using them to demonstrate a point.
---

 <div style='margin: 0 auto;'><p align='center'><img src='pictures/python-logo.png'></p></div>  <!-- .slide: class="center" -->

Note: Serverside, we want to use Python
---

<pre class="cli"><code>def valid_username(un):
&nbsp; 
&nbsp; 
&nbsp; 
&nbsp; 
&nbsp; 
&nbsp; 
&nbsp; 
</code></pre> 
Note: So we declare a method in our server-side python API to validate a username is valid
---
<pre class="cli"><code>def valid_username(un):
&nbsp; usr = un
&nbsp; 
&nbsp; 
&nbsp; 
&nbsp; 
&nbsp; 
&nbsp; 
</code></pre> 
Note: One way to do this, is to take a copy of the username object


---
<pre class="cli"><code>def valid_username(un):
&nbsp; usr = un
&nbsp; 
&nbsp; 
&nbsp; if usr != un:
&nbsp; &nbsp; return False
&nbsp; 
&nbsp; return True
</code></pre> 
Note: and then after out maipulations, if they match, return True

---
<pre class="cli"><code>def valid_username(un):
&nbsp; usr = un.lower()
&nbsp; 
&nbsp; 
&nbsp; if usr != un:
&nbsp; &nbsp; return False
&nbsp; 
&nbsp; return True
</code></pre> 
Note: For example, allowing usernames that are idential apart from case is bad, so we should
only allow lowercase usernames to be entered to start

---
<pre class="cli"><code>def valid_username(un):
&nbsp; usr = un.lower().strip()
&nbsp; &nbsp;
&nbsp; &nbsp;
&nbsp; if usr != un:
&nbsp; &nbsp; return False
&nbsp; 
&nbsp; return True
</code></pre> 
Note: also, we want to strip whitespace from the start and end.

This is particularly useful for mobile entry, where when autocorrecting a space is added to the end
in some keybaords.
---
<pre class="cli"><code>def valid_username(un):
&nbsp; usr = un.lower().strip() \
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; .encode("ascii","ignore") \
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; .decode("utf-8")
&nbsp; if usr != un:
&nbsp; &nbsp; return False
&nbsp; 
&nbsp; return True
</code></pre> 
Note: And because we hate emoji, we may want to ensure that only ascii

This is great, we now have a function in python that does exactly what we want, that works
exactly for our business logic in the API


---

 <div style='margin: 0 auto;'><p align='center'><img src='pictures/client.png'></p></div>  <!-- .slide: class="center" -->

Note: But what if we want to use this same logic client side?

It might be easier to have some of these tests on the browser for performance benefits.

Of course we're still going to have the same code serverside, but having the form validate in the client means quicker feedback when things are wrong, what with server round trip times being as they are

---

 <img src="pictures/javascript-logo.png" />
Note: But because we're in the web, we have to use JavaScript

JavaScript won the great language war in the browser, defeating such foes as Flash, Visual basic, JScript and ActiveScript.

Luckily. 
---
<pre class="cli"><code>function valid_username(un) {
&nbsp; 
&nbsp; 
&nbsp; 
&nbsp; 
&nbsp; 
&nbsp; 
} 
</code></pre> 
Note: To ensure that we have the same validation on the front and back end, we need to translate our python code to javascript exactly
---

<pre class="cli"><code>function valid_username(un) {
&nbsp; <h>usr = un</h>
&nbsp; 
&nbsp; 
&nbsp; 
&nbsp; 
&nbsp; 
} 
</code></pre> 
Note: Firstly, take a copy of the string. which is the same syntax in python as in javascript
Except no it's not, because in this case, usr would be a global variable

---
<pre class="cli"><code>function valid_username(un) {
&nbsp; <h>var</h> usr = un
&nbsp; 
&nbsp; 
&nbsp; 
&nbsp; 
&nbsp; 
} 
</code></pre> 
Note: We need to the the 'var' prefix to ensure it's local.

Okay, this is fine.

---
<pre class="cli"><code>function valid_username(un) {
&nbsp; var usr = un
&nbsp; 
&nbsp; if usr != un {
&nbsp; &nbsp; return False;
&nbsp; }
&nbsp; return True;
} 
</code></pre> 
Note: we can then just add our if and return statements, swapping out the colon in python for braces in javascript, right?

Well, no, this isn't valid

---

<pre class="cli"><code>function valid_username(un) {
&nbsp; var usr = un
&nbsp; 
&nbsp; if <h>(</h>usr != un<h>)</h> {
&nbsp; &nbsp; return False;
&nbsp; }
&nbsp; return True;
} 
</code></pre> 
Note: you need to wrap the if statement comparison in brackets
---

<pre class="cli"><code>function valid_username(un) {
&nbsp; var usr = un
&nbsp; 
&nbsp; if (usr != un) {
&nbsp; &nbsp; return <h>f</h>alse;
&nbsp; }
&nbsp; return <h>t</h>rue;
} 
</code></pre> 
Note: and you need to set the booleans to lowercase, because they spelt differently in javscript
---

<pre class="cli"><code>function valid_username(un) {
&nbsp; var usr = un
&nbsp; 
&nbsp; if (usr !=<h>=</h> un) {
&nbsp; &nbsp; return false;
&nbsp; }
&nbsp; return true;
} 
</code></pre> 
Note: and you need to use a not equals equals in javascript because otherwise you
may be comparing the equality between a string and a number, which would be bad

Now, now, we can get to the bit where we actually get to the validation

So, converting a string to lowercase in javascript. A quick check of the mozilla develoepr network shows that we need
---

<pre class="cli"><code>function valid_username(un) {
&nbsp; var usr = un<h>.toLowerCase()</h>
&nbsp; 
&nbsp; if (usr !== un) {
&nbsp; &nbsp; return false;
&nbsp; }
&nbsp; return true;
} 
</code></pre> 
Note: toLowerCase. that's fine. Next is strip. But there's no native strip function in javascript

---

<pre class="cli"><code>function valid_username(un) {
&nbsp; var usr = un.toLowerCase()<h>.trim()</h>
&nbsp; 
&nbsp; if (usr !== un) {
&nbsp; &nbsp; return false;
&nbsp; }
&nbsp; return true;
} 
</code></pre> 
Note: There is a trim though. Except that won't work in all browsers, beacuse it was only introduced a few years ago, and IE8 won't understand this command

And then there's the converting of the string from potentually unicode to ascii.

---
<pre class="cli"><code>function valid_username(un) {
&nbsp; var usr = un.toLowerCase().trim()
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <h>.??????? </h>
&nbsp; if (usr !== un) {
&nbsp; &nbsp; return false;
&nbsp; }
&nbsp; return true;
} 
</code></pre> 
Note: how can we replicate the same functionality as an purposefully lossy encode decode in python in javascript

There doesnt appear to be anything that natively does it in js. So we'd have to make our own

We could iterate over all the elements and use a charCodeAt to check if it's character id is less than 127

Or we could use a regex

We could probably use encodeURIcomponent to convert any of the non-ascii characters, then compare with the original string to spot any differences

Or we could


---

# Gah! <!-- .slide: class="center" -->

Note: 
GAH 

It's just too complicated, and highly prone to translation errors

Why can't we just use the python code, that works, in the browser?

Well. we can

---
 <img src="pictures/beeware.png" />

Note: Beeware, is a series of libraries and tools that helps get python everywhere.

Remember our bytecode from earlier? We run that in the browser, using a BeeWare suite tool called Batavia

---
 <div style='width: 100%; margin: 0 auto;'><p align='center'><img height='200px' src='pictures/space.svg'><img height='200px' src='pictures/html_logo.png'><img height='200px' src='pictures/css_logo.png'><img height='200px' src='pictures/space.svg'></p></div> <!-- .slide: class="center" -->
 <div style='width: 100%; margin: 0 auto;'><p align='center'><img height='200px' src='pictures/space.svg'><img height='200px' src='pictures/javascript-logo.png'><img height='200px' src='pictures/python-logo.png'><img height='200px' src='pictures/space.svg'></p></div> <!-- .slide: class="center" -->
---

 <div style='width: 100%; margin: 0 auto;'><p align='center'><img height='200px' src='pictures/space.svg'><img height='200px' src='pictures/html_logo.png'><img height='200px' src='pictures/css_logo.png'><img height='200px' src='pictures/space.svg'></p></div> <!-- .slide: class="center" -->
 <div style='width: 100%; margin: 0 auto;'><p align='center'><img height='200px' src='pictures/space.svg'><img height='200px' src='pictures/javascript-grey.png'><img height='200px' src='pictures/python-logo.png'><img height='200px' src='pictures/space.svg'></p></div> <!-- .slide: class="center" -->

---
# Batavia
 <img src="pictures/batavia_full.png" />

Note: 

Batavia is a Python virtual machine, written in javascript.

Why is it called batavia?

---

 <img src="pictures/batavia_2.jpg" style="margin-top: -50px" />

Note: This is the batavia

And that's a model of the batavia

---

 <img src="pictures/batavia_1.jpg" style="margin-top: -50px" />

Note: this is the batavia

Batavia was the name of a Dutch merchant ship in the 1600's. It sorta.. crashed.. into Australia

Not far from Perth, actually, which is where the Bee-levolent Dictator For Now of BeeWare,
Russell Keith-Magee, hails from.

Now, the batavia had a small problem with it's crew, mainly mutiny.. but where it was suppoesd to be going
was what is now Indonesia, to a small island called Java

So the Batavia was the world's first Java ship.

---

### ba doom tish <!-- .slide: class="center" -->


---

 <img src="pictures/snakebee.jpg" />

Note: Using batavia, our little helper be can help lead the way for snek to be in the browser
---

<pre class="cli"><code>def valid_username(un):
&nbsp; usr = un.lower().strip() \
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; .encode("ascii","ignore") \
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; .decode("utf-8")
&nbsp; if usr != un:
&nbsp; &nbsp; return False
&nbsp; 
&nbsp; return True
</code></pre> 
Note: Here's our python function from before
---
<pre class="cli"><code>$ cat validate.py
def valid_username(un):
&nbsp; usr = un.lower().strip() \
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; .encode("ascii","ignore") \
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; .decode("utf-8")
&nbsp; if usr != un:
&nbsp; &nbsp; return False
&nbsp; 
&nbsp; return True
</code></pre> 
Note: Let's put it in a file called validate.py

---
<pre class="cli" style="margin-left: -20px"><code>$ python
&gt;&gt;&gt; import py_compile

</code></pre> 
Note: 
Then open up Python again, import _pycompile
---
<pre class="cli" style="margin-left: -20px"><code>$ python
&gt;&gt;&gt; import py_compile
&gt;&gt;&gt; py_compile.compile("validate.py", \
...&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cfile&equals;"compiled.pyc") 
</code></pre> 
Note: and then force python to compile the code into a file of our choosing.
---
<pre class="cli" style="margin-left: -20px"><code>$ cat compiled.py
</pre></code> 

Note: We can then inspect the file

---
<pre class="cli" style="margin-left: -20px"><code>$ cat compiled.py

dY��@sdd�ZdS)cCs;|j�j�jdd�jd�}||kr7dSdS) 
N�ascii�ignorezutf-8FT)�lower�strip�encode 
�decode)ZunZusr�r� 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;validate.py�valid_usernames 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;r&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;N)r&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rrr<module>s 
</code></pre> 
Note: and see the wonderful machine code that we saw earlier
---

<pre class="cli" style="margin-left: -20px"><code>$ cat compiled.py

dY��@sdd�ZdS)cCs;|j�j�jdd�jd�}||kr7dSdS) 
N�ascii�ignorezutf-8FT)�<h>lower</h>�<h>strip</h>�<h>encode</h> 
�decode)ZunZusr�r� 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;validate.py�<h>valid_usernames</h> 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;r&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;N)r&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rrr<module>s 
</code></pre> 
Note: we can see some of our methods in here.

But this isn't very portable.

So what we do for batavia

---
<pre class="cli" style="margin-left: -20px"><code>$ python
&gt;&gt;&gt; import py_compile
&gt;&gt;&gt; py_compile.compile("validate.py", \
...&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cfile&equals;"compiled.pyc") 
</code></pre> 
Note: is we take the code from earlier

---
<pre class="cli" style="margin-left: -20px"><code>$ python
&gt;&gt;&gt; import py_compile
&gt;&gt;&gt; py_compile.compile("validate.py", \
...&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cfile&equals;"compiled.pyc") 
&gt;&gt;&gt; import base64
</code></pre> 
Note: import base64
---
<pre class="cli" style="margin-left: -20px"><code>$ python
&gt;&gt;&gt; import py_compile
&gt;&gt;&gt; py_compile.compile("validate.py", \
...&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cfile&equals;"compiled.pyc") 
&gt;&gt;&gt; import base64
&gt;&gt;&gt; with open("compiled.pyc", 'rb') as f:
... &nbsp;&nbsp; payload = base64.encodebytes(f.read())
</code></pre> 
Note: we then read in our compiled file, ensuring we're using the read and byte flags, then encode in base64

---
<pre class="cli" style="margin-left: -20px"><code>$ python
&gt;&gt;&gt; import py_compile
&gt;&gt;&gt; py_compile.compile("validate.py", \
...&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cfile&equals;"compiled.pyc") 
&gt;&gt;&gt; import base64
&gt;&gt;&gt; with open("compiled.pyc", 'rb') as f:
... &nbsp;&nbsp; payload = base64.encodebytes(f.read())
&gt;&gt;&gt; print(payload)
</code></pre> 
Note: thsi payload
---
<pre class="cli" style="margin-left: -20px"><code>b'Fg0NCmRrCFmoAAAA4wAAAAAAAAAAAAAAAAIAAA
&nbsp; BAAAAAcxAAAABkAABkAQCEAABaAABkAgBTKQNj
&nbsp; AQAAAAAAAAACAAAAAwAAAEMAAABzOwAAAHwAAG
&nbsp; oAAIMAAGoBAIMAAGoCAGQBAGQCAIMCAGoDAGQD
&nbsp; AIMBAH0BAHwBAHwAAGsDAHI3AGQEAFNkBQBTKQ
&nbsp; ZO2gVhc2NpadoGaWdub3JlegV1dGYtOEZUKQTa
&nbsp; BWxvd2Vy2gVzdHJpcNoGZW5jb2Rl2gZkZWNvZG
&nbsp; UpAloCdW5aA3VzcqkAcgcAAAD6C3ZhbGlkYXRl
&nbsp; LnB52g52YWxpZF91c2VybmFtZQEAAABzDAAAAA
&nbsp; ABEgEMAQkBDAEEAnIJAAAATikBcgkAAAByBwAA
&nbsp; AHIHAAAAcgcAAAByCAAAANoIPG1vZHVsZT4BAA
&nbsp; AAcwAAAAA&equals;'
</code></pre> 
Note: we get base64 encoded bytecode.

Now, this is still not readable, in face it's less human readable; however in this form

it's super easy to copy around. Less mojibake!

---
<pre class="cli"><code>&lt;html>
&lt;head> 
</code></pre> 

Note: Back in our HTML code

---
<pre class="cli"><code>&lt;html>
&lt;head> 
&lt;script src="batavia.js">&lt;script>
</code></pre> 

Note: we can import Batavia

---
<pre class="cli"><code>&lt;html>
&lt;head> 
&lt;script src="batavia.js">&lt;script>
&lt;script type="application/python-bytecode">
Fg0NCmRrCFmoAAAA4wAAAAAAAAAAAAAAAAIAAA 
BAAAAAcxAAAABkAABkAQCEAABaAABkAgBTKQNj 
AQAAAAAAAAACAAAAAwAAAEMAAABzOwAAAHwAAG 
... 
AAcwAAAAA&equals; 
&lt;/script> 
</code></pre> 


Note: And put the base64 validation code right in there

You can use your existing pipelines to automatically generate this and insert it if you prefer

But 
---
<pre class="cli"><code>&lt;script type="text/javascript">
function validate_form() {
&nbsp; usr = $("username")
&nbsp; if !valid_username(usr) {
&nbsp; &nbsp; alert("you don't surf")
&nbsp; }
} 
&lt;/script> 
</pre></code> 

Note: if we, for this demo, add a little bit of code that

runs our python code
---
<pre class="cli" ><code>&lt;form>
&nbsp; &lt;label>Username: &lt;/label>
&nbsp; &lt;input type="text"
&nbsp; &nbsp; &nbsp; &nbsp;&nbsp; id="username">
&nbsp;&lt;button>Surf!&lt;/button> 
&lt;/form> 
</code></pre> 
Note: and edit our existing form
---

<pre class="cli" ><code>&lt;form <h>onSubmit="validate_form()"</h>>
&nbsp; &lt;label>Username: &lt;/label>
&nbsp; &lt;input type="text"
&nbsp; &nbsp; &nbsp; &nbsp;&nbsp; id="username">
&nbsp;&lt;button>Surf!&lt;/button> 
&lt;/form> 
</code></pre> 

Note: to include this new method

We can then get our validate code working client side
---

 <img src="pictures/form-window.png" />
Note: we have our form
---

 <img src="pictures/form_input.png" />
Note: and we enter in something invalid
---
 <img src="pictures/form_input_invalid.png" />
Note: and we get the popup!
---
## But how? <!-- .slide: class="center" -->
Note: but how does Batavia get it all to happen?

Batavia is a Python virtual machine, so it works not unlike cpython does
---

 <img src="pictures/batavia_3.jpg" style="margin-top: -50px" />

Note: so let's take a look inside batavia, and see it's framework

The following is code directly from the batavia javascript marshalling module, which has been cut down for readability
---

<pre class="cli" style="margin-left: -20px"><code>$ cat batavia/modules/marshal.js
... 
marshal.load_pyc = function(vm, payload) {
&nbsp; return marshal.read_object(vm,
&nbsp; &nbsp; &nbsp; new PYCFile(base64js.toByteArray(payload))
} 
</code></pre> 


Note: bavatia starts by decoding the base64, and then reading the object

---
<pre class="cli" style="margin-left: -20px"><code>marshal.r_object = function(vm, p) {
&nbsp; ...
&nbsp; var code = marshal.r_byte(vm, p)
&nbsp; ...
&nbsp; type = code & ~marshal.FLAG_REF
</code></pre> 
Note: then it just steps through the code by byte, getting the type
---

<pre class="cli" style="margin-left: -20px"><code>&nbsp;&nbsp;...
&nbsp; switch(type) {
&nbsp; &nbsp; case marshal.TYPE_null:
&nbsp; &nbsp; &nbsp; ...
&nbsp; &nbsp; case marshal.TYPE_NONE:
&nbsp; &nbsp; &nbsp; ...
&nbsp; &nbsp; case marshal.TYPE_STOPITER:
&nbsp; &nbsp; &nbsp; ...
&nbsp; &nbsp; case marshal.TYPE_ELLIPSIS:
&nbsp; &nbsp; &nbsp; ...

Note: and then running a great big switch statement

This then forks off to other functions, sometimes having to get multiple bytes, float fun, and a whole lot of other stuff

This is literally a virtual machine, processing machine code.

Basic assembly-style language, in a stack
---

## Snek in the Browser <!-- .slide: class="center" -->

Note: and that's snek int he browser

Python running where normally only javascript lives

---

## Doesn't this already exist? <!-- .slide: class="center" -->

Note: Can't we already get python in the browser? Well, yes and no.
---

## Brython, Skulpt, PyPy.js <!-- .slide: class="center" -->
### Compiler + Interpreter<br>+ REPL + Python Virtual Machine

Note: Brython, Skult and PyPyJS all exist, and all solve the problem of getting Python
in the browser, but in different ways.

Brython and Skulpt are full implementations of the Python compler and interpreter, complete with interactive prompt.

PyPyJS is similar, except it's used emscripted to compile the PyPy source code into javaScript.

These implementations are big. Like, 5 megabytes for PyPy.js.

I mean, 5MB may not be a lot, but it's a noticable load time. It's even more noticable on mobile. Even more
noticable if you live on a small island in the middle of the pacific, like I do. Or, say, on conference wifi.


---
# Batavia <!-- .slide: class="center" -->

### ~~Compiler + Interpreter<br>+ REPL +~~ Python Virtual Machine

Note: batavia, however, doesn't need a compiler, since we're proving the compiled code already.

We don't need an interpreter and repl because we already have our code, and our users aren't inputing code directly

All we need is the python virtual machine.

Add it all up, and add javascript compression, batavia is currently under a quarter of the size, just under 800kb, which is negligable, even over Australian mobile internet.

---

## But wait, there's more. <!-- .slide: class="center" -->

Note: So that's Batavia

but that's only one part of the beeware suite.

---

<pre class="cli" ><code>&lt;form>
&nbsp; &lt;label>Username: &lt;/label>
&nbsp; &lt;input type="text"
&nbsp; &nbsp; &nbsp; &nbsp;&nbsp; id="username">
&nbsp;&lt;button>Surf!&lt;/button> 
&lt;/form> 
</code></pre> 
Note: Remember this markup from earlier? This will allow us to implement a form on the web

---


 <div style='width: 100%; margin: 0 auto;'><p align='center'><img height='200px' src='pictures/space.svg'><img height='200px' src='pictures/html_logo.png'><img height='200px' src='pictures/css_logo.png'><img height='200px' src='pictures/space.svg'></p></div> <!-- .slide: class="center" -->
 <div style='width: 100%; margin: 0 auto;'><p align='center'><img height='200px' src='pictures/space.svg'><img height='200px' src='pictures/javascript-grey.png'><img height='200px' src='pictures/python-logo.png'><img height='200px' src='pictures/space.svg'></p></div> <!-- .slide: class="center" -->

Note: 
We've already gotten rid of the JavaScript with BeeWare, but what about the HTML and the CSS?

Can we remove those too?
---

 <div style='width: 100%; margin: 0 auto;'><p align='center'><img height='200px' src='pictures/space.svg'><img height='200px' src='pictures/html_grey.png'><img height='200px' src='pictures/css_grey.png'><img height='200px' src='pictures/space.svg'></p></div> <!-- .slide: class="center" -->
 <div style='width: 100%; margin: 0 auto;'><p align='center'><img height='200px' src='pictures/space.svg'><img height='200px' src='pictures/javascript-grey.png'><img height='200px' src='pictures/python-logo.png'><img height='200px' src='pictures/space.svg'></p></div> <!-- .slide: class="center" -->

Note: 

Yes. 

---


# Toga
 <img src="pictures/toga.png" />

Note: we've already shaved that yak


Toga is a Python native, OS native, cross platform graphical uiser interface toolkit

Why is it called toga? Well, when in Rome

---
### sorry, not sorry <!-- .slide: class="center" -->

---
<pre class="cli" ><code>&lt;form>
&nbsp; &lt;label>Username: &lt;/label>
&nbsp; &lt;input type="text"
&nbsp; &nbsp; &nbsp; &nbsp;&nbsp; id="username">
&nbsp;&lt;button>Surf!&lt;/button> 
&lt;/form> 
</code></pre> 

Note: this is our form from earlier. All we're doing here, is telling a machine to put pixels and vectors on screen. We're just drawing.

This is a high-level abstraction of drawling, so we don't have to draw the individual characters and boxes on a screen. HTML and CSS is just one way of getting stuff on a screen, but we don't have to use this CSS Box Model
---
<pre><code>import toga
&nbsp; 
class SuperHighway(toga.App):
&nbsp; &nbsp; def valid_username(un):
&nbsp; &nbsp; &nbsp; &nbsp; ...
&nbsp; &nbsp; def validate_user(self, widget):
&nbsp; &nbsp; &nbsp; &nbsp; if not valid_username(self.username.value):
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;self.main_window.info_dialog("Denied", "you don't surf")
&nbsp; 
&nbsp; &nbsp; def startup(self):
&nbsp; &nbsp; &nbsp; &nbsp; self.main_window &equals; toga.MainWindow(self.name)
&nbsp; &nbsp; &nbsp; &nbsp; self.main_window.app &equals; self
&nbsp; 
&nbsp; &nbsp; &nbsp; &nbsp; <c># insert UI here</c>
&nbsp; 
def main():
&nbsp; &nbsp; return SuperHighway("Super Highway", "org.pybee.superhighway")
</code></pre> 
Note: Here's a basic toga app

We have our class, with our validation functions from earlier

And we setup a window, do stuff to it, then return it
---
<pre><code> 
<c># UI elements</c>
un_label &equals; toga.Label("Username")
self.username &equals; toga.TextInput()
button &equals; toga.Button("Surf", on_press&equals;self.validate_user)

box &equals; toga.Box()
box.add(un_label) 
box.add(self.username) 
box.add(button) 
self.username.style.set(width&equals;100) 
un_label.style.set(width&equals;100) 
button.style.set(width&equals;100) 
box.style.set(padding&equals;30, flex_direction&equals;"row")

self.main_window.content &equals; box
self.main_window.show() 
</code></pre> 

Note: and this is the stuff

we make a label
we make a text input
we make a button

we make a box

inside that box, we put the label
inside that box, we put the button and the text input

we add some pretty

then we put everything in the window
and show it


---

<pre class="cli"><code>

$ python -m highway</code></pre>

Note: we can then run this code, and we get...
---

 <img src="pictures/toga-app.png" />

Note: our program as a native platform application; in this case, macOS
---

 <img src="pictures/toga-app-popup.png" />

Note: including the popup

But if we want to take this away somewhere...

---

# Briefcase
 <img src="pictures/briefcase.png" />

Note: then, we can take this code, and wrap it in breifcase

Why is it called briefcase? Because it allows you to carry your apps around

Sorry. I didn't name these things

---

<pre class="cli"><code>

$ python setup.py macos
</code></pre> 
---

 <img src="pictures/toga-icon.png" />

Note: See? nice little self-contain macOS app
---
 <img src="pictures/toga-app.png" />
---

<pre class="cli"><code>

$ python setup.py django
</code></pre> 
---

 <img src="pictures/validate_django.png" />
---

<pre class="cli"><code>

$ python setup.py ios
</code></pre> 
---

 <img src="pictures/validate_ios.png" style="margin-top: -50px" />
---
<pre class="cli"><code>

$ python setup.py android
</code></pre> 
---

 <div style='margin: 0 auto;'><p align='center'><img src='pictures/validate_android.png'></p></div>  <!-- .slide: class="center" -->
---
<pre class="cli"><code>

$ python setup.py windows
</code></pre> 
---

 <div style='margin: 0 auto;'><p align='center'><img src='pictures/validate_windows.png'></p></div>  <!-- .slide: class="center" -->

---

<pre class="cli"><code>

$ python setup.py linux
</code></pre> 
---

 <div style='margin: 0 auto;'><p align='center'><img src='pictures/validate_linux.png'></p></div>  <!-- .slide: class="center" -->

---

 <div style='width: 100%; margin: 0 auto;'><p align='center'><img height='266px' src='pictures/space.svg'><img height='266px' src='pictures/sparkles.svg'><img height='266px' src='pictures/space.svg'></p></div> <!-- .slide: class="center" -->
---

## But wait, there's still more. <!-- .slide: class="center" -->

Note: the thing is, Toga is a toolkit that is a collecton of cross-platform widgets.

Which means,
---

 <div style='margin: 0 auto;'><p align='center'><img src='pictures/browser_window.png'></p></div>  <!-- .slide: class="center" -->

Note: you rememebr that browser window from before?

We can recreate that in Toga
---
<pre><code>#!/usr/bin/env python

import toga
from colosseum import CSS

class Graze(toga.App):
&nbsp; &nbsp; def startup(self):
&nbsp; &nbsp; &nbsp; &nbsp; self.main_window = toga.MainWindow(self.name)
&nbsp; &nbsp; &nbsp; &nbsp; self.main_window.app = self

&nbsp; &nbsp; &nbsp; &nbsp; self.webview = toga.WebView(style=CSS(flex=1))
&nbsp; &nbsp; &nbsp; &nbsp; self.url_input = toga.TextInput(
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; initial='https://pybee.com/',
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; style=CSS(flex=1, margin=5)
&nbsp; &nbsp; &nbsp; &nbsp; )

&nbsp; &nbsp; &nbsp; ...
</code></pre> 
---

 <img src="pictures/toga-browser.png" />
Note: Which means we can make our own brower that runs as a native app

And yes,
---

 <img src="pictures/toga-django-browser.png" />

Note: this means we can have a browser in a browser.
---

## (inception horn) <!-- .slide: class="center" -->

---

## Python 3.4, 3.5 Compatible <!-- .slide: class="center" -->
Note: The entire BeeWare suite is compatible with Python 3.4 and 3.5

---

## Python 3.6? <!-- .slide: class="center" -->
Note: but what about 3.6?

Well, some parts work, but 3.6 presents and interseting problem
---

## Bytecode vs Wordcode <!-- .slide: class="center" -->

Note: remember how I said that bytecode was a cpython implementation? Well, even through it is documented, it's not formal, it's considered 'internal', and they made no guarentee of backwards compatbility

The basis of this particular change is changing the underlying opcodes to use 16 bit units for various optimisations. The thing is, this is changes the marshelling that batavia does to wrangle bytecode around, so it doesn't work for 3.6
---
<pre class="cli"><code>
$ cat snek.cpython-35.pyc | md5sum
4d3509f8148fb7f6da1d2803f1ed9341 -
<br> 
</pre></code> 
---
<pre class="cli"><code>
$ cat snek.cpython-35.pyc | md5sum
4d3509f8148fb7f6da1d2803f1ed9341 -
<br> 
$ cat snek.cpython-36.pyc | md5sum
f213a5b50590cad5abeacbc53ff752ed -
</pre></code> 
---

## You can help! <!-- .slide: class="center" -->

Note: However, you can totally help! We have an open offer to mentor anyone who wants to contribute, even if you've never contributed to open source.

If you do contrinue to the project

---
## Contribute to BeeWare <!-- .slide: class="center" -->
### pybee.org/contributing/how/first-time/ <!-- .slide: class="center" -->
---
 <img src="pictures/challenge-coin.png" />
Note: 
You get one of the famous BeeWare challenge coins. If you have already contributed to beeware and haven't received your coin, I have a few here tonight, come and see me afterwards
---
## Become a member <!-- .slide: class="center" -->
### pybee.org/bee/join
---
## Expo Hall Booth 103 <!-- .slide: class="center" -->
## Win an Android Phone <!-- .slide: class="center" -->
 <img src="pictures/kogan.png" />
## `#teampurple`

Note: Also, we have a booth! If you come to the exhibit hall, down near (LOCATION TODO), you'll see us, covered in bees

---
# &nbsp;
<table><tr><td><img src="pictures/revsys.png"></td><td><img src="pictures/stickermule.png"></td></tr>
<tr><td><img src="pictures/github.png"></td><td><img src="pictures/travis.png"></td></tr></table>
Note: 


Revsys coin

Stickermule stickers

Github coin 2.0 Yak Herder

Travis CI concurrency

---
 <div style='width: 50%; margin: 0 auto;'><p align='center'><img height='400px' src='pictures/claps.svg'></p></div> <!-- .slide: class="center" -->

### glasnt.com/talks