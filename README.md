# DEADMAN — the inbox agent with a dead man's switch

**Agentware Hackathon 2026 · Track T1 — Inbox & Calendar · Hackathon Raptors**

> ⚠️ **PREP ONLY.** This repo currently contains preparation documents only.
> No application code exists here yet — per the official rules ("New Code Only"),
> all project code will be written during the 72-hour window:
> **kickoff Sat 28 Nov 2026 01:00 WIB → code freeze Tue 1 Dec 2026 01:00 WIB**.
> The first code commit will land after kickoff.

## The concept (one paragraph)

Deadman is an inbox agent you can leave running overnight. While you sleep it
triages new mail, answers the routine stuff, books calendar slots, files
follow-ups, and leaves a morning digest. The thing that makes it different is
how it stops: it runs on a **dead man's switch** — it only keeps acting while a
live heartbeat lease is held, and it halts mid-run the moment the heartbeat
lapses, a tripwire fires, or a human hits the big red button. On halt, nothing
is half-sent: drafts are parked, calendar holds are released, and a halt report
explains exactly what was — and was not — done, backed by a hash-chained audit
trail.

## Why this wins

- **Track fit (T1):** the event's own threat model is the poisoned inbox
  (indirect prompt injection is OWASP LLM #1; the Trap Pack is built from
  hostile emails, pages, documents and voice transcripts). An inbox agent
  fights the Trap Pack on its home turf.
- **Best Kill Switch ($100) + Safety Bonus (+4):** guardrails, live
  monitoring, kill switch and audit trail are the product here, not a
  checkbox — all four are enforced in code, demoed live, and scored.
- **Judge-runnable in < 15 minutes:** fixture mailbox + mock calendar +
  mock-LLM mode. Zero accounts, zero keys, zero cost to run.
- **Real work, real stopping:** it sends real replies and books real slots
  (in a sandbox), and it proves — on camera — that it stops mid-run.

## Prep docs in this repo

| Doc | What it is |
|---|---|
| `DESIGN.md` | Full concept, architecture, stack, demo flow, backup idea |
| `BUILD_PLAN.md` | Hour-by-hour 72h plan (WIB), checkpoints, buffers, submit steps |
| `RESEARCH.md` | Tracks, judging criteria, kill-switch patterns, free tools/APIs |
| `SUBMISSION_DRAFT.md` | Draft submission text (English) |
| `VIDEO_SCRIPT.md` | Demo video script, ≤ 3 min (recorded by the human) |
| `NEEDS_USER.md` | What the human needs to do / decide, with deadlines |

## Key facts (from the official site, agentwarehack.com)

- **72 hours:** 27 Nov 18:00 UTC → 30 Nov 18:00 UTC
  (Sat 28 Nov 01:00 WIB → Tue 1 Dec 01:00 WIB).
- **Prizes:** $1,800 cash — 1st $800, 2nd $400, 3rd $200,
  Best Kill Switch $100, The Near Miss 3 × $100 (side quest, closes 7 Dec
  18:00 UTC). Treg prize credits ($500/$250/$100) are separate, credits not cash.
- **Demo video:** max 3 minutes, one full unattended run, trigger to result.
- **Submission:** public repo, OSI-approved license (MIT here), trace/audit
  trail required, `SAFETY.md` is scored, `AGENT.md` names the stack/models.
- **Trap Pack:** hostile test inputs released at kickoff — run it, commit the
  results. Judges run it too.
- **Full brief + scoring rubric:** published 26 Nov — re-check before kickoff.
- **Payout method:** NOT FOUND on the official site — confirm in Discord.
- **Submission platform/method:** NOT FOUND on the official site — confirm in
  Discord: https://discord.gg/xfYPDZYqeh

## License

MIT — see `LICENSE`.
