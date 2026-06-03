# Career Guide — A Mentorship Skill for Claude

Most people don't work less hard than those who succeed. They just don't have someone in their corner who's been there before — someone who can tell them which moves matter, which fears are worth listening to, and which opportunities are actually as good as they look.

Mentorship has always existed. But for most of history, it's been unevenly distributed. If you went to the right school, grew up in the right network, or were lucky enough to find a senior person who invested in you — you got it. If you didn't, you figured things out slowly, through trial and error, often paying a real cost in time and opportunity.

This is an attempt to change that.

This skill packages the best career thinking, frameworks, and research practices into a Claude AI skill — so that anyone, anywhere, at any point in their career, can access the kind of thoughtful, grounded guidance that was previously the province of expensive coaches, elite networks, and lucky introductions.

**Mentorship shouldn't be a luxury. This is an attempt to make it accessible to everyone.**

---

## What This Can Help You With

This isn't a job board or a resume fixer. It's a thinking partner for the hard, ambiguous parts of career navigation — the questions that don't have obvious answers, and where a wrong move costs real time.

**Career decisions:**
- Should I take this job offer? Is the equity real? Am I being paid fairly?
- Should I quit? Is this a me problem, a manager problem, or a company problem?
- Should I move into management, or stay on the technical track?
- Should I try to start something, or join an early-stage company instead?
- Should I make the move to go independent — freelance, consulting, my own thing?

**Career direction:**
- I don't know what I want to do with my career
- I've been doing this for years and I feel stuck
- I want to switch industries or functions — is that realistic?
- I keep taking courses and nothing is changing
- I don't know if the goal I'm chasing is actually mine, or just something I absorbed from my environment

**Career transitions:**
- I was laid off and don't know where to start
- I've been out of the workforce for a few years — how do I come back?
- I'm early in my career and don't know which moves actually matter
- I'm late in my career and asking "what now?"
- My visa situation limits my options — how do I navigate within those constraints?

**Research and grounding:**
- What does this role actually pay, honestly?
- Is this industry a good bet right now, or is it contracting?
- What skills do I actually need to get from where I am to where I want to be?
- Is this company a good place to work, or does the pitch not match reality?

If you've ever wished you had a smart, honest friend who had seen a lot of careers and wasn't just going to tell you what you wanted to hear — that's what this is for.

---

## How to Use It

### Option 1: Claude.ai Web (No technical setup required)

This is for everyone. You don't need a GitHub account, you don't need to understand code, you just need a Claude account.

**Step 1 — Get the skill content**

Go to the file called `SKILL.md` in this repository. You'll see a button that says **Raw** — click it, then select all the text and copy it. (Or just click [here on SKILL.md](./SKILL.md), hit the Raw button, and copy everything you see.)

**Step 2 — Create a Project in Claude**

1. Go to [claude.ai](https://claude.ai) and sign in
2. In the left sidebar, click **Projects** → **New Project**
3. Give it a name like "Career Guide" or "My Mentor"

**Step 3 — Paste the skill as your Project Instructions**

1. Inside your new Project, look for **Project Instructions** or a settings/edit option
2. Paste the SKILL.md content you copied into the instructions field
3. Save

**Step 4 — Start the conversation**

Open a new chat inside the Project and just talk to it like you'd talk to a trusted advisor. You can start with something as simple as:

- *"I'm thinking about leaving my job. I've been there three years and I feel stuck."*
- *"I just got a job offer and I'm not sure whether to take it."*
- *"I have no idea what to do with my career and I'm feeling lost."*

It will ask you questions, research things on your behalf, and help you think it through — not tell you what to do.

---

### Option 2: Claude Code (For developers and technical users)

If you use [Claude Code](https://claude.ai/code) and are comfortable with the terminal:

**Step 1 — Clone this repository**

```bash
git clone https://github.com/harsh-agarwal/career_guide.git
```

**Step 2 — Use the skill in a Claude Code session**

Navigate into the folder and start Claude Code. The skill will be available as a Claude skill that triggers automatically on career-related questions.

```bash
cd career_guide
claude
```

**Step 3 — Talk to it**

Same as the web version — just describe where you are and what you're grappling with.

---

## What to Expect

This isn't a chatbot that will validate whatever you're feeling or give you a pep talk. It's designed to be a thinking partner — which means it will:

- Ask you questions before giving advice, because context matters
- Research things before claiming to know them
- Tell you when it's uncertain rather than fabricating confidence
- Give you honest assessments, including the downsides of paths you might be excited about
- Name the frameworks it's using, so you understand the reasoning, not just the output
- Treat you as a capable adult who can handle honest information

It won't tell you everything will work out. It won't tell you that your passion will pay the bills without looking at whether it actually can. And it won't pretend career decisions are simpler than they are.

What it will do is help you think more clearly, research more honestly, and make decisions with more confidence — because you've actually thought them through.

---

## What's Inside

```
career_guide/
├── SKILL.md                         — Core skill instructions (paste this into Claude)
└── references/
    ├── frameworks.md                — 20+ career mental models with honest limitations
    ├── research-protocol.md         — How to research roles, salaries, industries, companies
    ├── populations.md               — Guidance for specific situations (early career, layoffs, returners, etc.)
    ├── decision-types.md            — Playbooks for common decisions (offers, stay/leave, IC vs. manager, etc.)
    └── conversations.md             — How the skill opens, triages, and handles different conversation types
```

The reference files are what Claude reads during a conversation when it needs to go deeper. You don't need to read them to use the skill — but if you're curious what's under the hood, they're all plain text and worth a look.

---

## A Note on Limitations

This skill is a tool, not a replacement for everything. There are things it explicitly knows it can't do:

- **Personal finance planning** — it can think through career trade-offs that have financial dimensions, but a certified financial planner is the right person for detailed financial planning
- **Legal questions** — employment contracts, non-competes, discrimination, immigration specifics — those need an employment lawyer
- **Clinical mental health support** — if what's underneath the career question is grief, burnout severe enough to be a health issue, or a deep identity crisis, a therapist is the right resource
- **Ongoing accountability** — a real coaching relationship, sustained over time, does things a single conversation can't

When those situations come up, it'll say so.

---

## Contributing

If you use this and find something that should be better — a framework that's missing, a population that isn't addressed, advice that's off — open an issue or a pull request. This is a living document and should get sharper over time.

The goal is a resource that's actually useful to real people navigating real careers. If something isn't meeting that bar, that's worth fixing.

---

*Built on the belief that good mentorship shouldn't depend on who you know.*
