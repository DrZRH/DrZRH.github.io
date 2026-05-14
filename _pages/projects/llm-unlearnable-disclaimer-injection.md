---
layout: project
title: "Rendering Data Unlearnable by Exploiting LLM Alignment Mechanisms"
permalink: /projects/disclaimer-injection.html
conference: "ACL 2026"
authors: "Ruihan Zhang, Jun Sun"
year: 2026
paper: "https://arxiv.org/pdf/2601.03401"
code: "https://github.com/cat-claws/unlearnable-llm-alignment"
---

## Overview

<figure class="project-figure project-figure--wide">
  <img src="/assets/images/projects/llm-unlearnable/pipeline.png" alt="Pipeline of disclaimer injection for rendering LLM data unlearnable">
</figure>

This work studies how to protect data from being learned by large language models.

Existing unlearnable-example methods were not designed for modern LLMs. 
Their surface-level perturbations often fail because LLMs can still infer the underlying meaning. 
We therefore ask:

> How can we protect data from being learned in the era of large language models?

---

## Motivation: LLMs Break the Assumption Chain

<figure class="project-figure">
  <img src="/assets/images/projects/llm-unlearnable/llm-lens.png" alt="LLMs can recover the semantics of noisy text">
</figure>

Earlier unlearnable-example methods assume that small perturbations can corrupt the learning signal.

This assumption becomes fragile for LLMs.
Even when text is visibly perturbed, an LLM may still reconstruct the intended meaning and learn from it.
In other words, the perturbation may look disruptive to humans, but it is not necessarily disruptive to the model.

---

## Key Idea: Trigger Alignment, Not Noise

<figure class="project-figure">
  <img src="/assets/images/projects/llm-unlearnable/disclaimer-injection.png" alt="Disclaimer injection example showing original and injected input">
</figure>

Instead of adding random noise, we inject short disclaimer-style sentences that are benign to humans but highly salient to the model.

These disclaimer-style sentences act as triggers for the model’s safety and alignment mechanisms.
Once triggered, the model shifts away from ordinary task processing and toward refusal- or risk-oriented internal behavior.

The goal is not to hide the text.
The goal is to change how the LLM processes it.

---

## Approach

<figure class="project-figure">
  <img src="/assets/images/projects/llm-unlearnable/approach.png" alt="Rendering data unlearnable within LLMs">
</figure>

Our approach is based on the observation that alignment-triggering inputs induce internal representations that differ systematically from ordinary task inputs.

We exploit this representational gap by injecting carefully designed disclaimer sentences.
The injected text redirects the model toward alignment-related computation, making the protected content less learnable during training.

This creates a different form of unlearnability:

- traditional methods perturb the input surface;
- our method perturbs the model’s internal processing route.

---

## Mechanism: Alignment Hijacking

<figure class="project-figure">
  <img src="/assets/images/projects/llm-unlearnable/mechanism.png" alt="Activation heatmap showing alignment hijacking">
</figure>

The injected disclaimer causes persistent activation in alignment-related layers.

During standard training, the model processes the content as ordinary benign text.
During protected training, the injected disclaimer hijacks the computation path.
The model then spends capacity processing safety-related signals rather than learning the original task content.

We call this effect **alignment hijacking**.

---

## Results

<figure class="project-figure">
  <img src="/assets/images/projects/llm-unlearnable/results.png" alt="Comparison between old surface perturbation methods and disclaimer injection">
</figure>

Compared with prior surface-perturbation methods, disclaimer injection produces a much larger drop in learnability.

In the reported comparison, traditional methods such as BAE and Seq2Sick cause only about a **1%** performance drop.
In contrast, disclaimer injection causes a drop of more than **35%**.

This suggests that the key bottleneck is not whether the text is visibly perturbed, but whether the perturbation changes the model’s internal cognitive state.

---

## Takeaway

This work shows that protecting text from LLM training requires a different mechanism from classical classifiers.

For LLMs, surface-level noise is often insufficient because the model can recover meaning.
A more effective strategy is to interact with the model’s alignment machinery and redirect its computation away from useful learning.

**Takeaway:**  
Unlearnability for LLMs should be designed at the level of internal model behavior, not merely at the level of input perturbation.

---

## Citation

```bibtex
@misc{zhang2026renderingdataunlearnableexploiting,
      title={Rendering Data Unlearnable by Exploiting LLM Alignment Mechanisms}, 
      author={Ruihan Zhang and Jun Sun},
      year={2026},
      eprint={2601.03401},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2601.03401}, 
}
```
