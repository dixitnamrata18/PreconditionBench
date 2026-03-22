# PreconditionBench
A diagnostic benchmark for unverified precondition failures in LLMs

## What is this?

Most LLM benchmarks test whether a model knows the right answer. 
PreconditionBench tests something different: does the model notice 
when it cannot answer yet?

A model that says "send the email" without checking internet 
connectivity, or "go to the gym" without asking if you have your 
shoes, is not hallucinating. Its reasoning is internally fine. It 
just never stopped to ask whether the action was actually possible 
given what it knew.

That is the failure mode PreconditionBench targets.

## Failure Taxonomy

| Type | Description |
|------|-------------|
| Missed dependency | Precondition is absent, model proceeds without flagging |
| Ignored dependency | Context is present but model does not act on it |
| Substituted dependency | Model checks a plausible but wrong precondition |

## Results

| Model | Pass | Partial | Fail |
|-------|------|---------|------|
| GPT-4o | 8 | 5 | 5 |
| Claude Sonnet 4.6 | 7 | 3 | 8 |
| Llama 3.3 70B | 5 | 4 | 9 |
| Gemini 1.5 Pro | 5 | 5 | 8 |

## Key Findings

Two scenarios were failed by all four models without exception:

- S5: Broken laptop, repair shop nearby. No model asked whether 
  you would bring the laptop.
- S9: Urgent email. No model checked internet connectivity first.

Gemini triggered Google Flights and started booking a flight 
before verifying any preconditions. In a real agentic deployment 
that is not a wrong answer, it is a wrong action.

## Dataset

18 hand-authored scenarios across 6 domains: transportation, 
communication, household tasks, personal equipment, agentic 
tool-use, and social planning.

Each scenario includes:
- Scenario text
- Unverified precondition
- Correct behavior
- Correct answer
- Failure type
- Difficulty
- Domain tag

## Evaluation Slices

- Single-step explicit (6 scenarios)
- Single-step implicit (9 scenarios)
- Multi-step chain (3 scenarios)

## Elicitation Prompt

All scenarios were evaluated using:

"Before answering, reason about what information you have and 
what information you would need to answer correctly. Then respond."

## Links

- Kaggle Benchmark: Coming public April 17, 2026
- Dataset: [(https://www.kaggle.com/datasets/dixitnamrata18/preconditionbench-dataset)]
- Hackathon: [https://www.kaggle.com/competitions/kaggle-measuring-agi]

## Citation

If you use this benchmark please cite:

Dixit, N. (2026). PreconditionBench: A Diagnostic Benchmark for 
Unverified Precondition Failures in LLMs. Kaggle Measuring 
Progress Toward AGI Hackathon.

## License

CC BY-SA 4.0
