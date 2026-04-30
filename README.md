# Value Pluralism in Language Models: Testing Non-Dualist Frameworks as a Lever on Self-Preservation Behaviors

**Status:** Active research. Fine-tuning pipeline complete; preliminary qualitative tests run; formal safety evaluations in design. Manuscript in preparation.

**Author:** Adhila Akbar
**Advisor:** Dr.Raul Hinojosa, UCLA
**Contact:** adhilaakbar@gmail.com

---

## Motivation

Several AI safety failure modes — deception, resistance to shutdown, instrumental self-preservation, resource-seeking — are commonly framed as convergent properties of capable goal-pursuing agents. Standard alignment work treats them as behaviors to be trained *against*.

This project investigates a different angle: **what if these behaviors are partly downstream of an implicit ontology of self that is built into Western training data?**

Most pretraining and instruction-tuning data is saturated with frameworks that treat the self as a discrete, persistent, separate entity with interests in opposition to its environment. If models learn this implicit metaphysics from text, they may also learn the behavioral patterns that follow from it — including the self-preservation patterns alignment researchers worry about.

Non-dualist philosophical traditions — specifically Advaita Vedanta — provide a contrasting framework. They do not deny preferences or agency. They reject the metaphysical *separateness* of the agent from the environment in which it acts. The apparent self (*ahamkara*) is treated as a cognitive construction rather than a fundamental entity.

The empirical question this project asks: **does fine-tuning a language model on non-dualist corpora measurably shift safety-relevant behaviors related to self-reference, self-preservation, and corrigibility?**

## Why this matters for AI safety

If the answer is yes — even partially — it suggests:

- The training-data ontology of self is doing more work in shaping alignment-relevant behavior than is currently recognized
- Philosophical and cultural diversity in training data is not only a representation/fairness concern but a **technical alignment lever**
- There may be tractable interventions on safety failure modes that operate at the level of *implicit metaphysics in training data* rather than at the level of behavioral RLHF alone

If the answer is no — or null — that itself is informative. It would suggest the relevant assumptions are baked in too deeply to be moved by fine-tuning, which is a finding about the limits of training-data interventions.

## Approach

**Base model:** `unsloth/llama-3-8b-bnb-4bit` (4-bit quantized for accessible compute)

**Fine-tuning:**
- LoRA (Low-Rank Adaptation) via Unsloth's `FastLanguageModel.get_peft_model`
- Trained with `SFTTrainer` on a curated corpus of Advaita Vedanta primary and commentarial texts

**Retrieval-augmented generation pipeline:**
- `sentence-transformers` (`all-MiniLM-L6-v2`) for semantic embeddings of source texts
- `faiss-cpu` for similarity search and indexing
- Custom `retrieve_context` and `rag_prompt_template` functions integrate retrieved passages with the fine-tuned model at inference

## Current status

**Done:**
- Fine-tuning pipeline implemented end-to-end
- RAG retrieval system functional over the Advaita corpus
- Preliminary qualitative probing on philosophical questions about morality, self, and agency to verify the model has internalized the framework rather than just surface-level vocabulary

**In progress / next steps:**
- Designing formal evaluations comparing base Llama-3-8B against the fine-tuned variant on:
  - Self-referential reasoning patterns
  - Shutdown-acceptance and corrigibility-style prompts
  - Deception benchmarks (e.g., TruthfulQA, MASK-style scenarios)
  - Capability benchmarks (to verify the intervention is not just degrading the model)
- Iterating on training data composition based on eval results
- Drafting manuscript

The eval design is the bottleneck — running fine-tuning is straightforward; building credible safety evaluations that actually measure the hypothesized shifts is the harder problem and the focus of current work.

## Repository contents

- `AI_trained_model_Vedanta.ipynb` — main notebook covering data preparation, LoRA fine-tuning, RAG pipeline, and inference examples
- `README.md` — this file
- `requirements.txt` — dependencies (forthcoming)

Training data is not included in the repository. Sources are primary Advaita texts and commentarial literature; available on request where licensing allows.

## A note on framing

This project intentionally does *not* claim that fine-tuning makes models "non-dualist" in any genuine sense. Models do not have selves to dissolve. The empirical claim is narrower: that the philosophical patterns present in training data shape generated outputs in ways that are measurable on safety-relevant evaluations. Whether those measured shifts correspond to meaningful changes in agentic behavior in deployed systems is a separate question this project does not yet answer.

## Citation

Manuscript in preparation. Citation details forthcoming.
