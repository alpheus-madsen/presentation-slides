Presentation Slides
===================


These are slides of some of the presentations I have given at various conferences and meetups.


Common Lisp:  Everything You Can Do I Can Do Better
===================================================

(2013-openwest-common-lisp-everything-you-can-do-i-can-do-better.odp)

An introduction to Common Lisp presented via OpenOffice Impress.  One of the things that
fascinates me about Common Lisp is how it does everything better than everything else, how a
lot of that was done even *before* other languages did it (only doing it worse), and how
even stuff added *after* Common Lisp was created can be better than the languages where the
ideas are pulled from.

Hence, I was unable to resist subtitling this presentation with the famous song from "Annie
Get Your Gun"!



Open Source Mathematics
=======================

(2013-openwest-open-source-mathematics.odp)

As a mathematician, I have always appreciated software systems like Maple and Geometer's
Sketchpad.  As I became more familiar with Open Source projects, I naturally explored what
kinds of open source mathematics software was available.  This presentation gives an overview
of various projects useful for exploring mathematical ideas.



Parentheses on the Web
======================

(2014-openwest-parentheses-on-the-web.pdf)

A presentation summarizing my explorations using Lisp (particularly Common Lisp and ParenScript)
for web development.  This presentation was shorter than I would have liked, in no small part
because it was created and presented around the time my youngest daughter was born!



Computing From Scratch
======================

(2015-openwest-computing-from-scratch.pdf)

A presentation on the "physical" aspects of creating a computer.  It discusses tools available for
circuit design, how much (in 2015 prices) components for a computer might cost, and various "hacky"
techniques that can be used to create a printed circuit board, apply solder paste, and melt the
solder for surface-mounted transistors, resistors, and capacitors.



Introduction to Forth
=====================

(2015-openwest-intro-to-forth.md)

An introduction to the Forth computer language, a language so powerful, it was considered by
its creator Chuck Moore to be the first "Fourth Generation" language (called "Forth", however,
because his computer system only allowed for five-letter file names).  This is an amazingly small
and quirky language that has the ability to run as an interpreter *and* compiler  on a 2 *kilobyte*
Arduino system.

Because I wanted to emphasize the simplicity of the language, I thought it would be fun to present
the slides via Markdown slides.  The presentation can be viewed as a text file, but is meant to be
presented via ["mdp"](https://github.com/visit1985/mdp) - a command-line markdown presentation tool.



An Introduction to J for Data Analysis
======================================

(2016-openwest-intro-to-j-for-data-analysis.pdf)

An introduction to the quirky J computer language, a language created by Kenneth Iverson (the creator
of APL) and Roger Hui, for exploring mathematics and for data analysis (at least, for loose values of
"data analysis").



LaTeX as an Alternative to Office
=================================

(2016-openwest-latex-as-an-alternative-to-office.pdf)

An introduction to LaTeX as an alternative to Office Software.  As a mathematician, I had the
privilege of learning to use LaTeX, a system for typesetting mathematical papers.  I have always
joked that LaTeX is the worst way you can typeset mathematics, except for all the others.  While
I have always felt that typesetting equations is kindof clunky, LaTeX nonetheless *shines* as an
alternative to Word and OpenOffice Write, and to PowerPoint and OpenOffice Presentations.  LaTeX
is particularly nice for creating letters, and I enjoy using Beamer for creating PDF slides for
presentations!



An Introduction to BRL CAD
==========================

(2018-openwest-intro-to-brl-cad.pdf)

Years ago, someone suggested I look into Finite Element Analysis as a potential career path for
a mathematician.  BRL CAD is a Computer-Aided Drafting system designed by the Ballistics Research
Laboratory of the Air Force, specifically designed to provide the 3D models needed to perform FEA
that 2D-based programs like AutoCAD and 3D-skin programs like Blender could not provide.  I spent
some time learning how to use BRL CAD and shared what I learned in this presentation.



An Introduction to Solitaire Encryption
=======================================

(2018-plug-intro-to-solitaire-encryption.pdf)

An introduction to cryptography using playing cards.  Solitaire is an algorithm created by Bruce
Schneier for Neal Stephenson's *Cryptonomicron*.  This presentation uses the algorithm as an
introduction to cryptography, discussing the goals for the algorithm and its security flaws.



Fundamentals of Haskell
=======================

(2019-openwest-fundamentals-of-haskell.pdf)

My employer was using Haskell to create a lightning-fast cryptocurrency consensus algorithm.  As
it had been a while since I had last used Haskell, I thought it would be good to give a presentation
about Haskell, its goals, and some of its fundamentals.

I have a fractal quantum love-hate relationship with Haskell:  I simultaneously love and hate the
language -- but I simultaneously love and hate each feature of the language as well!



A Whirlwind Introduction to Alien Technologies
==============================================

(2019-openwest-whirlwind-intro-to-alien-tech.pdf)

Over the years, I have collected a *lot* of interests in some rather bizarre things, ranging from
keyboards (both typing and musical) to command-line build-your-own IDE to nuclear power to
weird and fantastic computer languages to analog robotics.  This presentation is a whirlwind
introduction to these topics, all of which probably deserve a presentation of their own!



Exploring the Unseen World of Ideas:  An Introduction to the Philosophy of Mathematics
======================================================================================

(2021-ltue-exploring-the-unseen-world-of-ideas-philosophy-of-math.pdf)

A discussion on how mathematicians view the world, and an exploration of just what is this
thing we call "mathematics" anyway?  This is an overview of the history of mathematics and what
people think it is (and isn't), and how it affects our exploration of truth and scientific
understanding of the world.

A couple of weeks after I gave this presentation, I had a realization I wish I could have
put into the presentation itself.  In the presentation, I mentioned that a particular
philosopher suggested that it's possible to do science without mathematics, and then went on
to provide an outline of sorts that removed equations from Sir Isaac Newton's classical
mechanics framework -- and then suggested that the same can probably be done with Einstein's
General Relativity.  The idea behind this, if I recall correctly, is to reinforce the notion
that mathematics is strictly a fiction, and has no attachments to the "real world".

My initial thought about this was "well, sure, but those equations are just simplifications of
what we think, and thus you're going to be shooting yourself in the foot.  After thinking about
this for a couple of weeks, however, I realized that the error was far more fundamental than
that:  likely due to how we learn mathematics, we have this idea that mathematics is about
equations and numbers, and if only we could get rid of those, we'd be rid of this icky curse!

But it's not.  Mathematics is about taking an idea, distilling it to its fundamental axioms,
and then logically proving theorems with those axioms.  Numbers are the essence of counting,
so they are susceptible to this type of reasoning -- but lines and circles in a plane are
*also* susceptible to this process, so geometry is *also* naturally "mathematical", even if
it doesn't inherently have equations or numbers.  (One can, however, construct numbers using
lines and circles; this is how Euclid squeezed number theory into a book about geometry!)

Now, what is science?  It is looking at data, deriving *assumptions* about that data,
*simplifying* those assumptions into something fundamental, *proving* things with those
assumptions, and then collecting data to see if the *new* data matches your conclusions
from the assumptions -- if not, there is likely something fundamentally wrong with your
assumptions.

While it's true that science is fundamentally different from mathematics -- the reliance and
outright emphasis on data *ensures* that this is so -- it is *nonetheless* true that the
*essence* of mathematics is baked into science.  There's no escaping it!  The reliance of
so much of our science on equations and numbers is a mere artifact of the fact that our
data collection is *necessarily* numerical.



An Introduction to Finite Element Analysis
==========================================

(2025-provo-linux-users-group-intro-to-fea--part-01.pdf)
(2025-provo-linux-users-group-intro-to-fea--part-02.pdf)

Finite Element Analysis is a method used by engineers to prototype objects without
physically creating them, to identify potential weak points and other issues in the
design that might need to be addressed.  This presentation gives a brief introduction
to Finite Element Analysis, and outlines how geometries are converted into meshes
that can then provide the pretty pictures and animations that illustrate the physical
deformations that a particular prototype might go through, when exposed to various
forces and pressures.

This presentation also briefly touches on both proprietary and open source tools
available for Finite Element Analysis.

Note that due to size limitations of files uploaded to GitHub, it was necessary to break
up this presentation into two parts.  These two parts can be reunited into one PDF
file using the "pdfunite" tool found in the "poppler" PDF utilities package that
*should* be available in any distribution under a variation of that name.
