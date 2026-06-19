---
layout: post
title: "Using AI to learn"
date: 2026-06-19
---
One of my favorite use cases for Claude is learning new things.

I've seen three basic flavors of use cases for having Claude teach me things beyond having it explain concepts. The first 
is to have it quiz me on the concepts with prompting that encourages it to be very precise in checking my
responses. This forces a mix of both active learning and a real grading that identifies weaknesses (rather than telling
me that I get the idea, when I don't *really* get the idea).

Here's an example prompt that I found helpful (literally copy-pasted, including typos, so you can feel okay about your
own sloppy prompting):

```
okay I am going to work through the CR feedback here: https://github.com/<redacted>

  I want to talk to you about some if it. My goal is to ensure i understand it, and what i want to do is tell you my understanding and then have you think about where I might have a mistaken mental model. Your goal is neither to simply validate me or re-explain things I don't understand, or 'flesh out' the mental model with a lot of details. YOur goal is to figure out what I probably do understand, where there is ambiguity in what I am saying that might hide a misunderstanding, and then specifically address that aspect of my understanding. Does thatm ake sense?
``` 

I found this prompt worked very well for making sure I really understood what was going on in that code review--although
Claude got over-eager and decided to find possible ambiguity in everything I said, even when there really wasn't any. Ah
well, I guess I taught it to be a lawyer.

The second is having Claude build interactive explainers for concepts. I'm not 100% certain how good an idea this is, in
the sense that I think that if it replaces me just drawing diagrams myself, it's probably a bad idea. But I think it's a
good idea where there is some concept for which drawing the diagram would be challenging and a sophisticated
visualization would be useful. For example, I was recently working on some fancy cryptography concepts, and I spent a
weekend having Claude build an interactive explainer of all the ideas. This was very useful. That said, part of what
made it useful was the *interactivity of building the tool*--I'd try it, still be confused by something, and then ask
Claude to refine it in some way. Or I'd consider what it would take to make it really clear to someone who didn't have
quite as good an understanding of the idea as I now had, and ask Claude to update the explainer.

At the end, it wasn't necessarily clear to me whether the explainer itself was the output, or if the *process of
creating the explainer* was the output. But in either case, I did learn a lot doing it, and I managed to skip over a lot
of the drudgery of mucking around in the JavaScript, HTML and CSS that I'd otherwise have had to go through to build
such a tool myself. So it felt like I really was operating at the right conceptual level to learn the thing I wanted to.

The third thing I've noticed is that you can build flight-simulator like tools with Claude for a range of tasks.  As an
example, I was recently learning a piano piece with a difficult rhythm--a triplet, followed by a quintuplet, followed by
a dotted eighth note and then a sixteenth note. For my level of skill, this is brain breaking. I tried to practice with a
normal metronome, but it was quite hard to tell if I was getting the interval subdivisions correct. I tried looking
around online to find a tool for this and nothing immediately came up. So I fired up Claude Code and asked it to help.

In about 2 minutes (literally) I had a custom rhythm builder that I could use to create this exact pattern. I then
worked with Claude to add new features like a 'clap tracking' mode so I could see how accurately I was doing, and making
other little tweaks. But the point is: this is the kind of thing that would have been too much of a pain to put together
before and now it just ... exists. (You can find it [here]({{ '/projects/rhythm-machine/' | relative_url }}).)

Of course, now I have to *use it* to practice--but that also feels much more motivating when I have a tool that makes it
clear what to do.

The theme across all of these is that instead of passively consuming content from Claude, what's going on is each of
these approaches helps me to *think* and notice when my skill or understanding isn't good enough.
