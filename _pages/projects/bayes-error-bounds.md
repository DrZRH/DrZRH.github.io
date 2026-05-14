---
layout: project
title: "Certified Robust Accuracy of Neural Networks Are Bounded Due to Bayes Errors"
permalink: /projects/bayes-error-bounds.html
conference: "CAV 2024"
authors: "Ruihan Zhang, Jun Sun"
year: 2024
paper: "https://arxiv.org/pdf/2405.11547"
code: ""
---

## Overview

<figure class="project-figure project-figure--wide">
  <img src="/assets/images/projects/bayes-error/overview.png" alt="Overview of Bayes-error-based robustness limits">
</figure>

Certified robustness has a data-dependent ceiling: larger Bayes error implies lower best-achievable certified robust accuracy.

Robust training effectively changes the target distribution through perturbation neighborhoods.
This shift increases class overlap, raises Bayes error, and creates a hard ceiling on certified performance.

---

## Motivation: Ambiguity Is Irreducible

<figure class="project-figure">
  <img src="/assets/images/projects/bayes-error/cat-dog.png" alt="Ambiguous cat-dog example motivating Bayes error">
</figure>

Some inputs are inherently ambiguous.
Even a perfect classifier cannot always assign a deterministic label when the data distribution itself contains uncertainty.

Bayes error captures this irreducible ambiguity.
This work asks whether such ambiguity also limits certified robustness.

---

## Key Idea: Robustness Changes the Target Distribution

<figure class="project-figure">
  <img src="/assets/images/projects/bayes-error/key-idea.png" alt="Robustness as fitting a convolved distribution">
</figure>

Certified robustness requires a classifier to make consistent predictions within a perturbation neighborhood.

This effectively changes the learning target:
instead of fitting the original distribution, robust learning fits a convolved distribution induced by the perturbation region.

The convolved distribution has larger class overlap, which increases Bayes error.

---

## Approach

We formalize the connection in two steps.

First, we show that optimizing for certified robustness is equivalent to fitting a convolved version of the original data distribution.

Second, we show that this convolved distribution has no smaller Bayes error than the original distribution.

Together, these results yield a model-agnostic upper bound on certified robust accuracy.

---

## Evaluation

<figure class="project-figure">
  <img src="/assets/images/projects/bayes-error/eval.png" alt="CIFAR-10 certified robust accuracy upper bound">
</figure>

We compare the derived upper bound with existing certified training results.

On CIFAR-10, our analysis gives a certified robust accuracy upper bound of **67.49%**.
Existing certified methods improved from **53.89%** in 2017 to **62.84%** in 2023, approaching but still below this theoretical ceiling.

---

## Takeaway

Robustness is not only an algorithmic or optimization problem.

It is fundamentally constrained by the intrinsic ambiguity of data distributions.
Improving certified robustness therefore requires understanding not only models and training methods, but also the data distribution itself.

---

## Citation

```bibtex
@inproceedings{zhang2024bayes,
author = {Zhang, Ruihan and Sun, Jun},
title = {Certified Robust Accuracy of&nbsp;Neural Networks Are Bounded Due to&nbsp;Bayes Errors},
year = {2024},
isbn = {978-3-031-65629-3},
publisher = {Springer-Verlag},
address = {Berlin, Heidelberg},
url = {https://doi.org/10.1007/978-3-031-65630-9_18},
doi = {10.1007/978-3-031-65630-9_18},
abstract = {Adversarial examples pose a security threat to many critical systems built on neural networks. While certified training improves robustness, it also decreases accuracy noticeably. Despite various proposals for addressing this issue, the significant accuracy drop remains. More importantly, it is not clear whether there is a certain fundamental limit on achieving robustness whilst maintaining accuracy. In this work, we offer a novel perspective based on Bayes errors. By adopting Bayes error to robustness analysis, we investigate the limit of certified robust accuracy, taking into account data distribution uncertainties. We first show that the accuracy inevitably decreases in the pursuit of robustness due to changed Bayes error in the altered data distribution. Subsequently, we establish an upper bound for certified robust accuracy, considering the distribution of individual classes and their boundaries. Our theoretical results are empirically evaluated on real-world datasets and are shown to be consistent with the limited success of existing certified training results, e.g., for CIFAR10, our analysis results in an upper bound (of certified robust accuracy) of 67.49\%, meanwhile existing approaches are only able to increase it from 53.89\% in 2017 to 62.84\% in 2023.},
booktitle = {Computer Aided Verification: 36th International Conference, CAV 2024, Montreal, QC, Canada, July 24–27, 2024, Proceedings, Part II},
pages = {352–376},
numpages = {25},
location = {Montreal, QC, Canada}
}
```