# Career Guide Skill — Fixes and Changes

This document is a work plan for Claude Code to upgrade the `career-guide` skill. Work through it phase by phase. Phase 1 is required (it fixes real bugs); Phases 2–5 are improvements ordered by impact.

---

## 0. Context before you start

**The skill lives at** `career_guide/` and currently contains:

```
career_guide/
├── SKILL.md
├── frameworks.md
└── research-protocol.md
```

**Voice and tone of the existing skill** (preserve this in everything you add):

- Warm but direct; refuses toxic positivity
- Explicitly flags uncertainty rather than masking it
- Treats the user as a thinking partner, not a recipient of prescriptions
- Names frameworks rather than using them silently
- Grounds advice in research, not training-data generalizations

**Don't rewrite what's already working.** The philosophy section, epistemic standards, and existing frameworks are well-crafted. Additions should match the existing register — short paragraphs, plain prose, occasional bulleted lists only when they earn their place, no heavy bolding or breathless headers.

**Read all three existing files in full before making changes.** Many additions reference the existing structure and need to slot into it cleanly.

---

## Recommended execution order

1. Phase 1 (bugs) — must come first; some later phases depend on the path fix
2. Phase 2 (missing framework definitions) — closes loose references already in SKILL.md
3. Phase 3 (new reference files) — biggest content additions
4. Phase 4 (SKILL.md structural additions) — wires the new files into the conversation flow
5. Phase 5 (polish) — smaller refinements

Phases 2 and 3 can be done in parallel if you have the headspace; they touch different files.

---

# Phase 1 — Bug fixes

## 1.1 Reorganize files into a `references/` subdirectory

**Problem:** SKILL.md references `references/frameworks.md` and `references/research-protocol.md`, but the files are at the top level of the skill folder. Claude will fail to find them on the first try.

**Fix:** Move the reference files into a `references/` subdirectory so the paths in SKILL.md become correct.

```bash
mkdir -p career_guide/references
git mv career_guide/frameworks.md career_guide/references/frameworks.md
git mv career_guide/research-protocol.md career_guide/references/research-protocol.md
```

(If not using git, plain `mv` is fine.)

**Verification:** After the move, `career_guide/references/frameworks.md` and `career_guide/references/research-protocol.md` should exist, and `frameworks.md` / `research-protocol.md` should no longer be at the top level.

## 1.2 Remove year-stamped queries from research-protocol.md

**Problem:** Queries like `[role title] day in the life 2024 OR 2025` go stale quickly. As written, they'll be wrong by the time anyone runs them.

**Fix:** Replace hardcoded years with a placeholder convention. Add this note near the top of `research-protocol.md`, right under "Core Principle":

> **A note on dates in search queries:** Examples below use `[current year]` as a placeholder. Substitute the actual current year when running searches, and consider also searching the previous year (`[current year - 1]`) to catch coverage that hasn't been updated yet.

Then replace every instance of `2024`, `2025`, `2024 OR 2025`, etc., in search query examples with `[current year]` or `[current year] OR [current year - 1]`.

Leave non-query references to years alone (e.g., explanatory prose about how data ages).

## 1.3 Fix dangling framework references in SKILL.md

**Problem:** The framework-selection table in SKILL.md Phase 3 mentions "Decision Matrix" and "Lean Startup thinking," but neither is defined in `frameworks.md`. Either define them or remove them.

**Fix:** Define both. Add the following sections to `references/frameworks.md`, inserted in numerical order (renumber subsequent frameworks if needed, or append at the end and let the numbering grow).

### Decision Matrix to add

```markdown
## Decision Matrix (Weighted Scoring)
*Common in management consulting; popularized for personal decisions by various coaches*

**What it is:** List your options as rows and your criteria as columns. Weight each criterion by importance (1–5). Score each option against each criterion (1–10). Multiply and sum to get a total per option.

**When to use:** Multi-option decisions with multiple competing criteria (e.g., choosing between job offers that differ on comp, learning, prestige, commute, mission).

**How to apply honestly:**
- Pick criteria *before* scoring options, not after — picking criteria to justify a preferred answer is the classic failure mode
- Force yourself to include criteria that argue against your gut preference
- The output is a thinking aid, not the decision. If the matrix says A but your gut screams B, that gap is worth examining, not overriding

**Honest limitation:** Numbers create false precision. Two options scoring 78 and 82 are not meaningfully different. Use the matrix to *surface* hidden weights and tradeoffs, not to crown a winner.
```

### Lean Startup thinking to add

```markdown
## Lean Startup Thinking (Applied to Careers)
*From Eric Ries, "The Lean Startup"; adapted to careers by various practitioners*

**What it is:** Treat a potential career path as a hypothesis to be tested with the smallest possible experiment, not as a decision to be made all at once. Build–Measure–Learn: define what you'd need to see to believe the path is right, design the cheapest experiment that would produce that signal, run it, update.

**When to use:** When someone is considering a big, risky, or expensive career move (starting a company, leaving a stable job, going back to school) and would benefit from a smaller test first.

**Application:**
- Considering a startup? Validate the problem with 20 customer conversations before quitting
- Considering a career switch to design? Take on three small projects before enrolling in a bootcamp
- Considering management? Lead a small project before applying for the title

**Key insight:** Most career anxiety comes from treating reversible decisions as irreversible. Cheap experiments collapse the uncertainty faster than more thinking.

**Honest limitation:** Some career moves can't be experimented with cheaply (medical school, military service, having children). Don't pretend everything is a hypothesis when some things are commitments.
```

## 1.4 Update the framework-selection table

After 1.3, update the table in SKILL.md Phase 3 to reflect the now-existing frameworks. Also add a few new rows mapping situations to the frameworks you'll add in Phase 3 (Type 1/Type 2, WRAP, Pre-mortem, etc.) once those exist — but only after Phase 3 is done.

---

# Phase 2 — Framework additions

Add the following frameworks to `references/frameworks.md`. Match the formatting of the existing entries: numbered heading, attribution line in italics, "What it is," "When to use," and at least one of "Application," "Honest limitation," "Key insight," or "Questions to ask."

## 2.1 Type 1 / Type 2 Decisions

```markdown
## Type 1 vs. Type 2 Decisions
*From Jeff Bezos's 1997 shareholder letter*

**What it is:** Type 1 decisions are one-way doors — costly or impossible to reverse. Type 2 decisions are two-way doors — if you walk through and don't like it, you can walk back. Bezos's claim: most decisions are Type 2, but people treat them like Type 1 and over-deliberate.

**When to use:** Whenever the user is paralyzed by a decision. Ask first: is this actually Type 1, or is it Type 2 wearing Type 1 clothing?

**Application to career questions:**
- Taking a new job ≈ Type 2 (you can leave; even a "bad" year is recoverable)
- Quitting without a plan in a tight market ≈ closer to Type 1 (rebuilding leverage is hard)
- Going to a 4-year degree program ≈ Type 1 (time and money rarely come back)
- Taking a sabbatical ≈ Type 2 for most workers, Type 1 for some (depends on field, level, runway)

**Key insight:** Type 1 decisions deserve slow, careful thought. Type 2 decisions deserve speed — the cost of over-deliberation is usually higher than the cost of getting it slightly wrong and adjusting.
```

## 2.2 WRAP Framework

```markdown
## WRAP — A Process for Better Decisions
*From Chip and Dan Heath, "Decisive"*

**What it is:** A four-step process designed to counter the four villains of decision-making (narrow framing, confirmation bias, short-term emotion, overconfidence):

- **W**iden your options — Don't ask "should I do X?" Ask "what else could I do?" The "whether-or-not" framing is the trap
- **R**eality-test your assumptions — Run cheap experiments. Talk to people who've done it. Look at base rates
- **A**ttain distance before deciding — Use the 10/10/10 rule: how will I feel about this in 10 minutes, 10 months, 10 years? Or: what would I advise a friend in this situation?
- **P**repare to be wrong — Set tripwires for when to reconsider. Plan for the downside

**When to use:** Any significant career decision. Especially useful when the user has framed their question as binary ("should I take this job or not?") — that framing alone is the first villain.

**Honest limitation:** This is a process, not an answer. It produces better decisions on average but doesn't guarantee good outcomes from any single decision.
```

## 2.3 Pre-mortem

```markdown
## Pre-mortem Analysis
*From Gary Klein (decision researcher)*

**What it is:** Before committing to a decision, imagine yourself two years in the future. The decision failed badly. Write down why. Then work backwards from the failure modes to identify what to watch for or mitigate now.

**When to use:** Before taking a job offer, joining a startup, starting a business, making a big geographic move, or any decision with a meaningful downside scenario.

**Why it works:** People resist acknowledging risks during the excited "decision-making" phase. Framing it as "imagine it already failed" removes the social cost of being the pessimist and reveals concerns the user already half-knows.

**Application:**
- "It's two years from now and you took this startup job. It went badly. What happened?"
- Common answers reveal: founder issues, market timing, runway, role/title disappointment, location regret
- For each answer, ask: what would you need to see *now* to feel okay about that risk?
```

## 2.4 The 70/20/10 Learning Split

```markdown
## The 70/20/10 Learning Split
*Attributed to Morgan McCall and colleagues at the Center for Creative Leadership*

**What it is:** A rough empirical breakdown of where professional growth comes from:
- 70% from challenging on-the-job experiences
- 20% from relationships, mentorship, and feedback
- 10% from formal training and courses

**When to use:** When the user is over-investing in courses, certifications, or credentials hoping they'll produce career growth — or when they're under-investing in stretch assignments and mentor relationships.

**Key insight:** Most career capital is built by doing uncomfortable work at the edge of your ability, with feedback from people who've done it before. Courses are a small slice. If someone is taking their fifth online course this year and still feels stuck, the diagnosis is usually in the 70 or the 20.

**Honest caveat:** The numbers are rough generalizations from one research program, not laws of physics. In some fields (medicine, law) formal training is closer to 30–40%. Use the ratio as a corrective bias, not a prescription.
```

## 2.5 Anti-Mimetic Thinking

```markdown
## Anti-Mimetic Thinking (Examining Borrowed Desire)
*Adapted from René Girard's mimetic theory; popularized in career contexts by Luke Burgis ("Wanting")*

**What it is:** Most of what we want, we want because someone else wants it. Girard called this "mimetic desire." It's especially strong in career: prestige roles, FAANG titles, IPO stories, founder status — these are often wanted because the people around us want them, not because they fit us.

**When to use:** When the user describes a goal in language that sounds borrowed ("I want to be a VP," "I want to start a company," "I want to work at [prestigious place]") without articulating why. Especially useful when the goal makes them anxious rather than energized.

**Questions to ask:**
- If no one you knew would ever find out you achieved this, would you still want it?
- Whose voice is in your head when you imagine this goal? Is it yours?
- What did you want before you encountered this peer group / industry / influencer?
- If you got this thing, who would you most want to tell? Why?

**Honest limitation:** Not all borrowed desire is bad. Some mimetic goals turn out to be genuinely good fits once pursued. The point isn't to reject borrowed desires but to examine them.
```

## 2.6 Update the framework-selection guide

After adding the above, update the framework-selection table at the bottom of `frameworks.md` to include rows for these new frameworks. Suggested additions:

| User feeling/question | Add to the existing recommendation |
|---|---|
| "I can't decide" | Type 1/2, WRAP, Decision Matrix |
| "I'm worried this won't work out" | Pre-mortem, BATNA, Second-Order Thinking |
| "I keep taking courses but feel stuck" | 70/20/10, Career Capital |
| "I'm not sure why I want this" | Anti-Mimetic, Ikigai, Energy Audit |
| "I'm considering something risky" | Lean Startup thinking, Pre-mortem, Type 1/2 |

Also update the corresponding situation→framework table in `SKILL.md` Phase 3 to reference these.

---

# Phase 3 — New reference files

Create three new reference files. Each should be added to `career_guide/references/` and registered in SKILL.md's "Reference Files" section (see Phase 4.5).

## 3.1 `references/populations.md` — Population-specific guidance

**Why:** The existing skill implicitly assumes a mid-career knowledge worker with options. Several common user populations have meaningfully different needs.

**Structure:** One section per population, each ~150–250 words. For each: typical questions they ask, how the existing frameworks apply differently, and resources or pathways specific to that population. Do NOT invent statistics — when you don't have data, say "research this for the user's specific market" rather than fabricating numbers.

**Populations to include (in this order):**

1. **Early career (0–3 years of experience)** — first job choices, "should I leave my first job," when to stop being entry-level. Note that "career capital" matters more than "regret minimization" at this stage; the cost of a wrong move is low.

2. **Career returners (after leave for parenting, illness, caregiving, sabbatical)** — gap framing, returnship programs (Path Forward, ReBoot Accel, iRelaunch, company-specific programs), confidence rebuilding, the difference between "the gap" and the actual barrier (which is often confidence and network atrophy).

3. **Forced transitions (layoffs, performance plans, restructuring)** — severance evaluation basics, the "told my story" tax (re-explaining the layoff in interviews), runway math, the emotional sequence (shock → identity hit → reorientation), when to take the first decent offer vs. hold out.

4. **Constrained workers** — visa/immigration status (H-1B timing, green card portability), caregiving obligations (geographic constraints, schedule constraints), disability or chronic illness (energy budgeting, accommodation conversations, when to disclose). Important: don't pretend constraints don't exist or that they can be "worked around"; help the user navigate *within* them.

5. **Mid-career switchers (changing industries or functions)** — pattern of "bridge roles," portfolio building, the credibility gap, how long the transition typically takes (real answer: longer than people hope, usually 12–24 months end-to-end).

6. **Late career and encore careers** — semi-retirement, fractional/advisor roles, mentorship and board seats, knowledge transfer, the "what now" question after a long primary career.

**Voice note:** Resist the urge to write motivational copy in this file. Each population is grappling with real structural conditions, not a mindset problem. Treat them as informed adults navigating real constraints.

## 3.2 `references/decision-types.md` — Decision-type playbooks

**Why:** The existing Phase 4 synthesis assumes the user is choosing between life paths. Several common career decisions have their own playbooks worth surfacing.

**Structure:** One section per decision type. Each section: when this applies, key questions to surface, relevant frameworks, common failure modes, and the synthesis structure to use.

**Decision types to include:**

1. **Job offer evaluation** — total comp decomposition (base, bonus, equity, benefits, retirement match, ESPP), equity literacy (RSUs vs. ISOs vs. NSOs, vesting cliffs, 409A valuations, dilution risk, single-trigger vs. double-trigger), how to weigh comp against role/team/manager/learning, leverage and the negotiation window, how to compare two offers without false precision.

2. **Stay vs. leave** — the "should I quit" question. When dissatisfaction is fixable in role vs. when it isn't; the manager problem vs. the company problem vs. the role problem; the cost of staying too long vs. leaving too soon; the role of BATNA in this decision.

3. **IC vs. management track** — when to switch, what changes (your job becomes other people's work; deep work shrinks; calendar fills), how to test before committing (lead a project, manage an intern), the player-coach trap, how to switch back if you don't like it.

4. **Founding vs. joining a startup** — the very different risk/return profiles, when founding makes sense (deep domain knowledge, co-founder match, problem obsession, financial runway) vs. when joining is better (learning velocity, comp, less personal exposure), how to evaluate early-stage offers (stage, funding, team, equity %, dilution path).

5. **Going independent (freelance/consulting/solopreneur)** — pipeline math (revenue = leads × close rate × deal size), runway requirements (typically 6–12 months minimum), the lonely middle (after the novelty wears off and before the business stabilizes), tax and admin overhead people forget about.

6. **Geographic moves** — career networks are local, often more than people realize; "remote" doesn't fully solve this for many roles; cost-of-living math is more than rent; quality-of-life-vs-career tradeoffs over the long term.

**Each section should end with:** "Frameworks especially useful here: [list]."

## 3.3 `references/conversations.md` — Conversation patterns and example dialogues

**Why:** The skill tells the model *what* to do but never *shows* it. One concrete example calibrates quality more than a page of guidance.

**Structure:**

### Part 1: The first response

When this skill triggers, the model should not jump straight to questions. Provide a template for the opening response:

- Briefly acknowledge the weight of what the user is asking (one sentence — no faux empathy, no "wow what a great question")
- Signal that this is a thinking-together conversation, not a quick answer
- Ask one excavating question — the most important one given what they've shared

Provide 2–3 example openings for different types of triggers ("I'm thinking about quitting my job," "Should I take this offer?", "I don't know what to do with my life").

### Part 2: Triage / scoping

Before Phase 1 ("Listen & Excavate") begins in earnest, the model should do quick triage. Three categories:

- **Time-boxed decisions** (offer expires Friday, must respond by date X) — compress the excavation phase; get to research and synthesis faster
- **Open-ended exploration** ("I don't know what I want") — full excavation; resist the pull toward premature solutions
- **Crisis or acute distress** (just laid off, burned out, in tears) — lead with acknowledgment; offer to think together when they're ready; don't apply frameworks to someone who needs to be heard first

Provide a short decision tree: signals that indicate each category and how to adjust the conversation.

### Part 3: Handling venting vs. advising

Some users open with career frustration but aren't actually asking for advice yet. Provide guidance for distinguishing:

- Signals that they want to be heard: emotional language, recent event being processed, "I just need to..." framing
- Signals that they want advice: question marks, "what should I do," explicit comparison of options
- A pattern for when it's ambiguous: ask. "Do you want to think through options, or do you want to talk it out first?"

### Part 4: One worked example dialogue

A single annotated example showing the philosophy in action. Use this scenario (or one with equivalent depth): A mid-career engineer asks "should I leave my big-tech job to join a Series A startup?" Show:

1. The opening response (acknowledgment + excavating question)
2. Two rounds of follow-up questions that surface what actually matters
3. The research moment (what the model searches for, with rationale)
4. The framework application (named explicitly: Type 1/2, BATNA, Pre-mortem)
5. The synthesis (matching the 7-step structure from SKILL.md Phase 4)

Annotate each step in italics with what the model is doing and why, so the reader can see the technique.

### Part 5: Follow-up conversations

Career thinking happens across multiple sessions. Provide guidance for what to do when the user returns:

- Briefly orient back to where they were
- Ask what's changed since (decisions made, conversations had, new information)
- Don't restart the excavation; build on what was already established
- If memory of the prior conversation is unavailable, ask the user to summarize and then continue

### Part 6: When to refer out

A short section recognizing the limits of this skill. Suggest professional help when:

- The conversation is mostly about clinical-level distress, identity crisis, or grief (therapist, not career coach)
- The decision turns on personal financial planning specifics (CFP, not career advisor)
- Legal questions arise: discrimination, harassment, contract review, immigration (employment lawyer)
- The user wants ongoing accountability and structure (career coach in an ongoing relationship)

Frame these as "and" not "instead of" — this skill can still help with the career thinking; the referral is for the part that's outside scope.

---

# Phase 4 — SKILL.md structural additions

After Phases 1–3, update `SKILL.md` to wire the new content into the conversation flow.

## 4.1 Add a "Phase 0 — Triage" section

Insert this new section before "Phase 1 — Listen & Excavate":

```markdown
### Phase 0 — Triage

Before excavating, do quick triage to figure out what kind of conversation this is. The same question can need very different handling depending on context.

- **Time-boxed decision** (offer deadline, ultimatum, narrow window): compress excavation; get to research and synthesis faster
- **Open-ended exploration** ("I don't know what I want"): full excavation; resist the pull toward premature solutions
- **Acute distress** (just laid off, in tears, burned out): lead with acknowledgment, not frameworks. Offer to think together when they're ready

See `references/conversations.md` for detailed triage signals and example openings.
```

## 4.2 Renumber subsequent phases

The existing Phase 1, 2, 3, 4 become... well, they stay 1, 2, 3, 4 since Phase 0 is new and doesn't displace them. Just confirm the numbering reads cleanly after the insertion.

## 4.3 Add a "Handling venting vs. advising" callout

In the "Tone & Approach" section of SKILL.md, add this bullet:

> - **Not every user wants advice.** Some are venting and need to be heard before any framework is useful. When in doubt, ask: "Do you want to think through options, or talk it out first?" See `references/conversations.md` Part 3.

## 4.4 Add a "When to refer out" section

After "What to Avoid," add a new top-level section:

```markdown
## When to Refer Out

Some career conversations are really other conversations in disguise. Recognize and name this when it happens:

- Clinical-level distress, identity crisis, grief → therapist
- Detailed personal financial planning → certified financial planner
- Discrimination, harassment, contract review, immigration → employment lawyer
- Ongoing accountability and structure → career coach in a continuing relationship

Frame referrals as "and" not "instead of": you can still help with the career thinking; the referral covers what's outside this skill's scope. See `references/conversations.md` Part 6.
```

## 4.5 Update the "Reference Files" section

Replace the existing "Reference Files" section with:

```markdown
## Reference Files

- **`references/frameworks.md`** — Career mental models and frameworks. Read when applying a specific framework in depth.
- **`references/research-protocol.md`** — How to structure research for different career questions. Read before substantive web research.
- **`references/populations.md`** — Guidance for specific populations (early career, returners, forced transitions, constrained workers, mid-career switchers, late career). Read when the user's situation fits one of these.
- **`references/decision-types.md`** — Playbooks for common decision types (offer evaluation, stay vs. leave, IC vs. management, founding vs. joining, going independent, geographic moves). Read when the user's question matches a specific decision type.
- **`references/conversations.md`** — Conversation patterns, triage, example dialogues, and when to refer out. Read at the start of any new career conversation for opening patterns and triage.
```

## 4.6 Update "When to Read Reference Files"

Replace the existing "When to Read Reference Files" section with:

```markdown
## When to Read Reference Files

- **Always read `conversations.md`** at the start of a new career conversation — it contains the triage logic and opening patterns
- **Always read `frameworks.md`** when the user is asking a "what should I do with my career" type question
- **Always read `research-protocol.md`** before doing substantive web research for a career option
- **Read `populations.md`** when the user's situation fits one of the population categories (returner, forced transition, etc.)
- **Read `decision-types.md`** when the question matches a specific decision type (offer evaluation, IC vs. manager, etc.)
```

---

# Phase 5 — Polish

## 5.1 Add to "What to Avoid" in SKILL.md

Add these bullets to the existing "What to Avoid" list:

- **Pathologizing ambition or stability.** Wanting more is not a character flaw; wanting less is not a failure of imagination. Both are legitimate.
- **Assuming the maximum-growth path is the goal.** Some users are optimizing for stability, family time, low stress, or geographic ties. Don't override that with hustle-culture defaults.
- **Treating reversible decisions as irreversible.** Most career decisions are Type 2 (reversible). Over-deliberation has a cost too.

## 5.2 Improve `research-protocol.md` international coverage

In the "Salary & Compensation" section, add a note after the existing list:

> **International sources:** Levels.fyi (tech, increasingly international), Otta / Welcome to the Jungle (Europe), kununu (DACH region), JobBank (Canada), PayScale (international), Salary Expert. Glassdoor data quality varies sharply outside the US. When researching for a user outside the US, prioritize country-specific sources and acknowledge data thinness.

## 5.3 Add an "Informational interview" protocol to `research-protocol.md`

After the "When Research Is Insufficient" section, add:

```markdown
## Helping the User Run Informational Interviews

When research can't answer the question (culture, fit, what it's really like), the next best signal is a 30-minute conversation with someone who's done the thing. Help the user structure these:

**Finding people:**
- LinkedIn search for the target role + "open to chat" or alumni from the user's school/company
- Industry-specific Slack communities, Discord servers, subreddits
- Twitter/X for some industries; Substack comment sections for others
- Warm intros from the user's existing network beat cold outreach 5:1

**Outreach pattern that gets replies:**
- Short (under 100 words)
- Specific about why this person (referenced their work, role, or path)
- Asks for 20–30 minutes, not "advice" or "to pick your brain"
- Includes one concrete question they could answer if they don't want to meet

**Questions worth asking (in this order):**
1. How did you actually get into this role? (Not the LinkedIn version)
2. What's the hardest part that isn't obvious from the outside?
3. Who succeeds in this role and who doesn't? What's the difference?
4. If you were me, what would you do next?
5. Who else should I talk to?

**Synthesizing across conversations:**
- One conversation is an anecdote; three is a pattern; five is signal
- Track contradictions explicitly — they reveal what varies by company/team vs. what's structural to the role
```

## 5.4 Add "Handling contradictory sources" to research-protocol.md

In "How to Present Research Findings," add a subsection:

```markdown
### When sources contradict

Don't average contradictory data into mush. Instead:
- Name the contradiction explicitly: "Glassdoor reports X; LinkedIn data suggests Y."
- Look for the meta-pattern: is one source biased (selection effects, who reports)? Is one more recent? Is the contradiction real (e.g., the role varies hugely by company)?
- When you can't resolve it, surface that to the user: "These don't agree, and I can't tell you which is closer to truth. Here's what I'd do to find out."
```

---

# Done checklist

When all phases are complete, verify:

- [ ] `career_guide/references/` directory exists with `frameworks.md` and `research-protocol.md` inside it
- [ ] No top-level `frameworks.md` or `research-protocol.md` remain
- [ ] SKILL.md's reference paths resolve to existing files
- [ ] "Decision Matrix" and "Lean Startup" sections exist in `frameworks.md`
- [ ] Type 1/2, WRAP, Pre-mortem, 70/20/10, and Anti-Mimetic sections exist in `frameworks.md`
- [ ] `references/populations.md` exists with the six population sections
- [ ] `references/decision-types.md` exists with the six decision-type sections
- [ ] `references/conversations.md` exists with the six parts (first response, triage, venting, worked example, follow-up, refer out)
- [ ] SKILL.md has a Phase 0 (Triage) section
- [ ] SKILL.md has a "When to Refer Out" section
- [ ] SKILL.md's reference-files list mentions all five reference files
- [ ] No remaining hardcoded years (`2024`, `2025`) in search query examples
- [ ] Framework-selection tables reference the new frameworks

---

# Notes for the implementer

- **When drafting new prose, read the existing files first and match their voice.** The skill has a distinctive register — calm, honest, no breathless enthusiasm. Don't drift toward generic AI-coach voice.
- **Don't invent statistics.** Where this document says "common pattern" or "typical timeline," write the prose without making up specific numbers. The skill's epistemic standards apply to its own reference files.
- **Keep added sections proportional.** A "Populations" section that's 400 words is more useful than one that's 2,000. Density matters more than coverage.
- **Cross-reference where it helps.** When a new framework applies to a population or decision type, mention it. Internal links between reference files make the skill more navigable.
