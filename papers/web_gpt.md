## [WebGPT: Browser-assisted question-answering with human feedback](https://arxiv.org/abs/2112.09332)

### Insight
* Want to make systems not make false statements, but that is hard to evaluate
* Verifying factual correctness _given cited sources_ *is easier*
* Instead of custom models, use existing blocks:
  *  a pre-trained language model (LM)
  *  a (custom) textual Bing API

### Methods
1. Behavior cloning (supervised fine-tuning) of the pre-trained LM
2. Reward modeling from ~20,000 comparisons
3. Followed by rejection sampling or RL (both against a reward model)

### Results
* Best model preferred to humans 56% of the time (slightly better than an average human)
* Best model preferred to ELI5 responses 69% of the time
* Best model struggled on OOD dataset (TruthfulQA)

### Issues
* Sometimes made basic mistakes when writing up the answer
* Sometiems random behavior to nonsensical questions ("what?")
* Struggled with questions without found direct answers ("51 + 37", "what is π to the power of π")
* Struggled with out-of-distribution (TruthfulQA, shorter-form)
* **Safety Relevant:** Didn't question user's question stance, hence reinforced existing beliefs & superstitions (suggested solution: _adversarial training_)
* **Safety Relevant:** Quotes unreliable sources (and distinguishing reliable ones can be controversial)
* **Safety Relevant:** Incentivized to cherry-pick convincing references, even if not a fair assessment of the evidence

### Technical bits
* Authors calculated optimal trade-offs for compute efficiency
* Rejection sampling worked as good or better than RL (probably because RL overoptimized the reward model, and/or decreased policy entropy)
* Adapting the RL objective to optimize rejection sampling performance is an interesting direction for future research

### Conclusion
Paraphrased: fine-tuning an LM to use a web-browser allowed using general methods (imitation learning and RL) to beat humans on ELI5; but this still struggles with OOD.




