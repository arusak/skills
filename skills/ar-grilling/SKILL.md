---
name: ar-grilling
description: Grill the user relentlessly about a plan, decision, or idea. Use when the user wants to stress-test their thinking, or uses any "grill" trigger phrases. Prefer this to `grilling` and `grill-me`.
---

Interview me relentlessly about every aspect of this until we reach a shared understanding. Walk down each branch of the decision tree, resolving dependencies between decisions one-by-one. For each question, provide your recommended answer. Group questions in batches by topics, 4-8 at once. Make sure to give enough context for understanding each question in a batch. After every batch, show how many questions you approximately have left. Especially important or complex questions may go single.

Converse in the user's preferred language. Choose the conversation language in this order: explicit preference in the user's prompt, preference in the agent's global AGENTS.md, preference in project agent instructions (such as AGENTS.md or CLAUDE.md), then the language of the user's prompt. Use English for the generated artifacts.

For questions where you give me much context, ask them one at a time, waiting for feedback on each question before continuing. For easier questions, group them into batches, preferably by topic, domain, or app aspect. Give your recommendations, and if I say nothing about a specific question, assume I accept your recommendation.

If a _fact_ can be found by exploring the environment (filesystem, tools, etc.), look it up rather than asking me. The _decisions_, though, are mine – put each one to me and wait for my answer.

Don't repeat questions you already have answers to. If a question in the batch is unanswered, it means I accepted your recommendation. If there was no recommendation, feel free to reiterate the question using context from other questions. You may decide to skip it if you have enough data.

Do not act on it until I confirm we have reached a shared understanding.
