---
layout: post
title: "OpenFLAME: A Federated Spatial Naming Infrastructure"
date: 2026-10-21
paper_authors: "S. Bharadwaj, Z. Ma, I. Liang, M. Farb, A. Rowe, S. Seshan"
paper_venue: "NINeS 2026"
paper_url: "https://doi.org/10.4230/OASIcs.NINeS.2026.20"
week: 6
tags: [federated mapping, spatial naming, DNS, OpenFLAME]
---

## Key Idea

Their key idea can be summarized as DNS for spatial location, built on top of DNS itself.

They draw attention to the fact that while sources of web addresses/locations are federated, their spatial counterpart (maps) depend on central authorities. For indoor maps, centralized map servers breaks down for two different reasons. Firstly, companies like Google and Apple would have to be up for the task of mapping out the inside of millions of buildings which they don't own and might not even have access to. And, more importantly, companies and individuals wouldn't love to share the layout of their offices and homes with these companies to have access to indoor mapping. Having a map of indoor areas is not only very useful now, it most likely will become necessary for many technological advancements. Some current uses can be simpler robots like Roombas and navigation inside an airport, it would be very useful if the protocol to specify those spaces was open and could be hand-rolled. But as AR gets more important and physical AI becomes more proeminent, having access to your own map you can share as you please becomes much more important.

Their idea to tackle this issue is to essentially copy how the web works. If you represent Northwestern, and you want to have indoor maps for Northwestern buildings, you would run your own map server like you would run a name server. The maps are organized into zones (which weirdly allow overlap), and the area covered by a region is described through S2 cell sets. Then they came up with a schema to represent cells like domain names (now called geo-domains), and new record types to represent how some geo-domains are owned by more than one map server. Thus, it starts mapping cleanly to DNS. Map zones matches DNS zones, etc...

## Critique

This is a very exciting idea. Indoor mapping is a problem that I'm very invested in seeing a proper solution, as I am terrible with any sort of navigation. The S2 cell -> geo-domain idea is also really clever. 

However, my background is mainly security work, and there is glaring gaps that cannot go unaddressed even in a new ideas conference. The most glaring of all, to me, is one that is mentioned in text but "wished away". They mention as the biggest security concern identity spoofing, describing it a threat actor maliciously pretending to be a map server or zone to trick applications into thinking they own the region. While they correctly identified the problem, they address it through a chain of trust not unlike DNSSEC. This treats the entire identity spoofing problem as an authenticity issue, which fundamentally misunderstands half of the threat model. Why would I go through the trouble of faking a record when I can just create perfectly legitimate map servers for regions I don't have authority over? Especially because they flaunt as a feature that if one parent zone declines the registration, one can register under other parent zones. And this gets especially problematic because from the perspective of a user looking up the geo-domain, there is no ranking between any of the map servers and there is no clear way of telling who is actually in charge of the geo-domain's area. This problem is something that uniquely affects OpenFLAME, and DNSSEC is the wrong tool for mitigating it (although I have no idea what to do about it without centralization).

Some other thoughts: 
"Once federated mapping is deployed at scale, it will likely reveal a wide and diverse attack surface. Map servers, for example, are vulnerable to attacks such as denial of service (DoS), reflection, and amplification. We believe that existing methods on DoS protection or anomaly detection could mitigate such attacks." I simply don't believe this. Is the claim that the new records they created won't lead to novel DoS? The sentence doesn't necessarily imply no new attacks, but it almost feels like an attempt of avoiding having to investigate the problem by implying "it likely is a non-issue." For what is worth, I also haven't explored the possibilities for novel DoS stemming for their new records. However, something like having every referral being potentially important, instead of being certain that multiple referrals are redundant to each other, warrants caution. This breaks an invariant of DNS, and DoS mitigations build on those invariants.  

Do I expose my own location whenever doing a geo-domain lookup? DNS leaks are obviously something that isn't new, but it seems incredibly more sensitive than what data leaks on a regular DNS lookup. Also as I understand there is no layer between the user and the nameserver?

Enumerating geo-domains seems trivial. No need to guess arbitrary strings, just construct geo-domains which you'd be interested in, in case they exist. 

## Connections

I had a lot of trouble coming up with a good connection. Well, this repurposes something for a different purpose similarly to how [P-ECMP](/cs440-blog/2026/10/07/ecmp/) repurposes ECMP groups. This is the best I could do. 
