---
layout: post
title: "A report from the Field (Extension Institute)"
date: 2026-06-22
---
*This is a write-up of how I spent February to June of this year as part of the Field Extension Institute’s prototype Polynomial program for engineers, founders and the curious to explore ideas in advanced modern cryptography.*

One of my goals at the start of 2026 was to spend more time doing hands-on technical work. After leaving USDR, I'd gotten interested in the power of cryptography, and spent a lot of time with 0xPARC, an organization that is, frankly, difficult to describe and googling them doesn't help much. But basically 0xPARC advanced the state of thinking on how cryptography can do more than just keep secrets or power blockchains. (You can get a flavor of that [here](https://0xparc.org/writings/programmable-cryptography-1)).

However, most of that time had been spent at a more abstract level of thinking and the occasional doing. When I started working on my yearly goals for 2026, I realized that I wanted to shift the register of how I was operating. I started out by building some personal tooling with Claude, which was enlightening in that way that I felt when I first played chess against Jeff Sarwer (the unfairly-characterized villain of Searching for Bobby Fischer). Jeff is a very nice guy, and he happened to know my chess coach ([Alfred Carlin](https://thechessdrum.net/blog/2018/04/03/new-orleans-master-alfred-carlin-passes-away/)), so he swung by the Chess Academy of New Orleans. He hadn't played tournament chess in years, but we played some blitz. He pushed me off the board--I'd played strong players before, including my coach, but Jeff's sense for the game was a different level entirely. The ceiling for what I understood was possible went up. Claude did the same thing, except this time it was my ceiling for "what I could do" that went up.

The question, then: to what end?

In early February, I met up with my friend Albert, who was taking on stewardship of a project within a new organization, the Field Extension Institute. The project, originally incubated in 0xPARC and a sister organization called General Purpose, focused on building verifiable inference for LLMs. (I.e. proving that the tokens that were generated came from a specific model with a specific set of model weights, without revealing the weights of the model to the person who is doing the verification.)

Albert's proposal was pretty simple: we've made a lot of progress on this project, but it would be helpful to have someone come in and help stitch it together. Helping out with this would be both useful and educational: you'll learn a lot about how LLMs work, a lot about how modern cryptography works, and you'll get another codebase to experiment with using Claude. 

To be completely honest, it wasn't obvious that I'd have anything to contribute. The Field Extension Institute has some incredibly talented mathematicians (think: IMO gold medalists, Putnam fellows), and I was starting from near-zero on a bunch of this stuff. Anyway, I told Albert, just let me take a look at the codebase.

The core "pitch" for why doing this kind of proof of inference should be possible in any reasonable execution time is
that you can verify a matrix multiply faster than you can do the actual computation using Freivalds' algorithm (n^2 vs
n^3 or n^2.\<whatever the current asymptotic of an algorithm nobody uses is\>), and the reason NVIDIA is worth 5
trillion dollars isn't that they spend all their time making softmax fast.

Another core intuition is that the idea of applying cryptography to language models feels like it has the potential to be genuinely useful. One simple example: imagine you have data centers filled with geniuses responsible for making the most important economic and strategic decisions in the world. Seems like the kind of place that an attacker would be ... drawn to. Wouldn't it be nice to be able to prove that nobody tampered with the thinking of those geniuses?

But even beyond that: how do you control what might soon be the most powerful minds in the world? It would be nice to
have mathematically enforceable, unbreakable guarantees about what is, and isn't, possible. This is the sort of hard
guarantee cryptography is (probably) capable of: I can give you an encrypted file and you simply *cannot* decrypt it
without the key (in the case of a one-time pad, with absolute certainty; in cases involving symmetric key encryption,
assuming we live at least in
[minicrypt](https://www.quantamagazine.org/which-computational-universe-do-we-live-in-20220418/).) At some vibesy
intuitive level, it feels like there ought to be something useful here!

Something else that made this project extremely interesting at a personal level is that it touched on the cutting edge of several different technologies:

* Naturally, it would mean learning a number of core cryptographic primitives, how they fit together, and some of the core patterns of working with zero-knowledge proofs  
* In order to prove a model, you have to have a pretty good understanding of what the various parts of an LLM are doing  
* To accelerate performance of the prover, we used GPUs, which meant learning something about CUDA (one thing that I appreciated was that we had the GPU boxes in the office, so you could also get a physical sense for what these machines were like. Specifically, when the GPUs are running, they are LOUD. It’s also striking to see how physically small the actual GPU is compared to the size of the rack that’s supporting it.)  
* Plus I got a chance to experiment with using Claude on an existing codebase that other people were working on

There were a few other folks working on the project, but I didn't want to bother them with basic questions, and I was curious to try out an AI-first approach, so I spent the first few days having Claude walk me through all of the layers of the codebase, with a particular emphasis on explaining all of the core mathematical primitives.

This worked remarkably well--I was able to use Claude as a kind of onboarding buddy to the codebase, having it explain all the various technologies in the stack. In retrospect, I'm not 100% confident that this was the *most* efficient way to onboard. I can see a lot of value in having a human do a real whiteboarding session for onboarding or doing pairing (both because I think they'd be more calibrated on what would be most important but also because it's useful for a team to have shared knowledge of what other people know.)

I also think I underestimated the value of doing some hand-coding early on--at least for this project, there were 
a number of little details that mattered quite a lot (tensor shapes, how we handled large numbers, etc). Doing some kind
of hands-on implementation probably would have forced those to the surface more quickly and more deeply.

On the other hand, I'm pretty sure that a purely traditional onboarding process would have taken *longer* - there's just (probably) a hybrid that's even better than the extreme approach I took. (Perhaps with a model as smart as Fable, I could ask it to design a customized curriculum of both what to learn at a conceptual level and where to do some hands-on implementation to get that visceral experience?)

Either way, I went from being kind of confused about everything that was going on, to shipping a fairly meaningful
amount of code over a few weeks. I had Claude pull some stats--over about 10 weeks of active development, I ended up
with 77 commits and git blame showed I contributed roughly 33% of the main project's codebase (for a project that had
been going on for months before). Lines of code isn't an amazing metric, but the main point here is that it was
possible to get up to a competent level of contribution quickly. (This AI-powered ramp up velocity wasn’t unique to me.
Flo Mueller, who joined the project a week after I did and used similar Claude powered workflows, had a similar level of
contribution.)

As I worked on the project, I got a really visceral sense of the value in thinking across the layers of abstraction from mathematical concepts, to cryptography, to how models are implemented, to GPU hardware, to specific use cases. The more you understand each layer of abstraction, the more interesting the things you can do. For example, what if you decide it doesn’t matter whether your proof is non-interactive--does that buy you anything? (In our specific implementation, yes--it would have helped avoid a lot of unnecessary work!) Perhaps your use case allows for some kind of selective sampling of results. Perhaps not every single token needs a proof as long as it *can be proved* later, and whether that is true (or not) depends on understanding the details of how deterministic the computation is, and what information you'd need to keep around to create the future proof. (You have to future proof your future proof?)

In general, a lot of specific ideas for optimizations--and even more potential use cases--emerged from working across the layers and having enough detail to understand what might be possible. For example, understanding the model, the GPU, and cryptography together are also helpful for thinking about the most effective way to quantize the model. (What will be fast on GPU, while being relatively easy to prove, without compromising model quality *too* much?) I'm also quite confident that I merely scratched the surface here!

Overall, for this kind of project, I came away believing the ceiling for the kinds of contributions that are possible is *very* high. The more someone has deep familiarity with multiple aspects of the problem, the more ideas they can track down. I would place this in contrast with typical "SaaS software" where most of the problems today are business or product problems and the details of the technology are mostly irrelevant. This means that this kind of project is one of the handful of areas that have nearly unlimited returns to technical depth and skill, and therefore (to me) embody the true spirit of interesting engineering work. (This means that while it's easy to get to a competent level of contribution, I think it's also correspondingly challenging to get to mastery--there's a large skill tree.)

Similarly, this project continued to reinforce my bias that leading complex technical projects requires technical depth in addition to good general leadership skills. The technical details about the particulars are really important to know how to think about the project roadmap. For example, a simple goal of "prove the model end to end" is a good end goal, but too far from the technical details to align real efforts. It was more useful to think in terms of more concrete milestones of completing specific aspects of the implementation that would be opaque to someone trying to manage engineering as a black box. (For example, better milestones might be things like: we need to build a hadamard claim we can use to prove the RoPE step or someone needs to ensure every part of the model forward pass is being done with integers instead of floats.)

Moreover, because of this high ceiling, it was clear that at least as of Claude Opus 4.8, there was still plenty of room
for humans to do useful work. It was pretty common for Claude to make subtle mistakes in the cryptography or to run
experiments with different assumptions than I wanted (ex: when I had it experiment with comparing Freivalds' without any
cryptography to vanilla matmuls on tensorcores, it didn't initially optimize Freivalds' at all, which is obviously not
the point of that kind of comparison. It turns out Freivalds' is eventually faster, but only at a relatively narrow
slice of the matrix sizes that are relevant to modern open source models.) After a few weeks of onboarding, I was
hitting the point where I could catch and fix issues that Claude wouldn't think about or notice.

Aside: Fable 5 came out at the tail end of the project, but I'd put together a mini-benchmark where I had Claude trawl through all of our commits on the project to find well-tested bug fixes and use the tests as an oracle for a mini-cryptography benchmark. No model, as of this writing, was able to find all four of the issues in the benchmark. Fable 5 and GPT 5.5 were tied at finding one issue each (albeit different issues).

Having an extremely well-versed AI that could answer any academic question I could possibly think of was also not the
same as having an internalized map of the conceptual landscape when it came to figuring out where to go next. Nor could Claude effectively substitute. It was much more excited about making things work end-to-end or making something production ready rather than recognizing that the codebase was entirely experimental and the goal was to enhance our learning. In general, it felt tough to get Claude to think and operate across the levels of abstraction effectively. I did try scaffolding Claude to do this, and with prompting I could sometimes get it roughly there, but it made it difficult to use as a true co-equal thought partner. A brilliant (if sometimes off key) implementor, but not a strategist.

Not surprisingly, then, it turned out that most of the interesting insights and breakthroughs to try came about through talking to other humans. A big part of that was being able to easily inhabit the same project context and work simultaneously across the layers of abstraction fluidly. Flo and I, in particular, spent a lot of time brainstorming and sensemaking together–and some of the most productive times in the project were when he flew into SF to work together in person with the rest of the team. If I were to continue on the project, I'd put a lot more emphasis on trying to optimize the working environment so that the chance of getting there with Claude was much higher. I suspect this would involve doing a lot more to record all of the team interactions in github in a machine-readable way, having Claude synthesize for itself project goal updates and conclusions from meetings, and trying to figure out how to prompt Claude to think like a project leader.

I also found that writing some code by hand (and writing documents by hand) was still helpful. As much as having Claude
there to explain things was *useful*, the sweat work of having to be precise in specific ways (writing code and writing
text share a similarity here) was the only thing that forced me to grapple with important details. There's something
about the texture of an idea where if you don't engage *all the way* down to the surface, you miss whether the texture
is one of sandpaper or a baby's bottom - and it turns out that's sometimes quite important! You can't really cheat the process of understanding what is going on.

So I found myself reaching to some traditional methods of knowledge acquisition designed to give a breadth of perspective--for example, I found that reading (parts of) Justin Thaler's [Proofs, Arguments and Zero-Knowledge](https://people.cs.georgetown.edu/jthaler/ProofsArgsAndZK.pdf) was a good way to orient myself. I also found myself paying attention to the latest ArXiv and the [cryptology eprint archive](https://eprint.iacr.org/days/7) posts on cryptography and security, which was also very helpful for getting a sense for the kinds of problems that people are thinking about.

More generally, I began to see my own ability to understand as many of the layers as possible in as much detail as possible as the primary bottleneck to my progress using Claude. So I put some effort into finding ways to have Claude "prompt engineer" me by figuring out what it could put into my "context window" so that I'd learn the most in the quickest amount of time.

Three things that I found helpful for that were:

* With some prompting, Claude makes an excellent tutor and coach: for example, being very clear that I wanted Claude to look for any ambiguity in my responses tilted it from "oh sure, what you said, if we interpret it just right, sounds basically true" to the steel trap mind I want when evaluating my vague or vibes-y responses ("well, what you said there, interpreted normally, is probably correct, but did you *really* understand the specific thing--can you elaborate on that detail?")  
* Having Claude build interactive examples and explainers was also quite useful (and fun!) I found that this did take
* more rounds of iteration than I expected though. Lots of little details matter.  
* Finally, I also found having Claude run experiments to be a great way to build intuition around empirical questions. The more I got into thinking about the truly unanswered questions (like "how to deal with the fact that hardware is moving to fast paths for floating point matrix multiplies") the more I appreciated the ability to just run all sorts of experiments at high velocity with Claude where the limiting step would previously have been rapidly churning out code.

One warning on the last one: it's seductively easy to reach a (tentative) conclusion based on an experiment without
inspecting the details, but I found that those details often would matter a lot (see the example up above about not
optimizing Freivalds'). On the other hand, this still felt far faster than hand implementation because taking time to understand the experiments in detail often led to useful learnings while I still avoided a lot of boilerplate implementation. I do think the fact that [reality has a surprising amount of detail](https://johnsalvatier.org/blog/2017/reality-has-a-surprising-amount-of-detail) does act as a bit of a speed limit here though.

> If you're interested in more deeply understanding the cryptography behind this, you can go to this [interactive explainer
of a matmul proof](https://alexallain.com/projects/matmul-proof-explorer/) I had Claude create for me as part of that learning.

Okay, so I learned a lot--but, to what end?

Ultimately, I did decide to stop working on the project.

It had two parts to me:

* A personal learning journey - what could I do with the latest tools working on novel problems that nobody seems to have solved?  
* A moonshot AI safety project - could we find ways to make cryptography directly useful for safety or trustworthiness of AI systems?

The project clearly delivered on the first. I really enjoyed the technical challenges of the project and getting to learn a bunch of interesting--and clever--math as well as engineering and ML concepts.

On the second point, we ultimately decided to put the project on ice due to the challenges we ran into.

The first, but more tractable ones, were related to performance. For example, while we did have pretty fast individual matrix multiplies–it turned out that in the proof system (unlike normal inference) it’s the nonlinear functions that really hit us hard. Some of the quantization work we had to do also added a lot of overhead and complexity as well (among other things, due to the need to do a lot of rescaling proofs). That said, we had directions we could take to tackle most of those issues.

The bigger issue is that when we stepped back to look at the direction of modern hardware, we realized that the latest
generation of accelerators were all optimizing for floating point. Our proving system was built natively for field
operations (integers mod a 32-ish bit prime), and after looking at the hardware it became clear that the trends were
toward ever-less-precise versions of floating point (FP8, now
[FP4](https://www.nvidia.com/en-us/data-center/vera-rubin-nvl72/#specs)) being the fast paths, and those number formats are very difficult to work with in cryptography.

While you *can* precisely emulate floating point numbers in a finite field in principle, it’s slow. First of all, it's
just a baseline of about 50 times slower than doing a normal arithmetic operation. Second, you can't actually *use* the
Freivalds' algorithm I referenced up above because ... floating point addition is not associative, and Freivalds' reorders operations vs a regular matmul. So to prove a matmul, you have to do a proof of a full, exact matmul at n^3 vs n^2, on top of that 50x constant factor. This...sucks.

We initially thought that there was a path to handling floating point due to papers like this one on [approximate sumcheck](https://eprint.iacr.org/2025/2152) (sumcheck being one of the fundamental algorithms we relied on). This is a cool paper, but there are at least two challenges that it doesn't resolve. First, there's no 'commitment scheme' that works for floating point numbers. If you can't create a commitment, then you don't get the zero knowledge properties we need. The second issue is: well, approximate sumcheck says an attacker gets some wiggle room–it’s *approximate*. How much wiggle room is *too much* and allows an attacker to wiggle their way to ... an attack that flips the order of model logits? If you run your model in, say, FP8 and run approximate sumcheck, the amount of wiggle room is defined by how much natural noise is introduced when doing a matmul in that floating point format, and basically you have to allow the attacker more wiggle room when you have less precise floating point formats because the smallest representable difference is larger.

I spent a bunch of time playing with Claude to run different experiments to see whether this was a real concern, and my conclusion is that--while it obviously depends a lot on your model and query--it seems like a real issue and the defenses to defend against it felt quite ad hoc, making it hard to get excited about solving the first problem of finding a commitment scheme for floating point numbers.

As a result, the Field Extension Institute has shifted to other applications of cryptography for language models (for example, training and running models within fully homomorphic encryption). 

As for me, at a personal level it seemed clear the timeline of my contributions going from competently useful to far
enough along the skill tree to impact the key frontier mathematics we’d need to make progress was probably beyond the
horizon of "just wait for the AI to [get good enough](https://metr.org/time-horizons/) to solve it for you."

Toward the end of the project, we went to a verifiable AI conference where the two most compelling talks were by lab employees (OAI and Anthropic) whose main message was (to summarize coarsely): if you care about verifiable AI, you should work in a lab.

And, yeah, I decided they had a point.
