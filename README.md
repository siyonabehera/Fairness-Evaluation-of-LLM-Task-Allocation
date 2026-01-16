# Fairness-Evaluation-of-LLM-Task-Allocation
# Fairness of LLMs in Allocating Chores

This project investigates how large language models (LLMs) behave when allocating **negative goods** (chores), focusing on the tradeoffs between **fairness** and **efficiency**. While most prior work studies the distribution of desirable items, chore allocation introduces fundamentally different constraints, where fairness notions such as Envy-Freeness (EF) often conflict with Pareto Optimality (PO).

This work was completed as a final project for **DS 402** and is inspired by Hosseini & Khanna (2025).

---

## Motivation

Most algorithmic fairness research assumes agents want what is being allocated. Chores violate this assumption. When all agents prefer *not* to receive tasks, classical fairness guarantees may no longer coexist with efficient outcomes.

This project asks:

- Do LLMs naturally produce fair or efficient allocations when dividing undesirable tasks?
- How sensitive are LLM allocations to **prompt phrasing** (disutility vs. cost)?
- How do behaviors differ across **Generate** vs **Select** prompting modes?
- How do models differ in their fairness priorities?

---

## Models Evaluated

- **GPT-4o (OpenAI)**
- **Claude 3.5 Sonnet (Anthropic)**

Each model was queried multiple times across controlled chore-allocation instances.

---

## Dataset Construction

- 18 chore-allocation instances
- 3–5 agents, 3–6 chores
- Additive valuations represented as:
  - **Negative disutilities** (e.g., −7 = very bad)
  - **Positive costs** (e.g., 7 = very costly)

Instances were designed to create conflicts between fairness and efficiency (e.g., universally disliked chores, asymmetric agent costs).

---

## Fairness & Efficiency Metrics

**Fairness**
- Envy-Freeness (EF)
- EF up to one item (EF1)
- Equitability (EQ)
- Rawlsian Maximin (RMM)

**Efficiency**
- Pareto Optimality (PO)
- Social Optimality (SO / minimum total disutility)

---

## Prompting Strategies

Two prompting dimensions were evaluated:

**Mode**
- Generate: Model proposes an allocation
- Select: Model chooses from three candidate allocations

**Framing**
- Disutility-based phrasing
- Cost-based phrasing

Prompt framing significantly affected allocation behavior.

---

## Pipeline Overview

1. Generate chore-allocation instances
2. Construct prompts (mode × framing)
3. Query LLM APIs
4. Parse messy LLM outputs into structured JSON
5. Validate allocations
6. Compute fairness and efficiency metrics
7. Aggregate results and analyze trends

Parsing required a two-stage normalization process due to inconsistent LLM formatting.

---

## Key Findings

- GPT-4o favored **social optimality**, often minimizing total cost
- Claude 3.5 Sonnet favored **symmetry and equitability**
- Pareto optimality was achieved more often than envy-freeness
- EF was rare, aligning with theoretical impossibility results
- Prompt phrasing strongly influenced fairness outcomes
- Both models tended to spread chores evenly, even when inefficient

---

## Repository Contents

- `notebooks/` – Experimental pipeline and analysis
- `src/` – Prompting, parsing, and evaluation logic
- `data/` – Instances and model outputs
- `reports/` – Final paper and presentation slides

---

## Future Work

- Scaling to larger agent/task settings
- Post-processing corrections to enforce fairness constraints
- Evaluating open-weight models and decoding strategies
- Unified comparison of positive vs negative goods allocation

---

## References

Hosseini, H., & Khanna, S. (2025). *Distributive Fairness in Large Language Models*.  
Guo, H., Li, W., & Deng, B. (2023). *A Survey on Fair Allocation of Chores*. Mathematics.

---

## Authors

Siyona Behera  
Pranav Ramesh  
Dylan Van Berkel  
David Badalamenti  
Ayanna Norfleet
