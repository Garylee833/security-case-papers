# Ben Lee — Security Engineering (Entry-Level)

*One page. Everything below is something I built, run, or wrote — and can walk you through.*

---

## Who I am

Entry-level security engineering candidate working both sides of the line — offensive and defensive — toward purple-team work. I learn by building real systems and grading the results honestly: what fired, what missed, what I can't prove yet.

**Certifications:** Google Cybersecurity Professional Certificate · TryHackMe Cybersecurity Engineering · Cisco Cybersecurity Fundamentals. Security+ in progress (Professor Messer's SY0-701 series).

## The working kit

**Multi-service honeypot (Python, running daily)** — A 14-service honeypot (SSH, HTTP, SMTP, VNC, Elasticsearch, Docker, Postgres, MSSQL, MongoDB, RDP and more) with a fake interactive shell, per-session tracking, payload URLs logged but never fetched, and a per-service flood cap. It runs under daily monitoring with a self-resurrection guard; I review its logs as real-traffic detection practice.

**mysiem — a mini-SIEM (Python)** — A working alert loop and plumbing with log normalization, detection rules, YAML configuration, and an Active Directory pack. It flags and sorts; a human closes the case. Built as the vehicle for detection-engineering practice against my own honeypot's logs.

**Port scanner (Python)** — TCP connect scanning with banner grabbing and service identification, built with a scope guard: loopback allowed, private ranges need an explicit flag, public targets refused outright. Safety first, by construction, not by promise.

**Wardix** — A security-flavored Linux OS under development. Not yet released — I'd rather show it when it's done than describe it early.

**Drill range** — A seeded, deterministic purple-team simulation range (log hunting, network scanning, web attacks, incident response) with integrity-verified packages and sealed grading keys, grading patient and messy adversary behaviors separately.

## The paper shelf

Case papers I write from current threat reporting — facts and claims graded separately, my own takeaways, and the strongest counter-argument I can make against each one:

- **The Patch That Was Handed Over and Never Applied** — the FBIjobs.gov breach: a vendor patch, issued and never applied.
- **The Right Move That Hurts You** — the Shai-Hulud npm worm, where revoking a stolen token first can trigger a wipe.
- **Hunting When No Alert Fires** — the Corelight/Intel 471 Volt Typhoon exercise: blind hunting on linked telemetry.
- **Your Server Works for Somebody Else Now** — PoeLLM: 3,400 exposed AI servers mined and turned into scanners.

## Skills

Python security automation · Linux administration and hardening · Detection writing (Sigma / YARA, with countermeasure and variance notes) · Log analysis and threat hunting · Threat-intel vetting (source grading, indicators handled as fingerprints only — no live samples, ever) · Incident-response sequencing · Technical writing from primary reporting.

## How I work

Pre-test before anything goes live. A fix isn't done until its regression test fails on the old code and passes on the new. Silence from a sensor is a critical finding, never an all-clear. The verdict stays with the human.

I build with an AI partner named Ari, and I say so up front: she helps with research, drafting, and double-checking. Every judgment call, every line of shipped code, and every verdict is mine, and I can whiteboard any of it.

*Happy to walk through any project above in depth — how it works, where it's weak, and what I'd build next.*
