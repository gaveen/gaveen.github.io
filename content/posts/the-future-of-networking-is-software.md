---
title: The future of networking is software
date: "2019-10-01"
author: 'Gaveen Prabhasara'
categories:
  - Tech
  - Opinion
tags:
  - Networking
  - Open Source
  - Cloud
  - DevOps
draft: false
---

I believe the future of networking in the data center is software-based. The water is wet, and thank you for coming to my TED talk.

---

While what I just mentioned may be obvious to say—given how pretty much everything has its future in software—you would be surprised at the state of the networking industry if you came to it as an outsider. The cloud has already happened, and computing has embraced it with open arms,... tentacles, and whatever else is available. Storage is slower to move but not too far behind. Cloud-scale storage technologies are becoming closer and closer to being commoditized[^ceph]. Network—in a way—is the last frontier in the data center that is not yet fully subscribing to cloud ethos.

Things are certainly changing—more on that later. But networking vendors are still trying to sell you expensive switches, and they are only now getting serious about DevOps. Their idea of a software-defined network (SDN) is to run a bunch of software on top of their existing traditional network solution stack (i.e., [ASIC](https://en.m.wikipedia.org/wiki/Application-specific_integrated_circuit)-driven expensive boxes + mostly-black box [NOS](https://en.m.wikipedia.org/wiki/Network_operating_system)/firmware + ridiculous licensing + exorbitant professional services + consultancy that makes sure you stay with them).

I believe the future of networking—at least networking in the data center—is in software. Networking, in general, is gradually heading that way. The Telco industry has learned from what happened with the cloud and is trying to move towards NFV[^nfv], SDN[^sdn], and SD-WAN[^sdwan] already. But let me focus on the data center, where the clouds also reside.

I believe that the enablers of this shift will be multi-fold. For example, network virtualization[^netvirt] and network functions virtualization[^nfv] are precursors. Also, network equipment supporting alternative NOSs has been here for a while. For example, some brand vendors like Mellanox, Dell EMC, and whitebox switch vendors support multiple OSs, such as generic Linux, Cumulus, Open Network Linux, SONiC, and their own OSs on their switches.

One way things can go is the next wave of convergence, incorporating networking into already converged computing and storage. For the lack of a better term—and in line with the buzzword-based naming (e.g., CI[^ci]/HCI[^hci])—let us call it Fully-Converged Infrastructure (FCI). I feel an inspired OEM vendor can make it happen. However, if this comes to pass with significant enough adoption, it will be a salient indicator that the balance has been tipped from hardware to software. Technically, it could still happen without a noticeable wave of further convergence. Where the balance of power shifts from specialized hardware-based switch/network appliances to *software-based networking on generic computing platforms*.

I am not sure how the gap will be bridged exactly. Perhaps x86 server-based networking will become more powerful to catch up to ASIC/[FPGA](https://en.m.wikipedia.org/wiki/Field-programmable_gate_array)-accelerated networking. Perhaps network appliance hardware will become generic open platforms. Perhaps ASICs and FPGAs will become increasingly generic till they become commodity components in generic computing. It could be an amalgamation of all these conditions.

We already see some precursors in the evolution of the hardware aspect. For example, x86-based switches are now commonplace, while some ASICs are becoming more and more in the territory of generic platforms[^asics].

Software in the networking industry had been a little more agile. While proprietary software stacks of traditional vendors have been evolving further, interest in consolidating efforts on common infrastructure is happening, albeit with limited adoption. For example, [Linux Foundation Networking](https://www.lfnetworking.org/) and [Open Networking Foundation](https://www.opennetworking.org/) have received contributions from major network vendors such as Cisco, Arista, Juniper, and Mellanox. This has resulted in the development or improvement of interesting open source technologies such as [DPDK](https://www.dpdk.org/), [P4](https://www.opennetworking.org/p4/), [VPP](https://fd.io/), [SONiC](https://azure.github.io/SONiC/), [Stratum](https://www.opennetworking.org/stratum/), etc. Both open-source-based and proprietary vendor OSs[^propnos] have been available in the market.

The non-physical side of networking space (e.g., processing, forwarding, routing/switching decisions, protocols, virtual endpoints, segmentation, micro-segmentation, policy frameworks, telemetry, observability, etc.) will get much more exciting. I am not saying traditional networking equipment will become obsolete in a hurry. But I believe building networks with generic computing platforms that are at least akin to the x86 servers of today—perhaps augmented with FPGAs or ASICs—will at least become a mainstream option for ops teams at some scale. These networking infrastructures could be handled by the software they are running.

With cloud computing[^cloudcompute] becoming a mainstay—along with all the shifts in thinking it brings—networking is due for a re-imagining. While the body of domain knowledge, standards, abstractions, and even expertise can be reused, I believe that traditional thinking that involves believing in different switch boxes for different places[^boxen] in the network may—IMHO—antiquated and only serve to drive network vendor sales. In fact, cloud consumers mostly do not care about anything below Layer 4. Therefore, the skeuomorphic constructs such as, switches and virtual switches may not have an inherent purpose in these scenarios.

Application-aware Layer 4 (and above) software systems are already starting to do [pretty cool things](https://www.infoq.com/podcasts/open-source-cilium-security/)[^l24cni]. However, the Layer 2 - Layer 3 networking that enables and empowers these remains to catch up to the future. It will be an exciting journey to get there.

[^ceph]: e.g., [Ceph](https://ceph.io/), [MinIO](https://min.io/), etc.
[^netvirt]: [Network Virtualization](https://en.m.wikipedia.org/wiki/Network_virtualization) (e.g., VMware NSX)
[^nfv]: [Network Functions Virtualization](https://www.sdxcentral.com/networking/nfv/definitions/whats-network-functions-virtualization-nfv/) (e.g., OPNFV)
[^sdn]: [Software-Defined Networking](https://www.sdxcentral.com/networking/sdn/definitions/what-the-definition-of-software-defined-networking-sdn/)
[^sdwan]: [SD-WAN](https://www.sdxcentral.com/networking/sd-wan/definitions/software-defined-sdn-wan/)
[^ci]: [Converged Infrastructure](https://en.m.wikipedia.org/wiki/Converged_infrastructure)
[^hci]: [Hyperconverged Infrastructure](https://en.m.wikipedia.org/wiki/Hyper-converged_infrastructure)
[^asics]: Competing vendors like Arista and Cisco use the same Broadcom ASIC silicon series (e.g., Tomahawk, Trident, Jericho) in some of their comparable switches.
[^cloudcompute]: Cloud Computing and its inner aspects, such as public/hybrid clouds, Cloud Native Infrastructure, etc., have become a mainstay in the industry and continue to influence the thinking in adjacent areas.
[^l24cni]: Layer 4 - 7 software options include cloud-native software such as [Cilium](https://cilium.io/), Service Mesh software (e.g., [Envoy](https://www.envoyproxy.io/)/[Istio](https://istio.io/), and [Linkerd](https://linkerd.io/)), etc.
[^propnos]: e.g., Cumulus Networks, Big Switch Networks, and Pluribus Networks
[^boxen]: Either talking of older core/aggregation/access switch classification or the newer spine/leaf classification is still hinged on the fact that these switches are usually built for different purposes with different limitations and capabilities. However, if everything is software—running on sufficient compute power and necessary physical connectivity—there will not be much technical justification for why one of your switches cannot be a core switch and an order of magnitude more expensive than another one.
