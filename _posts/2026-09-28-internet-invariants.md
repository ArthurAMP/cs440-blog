---
layout: post
title: "There is More to Internet Invariants Than Meets the Eye"
date: 2026-09-28
paper_authors: "C. Misa, W. Willinger, R. Durairajan, R. Rejaie"
paper_venue: "NINeS 2026"
paper_url: "https://nines-conference.org/papers/p022-Misa.pdf"
week: 1
tags: [architecture, invariants, traffic, self-similarity]
---

## Key Idea

This paper proposes a framework for investigating proposed and estabilished invariants. The framework is divided in three parts, with the first two estabilishing the necessity for proper statistical modeling and mathematical rigor, and the third ensuring that the invariant is understood through actual facts about the Internet's design and usage. It also promotes the usage of a HOT-inspired approach to understand Internet invariants.

## Critique

This paper was successful in convincing me that its three-part framework can be useful for understanding Internet invariants, especially through the worked example. However, this paper also includes an effort to convince the reader that HOT is the basis of the framework, and that it is an integral approach to understanding invariants. 

It is not clear to me what being HOT-inspired means, and it is mentioned enough on the explanation of the framework that I believe this goes beyond a nitpick. HOT is a very specific method, and it seems useful (as they showed through usage) when meeting the third criteria of the framework. But the framework seems to stand on its own perfectly fine without HOT usage. Given the importance this paper gives to HOT, I would have appreciated either a clear separation of the general framework and the power of leveraging HOT or a stronger justification as to why it is so integral to the framework.

## Connections

I thought the [background paper](https://dl.acm.org/doi/epdf/10.1145/52325.52336) ties in with the third part of the framework, as it points out how important it is to understand the constraints which informed the design of the Internet to better understand of the design itself. Specifically, it reminds me of the constraint-aware analysis of the invariants and the understanding that the invariants themselves often are by definition attached to the design of the protocol. 
