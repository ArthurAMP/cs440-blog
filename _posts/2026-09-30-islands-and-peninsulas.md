---
layout: post
title: "Understanding Partial Reachability in the Internet Core"
date: 2026-09-30
paper_authors: "G. Baltra, T. Saluja, Y. Pradkin, J. Heidemann"
paper_venue: "NINeS 2026"
paper_url: "https://2026.nines-conference.org/papers/p004-Baltra.pdf"
week: 2
tags: [routing, reachability, internet reliability, network outages]
---

## Key Idea

This paper mainly serves two purposes. 

First, it defines several terms that are useful to understand and recognize partial reachability. From what I can tell, this formalization of an Internet core is novel, and so are the definitions of an Internet Island and Internet Peninsula  (dating back to a 2021 preprint of this same research project, [What Is The Internet? (Considering Partial Connectivity)](https://arxiv.org/abs/2107.11439v1)). The argument then is that by using these two classifications, they have a useful way of studying persistent unreachability that only depends on observation of traffic. 

Secondly, it introduces algorithms to identify Peninsulas and islands and validates them against Ark by labeling Ark's data according to their framework. Their method of not depending on a central authority is by probing /24 blocks from chosen Vantage Points (VPs). If a block is reachable by at least one but not all VP, it is classified as a Peninsula. If a VP fails to reach a strict majority of the blocks, it is classified as an Island.

## Critique

This paper is very self-contained, introducing all the concepts you need to know before they become useful. This makes for an enjoyable and seamless reading experience. I can't think of any part I thought was unclear after my second pass. 

One question I propose is about the definitions themselves. The decision to create definitions that are strictly observable is an excellent choice for the reasons they outline in the paper. However, I do wonder why not push it further and make formal definitions that are practically observable. For Peninsulas, they must approximate it by looking at /24 blocks instead of all potentially reachable IPs because there is no active measurement effort of all IP addresses, as it would be clearly unfeasible. So why not make a definition that could practically be measured? Same goes for Islands, as it is even harder to determine because it could be just an outage. A small implication of such a strong definition of a Peninsula is that it lumps together "not being able to reach a singular host" with "not being able to reach 49% of the hosts". I'm not convinced this is inevitable or useful. 

Additionally, I thought the amount of interpretation that went into the Ark labeling warrants suspicion. Take this specific quote from the text: "As a result, while positive Ark results support non-partitions, negative Ark results are most likely a missed target and not an unreachable block; we expand on this analysis in Appendix F.1 of [9]. We therefore treat this second most-common result (491k cases) as a true negative." I think this is a reasonable assumption, but with such a high volume I would appreciate more than two sentences explaining how they came to the conclusion this is a reasonable decision. Additionally, I did read Appendix F.1 of the technical report and it does not have information that supports that assumption. 

Some smaller points:
- The abstract and the presentation start with the geopolitical implications of partial reachability. But the section where the definitions are made doesn't make a case for Islands and Peninsulas to be a good proxy for anything. Constructing an example where it would be important would be a great addition.
- The 3-4 VPs (and by extension 6 VPs) being enough is a claim that is load-bearing to the point it would have been nice if that investigation went a little deeper.

## Connections

While there is no direct connection to "There is More to Internet Invariants Than Meets the Eye", I wonder whether there is case for treating Internet Islands and Internet Peninsulas as a candidate invariant. One certainly can come up with a mock dataset that could satisfy step 1 and 2. For the third requirement, I don't have a good proposal at the moment. However, one can get a clue of how an explanation would go both from the partial reachability paper itself and "Stable Internet Routing Without Global Coordination", such as financial incentive to disrupt ideal routing and peering disputes. 

## More thoughts

I think an interesting extension to this paper would be exploring adversarial induced partial reachability aside from sanctions. For example, whether the concept of Peninsulas and Islands could potentially allow for improved target selection for a malicious agent or quantifying how much infrastructure one must disrupt to induce partial connectivity.
