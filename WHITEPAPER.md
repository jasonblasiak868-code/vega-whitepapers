# Governance Above the Model
## A plain-language white paper on the AI paradox and a way to narrow it

**Jason Blasiak · October 2026 · Patent pending (U.S. provisional application 64/178,949 and others)**

---

## 1. The problem in one page

An AI that can only talk is easy to live with. An AI that can *do* things, send the email, move the money, change the file, call the service, is where the trouble starts. We want that power because it is what makes AI useful. We fear it for the same reason.

That is the paradox:

> **The more an AI can do for you, the more it can do to you.**

The usual answers do not break the paradox. They move it.

- **"We trained it to be careful."** Training changes how likely a model is to behave a certain way. It gives no guarantee, and you cannot inspect it.
- **"We wrote a policy."** A policy is a promise. Nothing stops the model, or a hacker steering it, from acting against it.
- **"The model checks itself."** The thing being checked is the thing doing the checking. If it is wrong, or manipulated, the check is wrong too.
- **"A human reviews everything."** Then the human is a bottleneck who stops reading and clicks yes. Approval becomes noise.

What is missing is not a smarter model. It is a way for a person to stay in charge that does not depend on the model behaving.

## 2. The idea: spend authority one action at a time

Think about how a bank treats a large wire transfer. The teller cannot do it alone, however trusted. A named person has to authorise *that* transfer, once, and the bank keeps the record.

Governance above the model works the same way:

1. **The model may think freely.** It can read, reason, plan and draft. None of that touches the world.
2. **Acting needs a commitment.** A *commitment* is a small signed note from a human that says: *this exact action, with these exact details, for a short time, once.* It is signed with a key the model never holds.
3. **A gate checks the note.** Before anything leaves the system, a gate checks that a valid commitment exists for exactly this action. No note, wrong details, expired or already used: the gate refuses. A failure of the gate itself also refuses. It fails closed.
4. **Everything is recorded.** Each step is added to a chain of records where every entry includes a fingerprint of the one before. Changing the past breaks the chain, and anyone can check that without trusting us.

Two properties do the work. **Authority is single-use**, so one approval cannot be replayed to do something else. And **authority is non-transitive**, so a model, a plug-in or another agent cannot create more of it or hand it on.

```
        ┌──────────────┐        ┌──────────────┐        ┌──────────────┐
 input ─▶│  ENTRY GATE  │──▶ MODEL ──▶│  EXIT GATE   │──▶ the world
        └──────────────┘ (reasons,  └──────▲───────┘
                          plans,           │ only with a human-signed,
                          drafts)          │ single-use commitment
                                     ┌─────┴──────┐
                                     │   HUMAN    │ key never on the model's side
                                     └────────────┘
        every step ──▶ append-only record (each entry fingerprints the last)
```

## 3. What is in the kits

This project is a family of small, separate software kits. Each does one job and can be used alone. Together they cover the path from "a person decides" to "the world changes" to "anyone can verify what happened".

- **Authority.** The commitment itself, the gate that enforces it, and a rule that no agent can mint or widen authority. (*governance-jacket, two-gate*)
- **Record.** The tamper-evident chain of custody, and sealed evidence with layers of protection that can be chosen to suit what is being protected. (*custody, superproof*)
- **The doorway.** An adapter between your system and anything outside it. What the owner announced is let through. Anything else is held in a dead-end room that holds nothing, answers from a fixed script and can reach nothing, so an unknown agent learns nothing and takes nothing. (*pareah*)
- **Knowledge and learning.** A graph of what the system knows, with the origin and licence of each fact, and training that records exactly what a model learned from, including keeping test data separate. (*dkg-lattice, train, librarian*)
- **Reasoning you can check.** Checks that run before an action, an audit of the reasoning, and traces of what happened. (*reasoning, metacog, trace*)
- **Seeing and steering.** A visible map of the knowledge, a governed terminal and a live governance feed. (*galaxy, terminal, governance-feed*)
- **The whole.** A registry and an audit tool that check the family fits together. (*umbrella*)

## 4. Which worries it speaks to

| A common concern | What the design does about it |
|---|---|
| "Who approved that?" | Every action needs a named human's single-use commitment; the record shows which. |
| "Can the AI give itself permission?" | No. Only the human's key can sign; authority cannot be passed on. |
| "Can I trust the log?" | You do not have to: each entry fingerprints the one before, so tampering shows. |
| "What if something hostile connects?" | It is held in the dead-end room and recorded. |
| "What did the model learn from?" | The training record names the data, its licence and the held-out tests. |
| "Did it really read what it says it read?" | Statements that something is absent are held back unless the reading is accounted for. |

## 5. What this is not

Honesty matters more than a good pitch.

- **It does not make a model aligned, truthful or kind.** It limits what a model can do, not what it believes.
- **It is not a finished product.** These are working reference implementations with tests. They show the architecture; they are not hardened for production.
- **No expert has reviewed the cryptography.** The code is plain software written for clarity. Do not protect real secrets with it before an independent review.
- **The hardware parts are designs, not chips.** The silicon and photonic versions exist as models and descriptions.
- **The human is still the weak point.** If a person approves carelessly, the gate cannot help. The design tries to make approvals specific and small so that careless approval is harder, but it cannot remove the human.
- **The law is not settled.** The licence is a draft not yet reviewed by an attorney, and nothing here is legal advice.

## 6. Try it

Each kit has a README with a quick start and runs its own tests. Start with **vega-umbrella-sdk** for the map of the family, then **vega-governance-jacket-sdk** for the commitment and the gate.

**Licence.** Source-available. Free for personal use and for registered small businesses; otherwise a commercial licence. See the LICENSE file in each repository. Commercial and registration questions: jasonblasiak.ai.mail@gmail.com.

---

*This paper describes the design and the reference code. It makes no claim about any particular deployment.*
