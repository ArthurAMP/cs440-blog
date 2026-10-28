---
layout: post
title: "DistTrain: Addressing Model and Data Heterogeneity with Disaggregated Training for Multimodal Large Language Models"
date: 2026-10-21
paper_authors: "Z. Zhang, Y. Zhong, Y. Jiang, H. Hu, J. Sun, Z. Ge, Y. Zhu, D. Jiang, X. Jin"
paper_venue: "SIGCOMM 2025"
paper_url: "https://doi.org/10.1145/3718958.3750472"
week: 5
tags: [distributed training, multimodal LLMs, resource allocation, DistTrain]
---

## Key Idea

The key problem they address is how mixed the training data and different components in LLM training are. You are simultaneously dealing with short texts, images, foundational models,m encoders, generators, and all of those have different computational demands and different traffic profiles. When you're doing something like Pipeline Parallelism, which benefits greatly from having the load distributed so there is no idle nodes, an engine that doesn't consider this can perform worse. Their solution for that is having separate resource allocation for each component and reordering microbatches to reduce idle gaps during training. 

## Critique

Not a critique to their methods, but something that cannot go unstated, is the fact that MoE models are missing from the benchmarks. This is a byproduct of how fast LLM development is accelerating, as on Llama 3 generation there were barely any open weights MoE models. Currently, we know that dense backbones are somewhat situational, mostly being useful for on-device inference, small classifiers, and for local inference. On a paper that champions supporting different models, missing such an important category hurts the conclusions. 

## Connections

Any LLM training networking is very dependent on RDMA and data center networking in general, so a related read to this problem would be the blogpost I wrote on [DcSim](/cs440-blog/2026/10/21/dcsim/).
