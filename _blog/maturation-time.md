---
title: Fluorescence maturation time - is it a bug or a feature?
subtitle: 
#status: inactive #active if you want it on the frontpage

category: paper

description: |
  Using fluorescent maturation delays to infer gene expression dynamics from static snapshots of cell-to-cell variability.

people: # add peope that are involved in this project
  - euan

layout: blog # do not change this
image: '/img/posts/maturation-time/mother_machine_timetrace.jpg'
#link:
no-link: false # if you don't want it's own webpage
last-updated: 2021-8-2
# do NOT add 0 (such as 06 for June). Will break everything lol
# take out the underscore in the name.
---


<sub><b>Giants this stands on[^1]:
M. Elowitz ([lab](https://www.elowitz.caltech.edu/)), P. Cluzel ([lab](https://cluzel.fas.harvard.edu/)), P.-S. Laplace ([wiki](https://en.wikipedia.org/wiki/Pierre-Simon_Laplace)), and D. Prasher ([wiki](https://en.wikipedia.org/wiki/Douglas_Prasher)).</b></sub>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<sub><b>10 minutes read </b></sub>



 

[^1]: and many many more of course! 



<img src="/img/posts/maturation-time/FPs.jpg" alt="idp" width="250px" align="right" style="padding:15px;">
Fluorescent proteins are an invaluable tool used to visualize cellular processes ([Exhibit A: Nobel Prizes 2008](https://www.nobelprize.org/prizes/chemistry/2008/illustrated-information/), [Exhibit B: Nobel Prize 2014](https:/www.nobelprize.org/prizes/chemistry/2014/prize-announcement/), [Exhibit C: This mind-blowing video of a brain](https://www.youtube.com/watch?v=c-NMfp13Uug)).
An important caveat when using fluorescent proteins is that freshly produced proteins are dark and take time before they fluoresce. The time that a fluorescent protein takes to become fluorescent is called the maturation time, and it can range from minutes to hours[^2].  Fluorescent proteins with short maturation times are thus used to avoid delays when probing dynamic systems[^m].



[^2]: This is a fascinating and complex process in [itself](https://link.springer.com/article/10.1007/s00216-008-2425-x#Sec3). 
[^m]: The figure on the right is taken from this great [post](http://book.bionumbers.org/what-is-the-maturation-time-for-fluorescent-proteins/) on fluorescent maturation times. 

Fluorescent maturation delays are analogous to the delayed response of COVID-19 case numbers. Delays in the onset of symptoms, the analyzing of tests, and the reporting of cases lead to a non-instantaneous read-out of the actual number of infections. Such delays are obviously bad for following (or controlling[^4]) dynamics in real-time, but there is an additional effect: the delays in the individual reports of infection are random and not a fixed number, which causes the average variability of the overal signal to be affected. <img src="/img/posts/maturation-time/COVID.jpg" alt="idp" width="250px" align="right" style="padding:15px;"> For example, even if COVID-19 case numbers were delayed by a year, but the delay is always exactly the same, we could still recover the maximum number of cases that actually occurred from retrospective time-traces. However, if some of the cases get reported immediately, some take months, and some take a year, the whole dynamics are washed out, and we can no longer identify the size of the peak. The variability of the curve will be washed out due to the probabilistic delay of individual reports. Similarly, the same is true for fluorescence levels in cells because the maturation time of an individual protein is random[^5] and not a fixed number. Picking a fluorescent protein with fast maturation is thus a key experimental consideration[^6], as large maturation times lead to this time-averaging effect in the fluorescence levels, acting as an experimental bug that washes out the information in the observed signal.


[^4]: See COVID-19 pandemic.
[^5]: Most are exponentially distributed, although some look more like a double exponential. The key is that it is not a fixed delay, i.e., if a fluorescent protein has a 20 min maturation time, some will take 1 min and some will take 40 min to mature.
[^6]:Other properties like brightness and toxicity matter as well.


However, instead of focusing on minimizing this experimental bug, we asked: can we use this built-in time-averaging effect of fluorescence levels to our advantage? The answer is *yes we can!*<sup>TM</sup> This is because the degree to which an exponentially distributed delay washes out a signal depends on the *dynamics* of the signal itself. As a result, the variability of a time-averaged signal implicitly encodes information about the dynamics of the upstream signal[^7]. 
In particular, if we have two different fluorescent proteins X and Y reporting the same upstream signal, i.e., the transcription rate of a gene of interest, then the differences in variability will tell us something about the time-scale of the transcription rate variability. In fact, it's not just the time-scale of the invisible upstream dynamics of the signal that matters, but also its temporal structure! That's the entire (very simple) idea we are exploiting. The rest is just filling in the mathematical details which are all in [this](https://journals.aps.org/pre/abstract/10.1103/PhysRevE.104.044406) paper[^8].

<p align="center">
<img src="/img/posts/maturation-time/mother_machine_timetrace.jpg" alt="idp" width="600px" style="padding:5px;">
</p>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<sub><b>Time-lapse microscopy data of single cells expressing two fluorescent proteins that share an oscillating transcription rate[^r]. </b></sub>

[^r]: This is work in progress. The fluorescent proteins were engineered to report the activity of a synthetic oscillator known as the   [Repressilator](https://www.nature.com/articles/nature19841).
[^7]: It turns out that the variability of a time-averaged signal corresponds to the Laplace transform of the upstream signal.
[^8]: Somewhere in Appendix A, Appendix B, Appendix C, Appendix D, Appendix E, Appendix F, Appendix G, Appendix H, Appendix I, Appendix J, Appendix K, Appendix L. Yes, we had to use almost the whole alphabet.





<br /> For example, oscillations are different from stochastic signals.  Time-averaged responses of the latter are constrained by
<p align="center">
<img src="https://render.githubusercontent.com/render/math?math=T_{m} \leq \frac{CV_{x}}{CV_{y}}," width="110">
</p>

<img src="/img/posts/maturation-time/Oscillation_bound.jpg" alt="idp" width="420px" align="right" style="padding:10px;">
where <img src="https://render.githubusercontent.com/render/math?math=T_{m} := \tau_{mat,y}/\tau_{mat,x}"> is the ratio of maturation times[^9] of the two fluorescent proteins, and CV is the coefficient of variation obtainable from static snapshots of cell-to-cell variability. Any violation of this inequality[^10] implies that the transcription must be oscillating, even without having to follow cells over time or directly observing the transcription rate. This is crucial, because in recent years there has been an explosion of data produced from high-throughput methods like single-cell RNA sequencing and flow cytometry. These methods lack temporal resolution and produce static snapshots of cell-to-cell variability. A key aim of systems biology is to translate such static datasets into gene expression dynamics.

[^9]: Maturation times have recently been precisely measured thanks to amazing [work](https://www.nature.com/articles/nmeth.4509) from the Cluzel lab, with all their data publicly available.
[^10]: We derive constraints on whole classes of systems so as to make few assumptions that can be tested. Here our classes are defined by co-regulation and exponential maturation kinetics.

<img src="/img/posts/maturation-time/Circuit.jpg" alt="idp" width="225px" align="right" style="padding:15px;">
Engineering co-regulated fluorescent reporters to readout a signal of interest is not new. In fact, such "dual reporters" have previously been used to quantify sources of non-genetic variability in gene expression[^11]. However, a fundamental issue remains when interpreting cell-to-cell variability: we generally do not know whether a component’s variability is due to stochastic upstream noise or whether a component is driven by deterministic variability. The above equation can thus become and experimental tool to distinguish cell-to-cell variability that is caused by deterministic oscillations[^12] from variability due to stochastic fluctuations. 

[^11]: Credit for this brilliant idea goes to Michael Elowitz who first used identical co-regulated reporters just like "identical twins" to quantify sources of variability in [cells](https://www.science.org/doi/10.1126/science.1070919).
[^12]: There are no truly deterministic oscillations in cells. Every signal will be to some extent stochastic, but we can still define signals as oscillatory if their stochasticity is not so strong as to wash out the periodicity of an oscillatory signal.

There are quite a few more ideas in this paper (such as detecting feedback), and if you're interested you can read about them [here](https://arxiv.org/abs/2109.00392). Currently we are working on an experimental collaboration to test these results in live cells using a synthetic biology approach. We hope to share with you the results of these experiments another time.




