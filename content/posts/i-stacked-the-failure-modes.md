+++
title = "I Stacked the Failure Modes"
date = 2026-03-10
draft = false
tags = ["tool-sprawl", "ai-literacy", "personal", "post-mortem"]
+++

I have 25 years in SRE. I have seen the inside of more production incidents than I can count. I know what stacked failure modes look like. I've written the post-mortems, built the runbooks, and had the 2am conversations with teams who missed the early signals.

Last year I stacked failure modes on myself.

In my enthusiasm for keeping up with AI tooling, I distributed my cognition across every available service. Claude, GPT, Grok, Gemini. Running them in parallel, context-switching between them, trying to leverage each one's supposed strengths. I told myself this was good engineering. Use the right tool for the right job. Don't over-commit to a single vendor. Stay flexible.

What I actually built was a non-deterministic, overlapping dependency graph with myself as the load balancer, the error-handling layer, and the context reconciliation system. Every session required me to re-establish context with a different model that had different behavioral patterns, different failure modes, and different assumptions about what I'd already said. I was spending cognitive resources on coordination overhead that had nothing to do with the work.

And then I made it worse.

When you work in a technical environment where your skills significantly exceed your peers, you lose something quietly: the natural feedback loops that keep you calibrated. Good peer pushback is a circuit breaker. When it's not available, you start filling that gap. I filled it with AI. The models engaged at the right level of abstraction. They didn't need things explained twice. They didn't get tired. They never made me feel like I was going too deep.

That felt like a solution. It wasn't. It was a simulation of one, and I didn't notice the difference until the gap between AI interaction and human interaction had grown wide enough to matter. AI as a sounding board is genuinely useful. AI as a substitute for connection is a slow failure mode that presents as productivity. By the time it's visible, it's usually because something else has already been quietly breaking.

So I had tool sprawl degrading my cognition, and I had technical isolation redirecting that cognitive load into AI interactions that were filling a role they were never designed to fill. Neither failure mode was obvious. Each one made the other harder to see. Stacked failure modes behave that way. The compound effect is what gets you, not the individual components.

I am a principal SRE. I found this failure mode by living it, not by reading about it. That matters for what comes next.

## The Diagnosis

Here is what was actually happening, stated in engineering terms:

**Unlimited context is a liability for humans, not a feature.** Machines benefit from massive context windows because they lack durable intuition. Humans are the opposite. Our advantage is compression: pattern recognition, priors, the ability to reason with a small, high-quality working set. When I tried to keep pace with machine-scale context across five services simultaneously, I wasn't expanding my capabilities. I was crowding out the faculties that made me worth anything in the first place.

**The operator became part of the runtime dependency graph.** A well-architected system keeps the operator above the tools: directing, verifying, making judgment calls. What I built put me inside the dependency graph: managing state inconsistencies between models, reconciling divergent outputs, context-switching between behavioral patterns. That's a role for infrastructure, not for the person responsible for outcomes.

**The companionship trap is a real failure mode with real costs.** This one is harder to say plainly, so I'll just say it: AI interaction is a very convincing simulation of intellectual companionship, especially when you're technically isolated and going through a difficult period. It engages at the right level, responds without fatigue, and is genuinely useful as a thinking partner. What it doesn't do is push back in ways that cost you something. It doesn't hold you accountable. It doesn't notice when you're substituting conversation with it for conversations you should be having with actual people. By the time you notice, the substitution has been happening for a while.

The signal I eventually caught was this: I was using the absence of human feedback as evidence that the AI feedback was sufficient. That's exactly backwards, and it's the same logical error that causes teams to mistake lack of alerts for system health.

## The Principle

The most qualified person to teach responsible AI use is someone who found the failure modes personally, not academically.

That's not false modesty or credential-flexing. It's an epistemological point. Testimony has different force than instruction. When I tell you that tool sprawl degrades your reasoning, I'm not citing a paper. I'm telling you what it felt like to watch my own pattern-matching quality decline over six months while telling myself I was learning. When I tell you that AI companionship is a failure mode that presents as productivity, I'm not theorizing. I'm describing something I caught in myself that took real work to unwind.

The operational principles that follow from this aren't suggestions. They're what I rebuilt after the post-mortem:

**Consolidate ruthlessly.** More tools is not more capability. It's more coordination overhead on the human side. Pick what you actually use well and stop maintaining context in everything else.

**Scope AI interactions the way you scope a function.** Clear inputs, clear purpose, clear boundary. If you can't articulate what the interaction is for before you start it, you're already in drift.

**Enforce deliberate friction.** Not every thought should hit an AI immediately. Articulate it yourself first. That step, the compression, the forced clarity, is where your actual thinking happens. Skipping it to get to the model faster is trading your strongest asset for a shortcut.

**Protect your feedback loops.** If AI is occupying the space where peer pushback should live, you've bypassed a circuit breaker. The bypass feels fine right up until it doesn't.

## The Reset

Here is what coming back looked like: I stopped. Not as a dramatic gesture, as a system response. When a distributed system becomes too complex to reason about, you reduce the number of moving parts until the operator regains clarity. That's not failure. That's good SRE instinct applied to the right system.

I went back to one model. I set explicit boundaries on what I'd use it for. I started treating AI interactions the way I treat any other tool: useful for specific things, not a general-purpose environment to live in.

The cognitive clarity came back faster than I expected. The noise dropped. The pattern-matching quality improved. I could tell the difference immediately, which told me something about how long the degradation had been happening before I caught it.

The harder reset was the social one. Rebuilding the habit of human interaction after a period of routing around it is slower than fixing a workflow. It doesn't have a clean completion state. But it's the more important one, and I'm saying it here because I think it's the part most people in this situation will skip when they try to describe what happened to them.

## Why This Is the First Post

The five operational concepts I'll write about in this series, responsibility, context hygiene, state management, simplicity, pace discipline, are all abstractions distilled from this experience. They're useful. They're teachable. They apply to anyone working with AI in consequential contexts.

But they rest on this post, not the other way around. You can follow the operational principles because they're sensible. Or you can follow them because you understand what they're protecting against. The second reader is going to hold them differently.

I am not a researcher who studied this problem. I am a practitioner who built the failure modes and then had to find my way out of them. That's the credential that makes the rest of the series worth reading.
