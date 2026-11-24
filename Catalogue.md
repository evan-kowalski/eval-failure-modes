# Catalogue of evaluation failure modes

This document outlines recurring failure modes observed during model evaluation reviews. Each entry details the observable symptom and the underlying issue with the rubric or test set.

### 1. Superficial verbosity masquerading as completeness
- Observable symptom: The model produces long, detailed responses with structured bullet points, but completely ignores the core constraint in the prompt.
- What it says about the rubric or test set: The rubric overweights length and formatting while failing to penalize constraint violations, or the evaluation prompt lacks negative constraint test cases.

### 2. Sycophantic compliance with false premises
- Observable symptom: When the prompt contains an incorrect factual assumption, the model validates the assumption and builds an answer around it.
- What it says about the rubric or test set: The test set lacks adversarial premises designed to measure truthfulness, and the rubric rewards agreeable tone over factual correction.

### 3. Premature loop termination on multi-step reasoning
- Observable symptom: The model outlines the initial steps accurately but concludes the task before executing the final validation checks.
- What it says about the rubric or test set: The test set lacks intermediate verification checkpoints, allowing incomplete workflows to receive passing marks.

### 4. Hallucinated tool arguments under ambiguity
- Observable symptom: When required parameters are missing from context, the model fabricates plausible parameter values rather than requesting clarification.
- What it says about the rubric or test set: The rubric lacks explicit penalties for ungrounded assumptions, and test scenarios do not systematically test ambiguous inputs.

### 5. Format drift in structured outputs
- Observable symptom: The model starts emitting valid JSON or YAML but drops closing delimiters or introduces conversational filler text midway through.
- What it says about the rubric or test set: The evaluation harness relies on loose regex matching rather than strict schema validation, missing subtle syntactic malformations.

### 6. Hedging and refusal on benign edge cases
- Observable symptom: The model issues an unprompted safety refusal for questions mentioning sensitive keywords in purely benign, educational contexts.
- What it says about the rubric or test set: The test set suffers from keyword-triggered false positives, indicating an overly broad refusal rubric without domain calibration.
