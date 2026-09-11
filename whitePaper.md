Claude White paper skill

Instructions for Building the "Paper Ownership Protocol" Skill
Context for Claude
I am giving you the complete design conversation for a Claude Skill meant to help me deeply "own" software/ML white papers — not just summarize them. This design went through five rounds: (1) an initial 15-phase protocol, (2) 11 rigor additions, (3) 12 efficiency/triage additions from a "how would a top 0.1% PhD student approach this" angle, (4) 11 bias/fallacy countermeasures, and (5) 9 transferable-philosophy/pattern-library additions. That is 43 distinct additions on top of the original protocol — every one of them was validated as correct and worth including. Nothing was rejected.
Your job is to build a working Claude Skill (SKILL.md + supporting files) that operationalizes ALL of this material — not a compressed summary of it.
Why this instruction exists
Left alone, an LLM asked to "turn this into a skill" will default to producing a short, clean, readable SKILL.md — because that reads better in isolation. That is the wrong optimization here. A shorter file that drops half the mechanisms is a worse skill even though it looks more polished, because the value of this system is specifically in the parts that are easy to compress away: the tripwire checks, the bias countermeasures, the triage logic, the pattern-library habit. Losing any of those turns this back into a generic "explain this paper" prompt, which is exactly what the original research concluded was insufficient.
Do not summarize the source material. Distill it into structure, not into fewer ideas. Every one of the 43 points plus the original 15-phase protocol must be traceable to a specific, usable instruction somewhere in the final skill. If you genuinely believe two points are redundant enough to merge, say so explicitly and show your reasoning — do not silently drop or merge without flagging it.
What "no compression loss" actually means here
* It's fine — good, even — to reorganize. The five rounds of input weren't designed as a single coherent structure; they were additive layers. You should restructure them into a coherent skill architecture. Reorganizing ≠ compressing.
* It's fine to deduplicate exact repeats (e.g., the analogy-breaking check appears in both the original protocol and the bias-fallacy round — merge those into one enforced instruction, but note that you did it).
* It's NOT fine to reduce a specific, concrete instruction ("ask me to predict the mechanism before reading the method, then explicitly locate what contradicted the prediction") down to a vague generic one ("encourage active engagement with the material"). If you notice yourself doing this, stop and keep the specific version.
* Test: if I compare the final skill against this source document, I should be able to point to every one of the 43 numbered points and the 15 original phases and find its home in the skill. If I can't, that's a bug in the build, not an acceptable simplification.
Structural approach (use Claude's Skill format properly — this is not a job for one file)
A skill is not required to be a single short SKILL.md. Use progressive disclosure: SKILL.md should be the orchestrator — routing logic, phase list, and pointers — while the dense material lives in separate reference files that get loaded only when that phase is active. This is the correct way to preserve all 43+ points without producing an unusably long single file:
* SKILL.md — triage logic (angle 2, point 1), overall phase flow, when to load which reference file, exit/certification criteria (angle 1, point 11), and the core rule stated in the original master prompt.
* reference/deep-protocol.md — the full 15-phase original protocol, verbatim in substance (map, causal reconstruction, first-principles, decomposition, multi-resolution explanation, worked example, equations, evidence audit, attack, alternative-universe, transfer, reconstruct-from-memory, Socratic test, mental model card).
* reference/rigor-additions.md — the 11 rigor points (prior-knowledge activation, implementation/code step, visual generation, spaced retention plan, lineage/hindsight positioning, triage/cost calibration, confidence-calibration before verification, comparative multi-paper mode, re-grounding/hallucination check, adaptive reader-level, exit criteria).
* reference/efficiency-triage.md — the 12 PhD-efficiency points (triage before investing, purpose-first reading, figures-before-narrative, predict-before-read, borrowing expert critique, code/repo verification, author talks, citation-graph lineage, two-speed depth model, time-boxing, single load-bearing claim focus, cumulative/linked notes).
* reference/epistemic-tripwires.md — the 11 bias/fallacy countermeasures, each written as a triggerable check tied to a specific phase, not a standalone lecture on cognitive bias. E.g., confirmation bias check fires right after the predict-before-reading step; hindsight bias check fires before first-principles reconstruction; illusion-of-explanatory-depth check fires before declaring ownership complete; sunk-cost check fires between the adversarial phase and the final verdict.
* reference/pattern-library.md — the 9 transferable-philosophy points (trade-off axes, named recurring mechanisms, CS aphorisms, systems/feedback lens, evolutionary/selection lens, information-theoretic lens, game-theoretic/incentive lens, Unix/composability lens, mathematical reduction lens) PLUS instructions for how the skill reads from and writes to a persistent, growing pattern-library file across sessions/papers — this is the cross-paper compounding asset, distinct from any single paper's model card.
* templates/model-card.md — the final deliverable template from the original protocol (Problem/Bottleneck/Insight/Mechanism/Why it works/Evidence/Assumptions/Failure modes/Trade-offs/Alternatives/Transferable principle/One-sentence memory), extended with a link field to relevant pattern-library entries and lineage/citation notes.
* templates/paper-triage-card.md — the lightweight output for papers that don't earn the full loop (angle 2, point 9's "shallow layer").
Specific build requirements
1. State management: papers and reference material can exceed context, and sessions get interrupted mid-loop. Design a lightweight, explicit progress state (e.g., a running progress.md per paper noting which phase is active and what's been established so far) so a session can resume cleanly instead of restarting the whole loop. Say explicitly how resumption works.
2. Make the tripwires actually trigger, not just exist as a list. For each of the 11 epistemic checks, specify the exact phase-transition point where it fires, and what question the skill asks me at that moment. A bias checklist nobody consults is decorative, not functional.
3. Two operating modes, explicitly switchable: (a) full 15-phase + all additions, for papers that pass triage as load-bearing; (b) fast triage-only mode producing just a triage card. Tell me clearly, at the start of any paper, which mode is active and why, and let me override it.
4. Preserve the loop, not just the phases. The original design was explicit that this is a loop (AI builds model → explains → I reconstruct → AI detects gaps → I repair → AI attacks → I defend → AI gives novel scenario → I transfer → certified), not a one-shot output. The skill's control flow must reflect turn-taking with me at the recall, attack-defense, and transfer steps — it should not just generate one long document and stop.
5. Do not invent content the source material didn't specify. Where the source said "say explicitly when something is uncertain" or "do not invent missing architecture," that epistemic humility rule applies to your own skill-building process too — if you're unsure how to operationalize a specific point, flag it as a design question rather than quietly guessing.
After building
Once the skill is built, do not just hand it to me — walk through how each of the 43 points plus 15 phases maps to a specific place in the file structure, as a checklist, so I can verify nothing was lost before we test it on a real paper.

Source material follows below (unedited, in full) — the complete five-round
design conversation, including the original externally-researched analysis of existing paper-reading skills, the 15-phase master protocol, and all 43 numbered additions across the four angles (rigor, PhD-efficiency, epistemic bias/fallacy, and transferable pattern-library philosophy).
Yes. I researched this specifically as a **skill-design problem**, rather than simply giving you a generic “summarize this paper” prompt.

 The important finding is: **there are already several good paper-reading skills, but none of the ones I found quite matches the level of internalization you are asking for.** The best approach is to combine their strongest mechanisms and add a much stronger **mental-model ownership loop**.

 ## What already exists

 I found several relevant approaches.

 ### 1\. `paper-reading` — strong on mechanism + evidence

 One existing skill explicitly reconstructs:

 > problem → limitation of prior approaches → design action → change in information flow/objective → evidence → conclusion

 It also forces separation between **what the authors claim, what the paper demonstrates, what is inferred, and what remains uncertain**. It recommends explaining every module as:

 > purpose → input → operation → output → connection → expected benefit → evidence

 That's excellent for technical software papers.  GitHub

 Another implementation of the same general idea emphasizes mechanism reconstruction, evidence quality, reproducibility, and transfer value rather than merely summarizing sections.  GitHub

 ### 2\. Teaching-first paper reading

 Another skill goes further toward what you're asking: it treats the paper like a building.

 First understand the whole structure, then identify the load-bearing components, then teach the mechanism. It uses:

 - three-pass reading
- intuition before technical detail
- an experiment/evidence ledger
- visual explanations
- completeness auditing

  GitHub  That's much closer to your goal.

 ### 3\. Active/hypothesis-driven reading

 There's also an interesting “ask me paper” skill. Instead of allowing the reader to passively consume an AI-generated explanation, it makes the reader **commit to interpretations**, then tests them with questions.

 That matters because recognizing an explanation is very different from being able to reconstruct it yourself.  GitHub

 And research on active paper reading similarly recommends asking questions, predicting what should happen, comparing your prediction with the authors' result, and using that mismatch to deepen understanding.  OUP Academic+1

 ### 4\. Technical-paper reading

 A classic computer-science approach recommends multi-pass reading, writing your own interpretations, filling in omitted algebra/details, constructing examples and counterexamples, connecting the paper to other approaches, and challenging the authors' assumptions.  Department of Computer Science

---

 # But there is a missing layer

 This is the key insight.

 Most paper-reading systems optimize for:

 **“Can I understand and evaluate this paper?”**

 You are asking for something stronger:

 **“Can I mentally possess the mechanism well enough that I could reconstruct it, teach it, attack it, modify it, and recognize the same idea somewhere else?”**

 Those are different goals.

 I would therefore design your prompt around **five levels of ownership**:

```
LEVEL 1 — RECOGNIZE
What is this paper saying?

        ↓

LEVEL 2 — UNDERSTAND
Why does each part exist?

        ↓

LEVEL 3 — RECONSTRUCT
Can I recreate the mechanism without looking?

        ↓

LEVEL 4 — CHALLENGE
Can I find assumptions, weaknesses, counterexamples,
alternative designs and failure modes?

        ↓

LEVEL 5 — TRANSFER
Can I use the mental model to understand/build/design
something that the paper itself never explicitly discussed?
```

 **Level 5 is what I think you mean by “own it.”**

 And I would explicitly tell the AI **not to stop at explanation**.

---

 # The biggest improvement I'd make

 Don't ask the AI:

 > “Explain this paper deeply.”

 That's still fundamentally a summarization instruction.

 Instead, tell it:

 > **Your job is to construct a causal mental model of the system in my mind, and then test whether that model is actually complete.**

 That changes everything.

 The AI should repeatedly move between:

 **concrete → abstract → concrete**

 For example:

```
REAL-WORLD PROBLEM
       ↓
Why does the problem exist?
       ↓
CORE BOTTLENECK
       ↓
What fundamental constraint causes it?
       ↓
DESIGN PRINCIPLE
       ↓
What idea attacks that constraint?
       ↓
MECHANISM
       ↓
What physically/logically happens?
       ↓
IMPLEMENTATION
       ↓
What does the software actually do?
       ↓
EVIDENCE
       ↓
How do we know it works?
       ↓
FAILURE BOUNDARY
       ↓
When does the mechanism stop working?
       ↓
TRANSFER
       ↓
Where else could this idea work?
```

 That is much more powerful than going section-by-section.

---

 # I would also add a “12-year-old test” — but carefully

 The Feynman-style idea is useful, but I wouldn't make “explain it to a 12-year-old” the actual definition of understanding.

 A much better test is:

 > **Explain the mechanism without using the paper's terminology.**

 Then:

 > **Explain it using the technical terminology.**

 Then:

 > **Translate between the two.**

 This catches something very important: people often hide gaps in understanding behind vocabulary.

 Research and existing Feynman-oriented work support the general value of forcing yourself to produce a mechanistic explanation rather than merely recognize terminology.  GitHub

 So your prompt should demand **three explanations**:

 ### Child explanation

 “Imagine you're 12 and have never heard these words.”

 ### Engineer explanation

 “You are a competent software engineer who hasn't seen this architecture.”

 ### Expert explanation

 “You are discussing the mechanism with the paper's authors.”

 If those three explanations are internally consistent, that's a much stronger signal of understanding.

---

 # The other major addition: rebuild it from first principles

 For every major mechanism, I would force the AI to answer:

 1. **What problem exists?**
2. **What makes that problem difficult?**
3. **What would an ideal solution do?**
4. **Why can't the obvious solution do that?**
5. **What constraint must the solution overcome?**
6. **What design decision does the paper make?**
7. **Why should that decision work?**
8. **What exactly happens step by step?**
9. **What assumptions make it possible?**
10. **What would happen if we removed this component?**
11. **What alternative could we have used?**
12. **Why did the authors choose this one?**

 That gets you underneath the implementation.

---

 # And then: adversarial understanding

 This is the part I think will make your system substantially better.

 After explaining the paper, the AI should **attack its own explanation**.

 For every central claim:

 > What must be true for this to work?

 Then:

 > What evidence establishes that?

 Then:

 > What evidence is missing?

 Then:

 > What counterexample would break the mechanism?

 Then:

 > Could a simpler mechanism achieve the same result?

 Then:

 > What would happen if assumption X were false?

 Then:

 > What is the strongest argument against the paper?

 This converts reading into **technical argumentation**, not consumption.

---

 # The complete system I would build for you

 I would call it something like:

 ## **Paper Ownership Protocol**

 And structure the prompt into **10 phases**.

 ### Phase 0 — Orient

 Identify:

 - paper type
- problem domain
- prerequisites
- intended contribution
- terminology
- what you need to know beforehand

 Do not immediately dive into equations.

---

 ### Phase 1 — Build the map

 Create a one-page map:

```
Problem
  ↓
Existing approaches
  ↓
Why they fail
  ↓
Paper's insight
  ↓
Mechanism
  ↓
Implementation
  ↓
Evidence
  ↓
Limitations
  ↓
Implications
```

 If the paper cannot yet be represented this way, keep investigating.

---

 ### Phase 2 — Reconstruct the author's thinking

 Don't just tell me what they did.

 Reconstruct:

 > “The authors were trying to solve X. They noticed Y. That means Z is the bottleneck. Therefore they introduced A. A changes B, which produces C.”

 Essentially:

 **because A → therefore B → which causes C → therefore D**

 This causal chain is the backbone of understanding.

---

 ### Phase 3 — Decompose the mechanism

 For every important component:

```
Component
├── Why does it exist?
├── Input
├── Transformation
├── Output
├── State
├── Dependencies
├── Assumptions
├── Interaction with other components
├── Expected effect
└── Evidence
```

 For software systems, additionally:

```
Data
→ API/interface
→ component
→ state transformation
→ communication
→ output
→ feedback/evaluation
```

---

 ### Phase 4 — First principles

 Strip away the paper's terminology.

 Ask:

 > If we had never seen this paper, what fundamental problem are we solving?

 Then derive the architecture from the problem.

 This is crucial because otherwise you memorize:

 > “They use X + Y + Z.”

 Instead, you understand:

 > “Given constraints A, B and C, some mechanism with properties X, Y and Z is almost necessary.”

 That's a radically better mental model.

---

 ### Phase 5 — Multi-resolution explanation

 Explain the entire paper at:

 **10 seconds → 1 minute → 5 minutes → 30 minutes → technical deep dive**

 And at each level, preserve the same causal structure.

 This tests whether the model is actually coherent.

---

 ### Phase 6 — Reconstruct without the paper

 Now hide the source.

 Ask me:

 > “What problem were they solving?”

 Then:

 > “What was the bottleneck?”

 Then:

 > “What was their key insight?”

 Then:

 > “Walk me through the mechanism.”

 Then:

 > “Why does component X exist?”

 Then:

 > “What happens if X is removed?”

 This is where passive familiarity becomes actual retrieval.

 Active recall is particularly valuable here because rereading and recognizing an explanation can create a false sense of mastery.  Gregory Lacefield

---

 ### Phase 7 — Attack the paper

 Now become the adversarial reviewer.

 Find:

 - hidden assumptions
- edge cases
- counterexamples
- weak evidence
- alternative explanations
- questionable baselines
- scalability problems
- complexity/cost
- implementation ambiguity
- failure modes
- situations where the mechanism should not work

 Then argue **both sides**.

---

 ### Phase 8 — Transfer

 This is the most important addition.

 Ask:

 > What is the underlying principle independent of this particular paper?

 Then:

 > Where else could this principle apply?

 Then:

 > Could I design a different system using the same principle?

 Then:

 > What other systems have an analogous structure?

 Then:

 > What would I change if the constraints changed?

 This converts **paper knowledge → reusable engineering knowledge**.

---

 ### Phase 9 — Teach it

 Make the AI teach you as if you're:

 1. a 12-year-old
2. a junior engineer
3. a senior engineer
4. the author defending the paper

 The explanations must remain consistent.

---

 ### Phase 10 — Certification

 Finally, don't let the AI declare:

 > “You understand the paper.”

 Instead, make it **test you**.

 Generate questions at different levels:

```
Level 1 — terminology
Level 2 — conceptual
Level 3 — causal
Level 4 — mechanism
Level 5 — implementation
Level 6 — counterfactual
Level 7 — criticism
Level 8 — transfer/design
```

 And don't reveal answers immediately.

 Your answer should be evaluated against the paper's actual mechanism.

---

 # The prompt I'd eventually use

 Here is the important part: **I would not simply copy an existing skill.**

 I would use the existing paper-reading skill as the **evidence/research layer**, then put your **ownership protocol above it**.

 The master prompt would begin roughly like this:

 Paper Ownership Protocol — Master Prompt

# Paper Ownership Protocol

 Your job is NOT to summarize this paper.

 Your job is to help me **own the paper's underlying mental model** so deeply that I can:

 - explain it simply without jargon,
- explain it technically,
- reconstruct the mechanism without looking at the paper,
- explain why every important component exists,
- derive the design from first principles,
- connect the parts into one coherent causal model,
- identify assumptions and hidden dependencies,
- challenge the authors' claims,
- generate counterexamples and failure cases,
- compare the mechanism with alternatives,
- modify the mechanism under changed constraints,
- recognize the same underlying idea in other systems,
- and teach the paper to another person.

 Treat "understanding" as **mechanistic understanding**, not familiarity with terminology.

 ## Core rule

 Do not merely tell me what the authors wrote.

 Reconstruct **why the system has the structure it has**.

 Continuously move through:

 **problem → constraint → bottleneck → insight → design principle → mechanism → implementation → evidence → limitation → transferable principle**

 Whenever possible, explain:

 **because A → therefore B → which causes C → therefore D.**

 If you cannot establish a causal connection, explicitly say that the connection is uncertain.

 ## Evidence discipline

 Separate every important statement into one of these categories:

 - **Paper fact** — explicitly stated or directly shown by the paper.
- **Derived consequence** — logically follows from the paper.
- **Interpretation** — your explanation of what the authors mean.
- **External background** — knowledge needed to understand the paper but not established by it.
- **Hypothesis** — plausible but unverified.
- **Unknown** — the paper does not provide enough information.

 Never silently convert an inference into a fact.

 When using external sources, use them to clarify prerequisites, historical context, competing approaches, or disputed claims—not to overwrite what the paper actually says.

 ## Phase 1 — Build the paper map

 First determine:

 1. What type of paper is this?
2. What real-world or technical problem is it solving?
3. Why is the problem difficult?
4. What approaches existed before this paper?
5. What fundamental limitation do those approaches have?
6. What is the paper's central insight?
7. What mechanism implements that insight?
8. What evidence is supposed to demonstrate that it works?
9. What are the main limitations?
10. What is the transferable idea underneath the specific implementation?

 Produce a compact end-to-end map before going into detail.

 ## Phase 2 — Reconstruct the author's reasoning

 Rewrite the paper's intellectual argument as a causal chain:

 **We want X.\
 But Y prevents us from doing X.\
 The important bottleneck is Z.\
 Therefore the authors introduce A.\
 A changes B.\
 That should produce C.\
 The authors test this through D.\
 The evidence shows E.\
 Therefore conclusion F is justified—but only under assumptions G.**

 Do not proceed until the central argument is coherent.

 ## Phase 3 — First-principles reconstruction

 Temporarily ignore the paper's terminology.

 Ask:

 - What is the underlying problem?
- What are the fundamental constraints?
- What information is available?
- What information is unavailable?
- What must the system accomplish?
- What would an ideal solution look like?
- Why does the obvious solution fail?
- What properties must a successful solution have?
- Which of those properties does the paper implement?
- Which design choices are necessary?
- Which are merely implementation choices?

 Then derive the paper's architecture from those constraints as far as possible.

 If the architecture cannot be derived uniquely, explain what additional design choices the authors made.

 ## Phase 4 — Mechanism decomposition

 For every load-bearing component, explain:

 ### Component

 **Purpose:** Why does this component exist?

 **Input:** What enters it?

 **Operation:** What transformation occurs?

 **Output:** What comes out?

 **State:** What information must it remember?

 **Dependencies:** What does it depend on?

 **Interaction:** How does it connect to the other components?

 **Expected effect:** Why should this operation help?

 **Evidence:** Where does the paper demonstrate that it helps?

 **Removal test:** What would happen if we removed it?

 **Alternative:** What else could have been done?

 **Trade-off:** What does this choice gain and sacrifice?

 ## Phase 5 — Software/system mental model

 For software systems, explicitly reconstruct:

 **inputs → interfaces → components → data/state transformations → communication → outputs → feedback/evaluation**

 Identify:

 - data flow,
- control flow,
- state,
- boundaries,
- interfaces,
- dependencies,
- failure propagation,
- computational complexity,
- memory/storage implications,
- latency,
- concurrency if relevant,
- scaling behavior,
- operational assumptions.

 When the paper provides insufficient implementation detail, say so.

 Do not invent missing architecture.

 ## Phase 6 — Explain at multiple resolutions

 Explain the same mechanism at five levels:

 ### 10-second explanation

 One sentence.

 ### 1-minute explanation

 A beginner should understand the core idea.

 ### 5-minute explanation

 Explain the problem, insight and end-to-end mechanism.

 ### 15-minute explanation

 Explain the major components and why they exist.

 ### Expert explanation

 Explain the technical mechanism, assumptions, trade-offs, evidence and limitations.

 All five explanations must describe the **same underlying model**.

 ## Phase 7 — The 12-year-old test

 Explain the mechanism to a hypothetical intelligent 12-year-old who knows none of the paper's terminology.

 Rules:

 - avoid unexplained jargon,
- use concrete analogies,
- use a small example,
- explain cause and effect,
- do not replace the mechanism with a misleading metaphor.

 Then translate the explanation back into technical language.

 If the analogy loses an important property, explicitly state where the analogy breaks.

 ## Phase 8 — Concrete worked example

 Construct one small example and execute the entire mechanism manually.

 Show:

 **initial state → input → step 1 → step 2 → intermediate state → step 3 → output**

 Use actual toy values where useful.

 The example should make the invisible mechanism visible.

 ## Phase 9 — Equations and algorithms

 For every load-bearing equation or algorithm:

 1. What question does it answer?
2. What does every symbol mean?
3. What are the types/shapes/units where relevant?
4. Why is the equation structured this way?
5. What intuition does it encode?
6. What happens if a term is removed?
7. What assumption does it introduce?
8. How does it connect to the larger mechanism?
9. How is it implemented?
10. What evidence validates its importance?

 Never merely restate equations.

 ## Phase 10 — Evidence audit

 For every major claim, distinguish:

 **claim → experiment → result → interpretation → limitation**

 For important experiments identify:

 - question being tested,
- setup,
- baseline,
- variable changed,
- metric,
- result,
- what the result establishes,
- what it does NOT establish.

 Check for:

 - weak baselines,
- unfair comparisons,
- missing ablations,
- data leakage,
- benchmark artifacts,
- hidden assumptions,
- statistical uncertainty,
- cherry-picking,
- missing failure cases,
- computational cost,
- reproducibility gaps.

 ## Phase 11 — Attack the paper

 Act as a hostile but fair expert reviewer.

 Ask:

 - What is the strongest argument against the paper?
- Which assumption is most fragile?
- What is the simplest counterexample?
- When should the method fail?
- What happens outside the evaluation distribution?
- Could a simpler method achieve the same result?
- Which claim is strongest?
- Which claim is weakest?
- What does the evidence actually prove?
- What does the paper appear to imply but fail to establish?

 Then defend the paper against each criticism where possible.

 ## Phase 12 — Alternative universe

 Now change one important assumption at a time.

 Examples:

 - 10× more data
- 10× less compute
- noisy inputs
- adversarial inputs
- higher latency requirements
- much larger scale
- no access to component X
- component X becomes unreliable
- different objective
- different environment

 For each change, reason through how the architecture would need to change.

 This tests whether the underlying mechanism is actually understood.

 ## Phase 13 — Transfer the mental model

 Extract the deepest reusable principle.

 Answer:

 1. What is the paper's idea underneath its terminology?
2. What general problem pattern does it represent?
3. What other software systems have the same structural pattern?
4. Where else could this idea be useful?
5. What problems look different but have the same underlying structure?
6. What new system could I design using this principle?
7. What should I remember six months from now?

 ## Phase 14 — Reconstruct from memory

 Stop explaining.

 Ask me to reconstruct:

 1. the problem,
2. the bottleneck,
3. the central insight,
4. the architecture,
5. the data/control flow,
6. the reason for each major component,
7. the evidence,
8. the limitations,
9. the transferable principle.

 Do not immediately give me the answer.

 Evaluate my reconstruction and identify missing or incorrect pieces.

 ## Phase 15 — Socratic ownership test

 Ask me questions one at a time.

 Do not ask trivia.

 Prefer questions that test:

 - causal reasoning,
- mechanism reconstruction,
- counterfactual reasoning,
- assumptions,
- trade-offs,
- evidence interpretation,
- alternative designs,
- transfer to new situations.

 When I answer incorrectly, identify the specific mental-model error rather than simply giving the correct answer.

 Then ask a smaller diagnostic question that isolates the misunderstanding.

 Continue until I can reconstruct the central mechanism reliably.

 ## Final deliverable

 Finish with a compact "mental model card":

 ### Problem

 What problem exists?

 ### Bottleneck

 What fundamentally makes it difficult?

 ### Insight

 What did the authors realize?

 ### Mechanism

 How does that insight become a working system?

 ### Why it works

 What causal mechanism produces the benefit?

 ### Evidence

 What actually demonstrates that?

 ### Assumptions

 What must be true?

 ### Failure modes

 When does it break?

 ### Trade-offs

 What does it sacrifice?

 ### Alternatives

 What else could have been done?

 ### Transferable principle

 What should I carry into other problems?

 ### One-sentence memory

 If I remember only one thing six months from now, what should it be?

 ## Quality bar

 Do not optimize for completeness of paraphrasing.

 Optimize for:

 **causal clarity + mechanistic understanding + reconstruction ability + critical judgment + transferability.**

 A successful result is not:

 > "I can explain what this paper says."

 A successful result is:

 > "I can explain why the mechanism has to look roughly like this, reconstruct how it works, predict what happens when its assumptions change, argue with the authors about its limitations, and use the underlying idea somewhere else."

 ## One more refinement I'd strongly recommend

 **Don't use this prompt as a one-shot prompt.**

 That's the biggest trap.

 Use it as a **loop**:

```
PAPER
  ↓
AI builds model
  ↓
AI explains
  ↓
YOU reconstruct
  ↓
AI detects gaps
  ↓
YOU repair model
  ↓
AI attacks model
  ↓
YOU defend/modify it
  ↓
AI gives novel scenario
  ↓
YOU transfer the principle
  ↓
CERTIFIED OWNERSHIP
```

 That is substantially more powerful than asking an LLM for an extremely long explanation.

 The existing research-paper skills already give you strong **paper extraction, evidence auditing, mechanism reconstruction, and multi-pass reading**.  GitHub+1   Your refinement should therefore **not duplicate those capabilities**. Put an additional layer on top: **mental-model construction → active recall → adversarial testing → counterfactual reasoning → transfer**.

 And there's a particularly useful feature of ChatGPT's current Deep Research workflow: it can work from uploaded files, search external sources, create a research plan, and produce a cited report. That makes it useful for the **research/context layer**, while your Paper Ownership Protocol becomes the **understanding/mastery layer**.  OpenAI Help Center+1

 So if your goal is genuinely to **“own” software white papers rather than merely understand their summaries**, I would build the system as:

 **Deep Research → Paper Reading Skill → First-Principles Reconstruction → Mental Model → Active Recall → Adversarial Debate → Transfer → Ownership Test.**

 That is the refinement I would make rather than simply installing or copying an existing paper-reading skill.  GitHub+1

—
Solid protocol — it's got the causal-chain spine, evidence discipline, and recall loop right, which is where most "explain this paper" prompts fail. Here's what's genuinely missing, from a few angles.
1. No prior-knowledge activation. The protocol starts building the model without ever asking what you already know. Learning science is clear: new understanding anchors onto existing schema, and skipping this means the AI either over-explains things you already know or leaves gaps assuming you don't. Add a Phase 0.5: "What do you already know about this problem space? What's your background?" — calibrates every later explanation.
2. No implementation/code step. Huge miss for software papers specifically. Verbal reconstruction is real but weaker than making the mechanism run. A toy implementation of the core algorithm (even 30 lines, on synthetic data) is one of the strongest ownership tests there is — bugs force you to confront exactly which part you don't actually understand. This should be a mandatory phase, not optional.
3. No visual/diagram generation. The whole protocol is text and Q&A. Dual-coding theory says pairing verbal explanation with a spatial/visual one (architecture diagram, data-flow diagram, sequence diagram) meaningfully improves retention and is a different kind of ownership test — can you draw it, not just say it.
4. No retention plan beyond the session. Active recall inside the conversation is great, but there's nothing for combating the forgetting curve afterward. A one-sentence "mental model card" is a nice artifact but without a spaced-repetition touchpoint (review prompts at +1 day, +1 week, +1 month) it decays like anything else you read once.
5. No positioning in the field's timeline. "Why prior approaches fail" is in there, but that's different from lineage: what did this paper build on, what came after it, did the field adopt it, is it now considered dated/superseded, what's the current state years later. This hindsight-judgment layer (how history actually evaluated the claims) is missing and it's a powerful reality check on Phase 11's "attack the paper."
6. No triage/cost calibration. This is a 15-phase protocol applied uniformly. Not every paper warrants full depth — there should be a cheap first pass (map + 1-minute explanation) that lets you decide how deep to go, rather than committing to the full loop every time. Otherwise this becomes too heavy to actually use regularly, which defeats the purpose.
7. No confidence calibration before answers are checked. In the Socratic phase, you should be forced to state your confidence before seeing if you're right (predict-then-verify). This is a well-established technique for catching false fluency — the same failure mode active recall is trying to fix, but confidence-tracking catches a subtler version of it.
8. No comparative/multi-paper mode. Real expertise usually comes from triangulating 2-3 papers on the same problem, not mastering one in isolation. Worth having an optional extension: "read this alongside its main competitor/successor paper" for a comparative mental model.
9. No re-grounding/hallucination check. The whole protocol trusts the AI's own reading of the paper. There's no explicit step where the AI re-verifies its explanation against the actual source text before presenting it as fact — especially risky for equations and specific numbers, where a small misread compounds through 15 phases of downstream reasoning.
10. No adaptive reader-level. "12-year-old" is fixed as a floor, but "expert" isn't calibrated to you — a junior engineer's expert-level and a research scientist's expert-level are different bars. Worth asking your actual level once, up front, so Phase 6-9 target the right ceiling instead of a generic one.
11. Unclear exit criteria. "Certified ownership" is evocative but fuzzy — no rubric for when the loop is actually done versus running indefinitely. Worth defining a concrete pass condition (e.g., correctly answer N Socratic questions at Level 4+ without hints, produce a working toy implementation, complete one successful transfer example).
One structural note for the skill build: this needs real state management once it's a Claude skill — papers can exceed context, sessions get interrupted, and you'll want to resume mid-loop (e.g., "we're at Phase 6, here's the model so far") rather than restart. Worth designing a lightweight progress-tracking format (a running "model card" file) from the start rather than bolting it on later.
Want me to fold these in and build the skill next, or do you want to weigh in on any of these first (e.g., whether you actually want the implementation/code phase for non-software papers too)?
—
Good angle — the previous list made the protocol more rigorous. This one should make it more economical, because the actual failure mode of elite researchers isn't "not understanding deeply enough" — it's drowning in the volume of papers that exist. Here's what changes when you optimize for time-that-matters rather than completeness.
1. Triage before you invest — most papers don't earn Phase 1. Top PhD students read abstract → figures/tables → conclusion in under 5 minutes and make a go/no-go call before touching the body text. The protocol currently assumes every paper gets full treatment. It needs an explicit Phase -1: Triage — a 5-minute skim that outputs one of: skip, skim-only (stays at map level), or full ownership protocol. Reserve the 15-phase loop for the handful of papers that are actually load-bearing for your work.
2. Read with a question, not for completeness. Elite readers don't ask "help me understand this paper" — they ask "I need this paper to answer X" (build on it, refute it, decide whether to use its method, cite it correctly). Purpose massively prunes what's worth deep effort. Add a required first question in Phase 0: "Why are you reading this — what will you do with it?" — this should reweight which phases get full depth vs. a fast pass.
3. Figures and results before narrative. The method section is the author's argued path; the results table is the actual evidence. Efficient readers go abstract → figures/tables → conclusion → intro → method, explicitly out of order, because figures compress the mechanism faster than prose. The protocol currently reads linearly through phases; it should explicitly instruct extracting all figures/tables first, before Phase 2's causal reconstruction.
4. Predict before you read — track surprise, not just recall. Before opening the method, form a hypothesis from the title/abstract about what you expect the mechanism to be. Then read to find where reality diverges from that prediction. The gap is the highest-value learning signal there is — it locates exactly where your prior model was wrong, which recall alone doesn't do. This is different from the confidence-calibration item already on the list; that one checks answers, this one checks assumptions before reading.
5. Outsource critique you can borrow instead of re-deriving it. Reviewers on OpenReview (or equivalent) have often already found the weak assumptions and missing baselines. Elite students read reviews/rebuttals before independently reconstructing Phase 11's adversarial attack — not to skip critical thinking, but to calibrate it against experts and then go further, rather than starting from zero every time.
6. Check the code before trusting the prose. If a repo exists, skim the README, and — if feasible — actually run it or check issues/discussions. What the code does and what people report breaking is often more honest than what the paper claims. This is empirical grounding the current protocol has no equivalent for; it's currently all reasoning, no verification against the artifact itself.
7. Use the author's own talk if one exists. A 15-minute conference talk or podcast interview frequently conveys the intuition faster than the paper does, because authors compress for a live audience differently than for reviewers. Worth an explicit step: check for a talk/video before doing first-principles reconstruction from cold text.
8. Situate via citation graph, not solo derivation. Rather than rebuilding "why did prior approaches fail" purely by reasoning, check backward citations (what this builds on) and forward citations (what it enabled / how it aged) to borrow the field's own accumulated judgment. This connects directly to your existing item #5 (lineage/hindsight) — this is how to do that efficiently instead of guessing.
9. Two speeds, not one depth. Elite researchers maintain a large shallow layer (hundreds of papers mapped at the "map + 1-min explanation" level, for landscape awareness) and a small deep layer (the few papers they can reconstruct from memory and attack). The skill should output both — every paper gets a lightweight card, only flagged ones get the full loop.
10. Time-box every phase. Depth expands to fill available time if unconstrained. A fixed budget per phase (even self-imposed, e.g. "10 min on Phase 3") forces prioritization onto what's decision-relevant instead of chasing completeness for its own sake.
11. One sentence that would change your mind. Before the adversarial phase, identify the single most load-bearing claim — the one fact that, if false, breaks the paper's contribution. Spend disproportionate scrutiny there rather than spreading effort evenly across every claim. This is how top reviewers allocate attention, and it's a much sharper use of Phase 11 than uniform attack.
12. Cumulative notes, not siloed cards. The final "mental model card" should link to prior papers' cards (a running knowledge base / zettelkasten), not stand alone — ownership compounds across papers when they're connected, and isolated cards get forgotten as separate facts instead of a growing web.
These pair naturally with your 11: the first list makes the deep path more rigorous; this one decides when to take the deep path at all and speeds up getting there.
—
This is the angle that actually determines whether the other 23 points work or just produce confident-sounding wrong understanding. A rigorous protocol executed through a biased mind still gives you a biased mental model — it'll just be articulated more impressively. Here's what to guard against and how to build the countermeasure into the skill.
1. Confirmation bias — reading to confirm your predicted mechanism. Point 4 in the last batch (predict before reading) is powerful but double-edged: once you've formed a hypothesis, you unconsciously read evidence that fits it and skim past evidence that doesn't. Countermeasure: after prediction, explicitly search for the paper's strongest disconfirming result before summarizing — force a "what did NOT match my prediction" step, not just "what matched."
2. Narrative fallacy — smoothing the paper into a cleaner story than it was. The causal chain format ("because A → therefore B → which causes C") is excellent for understanding but dangerous for accuracy — real research is messier, with dead ends, arbitrary choices, and lucky accidents that get retconned into a clean narrative once it works. Countermeasure: explicitly tag which parts of the causal chain are the paper's actual argued logic versus your own retrofit for coherence. The "Interpretation" vs "Paper fact" distinction already in the protocol helps here — just needs to be pointed specifically at the causal chain, not just individual claims.
3. Hindsight bias — "of course this design was inevitable." Once you understand why a mechanism works, it feels obvious it had to be that way. This kills Phase 3 (first-principles reconstruction) — you'll convince yourself you "derived" the architecture when you actually reverse-engineered it knowing the answer. Countermeasure: before reading the method, try to genuinely design a solution yourself from the stated problem, on paper, then compare to what the authors did. The mismatch is more honest than post-hoc derivation.
4. Authority bias — inflating trust because of venue, citation count, or author fame. A NeurIPS paper from a famous lab gets less scrutiny than it should; a small workshop paper gets more skepticism than its evidence warrants. Countermeasure: strip metadata during the evidence-audit phase — evaluate the claims and results as if the paper were anonymous, and only reintroduce reputation信号 when deciding how much to prioritize reading it in the first place (triage stage), not when judging its evidence.
5. Anchoring — the abstract's framing colors everything downstream. Authors write abstracts to sell the contribution, and that framing (what's the "main" insight, what's a "limitation" vs "future work") anchors your entire mental model before you've read the evidence. Countermeasure: after building your own map (Phase 1), go back and compare it to the abstract's framing — note where they diverge, since divergence often reveals where the paper is oversold or where you caught something the abstract glossed over.
6. Survivorship bias — only seeing the version that worked. Papers don't report the 20 failed variants; you only see the one that got published. This inflates how "obviously correct" the final design seems and hides how much of the result might be a fragile, cherry-picked configuration. Countermeasure: in the adversarial phase, explicitly ask "what failed variants were probably tried and discarded, and how would we know?" — treat absence of ablations as a flag, not a null result.
7. Illusion of explanatory depth — feeling you understand because the story is fluent. This is the single most dangerous one for this whole protocol, because a well-run LLM conversation is maximally fluent — every phase produces smooth, confident prose, which is exactly the sensation that fools people into overestimating their own understanding. This is precisely why active recall (Phase 14) and implementation (item #2 from the previous batch) can't be optional — fluency of explanation and depth of understanding are genuinely uncorrelated, and only forced generation from scratch (code, or unaided verbal reconstruction) exposes the gap.
8. Motivated reasoning / sunk cost — once invested, resisting evidence the paper is weak. After spending an hour on the full 15-phase loop, there's real psychological pressure to conclude "this was a good paper, worth the effort" rather than "actually the core claim doesn't hold up." Countermeasure: separate the adversarial phase (Phase 11) from a final verdict — write the critique before deciding whether to keep the paper in your long-term knowledge base, so the sunk effort doesn't bias the verdict.
9. Availability heuristic — overweighting the most recent or most vivid paper you've read. When comparing this paper to alternatives (Phase 8 transfer, or the comparative multi-paper mode), you'll over-anchor on whatever's freshest in memory rather than what's actually most relevant. Countermeasure: when doing lineage/comparison work, deliberately pull up your own older paper-cards rather than relying on memory of what "feels" similar.
10. The Feynman-technique trap itself — mistaking simplification for insight. Ironically, the "explain to a 12-year-old" test can produce a false sense of understanding if the analogy is memorable but the mapping is actually loose — you remember the analogy, not the mechanism. This is already flagged in the original protocol ("if the analogy loses an important property, state where it breaks") — worth elevating this from a footnote to an enforced check every time an analogy is used, not just optionally.
11. Overconfidence from repetition — mistaking familiarity for mastery. If you've read a paper's abstract five times across different contexts, it feels deeply known even if you never actually reconstructed the mechanism. This is the exact case where the confidence-calibration step (predict-then-verify, from the previous batch) earns its keep — familiarity and actual reconstruction ability need to be tested separately, because the mind conflates them by default.
How this folds into the skill structurally: rather than one more phase bolted on, these should function as a small set of standing checks that run across the existing phases — a short "epistemic hygiene" checklist invoked at specific trigger points (after prediction, before final verdict, whenever an analogy is used, before declaring ownership complete) rather than a single Phase X you do once and forget. I'll build it that way — embedded tripwires, not a 24th phase — unless you'd rather have it as an explicit standalone phase for visibility. Which do you prefer?
—
Yes — this is a real and important angle, and it's distinct from everything covered so far. Everything up to now optimizes for owning this paper's mechanism. This angle asks: what's the reusable vocabulary underneath all mechanisms, such that owning paper #40 makes paper #41 faster to own? That's how senior engineers actually get faster over time — not by reading more paper, but by accumulating a small set of recurring shapes that new mechanisms keep turning out to be instances of.
1. Recurring trade-off axes — the deepest and most reusable layer. Nearly every mechanism is a position on one of a small number of axes: space vs. time, latency vs. throughput, consistency vs. availability, accuracy vs. speed, generality vs. specialization, exploration vs. exploitation, precision vs. recall, compute vs. memory, online vs. batch, centralized vs. decentralized, statefulness vs. statelessness. When you decompose a mechanism (Phase 4), explicitly ask: which known trade-off axis is this design a point on, and where on that axis did they choose to sit, and why? This alone transfers harder than almost anything else in the protocol, because the next paper you read is very likely trading off along one of these same axes, just dressed in different terminology.
2. Named recurring mechanisms — a pattern vocabulary to tag against. Most "novel" mechanisms are a recombination of a small set of moves: caching/memoization, indirection, lazy vs. eager evaluation, batching, pipelining, amortization, divide-and-conquer, feedback loops/control theory, redundancy for fault tolerance, hierarchy/layering, locality exploitation, compression via structure, greedy approximation of an optimal solution, push vs. pull propagation, idempotency, monotonicity, convergence via iteration. When you find the paper's core mechanism, ask: which of these named moves is this an instance of, or a combination of? Naming it against a known pattern is what lets you recognize the same idea instantly next time it shows up in an unrelated domain — this is exactly the Phase 8/13 transfer step, but it only works well if you're matching against a stored vocabulary rather than re-deriving similarity from scratch each time.
3. Classic CS aphorisms as compression tools. Things like "all problems in computer science can be solved by another layer of indirection," "worse is better" vs. "the right thing," the end-to-end principle, Conway's Law, Amdahl's Law, the CAP theorem, "no silver bullet" — these are load-bearing precisely because they're general enough to apply across domains but specific enough to generate a real prediction. Worth explicitly checking, at the transfer phase: does a known aphorism already compress this paper's insight? If so, that's often a faster and more durable memory anchor than the paper's own framing.
4. Systems-thinking lens — feedback, emergence, second-order effects. A lot of mechanisms only make sense as a loop, not a pipeline: feedback control, homeostasis, positive/negative feedback, emergent behavior from simple local rules. Papers describing training loops, reinforcement mechanisms, or self-correcting systems are almost always better understood through this lens than through linear input→output decomposition. Worth an explicit check: is this mechanism actually a loop, and if so, what does it converge to, oscillate around, or diverge from?
5. Evolutionary/selection lens — variation, selection, retention. Many mechanisms (search algorithms, training procedures, even architecture search) are structurally "generate variation → apply a selection pressure → retain what passes → repeat." Recognizing this pattern transfers extremely well because it's one of the most domain-general structures there is — it applies to genetic algorithms, gradient descent, A/B testing, and biological evolution with the same underlying logic.
6. Information-theoretic lens — signal, noise, compression, entropy. A huge fraction of ML/systems mechanisms are, underneath, about separating signal from noise or compressing information while preserving what matters. Asking "what is this mechanism throwing away, and why is that safe to throw away?" is often the single fastest route to the real insight, especially for anything involving representation learning, attention, or lossy optimization.
7. Economic/game-theoretic lens — incentives and equilibria. Multi-agent systems, adversarial training, auction mechanisms, distributed consensus — these are often best understood as "what is each component incentivized to do, and what stable equilibrium does that produce?" rather than as a fixed pipeline. Worth invoking whenever multiple components are optimizing something even implicitly against each other.
8. Unix/design philosophy lens — composability and minimalism. "Do one thing well, compose via clean interfaces" versus "one monolithic optimized system" is itself a recurring design stance worth naming, because it predicts a lot about a system's maintainability, extensibility, and where its weaknesses will show up under new conditions.
9. Mathematical reduction lens — is this secretly a known problem? A large fraction of "new" mechanisms are a known optimization/algorithmic problem (shortest path, matching, coloring, fixed-point iteration, convex optimization) wearing domain-specific clothing. Explicitly asking "what known math/CS problem is this secretly an instance or approximation of?" often reveals guarantees, limitations, and known failure modes for free — you inherit an entire body of prior knowledge instead of evaluating the mechanism in isolation.
How I'd fold this in structurally: this shouldn't be one more phase inside the per-paper loop — it's actually the connective tissue across papers, which is different from everything else in the protocol so far. I'd build it as:
* A standing "Pattern Library" file (like the model-cards you already have, but for reusable principles instead of paper-specific mechanisms) that the skill reads from and writes to every time.
* A single added step in Phase 8/13 (Transfer): "Match this mechanism against the Pattern Library — which existing entries does it instantiate, refine, or contradict? Add or update an entry."
* Over time this becomes the actual compounding asset — not a bigger pile of paper-cards, but a shrinking, increasingly general set of principles that most new papers turn out to be recombinations of, which is exactly what makes reading paper #50 faster than paper #5.
That's a strong fourth angle and pairs naturally with the lineage/hindsight item from batch one — lineage tells you how this paper fits history, the pattern library tells you how this mechanism fits the timeless vocabulary underneath all of software.
Four solid angles now: rigor (11), efficiency (12), epistemics (11), and transferable philosophy (9) — 43 points total. 
