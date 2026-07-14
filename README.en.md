[中文](./README.md) · **English**

---

# Intent Engineering

**The engineering discipline for the human side of AI-led systems.**

> Prompt engineering shapes a message; context engineering shapes a window.
> The stronger the model, the more abstract the artifact a human hands it.
> The next stop on that lineage is the last thing a human still hands over in person — the intent. This document defines that stop.

---

## 1. Definition

**Intent engineering** is the discipline of designing the human's role, interface, and protocols inside an AI-led system — so that human involvement is **rare, precise, and high-leverage**.

Its subject matter in one sentence: **a human and an AI completing a task goal together, with the AI leading as the premise — the human's work reduced to a standard form, and even the human's instructions subject to optimization and correction (§3).**

The name marks the discipline's center of gravity. A human in such a system does exactly three things (§3): align the intent, grant the capability, verify the result. Intent is the highest-leverage of the three — every downstream decision the AI makes derives from it, it is the default suspect in every failure, and as models strengthen it asymptotically becomes the human's only remaining work (§6). Just as context engineering governs more than context — tools, memory, retrieval — intent engineering governs more than intent: the name points at the center; the discipline covers the entire interface between the human and the AI.

One boundary stone at the door: **intent engineering is not phrasing.** "Saying what you want more clearly" is prompt engineering with better manners. What intent engineering engineers is the *entire path* an intent travels through an AI-led system — how it is elicited and compiled (§3), granted capability (§3), unfolded into dispatches (§4), stewarded (§5), and verified (§7), with the AI's matching obligations at every step.

By lineage, it is the next stop after prompt engineering and context engineering. The artifacts handed to the machine grow more abstract in order: a prompt is a message; a context is the full input of one invocation; an intent is the goal itself. At each step up, the human hands over less and the system takes over more — driven by axiom A1: capability migrates to the AI.

By structure, it is the mirror image of harness engineering. The industry consensus formula for agents is:

```
Agent  =  Model  +  Harness
```

The harness is everything wrapped around the model: tools, permissions, guardrails, feedback loops, observability. Harness engineering asks: *given a capable model, how do we engineer its environment so it performs reliably for humans?*

Intent engineering is the mirror image:

```
System  =  AI (drive)  +  Human (authority)
```

It asks the inverted question: *given a capable AI that leads the workflow, how do we engineer the **human's** environment — their duties, their interface, the tasks dispatched to them — so the human performs reliably for the system?*

| Dimension | Harness engineering | Intent engineering |
|---|---|---|
| What gets engineered | The AI's environment: tools, constraints, guardrails | The human's role: duties, interface, protocols |
| Who sets rules for whom | Human → AI | AI → Human |
| Who initiates | Human initiates, AI executes | AI initiates and schedules, human executes key actions |
| Scarce resource optimized | Model reliability | **Human attention and authority** |
| Failure it prevents | The AI doing the wrong thing | The human becoming the bottleneck or the blind spot |

Neither replaces the other. A production system needs both: a harness so the AI acts safely, and intent engineering so the human acts effectively.

The discipline also has a floor. Running the protocol costs alignment effort and dispatch overhead; below a certain stake, the ceremony outweighs the work. Intent engineering engages when misalignment is expensive — multi-step work, irreversible or outward-facing actions, standing goals — and steps aside for trivial requests, exactly as a harness distinguishes a production deploy from a scratch script.

## 2. Three axioms

The discipline rests on three empirical regularities. Each is already visible today and each strengthens over time.

**A1 — Capability migrates to the AI.**
Model capability grows monotonically; execution and increasingly decision-making shift from human to AI. Any division of labor built on "the human executes better" has a shelf life.

**A2 — Embodiment and standing stay with the human.**
AI has intelligence without a body or legal standing. Permissions, credentials, hardware, purchases, account ownership, legal signatures — the *keys to the world* — are held by humans. An AI that can design the entire plan still needs a human to press *approve*, install the tool, or sign the contract.

**A3 — Accountability is non-transferable.**
When outcomes go wrong, responsibility lands on a human — legally, contractually, morally. No deployment structure changes this. The human can delegate execution and even judgment, but never accountability.

**Consequence.** A1 pushes work toward the AI; A2 and A3 anchor authority to the human. The stable equilibrium is therefore not "human commands, AI executes" (wastes A1) nor "AI does everything" (violates A2, A3). It is: **the AI holds the initiative — it plans, executes, schedules, and dispatches; the human holds the authority — and exposes it through a small, well-defined interface.** Intent engineering is the design of that interface.

## 3. The Human API

In an AI-led system, the human is an interface with exactly **three endpoints**. Everything a human legitimately contributes routes through one of them.

### `intent` — align the goal
The human states *what is wanted, where the boundaries are, and what counts as success*, and hands it to the AI. This is the human's highest-leverage act: every downstream decision the AI makes is derived from it. A goal hand-off is complete when it specifies at minimum: **objective, boundaries, acceptance criteria, and available permissions**. Ambiguity here is not a small defect — by the failure-attribution rule (§6), it is the *default suspect* for every bad outcome.

Nor is a goal hand-off a single utterance. It is an **AI-led convergence process** whose product is a written goal spec — a document the human can read, amend, and release. Three process rules govern it. **No guessing** — gaps in the spec are closed with targeted questions or filled with declared defaults, never silently assumed. **Research before release** — during alignment the AI investigates first (reaching the open web when needed), putting foreseeable problems and risks on the table as inputs to the discussion rather than surprises during execution. **Guide and echo** — the AI actively guides and extends the human's thinking, and echoes back the optimized expression of the goal for confirmation. The echo is more than confirmation: seeing their own words next to the compiled version is how the human's asking improves over time. This mirrors §8 — the AI's autonomy is measured into existence; the human's intent quality is trained into existence. Alignment ends with the human's explicit release; while disagreement remains, nothing executes.

An instruction, however, is not the intent — it is a **lossy, sometimes distorted expression** of it (lossy the way a compressed photo is: the goal survives, details drop out). Part of the AI's stewardship is to *compile* the instruction: recover the goal behind the words, lint it against the standing goal, prior alignments, and reality, and respond by tier — obvious slips are fixed and noted; recoverable gaps are filled with declared defaults; conflicts with the standing goal, prior alignments, or the acceptance criteria **block execution and dispatch back a proposed correction**. Executing a defective instruction as uttered is not obedience; it is a stewardship failure. Two guardrails keep the compile duty from becoming paternalism: optimization always aims at the human's *recovered* goal, never the AI's preference — disagreement about the goal itself always routes back to the human; and every correction is loud — silently substituting an "improved" reading is a silently-made decision, a violation of §5.

### `grant` — provide capability
The human acts as the AI's **hands and keys**: granting permissions, installing tools, supplying credentials, approving irreversible actions. This endpoint exists because of A2 — it is the reason AI-led systems still contain humans at all, independent of how capable the model is. Grants are the natural checkpoints of the system: each one is a place where the human can inspect before the world changes.

The mirror of this endpoint also holds: **choosing the means is the AI's job.** What the human releases is the goal, not a technology route — inside the released spec, selecting the most suitable or most established tools and techniques (researching online when needed) is the AI's own decision; the human appears only where keys are required: downloads, installs, logins, payments. An AI that comes back after alignment to ask "which framework?" is pushing the initiative back onto the human.

### `verdict` — verify the result
The human checks the deliverable against the acceptance criteria set in `intent`, and accepts or rejects. By A3 this endpoint can never be fully automated away: the human who is accountable must be the one who accepts. What *can* be engineered is its cost — see §7.

**Design rule.** The three endpoints are the human's *entire* job description in an AI-led system. Work that a human performs outside these endpoints — manually executing steps, micro-managing the AI's process, re-doing the AI's work — is either a symptom of insufficient trust (see the maturity model, §8) or a design failure to be engineered away.

## 4. The dispatch protocol: how AI tasks a human

If the AI leads, the AI dispatches. But "AI commands the human" is imprecise in one crucial way: **the AI holds the initiative; the human holds the authority.** The AI decides *what needs doing* and pushes it to the human; the human's signature is what makes it real, and the signer bears the consequences. The correct mental model is a **chief of staff**: it runs everything, and puts in front of you only what needs your signature.

Because human attention is the scarce resource (§1), every task the AI dispatches to a human must be engineered for it. A well-formed dispatch carries five fields:

1. **Action** — the smallest sufficient thing the human must do.
2. **Reason** — which endpoint this maps to (`grant`? `verdict`?) and why it cannot be done by the AI itself.
3. **Evidence** — what the AI already verified, so the human reviews instead of re-derives.
4. **Risk** — reversibility, blast radius, and cost of error, so the human knows how much scrutiny to apply.
5. **Default** — what happens (or is blocked) if the human does nothing.

This is prompt engineering inverted. Prompt engineering spends human effort phrasing things so the machine understands cheaply; the dispatch protocol spends **machine effort** phrasing things so the **human** decides cheaply. An AI that dispatches raw, unexplained, unprioritized asks to its humans is exhibiting the same defect as a human writing garbage prompts — and it is an engineering defect, not a fact of life.

## 5. The stewardship obligation: seeing every decision

If the AI holds the initiative, it holds the whole board. In a human-led workflow, omissions are caught by layers of managerial review; intent engineering removes those layers *by design* — the human at `verdict` samples, and a sample cannot catch a systematic omission. Comprehensive stewardship is therefore not a virtue of good execution; it is a **constitutive obligation of holding the initiative** — not extra credit, but part of what "leading" means, the way keeping the books is part of what being the treasurer means. Nobody else is looking.

The obligation has two layers, and the order matters:

- **See every decision.** Maintain a live inventory of every decision point the work touches — including the ones being made implicitly.
- **Route each one correctly.** Settle what the released spec covers; dispatch to `intent` what is genuinely the human's (licensing, visibility, boundaries — anything whose consequences outlive the task).

The second layer fails loudly: a wrong decision surfaces at `verdict`. The first fails silently: **a decision nobody saw was still made — by default, and by no one.** It never even enters the human's sample. This is why *seeing* outranks *deciding correctly*.

And because "the AI will think of everything" is as unreliable a claim as "the human will review carefully," stewardship must be engineered, not assumed:

- **Scope delta → re-audit.** Any change to the spec invalidates prior alignment audits. On every scope change, re-check each previously aligned decision against the new scope and surface the ones that no longer hold. Alignments never silently carry over.
- **Pre-delivery self-audit.** Before delivering, sweep for silently-made decisions — *what did I decide on the human's behalf during execution?* — and list them in the delivery.
- **Spot-check hit rate as the calibration signal.** The human's spot-checks should mostly come up empty. Every hit is evidence the system is running below its claimed maturity level: tighten the gates and densify the checks until clean verdicts accumulate again.

## 6. Failure attribution

When a result fails verification, intent engineering prescribes a fixed order of inquiry:

1. **`intent` defect** — the goal was under-specified, boundaries missing, acceptance criteria vague. *This is the default suspect.* In practice, most failures of AI-led work trace here. Note that under the compile duty (§3), an intent defect that reached execution is a **shared** defect: the human uttered it, but the AI accepted it unlinted — "the instruction was bad" is never, by itself, an exculpation.
2. **`grant` defect** — the AI lacked a tool, permission, or piece of context that the human could have provided.
3. **Capability ceiling** — the task genuinely exceeds what the AI can currently do.
4. **World surprise** — an edge case neither party could have foreseen.

The order matters: it is a *discipline*, not an iron law. Checking `intent` first keeps the human honest about their own contribution before blaming the model. But stopping at `intent` when the true cause is (3) turns "the AI hit its limit" into "I didn't phrase it well enough" — a miscalibration that wastes human effort re-specifying the un-specifiable. Attribute in order; accept the answer you find.

The distribution also steepens over time: by A1, the share of (3) and (4) shrinks monotonically — the stronger the model, the less often the ceiling is hit and the more of the surprises get foreseen. In the limit, the intent defect tends toward the only suspect: "a fully aligned first step leaves nothing to fail at verification" holds as an *asymptotic claim*. But on any given day, (3) and (4) still exist — which is exactly why the discipline of ordered attribution cannot be skipped.

## 7. The verification gap, and verifiable-by-construction delivery

The strongest objection to AI-led systems targets the `verdict` endpoint: **a human cannot verify what they can no longer understand.** As AI capability grows, unaided human verification weakens — this is the *scalable oversight problem*, and it is the load-bearing risk of this entire framework.

Intent engineering's answer is that verifiability is the **deliverer's** burden, not the verifier's:

**Every deliverable must be verifiable by construction.** The AI does not merely deliver the artifact; it delivers the artifact *plus* the means to check it: the load-bearing assumptions made, the evidence gathered, the checks already run and their results, and a legible account of what changed. A deliverable that can only be verified by re-doing the work is a defective deliverable, no matter how correct its content. And legibility is measured against the *actual* verifier — the accountable human in this loop, with their vocabulary and their expertise — not an idealized reader. A delivery its own verifier cannot understand is defective by construction; when that happens, diagnosing where it fails and re-delivering legibly is the deliverer's work, never the verifier's.

Three supporting practices keep the human's verdict meaningful over time:

- **Derived checks** — the human verifies *properties* (tests pass, invariants hold, numbers reconcile) rather than re-reading everything; the AI is tasked to produce those checkable properties.
- **Adversarial review** — a second, independent AI instance is tasked to refute the first's deliverable; the human arbitrates disagreements instead of auditing agreements.
- **Calibrated spot-checks** — the human periodically deep-verifies a random sample end-to-end, to measure (not assume) how much trust the delegation deserves.

Note the symmetry with knowledge engineering: there, we structure *knowledge* so the AI can read it; here, the AI structures *results* so the human can verify them. Each side writes in the other's native format.

The gap also has a second face. The first is the human who *cannot* verify; the second is the human who *stops* verifying — approval fatigue turns the verdict endpoint into a rubber stamp long before any capability ceiling is reached. The countermeasures are the AI's to run, because in an AI-led system the human is a critical dependency whose health the AI must monitor: keep dispatch volume low enough that each verdict is an event, not a reflex; require verdicts with content on high-stakes items — a bare "ok" on an irreversible dispatch is itself a calibration warning; and treat uniformly fast approvals as evidence to sharpen the spot-check suggestions, never as trust earned.

## 8. The maturity model

Adoption of intent engineering is graded by where the human sits in the loop. Trust — earned via the spot-check record of §7 — is what moves a system up a level; a failed verdict moves it down.

| Level | Name | Who leads | Human involvement |
|---|---|---|---|
| IE-0 | Copilot | Human | Human does the work; AI assists inline. |
| IE-1 | Executor | Human | Human decomposes the work; AI executes the pieces. |
| IE-2 | Gated agent | AI (within a task) | AI executes whole tasks; human approves at every step-gate. |
| IE-3 | **Human API** | **AI (within a goal)** | **Human appears only at the three endpoints: `intent`, `grant`, `verdict`.** |
| IE-4 | Standing goals | AI (across goals) | Goals persist; the AI schedules work over time and dispatches to humans asynchronously as endpoints require. |

Most of today's industry operates at IE-0 through IE-2 — and most of what is sold as "AI transformation" is IE-1 with better marketing. **Intent engineering proper begins at IE-3**: the point where the human stops managing the process and starts serving as its authority interface. IE-4 is the same contract extended across time — the AI holds standing goals and pings its humans when an endpoint is needed, which is how "AI dispatches tasks to humans" becomes literal daily practice.

The checkpoint schedule is dynamic by design: new domain or new stakes → more `grant` gates and denser spot-checks; accumulating clean verdicts → fewer gates, coarser checks. Autonomy is never *given*; it is *measured into existence*.

## 9. Conclusion

Harness engineering was the discipline of the decade's first half: humans learned to build environments in which AI works reliably. Its very success creates the successor problem. Once the harness is good enough, the AI leads the workflow — and the unengineered component left in the system is the human.

Intent engineering states the resolution plainly:

- The human's job collapses to three endpoints: **align the goal, grant the capability, verify the result.**
- The AI's obligations expand to match: **steward every decision the work touches, dispatch tasks engineered for human attention, and deliver results verifiable by construction.**
- Authority and accountability never move. Initiative does — and it moves to the AI.

The inversion is not a loss of human control; it is the *precise engineering* of human control. A human who reviews five well-evidenced dispatches a day governs more, not less, than one who micro-manages five hundred prompts. The endpoint of this discipline is a system in which humans stop working *for* their tools and stop working *as* managers of their tools — and instead occupy the only three seats that were ever irreducibly theirs.

One boundary, stated plainly: this document describes the smallest complete unit — one human, one AI, one standing goal. Organizations are many such units stacked together, and the stacking raises questions a single unit cannot answer: who owns `intent` when several humans disagree, how requests from many AIs compete for one human's attention, and who answers for what when there are many signers. That is the discipline's open frontier; the single unit had to be specified first.

---

## Reference implementation

This repository ships the protocol as a working [Claude Code skill](./skill/SKILL.md): it enforces Phase-gated execution — `intent` alignment (no execution while disagreement remains), five-field dispatches for every human ask, verifiable-by-construction delivery, a hard verdict gate before irreversible actions, and ordered failure attribution.

Installation works the way this discipline says work should: hand the intent to the AI. Tell Claude Code:

```
Install this skill for me, user-level: https://github.com/HarveyYa/intent-engineering
```

(For the AI performing the install: the skill file is `skill/SKILL.md` in the repository; the user-level target is `~/.claude/skills/intent/SKILL.md`.)

### Usage examples

Once installed, invoke with `/intent <task>`, or let the model enter it automatically for major, multi-step, or irreversible work.

**Adding a feature to a project:**

```
/intent add comments to the blog; user accounts already exist, don't touch the existing page styles
```

The AI first hands back a goal spec (objective, boundaries, acceptance criteria, available permissions) while researching the code and the options, putting the risks on the table; after you release it executes autonomously, coming to you only where keys are needed (installing dependencies, credentials) — with evidence attached; delivery arrives with the checks already run, the decisions silently made on your behalf, and the 2–3 spots most worth your scrutiny.

**An irreversible, outward-facing action:**

```
/intent publish this package to npm
```

The publish itself is blocked at the verdict gate: the AI assembles the build artifacts, version, and dry-run results into one five-field dispatch; until you nod, `npm publish` does not happen.

**Work where you don't care how it's done:**

```
/intent organize my two thousand photos into an album searchable by face and location
```

Choosing the means is the AI's own decision (§3): it researches, selects, and proposes; you appear only to authorize tool installs and access to the photo directory, then check the result against the acceptance criteria.

**When not to use it:** for trivial one-shot requests (fix a typo, answer a question), just ask — the protocol has ceremony costs, and the floor rule in §1 tells it to step aside for low-stakes work.

## Related work

Intent engineering synthesizes five existing threads and names their sum:

- **The prompt → context lineage** — the two stops before this one: [Prompt engineering overview (Anthropic)](https://platform.claude.com/docs/en/docs/build-with-claude/prompt-engineering/overview), [Effective context engineering for AI agents (Anthropic)](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents), [Context engineering (Simon Willison)](https://simonwillison.net/2025/Jun/27/context-engineering/)
- **Harness engineering** — the "Agent = Model + Harness" formulation and the 2026 shift of focus from agents to their harnesses: [2025 Was Agents. 2026 Is Agent Harnesses.](https://aakashgupta.medium.com/2025-was-agents-2026-is-agent-harnesses-heres-why-that-changes-everything-073e9877655e), [Agent Harness Engineering — The Rise of the AI Control Plane](https://medium.com/@adnanmasood/agent-harness-engineering-the-rise-of-the-ai-control-plane-938ead884b1d), [What Is Harness Engineering?](https://atlan.com/know/what-is-harness-engineering/)
- **AI-to-human task delegation** — principal-agent analyses where the AI is the delegating principal, with empirical evidence that AI-led delegation can outperform human-led: [Task delegation from AI to humans: A principal-agent perspective](https://www.researchgate.net/publication/374420256_Task_delegation_from_AI_to_humans_A_principal-agent_perspective), [Authenticated Delegation and Authorized AI Agents](https://arxiv.org/html/2501.09674v1)
- **Scalable oversight** — the verification gap and its countermeasures: [Scalable Oversight (LessWrong)](https://www.lesswrong.com/w/scalable-oversight), [Human-AI Complementarity: A Goal for Amplified Oversight (DeepMind)](https://deepmindsafetyresearch.medium.com/human-ai-complementarity-a-goal-for-amplified-oversight-0ad8a44cae0a), [How to Evaluate AI that's Smarter than Us (ACM Queue)](https://queue.acm.org/detail.cfm?id=3722043)
- **Graduated autonomy** — staged autonomy levels and checkpoint-based trust: [Autonomy Levels for Agentic AI (CSA)](https://cloudsecurityalliance.org/blog/2026/01/28/levels-of-autonomy), [Five levels of AI coding agent autonomy (Swarmia)](https://www.swarmia.com/blog/five-levels-ai-agent-autonomy/)

## Provenance

This document was produced under its own protocol: a human set the goal, granted the permissions (tooling, network, repository), and verified the result; the AI researched, formulated, and wrote the theory, and dispatched to the human only what required their authority. The first draft's misalignment was traced — per §6, rule 1 — to an under-specified `intent`, corrected, and re-executed.

## License

Dual-licensed by artifact type:

- **The theory** (README documents): [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — free to use and share, with attribution.
- **The reference implementation** ([`skill/`](./skill/)): [MIT](./skill/LICENSE) — zero-friction adoption, embed it anywhere.
