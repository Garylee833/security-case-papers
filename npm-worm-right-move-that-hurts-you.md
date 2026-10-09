# The Right Move That Hurts You

*What I took from the Shai-Hulud npm worm and the tensorlake 0.5.144 compromise — written 2026-10-09, from public reporting (OX Security). I keep facts and claims in separate piles below, because that's the only honest way I know to read a story like this.*

---

## What happened, as best I can piece it together

A package called tensorlake, version 0.5.144, went bad on npm. Inside it was something wearing an old name — Shai-Hulud — and it wasn't just a stealer or just a worm. It was both, in the same box: steal what you can, then use what you stole to spread.

Here's how I understand the shape of it. The malware goes after credentials — GitHub tokens are the prize — and it doesn't just use them and leave. It plants a watcher, something called `gh-token-monitor`, whose whole job is to sit there and notice if the token it stole gets revoked. That's the part that matters. Because if it sees the token die, it can trigger the ugly option: wipe the home directory.

Read that again the way I had to. The malware *expects* you to respond. It has a dead man's switch aimed at the exact moment you do the obvious, correct, textbook thing — revoke the stolen credential.

## The timeline, short version

- **The compromise** — tensorlake 0.5.144 is published to npm carrying the infostealer-and-worm payload.
- **Installation does the work** — anyone who pulls that version gets the stealer, the worm logic, and the `gh-token-monitor` persistence.
- **The trap arms itself** — the monitor watches the stolen GitHub token. Revoke it before the machine is isolated, and the wipe can fire.
- **The reporting** — OX Security publishes the markers and the warning: the order of your response decides whether you lose the machine's home directory.
- **The name question** — the original Shai-Hulud operators were arrested, but this sample carries new keys. Somebody is wearing the name. That's a claim about attribution, and I grade it below.

## What I can actually stand behind

**Confirmed — from the primary reporting (OX Security), treated as the source of record for the markers:**
- tensorlake 0.5.144 on npm carried an infostealer plus worm combination, not a single-purpose payload.
- The worm side plants persistence in the form of a `gh-token-monitor` that watches the stolen GitHub token.
- Revoking that token before isolating the host can trigger a destructive payload against the home directory. The trap is real and it is aimed at defenders.
- The response order that avoids it: isolate the machine first, kill the monitor persistence second, *then* rotate everything the stolen token could reach.

**Claimed — possible, plausible, not proven:**
- That this is a copycat. The sample uses new keys and the original operators were arrested, which points that way — but "points that way" is all it is. A name in malware is a label anyone can sew on. I have no independent proof of who is running this round.
- Any specific victim count or spread numbers beyond what the primary report states. Worm math gets exaggerated in every retelling, and I won't repeat a number I can't tie to the source.

## Why the order matters, in plain words

Every incident-response instinct I have says: credential stolen? Revoke it. Now. That's the training. Revoke first, ask questions later.

This worm read the same training. It knows the first thing you'll reach for is the token, so it wired the token to the bomb. The "obvious" move is only obvious because it's predictable — and predictable is what an attacker designs around.

The fix isn't a new tool. It's a sequence. Isolate the machine so the monitor can't phone home or act on what it sees. Kill the monitor so nothing is watching the token anymore. *Then* rotate — the token, and everything that token could touch, because by the time you find a worm like this, you don't get to assume it only took the one thing you caught it holding.

I'll be honest: I don't know if I'd have gotten the order right on instinct alone, before reading this. That's exactly why I wrote it down.

## What I'm taking from it

1. **Sequence is a defense.** In a live incident, *what order* you do things in can be the difference between a cleanup and a wipe. Isolate, kill persistence, then rotate. I want that order written down before I ever need it, not improvised during one.
2. **Assume the attacker read your playbook.** If your first move is the documented best practice, somebody has already built a trap on it. Best practice stays best — but it isn't a surprise anymore, so don't expect it to work like one.
3. **A stolen token is never just one token.** A worm doesn't steal a key to use it once. Rotate everything reachable, and treat "what else could this open" as the real question.
4. **Famous names prove nothing.** Shai-Hulud's originators were arrested, and the name showed up anyway — with new keys. Names get recycled by copycats precisely because a scary name does half the work for them. I grade the name as marketing until evidence says otherwise.
5. **The trap is the tell.** A dead man's switch wired to revocation tells you the operator expected a competent defender, not a careless one. That's a read on who you're dealing with — file it as a lead.

## The other side of it

The strongest counter-reading I can make against my own lesson goes like this: *waiting to revoke is dangerous too.* Every minute a stolen token stays live, the attacker can use it — push code, open doors, steal more. Isolation isn't instant, and on a machine you can't take offline, "isolate first" might leave the token breathing longer than revoking would. A reasonable responder could say the wipe risk is one machine's home directory, weighed against an attacker actively using a live credential against everything it opens. That's not a foolish argument, and where the token reaches production systems, it might even be the right call.

Where I concede: if you cannot isolate — a shared build machine, a box you don't control — the clean sequence isn't available, and revoking hot may genuinely be the lesser loss. My order is written for a machine you can actually put in a box first.

What would change my conclusion: evidence that the wipe doesn't fire on revocation in the wild — say, confirmed incidents where tokens were revoked first and nothing was destroyed. If the switch turns out to be broken or absent in real samples, then revoke-first goes back to being the right instinct and my whole sequence is a precaution against a ghost. Until I see that, the reported marker wins: the switch is there, so I plan around it.

## What I still don't know

- Whether the wipe has actually fired on a real victim, or whether it's a loaded trap nobody has sprung yet. The reporting establishes the mechanism; a confirmed detonation is a different claim.
- Who is running this round. New keys and an old name don't add up to an identity.
- How far 0.5.144 actually spread before it was caught — install counts in early reporting are usually soft.
- Whether the monitor has other triggers I haven't seen described. A dead man's switch rarely travels alone.

---

*One last thing, because it's why I wrote this down at all: the headline is a poisoned npm package, and poisoned packages are getting common enough to feel routine. The part that isn't routine is a piece of malware that planned for my response — not my mistake, my* response. *That changes how I think about incident work. The attacker isn't just in the machine. They're in the checklist. I'd rather learn that from OX Security's report than from my own wiped directory.*

## How this paper was made

I didn't read the reporting and write this in one sitting. I work with Ari — an AI partner I've built alongside my other projects — and we split the labor the same way we split everything: Ari pulled the reporting, checked the claims against each other, and sorted what was confirmed from what was only claimed. The reading, the grading, and every judgment call in the last sections are mine. She drafts, she double-checks, she argues with me when a claim doesn't hold up. The verdict stays with me.

I'd rather say that out loud than pretend otherwise. The work is mine. So is saying who helped.

Sources: OX Security reporting on the Shai-Hulud / tensorlake 0.5.144 compromise (October 2026).

Ben's verdict: (blank)
