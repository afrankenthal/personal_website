---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Lazy photons at the LHC"
subtitle: ""
summary: ""
authors: []
tags: ["paper review"]
categories: ["paper review"]
date: 2019-11-24T23:30:55-05:00
lastmod: 2019-11-24T23:30:55-05:00
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


**Title: _“Search for long-lived particles using delayed photons in proton-proton collisions at $\sqrt{s}$ = 13 TeV”_**

**Author: CMS Collaboration**

**Reference: [https://arxiv.org/abs/1909.06166](https://arxiv.org/abs/1909.06166)** (submitted to Phys. Rev. D)

_(Originally published on [Particle Bites](https://particlebites.com))_

An interesting group of searches for new physics at the LHC that has been gaining more attention in recent years relies on reconstructing and identifying physics objects that are displaced from the original proton-proton collision point. Several theoretical models predict such signatures due to the decay of **long-lived particles (LLPs)** that are produced in these collisions. Theories with LLPs typically feature a suppression of the available phase space for the decay of these particles, or a weak coupling between them and Standard Model (SM) particles.

An appealing feature of these signatures is that backgrounds can be greatly reduced by searching for displaced objects, since most SM physics display only prompt particles (i.e. produced immediately following the collision within the primary vertex resolution). Given that the sensitivity to new physics is determined both by the presence of signal events as well as by the absence of background events, the sensitivity to models with LLPs is increased with the expectation of low SM backgrounds.

A recent search for new physics with LLPs performed by the CMS Collaboration uses **delayed photons** as its driving experimental signature. For this search, events of interest contain delayed photons and missing transverse momentum (MET$^1$). This signature is predicted in the LHC by various theories such as Gauge-Mediated Supersymmetry Breaking (GMSB), where long-lived supersymmetric particles produced in proton-proton (pp) collisions decay in a peculiar pattern, giving rise to stable particles that escape the detector (hence the MET) and also photons that are displaced from the interaction point. The expected signature is shown in Figure 1.


{{< figure src="diagrams.jpg" numbered="false" caption="Figure 1. Example Feynman diagrams of Gauge-Mediated Supersymmetry Breaking (GMSB) processes that can give rise to final-state signatures at CMS consisting of two (left) or one (right) displaced photons and supersymmetric particles that escape the detector and show up as missing transverse momentum (MET)." >}}

The main challenge of this analysis is the physics reconstruction of delayed photons, something that the LHC experiments were not originally designed to do. Both the detector and the physics software are optimized for prompt objects originating from the pp interaction point, where the vast majority of relevant physics happens at the LHC. This difference is illustrated in Figure 2.

{{< figure src="displaced_reco.jpg" numbered="false" title="Figure 2. Difference between prompt and displaced photons as seen at CMS with the electromagnetic calorimeter (ECAL). The ECAL crystals are oriented towards the interaction point and so for displaced photons both the shape of the electromagnetic shower generated inside the crystals and the arrival time of the photons are different from prompt photons produced at the proton-proton collision. Source: https://cms.cern/news/its-never-too-late-photons-cms" >}}

In order to reconstruct delayed photons, a separate reconstruction algorithm was developed that specifically looked for signs of photons out-of-sync with the pp collision. Before this development, out-of-time photons in the detector were considered something of an ‘incomplete or misleading reconstruction’ and discarded from the analysis workflow.

In order to use delayed photons in analysis, a precise understanding of CMS’s calorimeter timing capabilities is required. The collaboration measured the timing resolution of the electromagnetic calorimeter to be around 400 ps, and that sets the detector’s sensitivity to delayed photons.

Other relevant components of this analysis include a dedicated trigger (for 2017 data), developed to select events consistent with a single displaced photon. The identification of a displaced photon at the trigger level relies on the shape of the electromagnetic shower it deposits on the calorimeter: displaced photons produce a more elliptical shower, whereas prompt photons produce a more circular one. In addition, an auxiliary trigger (used for 2016 data, before the special trigger was developed) requires two photons, but no displacement.

The event selection requires one or two well-reconstructed high-momentum photons in the detector (depending on year), and at least 3 jets. The two main kinematic features of the event, the large arrival time (i.e. consistent with time of production delayed relative to the pp collision) and large MET, are used instead to extract the signal and the background yields (see below).

In general for LLP searches, it is difficult to estimate the expected background from Monte Carlo (MC) simulation alone, since a large fraction of backgrounds are due to detector inefficiencies and/or physics events that have poor MC modeling. Instead, this analysis estimates the background from the data itself, by using the so-called ‘ABCD’ method.

The ABCD method consists of placing events in data that pass the signal selection on a 2D histogram, with a suitable choice of two kinematic quantities as the X and Y variables. These two variables must be uncorrelated, a very important assumption. Then this histogram is divided into 4 regions or ‘bins’, and the one with the highest fraction of expected signal events becomes the ‘signal’ bin (call it the ‘C’ bin). The other three bins should contain mostly background events, and with the assumption that X and Y variables are uncorrelated, it is possible to predict the background in C by using the observed backgrounds in A, B, and D:

$$C\_{\textrm{pred}} = \frac{B\_{\textrm{obs}} \times D\_{\textrm{obs}}}{A\_{\textrm{obs}}}$$

Using this data-driven background prediction for the C bin, all that remains is to compare the actual observed yield in C to figure out if there is an excess, which could be attributed to the new physics under investigation:

$$\textrm{excess} = C\_{\textrm{obs}} - C\_{\textrm{pred}}$$

As an example, Table 1 shows the number of background events predicted and the number of events in data observed for the 2016 run.

{{< figure src="yields.jpg" numbered="false" title="Table 1. Observed yield in data ($N\_{\textrm{obs}}^{\textrm{data}}$) and predicted background yields ($N\_{\text{bkg(no C)}}^{\textrm{post-fit}}$ and $N\_{\textrm{bkg}}^{\textrm{post-fit}}$) in the LHC 2016 run, for all four bins (C is the signal-enriched bin). The observed data is entirely compatible with the predicted background, and no excess is seen." >}}

Combining all the data, the CMS Collaboration did not find an excess of events over the expected background, which would have suggested evidence of new physics. Using statistical analysis, the collaboration can place upper limits on the possible mass and lifetime of new supersymmetric particles predicted by GMSB, based on the absence of excess events. The final result of this analysis is shown in Figure 3, where a mass of up to 500 GeV for the neutralino particle is excluded for lifetimes of 1 meter (here we measure lifetime in units of length by multiplying by the speed of light: $c\tau$ = 1 meter).

{{< figure src="exclusion.jpg" numbered="false" title="Figure 3. Exclusion plots for the GMSB model, featuring exclusion contours of masses and lifetimes for the lightest supersymmetric particle (the neutralino). At its most sensitive mass region (around lifetimes of 1 meter) the CMS result excludes a mass of under 500 GeV for the neutralino, while for lower masses (100-200 GeV) the lifetime exclusion is quite high at around 100 meters or so." >}}

The mass coverage of this search is higher than the previous search done by the ATLAS Collaboration with run 1 data (i.e. years 2010-2012 only), with a much higher sensitivity to longer lifetimes (up to a factor of 10 depending on the mass). But the ATLAS detector has a longitudinally-segmented calorimeter which allows them to precisely measure the direction of displaced photons, and when they do release their results for this search using run 2 data (2016-2018), it should also feature quite a large gain in sensitivity, potentially overshadowing this CMS result. So stay tuned for this exciting cat-and-mouse game between LHC experiments!

### Further Reading

* CMS's press release: https://cms.cern/news/its-never-too-late-photons-cms
* CERN article about LLPs: https://home.cern/news/news/experiments/long-lived-physics
* Symmetry magazine article about LLPs: https://www.symmetrymagazine.org/article/the-secret-lives-of-long-lived-particles

### Footnotes

1: Here we use the notation MET instead of $P\_T^{\textrm{miss}}$ when referring to missing transverse momentum for typesetting reasons.
