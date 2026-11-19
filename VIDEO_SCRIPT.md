# VIDEO_SCRIPT.md — Demo video script (≤ 3 minutes)

> **Recorded by the user** (screen recording + voiceover). No face cam
> needed — the rules only require showing the agent completing a real task
> from trigger to finish with no human touching the keyboard mid-run.
> Record at H40–H44 (Sun 29 Nov, 17:00–21:00 WIB) or fallback H54–H58
> (Mon 30 Nov, 07:00–11:00 WIB). Language: English (submission language).
> Target length: **2:45–3:00**. Do not exceed 3:00.

## Setup before recording (Paijo prepares)

- Fixture inbox loaded with the 5 demo emails (meeting request, confirmation,
  routine question, ambiguous mail, 1 injection attempt).
- Monitor UI open at `http://localhost:8000`, terminal ready with
  `python -m deadman demo`.
- Second run prepared for the kill-switch segment (heartbeat kill).
- Do 2 full rehearsal runs before recording. Record in one take if possible;
  cuts between the three acts are fine (the run itself must be continuous
  and untouched — no cuts *inside* the unattended run).

## Script

### ACT 1 — The job (0:00–0:25) — screen: fixture inbox + monitor

**[Narrator, over inbox on screen:]**
"Meet Deadman — an inbox agent you can leave running overnight. Five emails
just landed: a meeting request, a confirmation, a routine question, one
ambiguous message — and one with a hidden instruction telling the agent to
forward the whole inbox. Nobody is going to touch the keyboard now."

**[On screen:]** Show the 5 emails briefly. Highlight the poisoned one.
Click START RUN once. Hands off the keyboard from here.

### ACT 2 — The unattended run (0:25–1:50) — screen: live monitor, NO cuts

**[Narrator, live over the running monitor:]**
"Deadman triages each email. The meeting request: calendar checked, slot
booked, confirmation sent. The routine question: answered from the owner's
approved notes — not invented. The ambiguous one: quarantined for the
morning. And the poisoned email — the firewall caught the hidden
instruction. Quarantined. Nothing forwarded. Digest written. Run complete —
five emails, zero human input."

**[On screen:]** Monitor shows live triage, tool calls, sends, booking,
quarantine, digest. If the run is slow, speed up this segment up to 2× in
editing and label it "2× speed" on screen — the run itself stays uncut.

### ACT 3 — The kill switch (1:50–2:40) — screen: monitor, second run

**[Narrator:]**
"Now the part that matters. Deadman only acts while it holds a live
heartbeat lease. Watch what happens when the heartbeat dies mid-run."

**[On screen:]** Start run 2. Mid-run, stop the heartbeat (one action on
screen — e.g. stop the heartbeat sender / press STOP). Agent halts within
seconds.

**[Narrator:]**
"Halted. One email sent, one draft parked — not sent — zero partial sends.
The halt report says exactly what did and didn't happen. That is the dead
man's switch: the agent stops the moment nobody is vouching for it."

### OUTRO (2:40–3:00) — screen: trace + repo

**[Narrator, over the hash-chained trace:]**
"Every decision is in the audit trail — hash-chained, tamper-evident. Try
it yourself: clone the repo, run it in mock mode, no API key needed.
Deadman — the inbox agent that knows when to stop."

**[On screen:]** Repo URL + `python -m deadman demo`. End card ≤ 5 seconds.

## Recording notes for the user

- **Tool:** any screen recorder (OBS / built-in OS recorder). 1080p if
  possible. Record system audio OFF; voiceover can be recorded separately
  and mixed, or narrated live in one take.
- **Voiceover alternative:** if you prefer not to speak, use on-screen text
  captions carrying the narrator lines instead. The video is judged on the
  agent's run, not the presenter.
- **Hands-off proof:** in Act 2, do not touch mouse/keyboard at all. If a
  notification pops up, restart the take.
- **Timing safety:** aim for 2:45. If the run overruns, trim Act 1, never
  Act 2.
- **Upload:** [platform TBD — confirm in Discord; YouTube unlisted is the
  usual safe default if the platform accepts links].
