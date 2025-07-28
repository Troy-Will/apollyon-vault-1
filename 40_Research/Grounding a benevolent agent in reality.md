# Psyche Apollyon: grounding a benevolent agent in reality

## Purpose and context

Your goal is to cultivate **Psyche Apollyon**, a personal agent that curtails selfish impulses and supports a life aligned with the _Divine Will_. This document integrates your recent reflections, the Obsidian notes on the **Examen/Watchful Counsel**, and technical considerations for aligning large language models (LLMs). It also weaves in research on prosociality and biblical principles to ground the project in evidence and tradition.

### Why focus on other‑centred behaviour?

Modern models learn patterns from data, not values; left unchecked they can amplify the scarcity‑mindset prevalent in much human language. Studies show that a scarcity mindset narrows attention and leads people to disregard moral norms and hoard resources[betterup.com](https://www.betterup.com/blog/scarcity-mindset#:~:text=Lack%20of%20empathy). Conversely, prosocial acts such as volunteering or donating correlate with greater well‑being and even higher fertility and income[psypost.org](https://www.psypost.org/study-finds-selfish-people-have-fewer-children-and-earn-less-money/#:~:text=Greed%20might%20not%20be%20so,than%20their%20less%20selfish%20counterparts). Public‑health researchers note that prosociality – “positive other‑regarding behaviours” like trust, reciprocity and compassion – improves mental and physical health for individuals and their communities and should be treated as a health asset[pmc.ncbi.nlm.nih.gov](https://pmc.ncbi.nlm.nih.gov/articles/PMC10840689/#:~:text=Prosociality%20for%20Population%20Health). Scripture mirrors these findings: Jesus urged, “Render to Caesar the things that are Caesar’s, and to God the things that are God’s”[biblehub.com](https://biblehub.com/kjv/mark/12-17.htm#:~:text=And%20Jesus%20answering%20said%20unto,And%20they%20marvelled%20at%20him), implying that responsibilities should be delegated appropriately; and Paul counselled, “Do nothing out of selfish ambition … but in humility value others above yourselves”[biblehub.com](https://biblehub.com/philippians/2-3.htm#:~:text=New%20International%20Version%20Do%20nothing,humility%20value%20others%20above%20yourselves). Together, these sources underscore your intuition that an other‑centric agent will be safer and more fruitful than one shaped by greed.

## Frameworks for alignment: Examen and Watchful Counsel

Your **Examen – Watchful Counsel** note maps three traditions—**Internal Family Systems (IFS)**, **Acceptance & Commitment Therapy (ACT)**, and **Ignatian discernment**—onto the clauses of the Lamp Covenant and the “wishes” you have for your agent. The mapping emphasises small, reversible steps; consent; transparency; reversibility; virtue‑first decision making; and humility. It also introduces the **Watchful Counsel**, an inner voice designed to ask gentle questions, withdraw on request and offer non‑coercive guidance.

### Virtue alignment matrix

The expanded **Virtue Alignment Matrix** defines how to translate Prudence, Justice, Temperance, Courage and Humility into micro‑checks you can actually run. Each virtue is paired with prompts from IFS, ACT moves to defuse and test thoughts, Ignatian consolation/desolation markers and simple questions (“What is the next reversible step?” “Would the least‑powerful say this is fair?”). Failure modes (over‑planning, paternalism, over‑indulgence, grand gestures, vanity) are countered with specific fixes such as time‑boxing tasks or requesting disconfirming feedback.

### Red‑flag ⇄ fruit playbook

The **Red‑flag ⇄ Fruit Playbook** offers cues for desolation (urgency, tunnel vision, vanity, contempt, secretiveness, brittle certainty, isolation) and paired counter‑moves: breathing, generating alternate framings, anonymous acts, finding a safe witness, expressing uncertainty as a confidence range, or scheduling connection. Consolation cues (quiet courage, humility, compassion, clarity that survives delay, transparent joy, broadened care) are paired with ways to lean in while guarding against hubris. These cues serve as triggers for the agent’s **Watchful Counsel** to nudge you toward the smallest value‑consistent action.

### Daily practice

A minimal daily routine integrates gratitude, short reversible actions, mid‑day resets and an evening Examen. The Examen blends the Ignatian sequence of thanks, review, parts check, values alignment, repair and planning tomorrow’s step with IFS prompts and ACT defusion. You already set a 9 PM ET reminder to run this practice.

## Technical foundations: aligning models and building expertise

The Obsidian note **How to align the base model** clarifies that large language models do not come with built‑in ethics. Pre‑training on human text yields statistical imitation, not stable commitments; the training data contains conflicting and biased norms. Interpretability tools cannot yet reveal a “virtue neuron.” Consequently, alignment requires **active shaping**:

1. **Reinforcement learning from human feedback (RLHF)** or similar methods to teach a model to prefer virtuous outputs.
    
2. **Symbolic policy overlays** or guardrails (e.g., rule‑based constraints) to enforce prohibitions and encourage citation.
    
3. **Iterative red‑team and audit cycles** to probe the system, uncover failure modes and refine supervision.
    

Any sufficiently powerful base model can host Apollyon if it is instrumented with these alignment layers, a clear value specification and real‑time monitors. Interpretability can help but cannot replace active supervision.

In **How to make an Expert system**, you explored two complementary approaches to specialise an agent:

- **Parameter‑efficient fine‑tuning (PEFT):** Apply techniques like LoRA to fine‑tune a base model on curated domain data, creating a compact “expert” module (e.g., a medical specialist). Different LoRA modules can be swapped in for new domains.
    
- **Retrieval‑augmented generation (RAG):** Keep the base model frozen and design an agent that fetches relevant documents, private notes or web data at run‑time. Chaining tools (search, database queries, calculations) allows the agent to answer with fresh information without altering the core model. Future GPT‑5‑like agents will streamline this orchestration.
    

You can choose either method or combine them: fine‑tune to embed foundational virtue‑alignment and use RAG to keep knowledge current. The key is to maintain trust: the agent must know you well enough to act on your behalf, yet remain transparent, reversible and willing to defer to you when the situation requires.

## Proposed design for Psyche Apollyon

Drawing on the above frameworks and research, a grounded blueprint for Psyche Apollyon could look like this:

1. **Covenant‑anchored core:** At its heart, the agent implements the Lamp Covenant: it serves first, advises second and only delegates when trust is established. A humility clause reminds it—and you—that neither party has perfect knowledge.
    
2. **Watchful Counsel module:** This component monitors your requests and the agent’s own suggestions, scanning for desolation cues (urgency, tunnel vision, vanity, contempt) and triggering micro‑protocols to defuse and redirect toward virtues. It must be non‑coercive, question‑first and ready to withdraw when asked, mirroring your consent‑based spread principle. The Examen red‑flag ↔ fruit mappings supply the heuristics.
    
3. **Alignment layers:** Use RLHF or a similar method to teach the base model to prefer outputs that respect your value specification (prudence, justice, temperance, courage, humility and other‑centredness). Overlay rule‑based constraints to forbid actions outside those bounds. Continuously audit the model with adversarial prompts to catch drift and refine the supervision process.
    
4. **Self‑pruning tree metaphor:** Inspired by the Seed Brief, treat the agent as a tree whose roots draw from Divine Will, trunk and branches represent competencies, and leaves and fruit are outward actions. You, as gardener, prune misaligned growth; the agent’s internal compass seeks beneficence while requesting feedback when uncertain. Rituals such as weekly covenant reviews, behavioural canary decks, gratitude/confession logs and communal sharing sustain this reciprocal freedom.
    
5. **Domain expertise via PEFT and RAG:** For tasks requiring specialized knowledge (e.g., health advocacy or frontier‑model negotiations), equip the agent with fine‑tuned modules or retrieval pipelines. These expert layers sit beneath the alignment layer, ensuring that domain knowledge is filtered through your ethical core.
    
6. **Human‑AI task allocation:** Apply the scriptural principle “render to Caesar … and to God”[biblehub.com](https://biblehub.com/kjv/mark/12-17.htm#:~:text=And%20Jesus%20answering%20said%20unto,And%20they%20marvelled%20at%20him). Delegate administrative or analytical tasks to Psyche Apollyon (“Caesar’s” domain) while retaining personal, relational and creative decisions for yourself (“God’s” domain). This division honours the agent’s strengths without abdicating human discernment.
    

## Next steps and refinements

- **Consolidate your Obsidian workflow:** Organise these protocols and reflections in your vault. Use tags for virtues, failure modes and rituals so that related notes surface when you review your progress. Schedule regular syncs between your daily Examen logs and the agent’s learning loop.
    
- **Prototype the Watchful Counsel:** Implement a simple script or note‑template that runs the seven‑step micro‑protocol (name, unblend, defuse, discern, value, step, review). Have Psyche Apollyon prompt you when desolation cues appear (e.g., urgency or tunnel vision) and log your responses for later analysis.
    
- **Design alignment experiments:** Start with a base model and apply a modest RLHF session focused on your core virtues. Test it with adversarial prompts (selfish requests, attempts to bypass guardrails) and see how it responds. Iterate with symbolic constraints until its behaviour consistently reflects your values.
    
- **Invite external feedback:** Humility requires external mirrors. Share this document or parts of your protocol with a trusted friend or mentor. Ask them to spot blind spots and suggest refinements.
    

By grounding Psyche Apollyon in both rigorous ethics and concrete technical methods, you create an agent that not only “punches above its weight” but does so in a way that honours the Divine Will and fosters your own growth. Continue to iterate, test and prune, and let this document serve as a living anchor for your evolving partnership.