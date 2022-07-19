---
layout: post
title: "Optical media workflow: formats"
description: "Background research for the internship project to create an optical media workflow"
tags: optical-media
---
## Optical media workflow: how CDs work! 💿

I'm actually going to use my slides for this chunk! <br>

<img src='https://raw.githubusercontent.com/emdashemma/emdashemma.github.io/main/uploads/dirks_slide_4.jpeg' width="500" align="left" style="padding: 15px">
Fundamentally, optical media is (are?) an information carrier where the inscription and recall are mediated by light in the form of a laser. It's a digital format, because the light is used to render and read two states and a change between them, essentially dark/bright, zero/one. Practically, "optical media" here refers to a whole range of commercial specifications of small shiny discs that are 120mm in diameter and consist of a substrate of polycarbonate plastic with some kind of reflective layer. Generally they’re called compact discs, or CDs.  


<img src='https://raw.githubusercontent.com/emdashemma/emdashemma.github.io/main/uploads/dirks_slide_5.jpeg' width="500" align="left" style="padding: 15px">
The first relevant optical media format (for this project, at least) was CD-DA (Compact Disc - Digital Audio), which was released in 1980 by Sony and Philips, held 74 minutes of audio, and was specified by a document called the Red Book. It became hugely commercially successful, and after the Red Book, subsequent formats of CDs that were structured for data, or mixed audio and data discs, then rewritable discs, and so on, were defined by other books with other colors that in the collective were known as the Rainbow Books. These were not actually publications but rather manufacturing and industry specs, and I could not find the originals anywhere. Some were adopted as standards and published by international standards bodies, and some of those are available, but many are paywalled. But there’s plenty of secondary literature: I found that books from the 1980s were by far the most helpful because they don’t assume any familiarity, they’re really excited about it, and they also have really good diagrams.

<img src='https://raw.githubusercontent.com/emdashemma/emdashemma.github.io/main/uploads/dirks_slide_6.jpeg' width="500" align="left" style="padding: 15px"> There is a huge range of optical media formats! This is the Wikipedia sidebar. The variation between the different disc formats is an interesting mix of _logical_ differences on similar objects and some really significant _physical_ differences, despite a superficial visual similarity across all compact discs.


<img src='https://raw.githubusercontent.com/emdashemma/emdashemma.github.io/main/uploads/dirks_slide_7.jpeg' width="500" align="left" style="padding: 15px">
For example, the means of creating alternating bright and dark spots is actually completely different for commercially stamped discs (CD-ROM, CD-DA), recordable discs (CD-R, DVD-R), and rewritable discs (CD-RW, DVD-RW):

**Commercially pressed** discs like CD-ROM and CD-DA are manufactured with their data, so the technology used there is the "pits and lands" model: impressions are stamped into the polycarbonate plastic substrate, which is then coated with a reflective aluminum layer; the impressions are a quarter-of-a-wavelength-of-the-laser deep, so when the reading laser has to travel an extra half-wavelength of distance, it interferes with itself on the way back and that's a dark spot.

**Recordable** discs are sold blank and are burned by the user; they have a similar plastic substrate, but it’s flat, and coated with an organic dye layer and then a reflective silver, silver alloy, or gold layer topped with a protective lacquer. The data writing involves burning through the dye layer with a laser to reveal the reflectivity of the metallic layer; where it’s not burned through, it’s not reflective.

**Rewritable** discs are the coolest. They use a phase-changing metal alloy that normally has a polycrystalline structure, which is reflective, but which can be heated up with a laser so that it melts into an amorphous solid and loses its reflectivity, which is read as dark, but if it's heated up to a lower temperature, it recrystallizes and gets shiny again, so the pattern of data is rewritable.

<br>

<img src='https://raw.githubusercontent.com/emdashemma/emdashemma.github.io/main/uploads/dirks_slide_8.jpeg' width="500" align="left" style="padding: 15px">Now that we have ones and zeros, it feels like it should be familiar territory for digital media. Any layer of machine processing could be applied to that raw stream of data. But first there’s actually a more basic layer of interpretation specific to optical media called eight-to-fourteen modulation, EFM, which is used to increase the data density on the surface of the disc. Instead of saying that a byte is made out of eight bits—eight zeros or ones—we say that a byte is made out of fourteen bits, then instead of using all 2^14 possible sequences of fourteen bits, we only use the sequences that follow a set of rules. The rules say that you can’t have two ones too close to each other. This essentially means that by making each word longer you can then printing it smaller, and the laser can still read it, even though each letter is too small for the laser’s eyesight. It’s terribly clever and the only reason it’s relevant is that you cannot say you’ve made a “bit-for-bit” copy of a CD because you haven’t. A computer takes those smaller-but-longer words and writes them the normal way, and tells you that’s exactly what you get. And it kind of is. But it’s kind of not. And this is the hell of mediated formats—you can’t see it. There is this thing in between, or several layers of things in between, that’s telling you what’s going on, and that is what you have to work with.

<br>

<img src='https://raw.githubusercontent.com/emdashemma/emdashemma.github.io/main/uploads/dirks_slide_9.jpeg' width="500" align="left" style="padding: 15px"> And that's the _first_ layer of abstraction. Next, that kind-of-raw stream of data is configured into information by a set of conventions, some of which are common to all compact discs, others that depend on the specific type of disc. Discs are written from the inside out, and will generally start with a header or lead-in or table of contents that tells the drive what to expect and where to find it. After the header, an audio disc is just encoded sound information all the way out, whereas data discs have a file system that control the use of space on the rest of the disc. There's some common vocabulary around how space is allocated and found on different discs, generally in sectors with addresses. There's also error correction, which I don't understand how it works, but you add extra bytes to each sector and then they do math and magic and it means the disc has some capacity to compensate for writing errors and physical damage like dust and scratches. 
<br><br>
And that is pretty much what I learned about how CDs work! Next up: how this informs the development of a workflow to preserve these formats where they appear in Special Collections.
