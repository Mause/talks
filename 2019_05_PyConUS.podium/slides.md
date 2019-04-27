class: title
# <br> A Right Stitch-up
## Creating embroidery patterns with Pillow
![Image](images/footer.svg)

???

FULL SCREEN ME!

⌘ + P

Monitors wrong? ⌘ + TAB
---

class: title
## ~~ <br>A long time ago <br> at a conference far away<br> ~~

---

background-image: url("images/osdc2014.png")

???

OSDC 2014

First ever lightning talk, for the "OtherSkills lightning talks"

(5 minute lightning talks, about stuff that's not computers)

There were talks about: bread, choirs, and me, about cross-stitching

---

background-image: url("images/green_display.jpg")

???

I was talking about this cross-stitch I made

---

background-image: url("images/pokebros.gif")

.footnotes[[Water](https://www.instagram.com/p/BjDp1eMFY3O/), [Grass](https://www.instagram.com/p/BjDpt4cFhh6/), [Fire](https://www.instagram.com/p/BjDpyXOFW1m/) Bros, Paul Robertson, 2011]

???

the original artwork was created by a pixel artist from Melbourne, Paul Robertson. He's known for his work on things like the Scott Pilgrim vs the World game, Mercenary Kings, and the videoclip for Architecture in Helsinki's Do the Whirlwind.

---
background-image: url("images/pokebros_green.gif")
.footnotes[[Grass Bros](https://www.instagram.com/p/BjDpt4cFhh6/), Paul Robertson, 2011]

???

Pixel art, especially those with distinct colour palettes, map really well to cross-stitching

Each pixel maps to one stitch.
---

background-image: url("images/green_design_clip.png")
???

so you can import your design into one of the many closed-source, Windows only programs, and generate a chart for you to reference.

Each cell has a colour and a symbol which maps to a specific thread colour.

---

background-image: url("images/green_working.jpg")

???

you then take that design, that chart, that graph, whatever you wish to call it, and one by one fill in the pattern onto your fabric, or canvas.

---

background-image: url("images/green_lynn.jpg")

.white[.footnotes[[Mike Pirnat](https://www.flickr.com/photos/mikepirnat/34782968461/in/photostream/)]]

???

Years after my original lightning talk, This particular design, well, all three of them, were auctioned off atht the PyLadies fundraising auction in 2017

As shown here by the wonderful Lynn Root.

---

# &nbsp;

???

now, as part of this lightning talk I gave, I mentioned that the program I used to take the source image and turn it into the chart in which to use as a reference for the stitching was made using a closed source, Windows-only program.

And I said:

---
# &nbsp;

*"If you know anything about image manipulation, colour setting, cross stitch charts...*
--

*If there is any [FOSS] software out there please tell me.*


--

*Otherwise I will make my own,*

--
*and present it here next year"*

--

&dash; me
--
, November 2014


???

it was my first ever lightning talk, and I made a promise. Yes, it's a bit late, but you know, a year was just an estimate.

---
# <BR><BR> Problems to solve

???

so, by my own unscripted ramblings 5 years ago, I set myself three problems to solve
--

### "image manipulation"

--

### "colour setting"

--

### "cross stitch charts"

---

class: title
## Problem 1:<br>Image manipulation

???

first step, image manipulation.

If I'm provided an image, I want to be able to go through every pixel in the image, and work out the colour

And we can do that in Python with
---
class: title
# `pillow`
### Python Imaging Library
---
class: title
## `getpixel((x,y))`
---

![Image](images/getpixel/large_3x3-2.png)
### 3x3.png
???

If I have a 3x3 image, with 9 pixels, all different colours, we can use this as a solid testing platform for testing getpixel

---

![Image](images/getpixel/large_3x3-4.png)
### 3x3.png

???

the co-ordinate system in Pillow starts in the top left, and works it's way across and down
---
.righthead[PIL.getpixel()]
.right-image[![img](images/getpixel/large_3x3-4.png)]
<BR>
<pre><code class="python">>>> from PIL import Image</code></pre>
--
<pre><code class="python">>>> im = Image.open("3x3.png")</code></pre>
--
<pre><code class="python">>>> im.getpixel((0,2))</code></pre>
--
<pre><code class="python">(255, 0, 0, 255)</code></pre>
--
<pre><code class="bash"># R .white[.] G.white[.] B .white[.] A</code></pre>
--
<pre><code class="bash"><br># (0,2) == red .white[ . . . . . . ] --></code></pre>

???

So we can address a single pixel in an image.

From here, we can loop through, and get the RGB values for every pixel in the image.

This will be useful later on.

But, onto the next problem
---
class: title
# Problem 2:<br>Colour setting

???

colour setting. Yes, colour with a "U"

But first.
---
class: title
## Let's learn about floss
---
class: title
# Dollfus-Mieg et Compagnie
### (DMC)

???

Dollfus-Mieg et Compagnie

Is an Alsatian textile company, founded in 1746

Not to be confused with the hiphop group.

When I talk about DMC, I mean
---
background-image: url("images/dmc-rack.jpg")
???

this stuff.

If you're Australian, you'll find a setup like this in your local Spotlight or Lincraft. In America, think Michaels, or Hobby Lobby
---
background-image: url("images/floss_macro.jpg")

???

this is the DMC Floss, floss like the stuff you use to get food out from between yur teeth.

DMC have hundreds of different colours, all referenced by a code, in this multitrand medium.

Most pre-made cross-stitch charts and software will refer to DMC as the floss only

However, they sell more than Floss
---
background-image: url("images/wool_macro.jpg")
???

they also sell wool. DMC Tapestry Wool is a thicker medium, and while I've been using the word "cross-stitch" so far, technically you can't really use it for Cross-stitch.

The physical medium of these thread is interesting.
---

class: title
# ⊠⊠⊠
### Cross Stitch
# ⧄⧄⧄
### Half Stitch

???

if you have a very tight canvas; in cross-stitch you'll have say an Aida 14ct Cloth, to fill a square you would use, say, three ply of the floss in a cross-pattern. Complete this around your canvas, and you fill in all the gaps and create a complete image.

With the wool, however, it's too thick to use 14ct. I personally work in 10ct canvas, and with this medium I can only use half-sttich. A single half-stitch fills the square, so it works at scale.

---

background-image: url("images/wool_macro.jpg")

???

but this is where the fun comes in.

You see, floss and wool are not cross-compatible. They don't share codes, and they don't share palettes.

And, as I said, a lot of charts only refer to the floss. So, we need to convert from floss to wool.

The colours you're seeing now are part of the set called 'Cranberry'
---

background-image: url("images/dmc-cranberry2.png")
???

while the names aren't strictly official, the codes are important.

There is a cross-compatibility chart, which is somewhat official as it has a terribly pjeg artefacted DMC logo, but it states that it's supposed to be used as a guide only. However, it does give us an aproximation of how to compare skeins of different medium (a skein being one 'spool')

The 'floss' from before has 600-series numbers for cranberry. And with this DF, you can see that the tapestry wool equivelent has a 7600 series

But they don't exactly match.
---
## The Cranberries - Analyze
.right-image[![pic](images/wool_6floss_crop.jpg)]
<pre><code style="font-size: 36px; line-height: 1.5;">

V DK Cranberry&nbsp;&nbsp;600&nbsp;&nbsp;&nbsp;&nbsp;7600
DK Cranberry&nbsp; &nbsp;&nbsp;601
MD Cranberry&nbsp;&nbsp;&nbsp;&nbsp;602&nbsp;&nbsp;&nbsp;&nbsp;7603
Cranberry&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;603&nbsp;&nbsp;&nbsp;&nbsp;7604
LT Cranberry&nbsp;&nbsp;&nbsp;&nbsp;604&nbsp;&nbsp;&nbsp;&nbsp;7605
V LT Cranberry&nbsp;&nbsp;605
</code></pre>

???

if we go through the chart, we can see that there are many more floss threads available than wool.

For the Cranberry series, there are 6 available floss threads, but only four wool. And in this picture, my local craft-store was even completely out of one of the wool skeins.

This out of stock issue will come up later.

As a matter of numbers, there's on average about a 3 to 2 ratio of floss to wool mappings.

---

## <br><BR><br> Floss → Wool ✓*
???

so, we can, mostly, convert a floss thread to it's wool equiv. That's great.

But we're working with computers. Pillow can get us RGB values
--

## DMC → RGB ??

???

so how can we

---
class: title
# No official mapping exists
### 'proprietary information'
.footnotes[[thread-bare.com](https://www.thread-bare.com/2017/09/20/creating-cross-stitch-charts-with-consistent-colors)]
???

Officially there's no official mapping.

It's 'proprietary information', colours can drift over time

Indeed, it's recommended that you buy your threads from the same dyelot to ensure they are from the same manufactured batch.

This mades sense. This is a company trade secret, from the 1800's.

It could allow competitors to "steal" and cheaply reproduce the colours.
---

class: title
## however

???

however. There are ways around this.

You can find, with a lot of searching, someone's unofficial mapping of colours. I've used it before.

However.

You could always create your own.
---

class: title
## however

???
You could go through every available thread, take a picture of the thread, work out the best colour, and go from there.

Now, you'll have to deal with a bunch of variables

lighting, the camera being used, the environment the picture was taken.

If these are consistent throughout the entire photoshoot, you can get a pretty good average colour.

And even then, you should always use these sort of things as a guide only.

The threads will change per dye lot, the colurs you have in your design may not look the nicest together.

But it gets a lot of the job done.

Lucky for me, since I first started looking into this problem space, DMC has updated their website.

---

background-image: url("images/dmc_floss_pink.png")

???

They have all the colours available for their threads with their codes on their website.

We can see here, the 600 thread from the cranberry series. Except for a few things --

It doesn't use the names any more.

The actual skein doesn't list any color, only the code; the color name is helpful, but is not a primary identifier.

The other thing?

---

background-image: url("images/dmc_wool_pink.png")

???

the equivelent colour in wool doesn't exist any more.

Indeed, in the old mapping I found, there was about 450 floss threads, and just under 300 wool threads.

According to their website now,
---

![Image](images/dmc_floss_count.png)
![Image](images/dmc_wool_count.png)

???

there's 489 floss threads, and only 100 tapestry wool threads left.

That's not a lot. We'll touch on this later; as both these numbers cause us issues.

---

background-image: url("images/dmc_wool_pink.png")

???

back to this page.

we can see that they've captured both swatches and the full skein for each thread.

From here, we can download these images, and use them to work out the average colour.

How?

---

class: title
## `getpixel((x,y))`
---

.righthead[PIL.getpixel()]
.right-image[![img](images/486_e_7202_150x150.jpg)]
<BR>
<pre><code class="python">>>> from PIL import Image</code></pre>
--
<pre><code class="python">>>> im = Image.open("486_e_7202_150x150.jpg")</code></pre>

???

we can import our image like before

and then...

--
<pre><code class="python">>>> count, r, g, b = [0,0,0,0]</code></pre>
<pre><code class="python">>>> for x in range(0, im.width):</code></pre>
<pre><code class="python">>>> &nbsp; &nbsp; for y in range(0, im.height):</code></pre>
<pre><code class="python">>>> &nbsp; &nbsp; &nbsp; &nbsp; i, j, k = im.getpixel((x, y))</code></pre>
--
<pre><code class="python">>>> &nbsp; &nbsp; &nbsp; &nbsp; r += i; g += j; b += k;</code></pre>
<pre><code class="python">>>> &nbsp; &nbsp; &nbsp; &nbsp; count += 1</code></pre>
--
<pre><code class="python">>>> print int(r/count), int(g/count), int(b/count)</code></pre>
--
<pre><code class="python">(210, 138, 149)</code></pre>

---

class: title
## <span style="color: rgb(210, 138, 149); background-color: rgb(210, 138, 149); padding: 50px">....</span>
![Image](images/486_e_7202_150x150.jpg)

???

I mean, I guess this is pretty close?

But if we repeat this cross all the images we have access to, we can at least process them all in the same way.


We can then get a list of color codes, and their aproxx rgb colors.

This is useful for later.

SO

the third issue.



---
class: title
## Reducing picture to only available colours

???

We have 100 wool colours to work with. So, we need to ensure that our source images only use these colours

Thankfully, we can solve this problem with a little bit of python
---
class: title
## `pillow`
???

pillow, again!
---
class: title
## `putpalette(data)`

???

there's a tiny function in Pillow called `putpalette()` that's somewhat underdocumented.

I'm including the code here as this is method that worked for me, and hopefully works for someone else.
---
.righthead[PIL.putpalette()]
<BR>
<pre><code class="python">>>> def get_palette_image(palette):</code></pre>
???

we have to define a palette. Do do that, we have to set the palette on a new image.

The data in this case is a list of 768 integers.

That is, 256 triples of RGB values.
--
<pre><code class="python">>>> &nbsp; data = # [ .. ]</code></pre>
--
<pre><code class="python">>>> &nbsp; image = Image.new("P", (16, 16))</code></pre>
--
<pre><code class="python">>>> &nbsp; image.putpalette(data)</code></pre>
--
<pre><code class="python">>>> &nbsp; return image</code></pre>

---
.righthead[Image.im.convert()]
<BR>
<pre><code class="python">>>> im = Image.open("source.png")</code></pre>

???

from there, we have to use the primative convert function to use our palette only.

This isn't a typo: there is a convert function ont he image object itself, but this is the C-level convert function. I haven't found a better way to do this functionality, although I do have some activity upstream in pillow to try and resolve this.

You may have noticed another issue here, tho
--

<pre><code class="python">>>> palette_image = get_palette_image(palette)</code></pre>
--
<pre><code class="python">>>> _im = im.im.convert("P", 0, palette_image.im)</code></pre>
--
<pre><code class="python">>>> return im._new(_im).convert("RGB")</code></pre>


---
class: title
## Problem: 256
???

pillow palette limited to 256 colours.

We have 100 colours in our Wool palette, so that's fine, we only define 100 colours, right?

---
class: title
## Problem: 256 exactly.
???

Well, no.

See, turns out here is where I was going to mention that there was this weird bug in pillow where when I defined my palette, the previous function I showed was allowing these weird grey colours to turn up.

Turns out that the default palette for any image is a 256-length sliding greyscale. That is, RGB values 0,0,0; 1,1,1; all the way up to 255,255,255.

Which means that if you don't override these values, you end up having greyscale colours in your resulting image.

The solution here is to always define exactly 256 colours. In my implementation, I pad out the palette by taking whatever the last colour is and repeating that until I have a complete palette.

---

class: title
## Problem: 256 only.

???

but on the other end of the scale, we have the problem that we have too many colours in our floss palette. We have 489 colours of floss, but we can only use 256. So instead of padding out our palette, we have to truncate it.

But how can we choose what colours to remove?

---

class: title
## ⚠️

???

now, this section might be a bit contraversial.

I want to remove colours from my floss palette.

And the problem is: all floss colours are different. Even colour that are by RGB value 'reasonably close' are in fact different colours. And removing any colours will reduce the fidelity of our image in floss.

I understand and acknowlege this, but I mean, having too many colours vs not having enough colours? Wool stitchers have a harder time, imho.

---

class: title
## Reduce the colour palette.

???

so, to reduce our colour palette, it makes sense to prune colours that are super close to each other.

---
class: middle, center, image
![Image](images/ciede2000.jpg)
## CIEDE2000
.footnotes[[wikipedia](https://en.wikipedia.org/wiki/Color_difference)]

???

Luckily there's math for that!

latest revision of the forumula from International Commission on Illumination (CIE)

Perceptual uniformity, in a function of colour distance. The smaller the number, the closer the colours.

Fun fact - largely based on experience with automotive paint on smooth surfaces.

And thankfully, because this is a fairly complex formula, we don't have to try and implement it ourselves, because it's already in scikit!

---
.righthead[deltaE_ciede2000]
<br>
<pre><code class="bash">$ pip install numpy scikit-image</code></pre>
<pre><code class="bash">$ python</code></pre>
<pre><code class="python">>>> from skimage.color<br>&nbsp; &nbsp; &nbsp;import deltaE_ciede2000</code></pre>
--
<pre><code class="python">>>> deltaE_ciede2000(color1, color2)</code></pre>
???

praise scikit

Color 1 and color 2 must be in a specific format here, but there are conversion helps to get us from RGB
---
background-image: url("images/similar-top-floss.png")
???

checking all the permutations and sorting by the smallest number from this formula, we can see which colours are extremely similar.

What's super interesting here is when the flosses are super similar but have different numbers

---

background-image: url("images/floss-comparisons.png")

???

based on the website images, we can barely see any difference between these threads.

In these three examples, the center set are from the same series - they are 640 and 642, but the difference are so minute that they allow for some extreme precision in the artwork; but for our perposes, we could remove

---

background-image: url("images/floss-thanos.png")

???

we could go full thanos and still get a pretty good palette.

So I took the 489 floss colours, and remove one of each of the similar pairs until I ended up with only 256 colours.

Again, not the best solution in the world, but as I've said, I have reasons.

---
class: title
## Problem 3:<br>Cross-stitch charts

???

so with our color setting problem solved, we can move onto problem three. Charts.

How do I easily turn all this data into a nice, clear, zoomable, copyable, exportable image?


---

class: title
# `pillow`?

???

Why not Pillow? It's been the solution to every other problem so far.

Well, I tried. I did.

I was using ImageDraw all over the place to try and build up a chart, trying to make tables and concatenate squares together.

And the results weren't what I wanted. It had weird fonts, I couldn't use unicode charactars for the image symbols, and I was sitting there thinking... there's gotta be a better way. A way you can typeset any character, use whatever fonts you want, make tables...


---
class: title
## `html`

???

turns out that's HTML

I can build up a page using divs and spans, the odd table here and there, whatever CSS styling I want. Test it in chrome, and it's great.

And if I need to create an image from that,

---

class: title
## `imgkit`
### `wkhtmltopdf` wrapper

???

I can use the python package imgkit which is a nice pythonic wrapper around wkhtmltopdf, which can generate images from html.

And that's great.

Except for the CSS part.

---

class: title
## `imgkit`
# class: title
## w(eb)k(it)htmltopdf

???

See, imgkit uses a webkit converter.

Chrome uses blink.

---

class: title
## `webkit` vs `blink`

???

Webkit and blink are the two biggest web rendering engines today. Blink was originally a fork of webkit, and a lot of folks are now migrating to one of the two implementations. In fact Microsoft Edge is now powered by Blink.


For those who were around for the browser wars, and remember the hellscape that was cross-browser compatibility, having only two engines is great! Your code will work everywhere, right? They're basically the same engine, right?

Well, heh, no.

Turns out I found a few of those lovely edgecases where I can still get css to display differently in different browser.

---
class: title
## `box-shadow: inset 0 0 0 0.5px`

???

I was using this: an inset box shadow. What I thought this would do was allow me to have rows and rows of spans, each with their own inset half-pixel border, which meant when placed next to each other it'd be 1px total, making everything lineup nicely in rows and columns.

---

class: title
## ~~`box-shadow: inset 0 0 0 0.5px`~~

???

Turns out that no, this isn't the case. Both engines implement box-shadow inset, but they differ in their intepretation of what to do with sub-pixel borders.

Blink works, and testing in Chrome my charts looked great.

Webkit, Safari and the image generation section? Not so much. Webkit ignored this styling. Which was annoying.

But I worked around it.

---

class: title
## `border-right: 1px solid black;`<br>`border-bottom: 1px solid black;`

???

With some terrible CSS hacks.

This around every cell of the chart, then a border around the entire chart itself works.

Mostly.

But it works!

---

class: title
## &nbsp;

???

but now, finally. I've solve the three problems.
---
class: title
## Result

???

the result of solving all these problems is
---
class: title
## `pip install ih`

???

A pip-installable package called Ih
---
class: image-main
![Image](images/green_screenshot.png)

???

I can now generate a chart that looks exceedingly similar

it also has some good features that I like, including giving me the actual amount of stitches.

---
class: title
## Here's something I prepared earlier.

???

as an example of how I can use this in practice.

Here's something you might recognise

---

background-image: url("images/pycon-banner.png")

???

The conference iconography for this year is pretty. Very pretty. And it has a distinct set of colours. Bold colours. .. We could cross-stitch this.

---

class: middle, center, image
![Image](images/pyconlogo.jpg)

???

the pycon twitter logo is a nice little square.. well circle.. representation of this ...

We can pass it through ih and get a chart.


---
.righthead[ih]
<br>
<pre><code class="bash">$ ih pyconlogo.jpg</code></pre>
???

so we load up our chart.. and because it's so big..
---
.righthead[ih]
<br>
<pre><code class="bash">$ ih pyconlogo.jpg -s6</code></pre>
???

we reduce the scale by 6 times
---
.righthead[ih]
<br>
<pre><code class="bash">$ ih pyconlogo.jpg -s6 -c8</code></pre>
???

and we use ony 8 colours.

AND WE GET

---

background-image: url("images/pyconchart.png")

???

something that looks a little bit crap, to be honest.
---

background-image: url("images/pyconchart-and-original.png")

???

the original logo has a gradient going on in the skyline, which doesn't work well.
It's also the JPG uploaded to twitter, which has artefacts, which is being picked up.

Unforunately my app is only as good as it's input data.

So let's clean up that image.


---

background-image: url("images/tinypycon10-border.png")
???

I mean, I'm no Paul Robertson, but I think this is pretty good pixel art.

If we throw this into our app

---
background-image: url("images/tinychart.png")

???

we get something quite good.

From there, I'm afraid it's a manual process.

---
background-image: url("images/littletrees/pyconmini_1.png")
---
background-image: url("images/littletrees/pyconmini_2.png")
---
background-image: url("images/littletrees/pyconmini_3.png")
---
background-image: url("images/littletrees/pyconmini_4.png")
---
background-image: url("images/littletrees/pyconmini_5.png")
---
background-image: url("images/littletrees/pyconmini_6.png")
---
background-image: url("images/littletrees/pyconmini_7.png")

???

tada!

IF PROP - SHOW


---

# &nbsp;

???

but you know what? that's boring.

We can go bigger.

---

background-image: url("images/pyconlogo-final.png")

???

IF AVAILABLE - show real tapestry now.

In what is now a tradition, this tapestry will be auctioned off tomorrow night at the PyLadies charity auction. Proceeds will go to PyLadies, so if you've got a ticket, I hope to see you there!

It makes me really happy to see that the python community really embraces physical crafts. It's great that we can be a community that can share interests outside of code. That OtherSkills lightning talks back in 2014, the auction now? It's really nice.

I mean I'm going to do some acroyoga later, at a tech conf. It's awesome.

ANYWAY.

---

class: title
## `pip install ih`
???

the package is up on pypi now, but if CLIs aren't your style
--

## ih-aas.glasnt.com

???

I've got a hosted ih as a service also available.

---
background-image: url("images/ih-aas.png")

???

you can either give it a URL of an image with a bunch of parameters like the scale, or the colours to use; or you can upload an image.

TODO - This is cloud run. Words here??


---
class: title
## Practical Applications

???

**if time permits**

You can also use this for practical applications.

For example, say you wanted to create a scannable QR code for your home wifi
---


.righthead[qrcode + ih]
<br>
<pre><code class="bash">$ pip install qrcode</code></pre>
<pre><code class="bash">$ qr "YourWifiPassword" > wifi.png</code></pre>
<pre><code class="bash">$ ih wifi.png -s10 -t</code></pre>

???

you can use the qrcode package, generate an image of the code, then pass that into ih


---
background-image: url("images/wifi-mock2.png")

???

If you stitch this, then it is scannable. I have this at home.
---
class: image-main
![Image](images/snap.png)

???

apparently this is a really good idea, because I tweeted about it earlier last year
---
class: middle, center, image
![Image](images/popular.png)

???

and it got a little bit of attention.

So, because peer pressure, I've turned it into a service
---
class: title
## qr.glasnt.com

???

you can go to this URL and generate your own.

---

class: title
## `pip install ih`<br>ih-aas.glasnt.com<br>qr.glasnt.com

![Image](images/footer.svg)

???

So that's all I had. For those of you with a ticket, I hope to see you at the auction tomorrow night.

Thank you all for your time~!