
[![Build Status](https://travis-ci.org/burnson/Belle.svg)](https://travis-ci.org/burnson/Belle)

# Welcome

(Last updated October 4, 2015)


Welcome to the repository of Belle, Bonne, Sage, an experimental music engraver in C++. Currently the project is inactive since June 2013. At this time, the author forked the repository to work on a proprietary project called MusicPal (<http://museami.com/musicpal>). Meanwhile, the project has also been forked by Illiac Software (<http://illiacsoftware.com>) to develop Harmonia. See below for a description of the project and its goals.

**Important note for newcomers**: if you are interested in playing around with music-related vector graphics, then Belle is a great way to do that. If you are looking for a full on engraver, you'll need to keep looking as the current typesetter for open source Belle was just one in a long line of experimental and incomplete typesetters.

If all the above doesn't deter you, here is how you can get started with this project (Mac OS X version):

1) Clone the repo

`git clone git://github.com/burnson/Belle.git`

2) Change directory to Belle

`cd Belle`

3) Run the CI script to build and run the examples

`Scripts/CI`

4) Open the generated example PDFs and have a look

`open *.pdf`

**NOTE**: the typesetter example makes use of the Belle proto-engraver. This engraver can not do anything meaningful in terms of printing music; rather, it was only created to determine how graphs may be useful as a data structure for music. As such, the following code directories are considered deprecated:

 * `Belle/Source/Graph`
 * `Belle/Source/Modern`

#Goals

Belle, Bonne, Sage is the “Beautiful, Good, Wise”—a C++ vector-graphics library dedicated solely to music notation!

##Introduction

Belle, Bonne, Sage is an abstract vector-graphics library which has neither predetermined inputs or outputs. Instead, it bridges some language of input to another language of output. Since music notation lends itself generally to vector-graphics representations, the only requirement for the output is that it be able to accept vector-graphics drawing commands.

Most importantly, Belle, Bonne, Sage does not assume a fixed model of representation. Instead, it provides processes to the engraver that are likely to be useful. For example, the ability to make a quarter note is a generally useful thing to be able to do, thus there is a special function that creates the vector path of a notehead based on the proportions and rotations of an ellipse, the thickness and roundness of its stem, etc.

##PDF and Onward

The library comes with a powerful and fast PDF reference renderer, built from the ground up and based on the PDF/X specification. The reference engine currently supports the standard vector graphics routines as well as a custom-built font system in which glyph collections are described in an SVG format that is additionally viewable by web browsers. These SVG glyph collections, or vector fonts as they are named in the library, greatly simplify the task of accessing Unicode characters.

Apart from the reference renderer, a user desiring some other output medium simply needs to write a vector-graphics painter that can translate a few vector-graphics operations into the language of the destination medium. There is no requirement that this output be a file or that it have permanence; for example, it could be a display within a music notation editor. At its lowest-levels, the library knows nothing about whether it is drawing to a file or to the screen. The translation from input to output occurs during the process of rendering, not as a separate step. The library uses C++ virtual functions to facilitate this process.
Belle, Bonne, Sage represents the beginning of a second generation of music notation software that is concerned with controlling the quality of the engraved music while simultaneously maintaining a no-assumptions model that provides total flexibility in the underlying representation of the music.

##Rationale

I can think of no better rationale for this project than my experience in creating my first graphic score. Initially, I wondered if it might be possible to distort the output of a commercial music notation editor to such ends, but it quickly became apparent that was needed was something built entirely from scratch with no underlying assumptions. After a summer's worth of work, I had produced a prototype of Belle, Bonne, Sage in order to create the score to my solo piano piece [Bike Ride](https://github.com/burnson/BikeRide) which is shaped literally as a bicycle.

Clearly, this would be impossible to do in any current music notation software, and would be extraordinarily difficult to accomplish manually through the use of a vector-graphics editor. Thus, it is extremely important to create software that allows for new aesthetics to be tried while at the same time increasing the quality and standards of computer-based music notation. These are the two primary goals for the Belle, Bonne, Sage project.

It is also important to recognize that creativity in notation has a long history and can be identifiably traced back to the score to [Baude Cordier's Belle, Bonne, Sage](https://en.wikipedia.org/wiki/Baude_Cordier) from which this project inherits its title. Hopefully, the library will some day be able to typeset this serendipitous blend of music and art as we strive to show that notational creativity is still just as important today as it was seven centuries ago.

##“But what about...”
Lilypond? Yes, GNU Lilypond is fantastic open-source engraving software, and undoubtedly maintains the highest merit among computer-based engraving software. However, Lilypond suffers intractable disadvantages compared to Belle, Bonne, Sage and commercial music editing software:

* No graphical interface, nor is there any possibility to fork the project since its source files are essentially declarative programs that generate PostScript files. None of this can happen in real time. User interfaces also need a way to cache object placement information so that the user can edit the score and get instantaneous feedback. Music notation is very much a visual art, and an engraver needs to be able to see the score at all times. The Denemo project is the only current attempt to build a GUI for Lilypond; however, the GUI itself does not use Lilypond. Instead, the software provides a way to enter in music into the Lilypond declarative scripts.
* The structure of the music representation is fixed—debatable in that Lilypond is built on a pluggable architecture. However, changing a fixed representation is tedious. For example, consider bendable staff lines; that puts a damper on a lot of pre-coded assumptions about note placement, beaming, and text. In such a model, one tries to account for all the possible notations in existence. This approach works for some pieces of music more than others. A better approach makes no assumptions about the types of notation required and brings instead an array of graphical tools to the fore to solve the problems of the individual engraver.
* The fonts are difficult to change unless you want to recompile the METAFONTs. The procedure is currently undocumented. METAFONT is one of Donald Knuth's creations that was, unfortunately, never widely accepted outside the Linux community. Though its design is superior in many respects (and would be especially useful for music notation symbols), no physical printer will ever have native METAFONT support. The fonts have to be converted to PostScript or TrueType somewhere down the line, so there is little point in jumping over extra hurdles for the same end result.
* Lilypond is, however, quite adept at typesetting many types of music and is capable of much more than the commercial music notation editors. Still, it is not an end-all solution to the problems of flexible music notation, which Belle, Bonne, Sage seeks to address.
 
It is very important to understand first of all that Belle, Bonne, Sage is not a standalone software program or an editor of any kind. It is best thought of as a library of C++ code governing interactions between an engraver (you) and some vector-graphics context (the display, a PDF file, etc.). Some of these interactions have already been defined in examples, but these are only examples, and do not imply any kind of limitation on the notational possibilities.

##Previous Examples
Belle, Bonne, Sage is packaged with several examples that show how the library can be used. You can use these as a starting point for your own applications or utilities. In conjunction with the comprehensive library reference you should be able to navigate through the library effectively. Here is an overview of the examples:

**Chorale Composer** was an open source version of University of Illinois' music theory software for four-part music editing, display, and analysis. It is now developed by Illiac Software and is known as [Harmonia](http://illiacsoftware.com).

**[Blume](https://github.com/burnson/Blume)** is a geometric-series rhythmic accelerando and decelerando notating utility. It would be a useful starting point for creating a new interface in that it can be easily modified to do something entirely else.

##Open Source Commitment
Belle, Bonne, Sage is now developed under the permissive Simplified BSD License (2-clause) in the hopes that such a library may find relevance in academic, open source, and commercial projects.