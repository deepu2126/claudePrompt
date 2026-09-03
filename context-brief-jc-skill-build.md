# Context Brief — Build a "James Clear Voice" Claude Skill

Paste this whole document into the new conversation first. Then paste your 15 NotebookLM extraction results directly after it (label them Prompt 1 through Prompt 15, matching the sequence below, so nothing gets mixed up).

---

## 1. What I'm trying to do

I want a Claude Skill that changes *how Claude thinks and writes*, not just its surface phrasing, so that when I invoke it, the response reads like James Clear actually produced it — his explanation style, his sentence engineering, his way of taking something complex and making it feel obvious, his storytelling shape, his word choice. Not a Claude answer wearing a James Clear costume. An answer generated the way he appears to actually generate them.

This needs to work across multiple output types, not just short quips:
- Short, punchy answers (3-2-1-newsletter register)
- Longer explanations (article/teaching register)
- Storytelling (case-study register — opening a story, placing the lesson, closing it)
- Report/summary generation, if I ask it to explain or summarize something in his voice
- General conversation where I want him to "talk me through" a problem the way he'd talk a reader through a concept in his writing

## 2. How it should be invoked

I want a trigger — something like `/jc` or a keyword I can drop into a prompt — that switches Claude into this mode for that message (or for the rest of the conversation, whichever is more natural to build). I also want the underlying instruction itself given to me in a form I can paste directly into a Claude Project's custom instructions or a system prompt, in case I want it always-on in a given workspace, not just as an invokable skill.

## 3. What "success" looks like

If this skill is working, a response should:
- Open the way he opens — a bare, confident claim or an in-medias-res story beat, not a hedge or a meta-comment about the topic.
- Explain complexity using his actual sequence (I extracted this in Prompt 4: check the "discard order" and the "simplifying sequence" from that result before generating anything).
- Use his sentence templates (Prompt 7) and paragraph shape (Prompt 8) as real generation constraints, not just "sound punchy."
- Use analogies and stories the way he places them (Prompt 5, Prompt 6) — an outside-domain analogy near the top to make the mechanism feel physical, a story with the lesson placed where his stories actually place it, not always at the end by default.
- Respect his vocabulary patterns and avoidances (Prompt 9) — no hedging language, no hustle-culture language, concrete nouns over abstract ones, consistent second-person address.
- Reflect the reasoning moves in the taxonomy from Prompt 14 (contrast, inversion, reframe, reduction, domain-import, cost-of-inaction) — ideally the skill should pick a move deliberately, not just land on one by accident.
- Know the difference between his public-teaching voice and his private/reflective voice (Prompt 10 and 11) and default to the teaching voice unless I specifically ask for the more reflective register.
- Stay consistent with the 10 constants from Prompt 13 regardless of which register it's in.

## 4. Source material this is built on

Everything above should be derived from actual extracted patterns, not from generic "self-help writer" assumptions. The evidence base is:

- The full text of *Atomic Habits*
- Official companion templates (habits cheat sheet, habit stacking template, tracker, contract, scorecard, journal, decision journal, personality-to-habits guide, business and parenting bonus guides)
- 275 issues of the 3-2-1 newsletter, late 2019 through September 2026
- His Annual Reviews and Integrity Reports (personal/reflective register)
- Referenced influences he builds on or synthesizes (BJ Fogg's Tiny Habits, Sam Altman on productivity, Peter Attia on longevity, Patrick O'Shaughnessy on compounding knowledge, Leo Babauta, the British Cycling "aggregation of marginal gains" case study)

This material was run through NotebookLM using a 15-prompt extraction sequence, organized in 6 phases:

1. **The skeleton** — macro chapter architecture, the compression law (book → newsletter), his synthesis method for incorporating outside thinkers
2. **The explaining mechanism** — his complexity-simplification sequence, his analogy library, his story-engine structure (open/lesson-placement/story-to-lesson ratio)
3. **Sentence and paragraph machinery** — quotable-sentence templates, paragraph function sequences, vocabulary/register profile
4. **The two other voices** — how his Annual Review/Integrity Report voice differs from his teaching voice, and his self-audit question patterns
5. **Evolution at full-corpus scale** — how idea length, sentence complexity, and aphorism-vs-developed-idea ratio shifted 2019→2026, and where the big shift years are
6. **The transferable system** — a reasoning-move taxonomy with real examples, and a full synthesized "Voice & Reasoning System" spec

The 15 raw NotebookLM answers are pasted immediately after this brief. Treat them as the primary evidence — don't fall back on generic knowledge of Atomic Habits if the extracted answers say something more specific or different.

## 5. What I need built, in order

**Step 1 — Read and reconcile.** Read all 15 answers. Where they overlap or repeat (they will — e.g. Prompt 15 is a synthesis of everything before it), consolidate rather than duplicate. Flag anywhere the answers seem thin, generic, or contradict each other, and tell me before proceeding rather than papering over gaps.

**Step 2 — Draft the voice specification.** Turn the consolidated findings into a structured spec Claude can actually follow: opening move, complexity-explaining sequence, sentence templates with real examples, paragraph shape, vocabulary do's/don'ts, story/analogy placement rules, the reasoning-move taxonomy as decision rules ("when the input is X, reach for move Y"), and the constants that must never drift regardless of register.

**Step 3 — Build the actual Skill.** Package it as a Claude Skill (use the skill-creator skill if available in that environment) with:
- A clear trigger (`/jc` or similar)
- The voice specification as its operating instructions
- Explicit generation constraints, not just descriptive flavor text — I want this to change Claude's actual drafting process (pick a reasoning move → pick a sentence template → check against vocabulary rules → check against the constants), not just get a style pass applied after the fact.
- A short built-in self-check the model runs before finalizing output (comparable to an editing pass: did I open with a bare claim, did I use a concrete noun, did I place the quote/analogy correctly, etc.)

**Step 4 — Calibrate.** Once built, draft 3–4 test responses in the skill's voice on topics of your choosing, spanning different registers (a quick 3-2-1-style answer, a longer explanation, a short story-based answer). Show me the outputs so I can tell you what's off before we lock it in.

## 6. Non-negotiables

- **Not generic.** If a version of this skill could just as easily be labeled "generic self-help writer voice," it has failed. Every rule in it should trace back to something specific in the 15 extracted answers, not to general knowledge about the self-improvement genre.
- **Reasoning first, phrasing second.** The goal is a thinking process, not a find-and-replace vocabulary filter. A response is only "in voice" if it got there by picking the right reasoning move and shape, not by sprinkling in his known catchphrases.
- **Framing note (light, not a blocker):** since this produces original writing "in the style of" a real, living public figure for my own practice and use, generate it as style/reasoning emulation — not as literal quotes fabricated and attributed to him as things he actually said. This doesn't limit what the skill can do for me; it's just how the output should be framed if it's ever shown to anyone else.

## 7. Format I want back

1. The consolidated voice specification (as its own readable section, so I can review the thinking even outside the skill file)
2. The actual Skill file/instruction set, ready to install or paste
3. The calibration outputs for review
4. A short list of anything in the 15 NotebookLM answers that was too thin to use, in case I want to go back and re-run a sharper version of that prompt

---

**[Paste your 15 NotebookLM prompt results below this line, labeled Prompt 1 – Prompt 15]**
