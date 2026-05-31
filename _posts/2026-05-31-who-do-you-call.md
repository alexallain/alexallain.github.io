---
layout: post
title: "Who do you call when it breaks?"
date: 2026-05-31
---
One of our favorite [stickerables]({% post_url 2026-05-25-stickerables %}) at USDR was, "who do you call when it breaks?" 

What this meant was: don't build something for a government and expect them to take ownership of it if they don't know
what to do when it inevitably stops working. This led us to creating a lot of low code solutions--often using tools that
the government already was comfortable with, and sometimes bringing in tools like Airtable when it was clear they'd be
comfortable owning it. (This worked very well--nearly every government we worked with was very happy, and when we pulled
in low-code tools they often enthusiastically adopted them and sometimes evangelized them!)

What we definitely didn't do was write code for them. I remember we had a handful of times where we tried writing custom
code. I won't say that none of them worked--we built tools for grant reporting and discovery that we committed to
maintaining, and that was largely custom code. But it did require us to make a significant commitment to building a
team, so we didn't do it very often.  (In fact, after I left USDR, we eventually transitioned ownership of the grants tool to
[Nava](https://www.usdigitalresponse.org/resources/transforming-federal-grants-access-usdrs-tools-find-a-new-home-with-nava-pbc)).

But I can't help but think that things are changing. I've personally found coding agents to be mediocre but still
helpful sysadmins (in addition to very useful in-house developers).

For a while when I was responsible for all the tools and ops work at USDR, I would periodically have to deal with a
script that someone else had written to do a mundane task like use a headless browser to click a button in the Airtable
UI. (Yes, it really needed to be a headless browser and not just curling the endpoint). This was never fun work: it was a
complicated script for good reasons, and I never wanted to take the time to really absorb how it all worked well enough
that it would be easy to fix next time. (This would have taken too long, and I'd forget it anyway.)

I have a very strong intuitive sense that if I'd had agentic coding tools, this would have been so. much. easier. Dealing with
this kind of self-contained script is *exactly* the sort of thing that they tend to be good at. I'd probably still
have needed to do some work poking in the browser sometimes, and LLMs tend to be somewhat mediocre at knowing exactly
what buttons a website has, but it does know *what it needs from the script* and that alone is probably enough to get
the job done. It's also possible that a tool like Cowork would make even this a trivial part of the workflow (though I
haven't tried it.)

So clearly these tools would have helped USDR's internal operations. 

But how does this help governments?

Do we have a new answer to "who do you call?" I admit that I think today the answer is no. It seems like Claude
Code is still a bit too esoteric for a non-technical user (I've helped a few folks get it set up, and it's illuminating
to see all the places--like, say, getting started with the terminal--that feel unnatural to people who aren't
developers.) To me this makes it pretty clear that Claude Code, today, doesn't solve this problem directly because so
many of the problems we solved at USDR required helping people overcome smaller barriers than that to using tools
productively. (Think: something like setting up Outlook email automations.)

The usability gap feels a little bit like the usability jump from 'raw database' to Airtable. Something that feels small
in principle, but that makes a huge difference in accessibility by getting a lot of little UX details right (ex:
Airtable feels like a spreadsheet, which many more people are familiar with, and then just gently layers in cross-table
references with an intuitive UI that makes it feel natural). It wouldn't be surprising to see these gaps close--but they
do need to be closed.

That leaves another potential path in the immediate term: commit to owning the maintenance for more projects because
the tools increase your technical capacity to do so.

This one seems more promising to me in the short to medium term because it heavily reduces the ramp-up tax and would
allow an organization like USDR to maintain projects without needing to go back and ask the original volunteer for
context--especially if the handover docs are halfway good.

That said, it only reduces the technical work. In practice there are a lot of challenges to owning maintenance that
aren't technical. You have email back and forths, coordinating times for meetings, figuring out how to walk someone
through making changes (since you might not have direct access to the underlying systems), and making sure that
the fix is solving the problem. Sometimes this issue will be something like "a third party service just happened to go
down" and you can't reproduce it anymore. Will you just believe Claude when it claims that's the case? I sure would want
to check that myself!

So I am not sure that it gets you necessarily a 10x scaling factor for the number of deliverable projects or something
like that--but it might get you 1.5 or 2x, and I think that could be pretty promising! And if that's 1.5 or 2x now, it
sure feels tantalizingly close to a lot more as the tools get better. So maybe, one day, the answer to who do you call
when it breaks will be: Claude!
