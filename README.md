# Security Case Papers

Case papers from public reporting, written as I learn. Every paper keeps facts and claims in separate piles, argues both sides — including the strongest case against my own lesson — and says out loud what I don't know yet.

I work with Ari, an AI partner I've built alongside my other projects. She pulls the reporting, checks outlets against each other, and argues with my drafts. The grading and the verdicts stay mine. I'd rather say that up front than pretend otherwise.

## The papers

- [Agents Holding Real Credentials](agent-credentials-controls.md) — the first one: controls that actually work when an AI agent holds real credentials. Where the shelf started.
- [The Patch That Was Handed Over and Never Applied](shinyhunters-fbijobs-patch-never-applied.md) — the FBIjobs.gov breach: a vendor was handed a patch and never applied it, and the FBI's whole workforce paid for the gap. Lesson: a fix isn't done until somebody proves it's on.
- [The Right Move That Hurts You](npm-worm-right-move-that-hurts-you.md) — the Shai-Hulud npm worm (tensorlake 0.5.144), where revoking the stolen token first can trigger a wipe of your home directory. Lesson: response order matters — isolate, kill the persistence, then rotate.
- [Hunting When No Alert Fires](volt-typhoon-hunting-no-alert.md) — Volt Typhoon hunted blind across four platforms on linked telemetry alone. Lesson: when nothing alerts, connected evidence is all you have. Vendor-sponsored research, and the paper says so.
- [Your Server Works for Somebody Else Now](poellm-your-server-works-for-somebody-else.md) — PoeLLM: 3,400+ exposed AI and LLM servers quietly mining for somebody else, then used as scanners. Lesson: exposure isn't the scandal; unmanaged exposure is.
- [Binding Laws from Day One](binding-laws-from-day-one.md) — a builder's account of constraining AI agents before they act: laws baked in from day one, the gate that decides, four case studies including the mistake we caught, and the objections answered. Lesson: stop bolting the laws on after.

## For recruiters

[Recruiter sheet](recruiter-sheet.md) — one page: the working kit, the certs, and what each project demonstrates.

## Standing rules for everything here

- Confirmed and claimed never share a pile; every claim travels with its source.
- No live malware, ever. Fingerprints and documentation only.
- If a paper's wrong, it gets corrected in the open, in the same file.

*Verdicts are mine and get filled in as the stories finish. A blank verdict means I'm still watching, not that I forgot.*
