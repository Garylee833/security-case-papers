# Six Days to Break Chrome: What XBOW's $250,000 AI-Assisted Exploit Chain Actually Proves

**Author:** Gary Lee
**Date:** October 17, 2026
**Classification:** Vulnerability analysis — browser full-chain exploit, AI-assisted offensive research

---

## What happened

A four-person team at the security startup XBOW broke Google Chrome wide open in six days. Not one bug — three, chained together into a full exploit that escapes both of Chrome's sandboxes and runs code on a Windows machine when the victim does nothing but load a webpage. No clicks, no downloads. Just open the page.

Google confirmed all three bugs, shipped fixes, and paid XBOW $250,000 — the top bounty for a full Chrome chain, and the first paid under the program's 2026 rules. The bugs never hit real users. XBOW estimates a billion people could have been affected.

The part that got everyone's attention: the team did it with a publicly available AI model — OpenAI's GPT-5.6 Sol — and about $40,000 in API calls.

## The six days need their frame

The headline writes itself: "AI hacks Chrome in six days." The truth is more useful.

XBOW's sprint ran August 2–7, 2026, during Black Hat and DEF CON week in Las Vegas. But that sprint wasn't the whole story. The company had set the challenge back in January, and their *first* full Chrome chain took two months to build. The six-day run was the rebuild — the second chain, done fast because they'd already learned the terrain.

That's not a knock on the achievement. It's the honest version, and the honest version is the one that teaches something.

## What the AI actually did

Brendan Dolan-Gavitt, who led the technical work, wrote it up plainly. The AI agents searched Chrome's source code, tested the team's hypotheses, built proofs of concept, and drafted early exploit code. The humans chose the targets, supplied context, challenged the agents' results, and decided which pieces to chain together.

Read that division of labor carefully, because it's the whole story:

- The AI did **speed and breadth** — searching code, running down ideas in parallel, discarding dead ends fast.
- The humans did **judgment** — picking where to look, questioning what the machine found, assembling the chain.

"We did apply a fair bit of our own human expertise and judgment," Dolan-Gavitt wrote. That's not modesty. That's the load-bearing wall.

The three bugs themselves tell the same story: one in the V8 JavaScript engine's Maglev compiler (giving read/write inside the V8 sandbox), one in the animated WebP decoder (an out-of-sandbox write), and one in Crashpad — Chrome's crash handler, which runs outside the sandbox — that turned the write into full code execution. The Crashpad flaw is tracked as CVE-2026-78952. Each bug is a real vulnerability a human had to recognize as chainable. The AI found candidates; the humans saw the chain.

## Why six days matters

XBOW's CEO, Oege de Moor, put it this way: a veteran from a three-letter intelligence agency told him his team used to spend six months finding this kind of vulnerability and getting total access. XBOW did it in six days.

XBOW's own estimate: without the models, four specialists would have needed six to nine months for comparable work. Dolan-Gavitt's warning to defenders: "Six days and $40k is not a lot of time or money when the payoff is a Chrome chain!"

That's the number to sit with. Not "AI replaces researchers" — the researchers are right there in the story, doing the parts that matter. It's that the *discovery bar has dropped through the floor*. A capability that used to belong to intelligence agencies and elite teams now costs $40,000 in API calls and a week of focused work.

## What this means for the rest of us

**For defenders:** Assume the other side has this too. If a defensive startup can chain three Chrome zero-days in six days with a public model, a motivated attacker with the same tools can do the same against your stack. The patching bar hasn't moved — but the discovery bar has, which means your window between "bug exists" and "bug is weaponized" just got shorter. Patch fast, and treat browser updates as urgent, not routine.

**For the "will AI replace security people" debate:** This story is the answer, and it's not the one either side wants. The AI didn't replace anyone — four researchers worked full weeks. But those four now do the work of a team ten times their size. The people who thrive aren't the ones competing with the model; they're the ones who learn to direct it. Target selection, context, skepticism, assembly — that's the job now.

**For bug bounty economics:** $250,000 for six days and $40,000 in compute is a remarkable return. Expect more teams to run this playbook. Expect Google's bounty budget to get a workout.

## Remediation

- The fixes shipped in Chrome 152 (152.0.7977.65 on August 25, 152.0.7977.82 on September 3). Chrome updates itself, but the fix only takes effect after a restart — **relaunch Chrome and confirm you're on 152.0.7977.82 or later**.
- Enterprise: verify fleet versions through your management console. Anyone still on 152.0.7977.65 or earlier without the follow-up patch is exposed.
- No action needed beyond updating — Google confirms the bugs were never exploited against real users.

## Methodology Note

This analysis was compiled from XBOW's published writeup (October 13, 2026), Google's Chrome release notes, and independent reporting (The Register, The Hacker News, CSO Online, Startup Fortune). No exploit code was executed or reproduced; all conclusions rest on published technical accounts.

---

*Sources: XBOW technical writeup (Oct 13, 2026); Google Chrome release notes (Aug–Sep 2026); The Register (Oct 14, 2026); The Hacker News (Oct 14, 2026); CSO Online (Oct 16, 2026).*
