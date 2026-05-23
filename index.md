---
layout: default
title: Home
---
Hey, welcome.

I have this idea that if I spend more time writing about things that interest me, that will be good.

So, that's the experiment I'm running.

A short summary of stuff I've done, roughly reverse chronologically:
* Hands on work with 0xPARC and now the Field Extension Institute, trying to figure out how to use techniques from
recent cryptography advances to make the world work better for specific versions of better that tend to have a flavor of
'make it possible to coordinate more easily in high trust ways on hard problems'. One recent example is working on
verifiable inference for LLMs.
* Various management/exec coaching projects, which I enjoy because people seem to find it helpful to talk to me about
tricky problems, and I like helping people think their best thoughts.
* Instructor and course creator at Reforge on Technical Foundations for Product Management, which I worked on with my
friend Anand. We created (or codified) a number of frameworks that I believe are pretty broadly useful for non-technical
folks engaging with technical topics.
* Board member at CivAI and Transluce, both of which are trying to help make AI go well.
* Decoding Sales, a podcast about what I like to call Authentic Sales, which is a particular approach to human
relationships that my friend Peter Ahn espouses. Came out of some of the early work at USDR where I realized that we
were doing a kind of non-financial sales process.
* U.S. Digital Response, an organization that started off helping governments respond to COVID-19 and has become a more
general government capacity building organization. USDR was an accident of good fortune coming out of an otherwise miserable time (the early days
of COVID-19). Learned a lot about how government worked.
* Dropbox, where I worked on Dropbox Business, a bunch of developer infrastructure, hiring and career processes, and
tried to start a product incubator. Learned a lot about management and scaling organizations.
* Wrote Jumping into C++, which a lot of people have found useful for learning to program. Through a particular quirk of
my approach to the writing process, I was able to write it quite quickly in wall clock terms (about 80 hours).
* Liquid Machines, where I worked a lot on interesting low level reverse engineering and also wrote a pretty neat
programming language. We got acquired by Check Point software, where I worked on slightly less interesting integration
work.
* Harvard CS, where I found the most joy academically and socially in TFing CS 50 and 51.
* Created the initial content that eventually became Cprogramming.com when I was ~13. The early internet was wild; I had
no right to become the person behind one of the leading sites on the internet (surely from a raw visit count perspective if nothing else)
covering C and C++ for a generation. But it happened. I am so excited for today's ambitious preteens and teenagers.

Stuff I enjoy doing:
* Chess - I played a lot as a kid, but my goal was to 'win' rather than appreciate the beauty of the game, so it isn't as
satisfying as an adult (although I'm still reasonably good at it). I did win the Louisiana high school championship
twice, which was cool.
* Crossword puzzles - I was very bad at them, so I decided to see how good I could get. I managed to once be both good
and bad enough to win the American Crossword Puzzle Tournament's division for "people who were demonstrably not very
good in prior years" (aka never finished in the top 65% before) in <a
href="https://www.crosswordtournament.com/info/history.htm">2010</a>.
* Piano - I started learning piano in January 2025 because I didn't understand music at all, and I thought it
would be another fun skill to get good at. Turns out it's really fun, and also a great way to understand more about
how music works.
* Slay the Spire (and StS 2) - I've spent an embarrassing amount of time playing StS but it is
really fun. I mostly play Ironclad (and yes, I can beat the heart at A20). Nowadays I try to limit this to either StS 2
multiplayer with friends or while traveling.
* Powerlifting - I've been lifting for roughly the last 9 years (since early 2017) and now have a home gym that is
 delightful. Deadlifts are my favorite lift.
* Rooting for the New Orleans Saints - Who Dat!
* Running - I mostly like 5ks and shorter runs, but I've done two (extraordinarily slow) Napa Valley half marathons
(whose course is fantastically beautiful).
* Travel - sometimes I write about it, with Alex, at the increasingly inaccurately named <a href="https://alexandalexacrossamerica.wordpress.com/">Alex and
Alex Across America</a>
* Generally, learning new things, making stuff that is satisfying and thinking about how things in the world really work
* Reading, in general, though especially anything written by Robert Caro. (Greg Egan is also quite good.)
* Writing, in theory, though I don't do that much of it these days. I want to experiment with doing more of it here.

Some random facts about myself:
* I've been a vegetarian since 2001.
* I'm from New Orleans originally, and spent ten years in the greater Boston area, so I've now lived a tricoastal life.
* On Fridays, I wear Hawaiian shirts (usually, a New Orleans Jazz Fest shirt)
* I am into the concept of spaced repetition learning and have been using SuperMemo for over a decade. I'm pretty sure I
remember more stuff I want to as a result.

I live in the wonderful city of San Francisco with my lovely partner, who is also named Alex, and our extremely docile cat, Ellie. 

I believe San Francisco still largely under-rated for its natural beauty, mild weather, access to nature, quirky
personality and neighborhoods, and hub of interesting innovation and talent. That isn't to say nothing is wrong with it (among
other things, we need more housing and broadly sane local governance and the tech centric perspective can sometimes feel
stifling), but the fact that it can survive some problems is a testament to its natural advantages. (I never believed
the 'downfall of SF' narratives post COVID, and I should get some Bayes points for being right about that.)


You can reach me at [alex.allain@gmail.com](mailto:alex.allain@gmail.com).

{% if site.posts.size > 0 %}
## Recent writing

<ul class="post-list">
  {% for post in site.posts limit:5 %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %-d, %Y" }}</time>
    </li>
  {% endfor %}
</ul>

[All posts →]({{ "/blog/" | relative_url }})
{% endif %}
