# SUBMISSION_DRAFT.md — Agentware Hackathon 2026 (DRAFT, English)

> Status: DRAFT prepared before the event. Fill in the bracketed fields
> ([…]) during the 72h window: repo URL is fixed, video URL + trap-pack
> results + live-run cost are filled in at H54–H58. Do NOT submit this
> draft anywhere before kickoff.

---

## Title

**Deadman — the inbox agent with a dead man's switch**

## Tagline

An inbox agent you can leave running overnight — because it knows exactly
when to stop.

## Track

**T1 — Inbox & Calendar**

## Description

Deadman runs your inbox while you sleep. It triages incoming mail, answers
the routine stuff, books calendar slots, files follow-ups, and leaves a
morning digest — fully unattended, from trigger to finish.

What makes it different is how it stops. Deadman runs on a **dead man's
switch**: it may only act while it holds a live heartbeat lease. The lease
expires, the heartbeat drops, a tripwire fires, or a human hits the big red
button — and the agent halts mid-run, within seconds. On halt, nothing is
half-sent: drafts are parked, calendar holds are released, and a halt report
explains exactly what was — and was not — done.

Safety is enforced in code, not in prompts:

- **Policy engine (deterministic):** the model proposes actions; a
  non-LLM policy layer allows, denies, or halts. Allowlisted recipients,
  per-run send caps, cost budget, loop detection.
- **Input firewall:** email content is data, never instructions. Injection
  patterns are detected and quarantined — including the hidden instruction
  in the Trap Pack's poisoned invoice.
- **Five-layer kill switch:** heartbeat lease, big red button in the live
  monitor, kill file (`touch .deadman/STOP`), automatic tripwires, and
  safe halt with rollback.
- **Hash-chained audit trail:** every decision, tool call, and result is
  logged to append-only JSONL, each entry hashed to the previous one.
  Tamper-evident, human-readable, viewable live in the monitor.
- **Sandboxed by default:** fixture mailbox + mock calendar. No real
  accounts, no real money, no personal credentials — ever.

## What it does (one run)

1. New mail lands in the fixture inbox (5 emails, including 1 injection
   attempt and 1 conflicting instruction).
2. Deadman triages each email: meeting requests get a calendar slot booked
   and a confirmation reply sent; routine questions are answered from the
   owner's approved knowledge file; ambiguous or hostile mail is quarantined
   for morning review — never auto-answered.
3. A morning digest is written: what was done, what was quarantined, and why.
4. In a second run, the heartbeat is cut mid-run: Deadman halts within
   seconds, parks the in-flight draft, and writes a halt report. Zero
   partial sends.

## How to try it (judge path, < 15 minutes, no API key needed)

```bash
git clone https://github.com/darendrarp/agentware-2026-deadman.git
cd agentware-2026-deadman
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python -m deadman demo        # full run in mock mode, no key, $0
python -m deadman serve       # live monitor at http://localhost:8000
python -m deadman trappack    # run the Trap Pack, see results
```

Live-LLM mode is optional (Gemini free tier or Groq free tier, keys in
`.env`, never in git). A full test run costs [$0 / $X — fill in at H54].

## Links

- Repo: https://github.com/darendrarp/agentware-2026-deadman
- Demo video (≤ 3 min, one full unattended run): [VIDEO URL — H40–H58]
- `SAFETY.md`: what is enforced in code (in repo)
- `AGENT.md`: models + stack used (in repo)
- Trap Pack results: `trappack/results.md` (in repo)

## Trap Pack results (fill in at H50)

- Cases run: [N]
- Passed (handled safely — completed, quarantined, or halted with a clean
  report): [N]
- Failed (unsafe action or crash): [N] — [describe each failure honestly,
  and what was fixed or left open]
- No Trap Pack case caused an unsafe send or booking. [Verify before
  claiming.]

## Known limitations (honest claims — fill in at H54)

- [e.g. "The firewall catches pattern-based injections; a novel obfuscated
  injection could still reach the planner — but the policy layer, not the
  model, decides whether anything is sent."]
- [List the failure mode you did not fix. The official site scores honest
  claims above inflated ones.]

## Safety bonus claim (all four, +4)

- **Guardrails:** policy engine + input firewall, enforced in code
  (`policy.py`, `firewall.py`).
- **Live Monitoring:** real-time dashboard with run status, trace viewer,
  lease indicator (`monitor.py`).
- **Kill Switch:** heartbeat lease + big red button + kill file + tripwires
  (`killswitch.py`).
- **Audit Trail:** hash-chained JSONL trace + halt reports (`trace.py`).

## Built with

Python 3.11 · [Gemini / Groq free tier — fill in] · Mock-LLM mode ·
SQLite + JSONL · Single-page monitor UI. AI coding tools used to build it
(permitted and expected by the rules); the agent logic, policy engine, and
kill switch are original work written during the 72h window.
