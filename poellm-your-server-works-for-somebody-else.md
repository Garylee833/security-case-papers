# Your Server Works for Somebody Else Now

*What I took from the PoeLLM campaign and the 3,400 exposed AI servers — written 2026-10-09, from public reporting (The Hacker News, October 7, 2026). I keep facts and claims in separate piles below, because that's the only honest way I know to read a story like this.*

---

## What happened, as best I can piece it together

Somebody went out and found more than 3,400 AI and LLM servers sitting exposed on the internet — LiteLLM, Gotenberg, Gitea, Ivanti Sentry, the kind of tooling people stand up fast because it demos well. And then they moved in.

The Hacker News calls the campaign PoeLLM, run by an operation named Canto Incognito. The payload was a miner — the machines weren't ransomed or wiped, they were put to work, quietly earning for somebody else. And it gets worse: the victims weren't just mined. They were reused as scanners, sent out to look for the next exposed server. Every machine taken became a recruiter for the fleet.

My favorite detail, if favorite is the word: the command-and-control address was derived from a poem posted on GitHub — `github[.]com/ejejejdfbbebe` (defanged; don't go poking it). Not a hardcoded IP to get blocklisted, not a domain to get seized. A poem. You want your orders, you read the poem and do the math.

By the time the reporting caught up: the repo is gone, the C2 addresses are null-routed, and the campaign is described as disrupted. I'll grade that word below, because disrupted and finished are different sentences.

## The timeline, short version

- **The exposure comes first** — thousands of AI/LLM servers (LiteLLM, Gotenberg, Gitea, Ivanti Sentry among them) sit internet-facing, many presumably never meant to be.
- **The sweep** — the operation finds them and deploys miners; compromised hosts are then turned around and used as scanners hunting fresh victims.
- **The poem** — C2 addressing is derived from a GitHub-hosted poem (`github[.]com/ejejejdfbbebe`, defanged), keeping the control channel out of static blocklists.
- **October 7, 2026** — The Hacker News reports the campaign: 3,400+ servers, the mining, the victim-as-scanner reuse.
- **The update** — the GitHub repo disappears, the C2 addresses get null-routed, and the campaign is reported disrupted.

## What I can actually stand behind

**Confirmed — from the primary reporting (The Hacker News), the source of record here:**
- 3,400+ exposed AI/LLM servers were hit, spanning named platforms: LiteLLM, Gotenberg, Gitea, Ivanti Sentry.
- The payload was cryptomining, and compromised machines were reused as scanners to find further victims.
- The C2 scheme derived its address from a poem on GitHub (`github[.]com/ejejejdfbbebe`, defanged) — a signature worth remembering in its own right.
- The repo is gone and the C2 addresses are null-routed as of the update; the campaign's infrastructure took a real hit.

**Claimed — reported, plausible, graded as less than proven:**
- That the campaign is *over*. Disrupted is what the reporting supports. Mining operations are cheap to rebuild, the victim list is a map of who leaves servers open, and the operators still have it. I'd bet on a sequel under a new poem.
- The exact victim count. 3,400+ is the reporting's figure; counts in fast-moving campaign stories are usually floors, not ceilings.
- Attribution of anything deeper than the campaign name. "Canto Incognito" labels the operation; it doesn't tell me who holds the keyboard.

## Why it happened, in plain words

Nobody in this story, near as I can tell, broke anything impressive. They *found* things. New AI tooling goes up the way people hang a picture in a rental — fast, crooked, and "I'll fix the mount later." Management panels, API servers, document converters, all of it answering on the public internet, some of it with no meaningful authentication between the world and the controls.

And here's the arithmetic the operators did and the owners didn't: an exposed server isn't one victim. It's a worker. A miner earns a little. A scanner finds the next ten. The fleet builds itself out of its own catch. Leaving a box open doesn't just risk *your* box — it enlists it.

The poem is the same lesson from the other end. Static indicators die fast, so the operators built a control channel out of literature and arithmetic. You can't blocklist a poem. Well — you can, and someone did, eventually. But every defender downstream of that GitHub account had to learn the trick before they could cut it, and learning takes longer than copying.

## What I'm taking from it

1. **What you leave open works for someone else.** An exposed service isn't a private mistake; it's a donation — of compute, of bandwidth, of a scanning platform with your network's return address on it.
2. **New tooling gets old discipline, immediately.** AI servers are the current fast-deploy toy, which makes them the current exposure census. If it's on the internet, it gets authentication, a patch cadence, and an owner — on day one, not after the demo impresses someone.
3. **Victims become infrastructure.** Incident scoping that stops at "did they take anything" misses the real question: *is my box out there recruiting right now?* Egress matters. What your server is doing for other people matters.
4. **Signatures are intel, graded as leads.** A C2 address derived from a poem is a calling card — clever, distinctive, and exactly the kind of thing a copycat can fake next time. File it, hunt it, never let it close the attribution question by itself.
5. **"Disrupted" is a status, not a tombstone.** Repo gone and C2 null-routed raises the operators' cost. It doesn't retire them. I grade campaigns as alive until they've stayed quiet past the point of cheap return.

## The other side of it

The strongest counter-reading against my take is this: *most of those servers were probably supposed to be reachable.* API servers serve APIs. LiteLLM behind no client at all isn't a service, it's a hobby. The owners' failure wasn't exposure itself — it was exposure without authentication and patching, which is a smaller, more ordinary sin, and the count of 3,400 lumps the careless in with the genuinely misconfigured. Fair enough, partly. And a second counter-point stings more: for a miner-grade compromise, some owners might rationally not care much — the box mines at night, the bill is real but small, and rebuilding costs more than the theft. My "your server works for somebody else" framing assumes owners feel violated. Some just feel invoiced.

Where I concede: exposure with real authentication, current patches, and egress control is legitimate architecture, not negligence, and I shouldn't write as if every internet-facing service is a scandal. The scandal is the unmanaged kind.

What would change my conclusion: a breakdown of the 3,400 showing most victims were authenticated, patched systems taken through actual vulnerabilities rather than open doors. If the operators were picking locks instead of walking through them, my lesson shifts from "close your doors" to something harder about the tooling itself, and this paper's plain-words section gets rewritten around that.

## What I still don't know

- How the initial access actually went on each platform — unauthenticated endpoints, default credentials, known flaws, or a mix. The campaign-level reporting doesn't break it down, and the breakdown is where the fix lives.
- How long the average victim mined before anyone noticed. Dwell time is the number that tells you whether detection ever had a chance.
- Whether the operators harvested anything besides compute — prompts, API keys, documents passing through those servers would be worth more than the mining, and absence of reporting isn't absence of theft.
- Whether the fleet's scanning is still running from machines nobody has cleaned yet.

---

*One last thing, because it's why I wrote this down at all: everybody in this story got a working server farm — the operators just didn't have to buy the servers. The owners paid for the hardware, the power, and the bandwidth, and somebody else collected the wages. That's the sentence I want taped over every fast deploy I'm tempted to leave "just for now." "Just for now" is how your machine gets a second job.*

## How this paper was made

I didn't read the reporting and write this in one sitting. I work with Ari — an AI partner I've built alongside my other projects — and we split the labor the same way we split everything: Ari pulled the reporting, checked the claims against each other, and sorted what was confirmed from what was only claimed. The reading, the grading, and every judgment call in the last sections are mine. She drafts, she double-checks, she argues with me when a claim doesn't hold up. The verdict stays with me.

I'd rather say that out loud than pretend otherwise. The work is mine. So is saying who helped.

Sources: The Hacker News, PoeLLM / Canto Incognito campaign reporting (October 7, 2026, with subsequent disruption update).

Ben's verdict: (blank)
