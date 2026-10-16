# Night Shift Ward 7


**Play:** https://supassk.github.io/Before-They-Wake-/ (works on phone and computer, no install)

**Course:** 273411 Communicative English for Computer and Information Technology: Practical Project

## Target learners
University students with English at **A2–B1** level (CEFR). Thai translations are optional and can be turned off.

## Language goals
- **Reading for detail (main goal):** compare what a patient says with written records (a referral, a nurse chart and a medical history) and find the sentences that contradict each other.
- **Vocabulary:** everyday health words for sleep, mood, worry, energy and the body. Players tap yellow words to see the Thai meaning, and each night ends with a vocabulary check.
- **Grammar in context:** each night has a focus: present simple → frequency words → past simple → *for / since / ago* → giving reasons (*because, so, might, probably*). From Night 3, players build each question from word tiles.
- **Listening (optional):** text-to-speech reads every answer aloud. Listening mode hides the text.

## How to play
You are a trainee doctor at the night-shift nurses' station of a psychiatric hospital. You look into an observation room, check each patient's papers, and decide.
1. A patient comes to your observation window and tells you their problem.
2. Open the **Interview Sheet** and choose questions. The number of questions is limited, and each one uses 10 minutes of the night.
3. Read the documents on your desk: the **Referral** (with an ID photo), the **Nurse Chart** and the **Medical History**.
4. If everything matches, stamp **ADMIT** and choose a diagnosis with the **Field Guide**.
5. If something does not match (the story, a document, or the photo), stamp **FLAG** and tap the **two pieces of evidence** that contradict each other.
6. See every patient before **6:00 AM**. A wrong decision or a patient left waiting costs 1 Trust. If you lose all 4, your shift is over.

## Core loop
**Input** (read the patient's words and the documents) → **Action** (ask questions, compare, then stamp ADMIT or FLAG with evidence) → **Feedback** (Correct / Wrong call, *why* the answer is right, the key evidence, and the signs you missed) → **Reward** (points, Trust, a night report and a vocabulary check). There are 5 nights with 15 patients, and each night is harder than the last: fewer questions, word-tile questions, and more patients to flag (0 → 1 → 1 → 1 → 2).

## AI and tools used
| Tool | What we used it for |
|---|---|
| Claude Code (Anthropic, Claude Opus 5.5) | Wrote the HTML/CSS/JavaScript code, the SVG code that draws the patients, and the Web Audio sound effects. Drafted the patient dialogue, the documents and the Thai translations. Helped us proofread the English. |
| Web Speech API (built into the browser) | Reads English text aloud. |
| *[add any other tools you used]* | |

**Our own work:** the game concept and design decisions (target learners, language goals, the FLAG/evidence mechanic, the shift clock, difficulty across nights, and a sensitive tone for mental health topics), checking every English sentence and Thai translation (see [LANGUAGE_REVIEW.md](LANGUAGE_REVIEW.md)), and playtesting.

## Inspiration
The "check the papers, then let them in or not" mechanic is inspired by *That's Not My Neighbor* (Nacho Sama) and *Papers, Please* (Lucas Pope). We did not use any of their art, characters, logos or text. We changed the idea for language learning:
- The player must **point to the two pieces of evidence** that contradict each other, so they have to read closely.
- Feedback **explains the reason** in English.
- The setting is a hospital, with our own art drawn in code.
- Patients are **never shown as monsters**. "Impostors" are people faking an illness or documents with errors, so the game does not stigmatize mental illness.

*Note:* the conditions in this game are simplified for language practice. It is not a medical tool.

## Team
| Name | Student ID | Role |
|---|---|---|
| | | |
| | | |
| | | |
