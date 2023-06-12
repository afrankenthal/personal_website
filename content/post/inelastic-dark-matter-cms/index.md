---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Fishing for dark matter using displaced muons"
subtitle: ""
summary: ""
authors: []
tags: ["paper review"]
categories: ["paper review"]
date: 2023-03-20T18:41:22-04:00
lastmod: 2023-03-20T18:41:22-04:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

**(Originally published as a [CMS Physics Briefing](https://cms.cern/news/fishing-dark-matter-using-displaced-muons))**

{{< figure src="EXO-20-010_4.png" numbered="false" >}}

Dark matter is mysterious. In some ways, we know a lot about it, including its average density in the universe and upper limits for how strongly the dark matter particles might interact with each other or with “normal” Standard Model particles. In other ways, however, we haven’t even scratched the surface of the “dark world”. In particular, we don’t know what kind of particle(s) makes up all of the dark matter whose gravitational effects are clearly seen across the universe. The strategy, therefore, is to make the net we cast as wide as possible, in the hope of catching an elusive sign of those subatomic dark matter particles.

CMS physicists recently completed the first search, at the LHC, in the context of the inelastic dark matter model (iDM). In this model (a well-motivated guess for what dark matter *might* be), a dark matter particle can be produced in a proton-proton (pp) collision, travel some distance in our detector, and eventually decay into a pair of muons, which are heavier cousins of the electron. Three distinct features in the iDM model help us to separate such a dark matter signal from look-alike Standard Model processes (“background”).

<ins>The missing transverse momentum</ins>: In an LHC pp collision, the two protons hit each other head-on, with zero net transverse momentum. Therefore, conservation of momentum (as taught in introductory physics classes) implies that there must be zero net transverse momentum after the collision. If we add up the momenta of all the particles that we observe and it does *not* add up to zero, then we have a good sign that something else (dark matter, hopefully) was produced and carried away the “missing” momentum.

<ins>A displaced dimuon vertex</ins>: One of the new particles predicted by the iDM model is “long-lived”, meaning that it can survive long enough to travel relatively far in our detector, before decaying into the two muons. This means that the origin of the muon tracks will be “displaced” with respect to the pp collision point, looking as if they popped out of thin air!

<ins>Close-by muon tracks</ins>: Even though “muon” is literally the middle name of the Compact Muon Solenoid experiment, finding the two muons emitted by iDM particles is challenging, because they are expected to be very close to each other (nearly overlapping) and have relatively low energies. On the other hand, these features make them different from most other collisions (“events”) with muons.

To maximize our ability to find displaced muons, we followed a strategy similar to that used by a [previous CMS analysis](https://cms.cern/news/detector-far-far-away-searching-elusive-long-lived-travellers-tracing-pairs-muons). Using complementary information from the silicon tracker (the innermost detector of CMS) and the muon system (the outermost detectors), we can look for muons with a wide range of displacements (distance between the dimuon vertex and the pp collision point), as shown in Fig. 1.

{{< figure src="comp_dsa_gm_vs_vxy_v4_markersSUBfig1.png" numbered="false" title="<b>FIGURE 1:</b> The efficiency of the “displaced reconstruction” algorithm (red) is much better than that of the standard reconstruction (blue), so that dimuons from long-lived dark matter particles can be identified much better, especially if produced between the external radii of the tracker and of the muon detectors (dashed gray lines)." >}}

As illustrated by the event display shown in Fig. 2, the iDM features are so distinct that, out of the billions of proton-proton collisions recorded by CMS, less than 4 events are expected to survive these “selection criteria”. This event is also shown in the header image. In the transverse view (right), it is clear that the muons were produced some distance away from the center of the detector.

<iframe height="526" loading="lazy" src="https://cms3d.web.cern.ch/EXO-20-010-embedded/" style="border: none;" align="middle" width="700"></iframe> <p style="padding-top: 2%"> <figcaption><b>FIGURE 2:</b> Event display showing an iDM candidate with two muons (red) and missing transverse momentum (purple). You can play with the event display also <a href="https://cms3d.web.cern.ch/EXO-20-010/">here</a> in a separate page.</figcaption></p>

Figure 3 shows that the measured muon displacement distribution agrees very well with the “background” expected from Standard Model events. This means that we do not see any evidence that elusive dark matter particles contribute to the observed events. In other words, our net came up empty this time, despite having been optimized over several years to be as sensitive as possible to the iDM particles. The good news is that there are many more kinds of fish in the theoretical sea, and many other ideas for how to snare dark matter in the CMS detector! Stay tuned to the next episodes.

{{< figure src="Fig3.png" numbered="false" title="<b>FIGURE 3:</b> The measured muon displacement distribution (black circles) agrees well with the “background” Standard Model expectation (red histogram, with the dashed region showing the uncertainty), meaning that we do not see any signal of dark matter particles (represented by the magenta, green, and blue lines for three different iDM scenarios)." >}}
