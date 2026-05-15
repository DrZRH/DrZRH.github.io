---
layout: project
title: "A Test Suite for Efficient Robustness Evaluation of Face Recognition Systems"
permalink: /projects/robface.html
conference: "IEEE TR 2025"
authors: "Ruihan Zhang, Jun Sun"
year: 2025
paper: "https://arxiv.org/pdf/2504.21420"
code: "https://github.com/cat-claws/RobFace"
---

## Overview

<figure class="project-figure project-figure--wide">
  <img src="/assets/images/projects/robface/pipeline.png" alt="Overview of the ROBFACE test suite pipeline for face recognition robustness evaluation">
</figure>

This work introduces **ROBFACE**, the first system-agnostic, search-free robustness evaluation method for face recognition systems.

Evaluating the robustness of a face recognition system is essential before deployment — and again after every update. Existing methods either require expensive iterative attacks or slow formal analysis, and most demand white-box access to the system under test. We ask:

> Can we evaluate the robustness of any face recognition system efficiently, without white-box access and without running expensive searches at test time?

ROBFACE answers yes. It uses a pre-optimised test suite of transferable adversarial face images that can be run against any system in the same way traditional software is tested — simply execute the system on the test inputs.

---

## Motivation

<figure class="project-figure">
  <img src="/assets/images/projects/robface/motivation.png" alt="Comparison of existing robustness evaluation approaches and their limitations">
</figure>

Face recognition systems are deployed in high-stakes settings — border control, payment authentication, access control. Their robustness against adversarial perturbations is critical. Yet evaluating that robustness is surprisingly hard.

Two main approaches exist, each with serious limitations:

**Empirical evaluation (attack-based):** Run state-of-the-art adversarial attacks and measure success rate. This is intuitive but slow — each attack requires constrained iterative search — and requires white-box access to the model. Comparing different systems fairly is also difficult due to the variety of attack configurations.

**Formal analysis (Lipschitz-based):** Compute a theoretical robustness bound such as the Lipschitz constant. This provides guarantees but is even slower — finding the exact Lipschitz constant for a two-layer network is NP-hard — and applies only to limited system types.

Neither approach scales to the practical need of re-evaluating robustness every time a system is updated.

---

## Key Idea: Test Suite for Robustness

<figure class="project-figure">
  <img src="/assets/images/projects/robface/key-idea.png" alt="Transferability of adversarial perturbations across different face recognition systems">
</figure>

ROBFACE is built on a well-known but under-exploited property: **adversarial transferability**.

Adversarial perturbations crafted against one model often transfer to other models — they remain effective even on systems they were not designed for. This means a carefully curated set of adversarial examples can serve as a universal probe for robustness, without needing to attack each system from scratch.

The key insight is that if a test suite is pre-optimised to correlate with formal robustness measures across a diverse set of surrogate models, it can estimate the robustness of unseen systems accurately — with no iterative search at evaluation time.

---

## Approach

<figure class="project-figure">
  <img src="/assets/images/projects/robface/approach.png" alt="ROBFACE construction process: constrained discrete optimisation over transferable adversarial samples">
</figure>

ROBFACE is constructed through a one-time offline optimisation process.

We collect transferable adversarial face images across multiple perturbation dimensions:
- **ℓ_p-norm perturbations** (ℓ_0, ℓ_1, ℓ_2, ℓ_∞)
- **Facial accessories** (glasses, hats, masks)
- **Natural transformations** (lighting, radial distortion, rotation)

For each perturbation type, we use constrained discrete optimisation to select a subset of adversarial examples whose aggregate evaluation result correlates strongly with both empirical attack-based evaluation and formal Lipschitz-based analysis on a set of surrogate systems.

The resulting test suite — **ROBFACE-01** — is published and reusable. Evaluating any new system requires only a single forward pass over the test inputs. To prevent overfitting by system developers, ROBFACE also supports randomisation of the test suite via a secret random seed.

---

## Results

<figure class="project-figure project-figure--wide">
  <img src="/assets/images/projects/robface/results.png" alt="ROBFACE evaluation results: accuracy, generalizability, efficiency, and diversity">
</figure>

We evaluate ROBFACE along four dimensions against empirical (PGD-based) and formal (Lipschitz-based) reference methods.

**Accuracy:** ROBFACE estimates are strongly correlated with both empirical and formal robustness evaluation across all perturbation types.

**Generalizability:** ROBFACE transfers across different face recognition architectures and perturbation dimensions, where existing methods are often limited to specific systems or attack types.

**Efficiency:** ROBFACE accelerates robustness evaluation by more than **200×** compared to existing approaches — eliminating iterative search entirely at test time.

**Diversity:** ROBFACE covers a comprehensive range of perturbation types, including both norm-bounded and realistic natural transformations.

---

## Takeaway

Robustness evaluation does not have to be slow, system-specific, or white-box. A well-designed, pre-optimised test suite built on adversarial transferability can provide accurate, scalable, and system-agnostic robustness estimates for face recognition systems.

**Takeaway:**  
ROBFACE brings old-school test suite methodology to deep learning robustness evaluation — system-agnostic, search-free, and 200× faster than existing approaches.

---

## Citation

```bibtex
@article{zhang2025robface,
  author={Zhang, Ruihan and Sun, Jun},
  journal={IEEE Transactions on Reliability}, 
  title={RobFace: A Test Suite for Efficient Robustness Evaluation of Face Recognition Systems}, 
  year={2025},
  volume={74},
  number={3},
  pages={3615-3628},
  keywords={Face recognition;Robustness;Perturbation methods;Testing;Estimation;Accuracy;Optimization;Neural networks;Face recognition;robustness},
  doi={10.1109/TR.2025.3554575}
}
```
