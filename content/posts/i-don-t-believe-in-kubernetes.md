---
title: I don't believe in Kubernetes
date: "2019-12-01"
author: 'Gaveen Prabhasara'
categories:
  - Tech
  - Opinion
tags:
  - Cloud
  - Cloud Native
  - K8s
  - DevOps
draft: false
---

I was always a believer in [Cloud Computing](https://azure.microsoft.com/en-us/overview/what-is-cloud-computing/). Even when some "big executives" called it a fad, I still believed in the cloud—or its promise.

The belief itself is not an achievement. As with so many other people in tech, it spoke to me from a place of understanding. It was not so much an achievement to be had. We may not have called it a cloud, but when Amazon opened the gates of their Web Services to everyone, we saw good things we recognized. We realized it was an opportunity to build better.

Cloud Computing was about making good IT infrastructure accessible to the rest of us. Finally, we did not need to be a sizeable enterprise or have a small army of ops and devs to run the necessary infrastructure. It was empowering. It was enabling. When cloud users can solve their problems conveniently, people interested in cloud infrastructure could enjoy building them and, in the process, change many professions and how the industry works.

After achieving the cloud, our mission should have been to make cloud computing accessible to more and more people. We dreamt of people having on-demand access to all the IT resources they want at an ever-reducing utility cost and being enabled to conveniently solve their problems. That should have been our mission.

Instead, here we are today, left fixated on things like *Kubernetes*[^k8s] and trying to emulate how giant companies—so-called hyperscalers—like Google and Microsoft operate their infrastructure. Instead of trying to get people closer to solving their problems, we are effectively erecting newer barriers in complexity.

To be clear, I am not trying to look down on [Kubernetes (K8s)](https://kubernetes.io/). I like Kubernetes—but with certain caveats. K8s is a system with many components and—as with any complex system—comes with inherent operational complexities. It is a system catering to specific needs. It has its place. IMHO, Kubernetes is a tool for cloud builders, not cloud consumers.

A problem with the current [Cloud Native](https://www.cncf.io/) narrative is that a lot of companies (and, in turn, a significant amount of ecosystem resources) who would otherwise be working with a consumer focus are busy with building tools for cloud builders. They then try to wrestle these into submission as cloud consumer technologies. You do not have to take my word for it—you can try deploying an application to production on Kubernetes.

What happened to bringing the best technology conveniences to the rest of us? Whatever happened to harnessing the power of IT so that it stops being an inhibitor and becomes the great enabling force that it can be? What happened to—may Cthulhu have mercy on my soul—powering "digital transformation"?

I do, of course, believe in the existence of Kubernetes. But, if you need to ask if you should be using Kubernetes, chances are you should not.

[^k8s]: **PSA**: Containers ≠ Docker ≠ Kubernetes
