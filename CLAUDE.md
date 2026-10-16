# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

"Night Shift Ward 7" is an English-learning game for Thai university students at A2–B1 level. It is a graded group project for course 273411; the brief is summarized in `README.md`. The player is a trainee doctor on a psychiatric ward, in the style of *That's Not My Neighbor*. For each patient, they interview them, read their documents, and then either stamp ADMIT and choose a diagnosis, or stamp FLAG and tap two contradicting pieces of evidence.

The whole game is `index.html`: inline CSS and vanilla ES5 JavaScript, with Google Fonts as the only external dependency. There is no build step or package manager. Open the file in a browser to play. It is published via GitHub Pages from `main`.

`LANGUAGE_REVIEW.md` lists the English text that people must proofread. Language accuracy is the biggest item in the rubric, so add any new or changed player-facing English to that file. The game uses American spelling.

## Architecture (inside the `<script>` block)

**Data tables (top of script):**
- `QUESTIONS`: 12 interview questions. Question ids such as `slp`, `mood` and `wor` are keys used everywhere else.
- `NORMAL`: the default "negative finding" answer for each question.
- `CONDS`: 9 conditions, each with `signs` (key question ids) and `a[qid] = [patientText, noteText]`.
- `FAKE`: Field Guide text for patients who fake an illness.
- `NIGHTS`: 5 nights, each with a question `budget`, a `puzzle` flag, and a grammar focus.
- `CASES`: 15 patients. Each case has `ref` (Referral form; overrides of `name`/`age`/`job`/`look` plant a mismatch), `med` (Medical History lines), `chart` (Nurse Chart lines), and optional `mix`/`over` answer overrides. A case with `flag` must be FLAGGED. `flag.pairs` lists the accepted evidence pairs; the first pair is the one shown as key evidence.

**Hard content rule:** a case without `flag` must have **no** contradictions across its chief complaint, every possible answer from `answer()`, `ref`, `chart`, `med` and its portrait. The game rule is "admit only if everything matches". So when you edit `NORMAL` or `CONDS` answers, re-check every non-flag case that uses them.

**Evidence ids:** `face`, `ref.photo`, `ref.name|age|job|by|why`, `chart.N`, `med.N`, `say.chief`, `say.<qid>`. `evText()` turns an id into the feedback text. In evidence mode, `ln()`, `evAttr()` and `evCls()` make any line selectable.

**Answer resolution:** `answer(c, qid)` checks `over`, then `mix`, then the case's own condition, then `NORMAL`.

**Vocab markup:** `[english|ไทย]` in any text. `vocab()` renders it as a tappable word, `collect()` feeds the vocabulary quiz, and `plain()` strips it.

**Case screen layout:** `vCase()` renders one 16:9 `.stage` scene: a night-shift nurses' station. The mechanic is inspired by *That's Not My Neighbor*, but the visuals are deliberately hospital-themed so the game does not copy its look. Keep it that way. The observation window (`.mon`) in the middle shows the patient and the latest line (`.subt`). The tiled wall holds a round clock, the Field Guide poster, the "Call senior doctor" FLAG panel, the shift-rota whiteboard, the Interview Sheet clipboard and the Medical History binder. The desk holds the Referral, Nurse Chart, Transcript, ADMIT stamp and Hint. Objects are absolutely positioned in `%` of the stage, and every size uses `cqw` (the stage is a size container). Never use `%` padding on stage objects, because it resolves against the stage width. Document pop-ups use `docHtml()`.

**State and rendering:**
- There is one global state object, `S`. `render()` rebuilds `#app` from a `v*()` view chosen by `S.screen`.
- Overlays are chosen by `S.sheet`: `doc` (with `S.cs.doc` = `ref`/`chart`/`med`/`ask`/`guide`), `dx`, `puz`, `help`, `result` or `shiftEnd`.
- All input goes through one delegated click handler keyed on `data-act`.
- `SND` maps actions to sounds made by `AU` (Web Audio, no audio files).

**Shift clock:** `S.clock` counts minutes after 23:00, and the shift ends at `SHIFT` (06:00). A `setInterval` adds 1 minute every `TICK_MS`. It does not run in Relaxed mode or while the help, result or shift-end sheet is open. Each question adds `Q_COST`. When the clock reaches 06:00, `endShift()` takes 1 Trust for each unseen patient.

**Scoring (`resolve`):**
- Correct ADMIT: `max(30, 100 + 10×questionsLeft − hintCost)`.
- Correct FLAG: the same formula with base 120, halved if the chosen evidence is not one of `flag.pairs`.
- Any wrong decision costs 1 Trust.

## Testing

There is no test suite in the repo. To check changes headlessly, extract the `<script>` body and run a Node script with a stubbed `document`/`window` that calls the click handler with fake `data-act` targets. For visuals, drive headless Chrome over CDP (Node has a built-in `WebSocket`) and take screenshots at 1280px and 390px wide. Check every FLAG case's evidence ids with `evText()`.
