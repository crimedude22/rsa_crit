---
title: "rsa crit"
author: "Jonny Saunders"
date: "2017-10-30"
site: bookdown::bookdown_site
documentclass: book
bibliography: /Users/jonny/Documents/BibTeX/rsa.bib
biblio-style: apalike
link-citations: yes
github-repo: crimedude22/rsa-crit
url: 'https://crimedude22.github.io/rsa_crit/'
---
# rsa crit

** https://www.math.upenn.edu/~ghrist/notes.html

** http://cns-classes.bu.edu/cn510/Papers/Theoretical%20Neuroscience%20Computational%20and%20Mathematical%20Modeling%20of%20Neural%20Systems%20-%20%20Peter%20Dayan,%20L.%20F.%20Abbott.pdf decoding chapter, need to incorporate the rest of the bayesian model, and have to account for the 'tuning' of the individual voxels for the particular stimuli. assumption that our representation is unbiased depends on law of large numbers -- have to have enough cells representing feature space roughly equally. to the degree that the strength of response (the dot product between stimulus features and voxel selectivity) is nonuniform, so to will be representation measured by RSA. Then, we are not measuring differences in representation, but differences in selectivity, and the procedure by which we select our ROI becomes the basis of the experiment.

** there is indeed no reason to believe that similar stimuli will be closely grouped in the vector space of voxel activations, because it is entirely possible that whatever "downstream" decodes this representation has its own set of weights that recombine that representation. give simple example of NNs

** fisher information gives a way of formulating the fact that different neurons give different amounts of information to a representation, and within a neuron, carries different amount of information depending on its fr/max fr.

** indeed very similar stimuli giving very similar patterns of activity would be suboptimal for a universal recognition scheme -- cf. to the hippocampal model of pattern orthogonalization. We would expect and want patterns to be maximally different for very similar stimuli. How do experts learn to tell very minute differences apart? 

** https://arxiv.org/abs/1212.4201
** https://arxiv.org/abs/1605.01905

** https://arxiv.org/pdf/1605.01905.pdf homotopy assumptions, good cover. Also idea of 'local obstructions', and constraint of neural codes


# Introduction

As neuroscience overcomes the technical barriers to observing neural activity at quantity and speed are being rapidly overcome, the problem of understanding those observations <soon> follows. An increasing complexity of neural data drives ever more ambitious interpretations, and the space between the data and its interpretation are necessarily filled with equally obscure methods of analysis and the philosophy that justifies them.

<we also jump into analysis techniques too quickly without thorough evaluation due to the pressure and pace of publication>

Representational Similarity Analysis (RSA), in its attempt to "connect the branches of systems neuroscience,<cite>" <is in need of some checkin of its homework> <the attempt shouldn't be to "abstract from particular emprical modalities," but we aware of the way that those modalities depart from the computational substance of the brain.> <statement of which RSA we are talking about, which papers were are using to build the decription and which have used it>

## Representational Similarity Analysis - Qualitatively

The premise of RSA is that the structure of neural representation can be estimated by the "second-order isomorphism" between sensory input and its representation [@Kriegeskorte2008 @Shepard1970]. Rather than attempting to estimate neural representation as a function of sensory input directly, RSA first compares the neural representations evoked by an array of stimuli and the properties of those stimuli within themselves and then compares those comparisons <give graphic here>. The purported advantage of this approach is that it provides a universal abstraction of the idiosyncratic implementation of neural representation, making comparisons between individuals, brain regions, and measurement modalities possible without estimating the specific transformation that relates them.

It assumes that measured brain activity is directly representative of a presented stimulus. The brain activity is assumed to be measured and summarized in a way that faithfully preserves the character of its code (example here?). This summarized brain data is assumed have a <numeric> structure that supports the calculation of dissimilarity between all values. Since summarized brain activity is directly representative of a stimulus, those dissimilarity measurements are assumed to be directly related to the dissimilarity measurements of the stimuli or the features they comprise -- the object of the technique is to evaluate that relationship. This assumption is the conceptual foundation of the second-order isomorphism framing: "although the internal representation for a square need not itself be squre, it should (whatever it is) at least have a closer functional relation to the internal representation for a rectangle than that, say, for a green flash or the taste of persimmon." [@Shepard1970].

In short, the dissimilarity measurements have to be correctly specified, and their comparison has to be meaningful.

Further assumptions depend on what is being compared and by whom. If two neural representations are being compared, it is assumed that they share "overlapping information" [@Kriegeskorte2008] in three senses: 1) that they literally share information -- they are representing the same stimulus, 2) that their dissimilarities were computed in a way that is equally compatible with, or, offers equal fidelity to the neural code they summarize 3) were computed such that their units can be meaningfully compared without transformation. If a neural representation is being compared to parametrically generated stimuli, it is typically <cites> assumed that the parameters are a good numerical specification of the features encoded in the neural representation. The technique is also restated as a framework for model testing, and when the dissimilarity structure of neural data is compared to that of a model, it is typically <cites> assumed that greater similarity between the two implies greater similarity in their representations.

These assumptions give a template for data analysis [@Kriegeskorte2008]. Typically, neural activity is summarized as a trial-average of its amplitude at each recording site over the duration of the stimulus. A dissimilarity matrix is computed from the population summary for each pair of stimuli using 1 minus the Pearson correlation coefficient or Spearman rank correlation coefficient. <figure fsho>. This dissimilarity matrix is then compared to a number of other dissimilarity matrices computed from other neural datasets, stimulus parameters, or models, typically with one minus the Pearson or Spearman correlation coefficients. Confidence intervals around the comparison are computed by randomly permuting the category labels.

## Representational Similarity Analysis - Mathematically

No mathematical description of RSA has been given. Such a description is useful for making assumptions and practices explicit.

Some population of neurons $\vec{N} = {n_{1}, n_{2}, \dots, n_{i}}$ represents some stimulus $s$ as some continuous pattern of spikes over time $\vec{R}^\vec{N}_s$

$$\begin{equation}
\vec{R}^\vec{N}_s = f(s, t) + e \mid \vec{R}^\vec{N}_s \in \mathcal{R}
\end{equation}$$

with some noise $e$, where $\mathcal{R}$ is a metric space. In this treatment, a single presentation of $s$ is functionally equivalent to many since $f$ is assumed to be identical on every presentation, and $e$ is assumed to be independent and identically distributed.

The representation $\vec{R}^\vec{N}_s$ can be summarized by an isometric function $g$ -- one that preserves the metric structure in the image of $f$ -- as

$$\begin{equation}
\vec{X_s^\vec{N}} = g(\vec{R}^\vec{N}_s) \mid \vec{X_s^\vec{N}} \in \mathcal{X}\\
d_{\mathcal{X}}(g(\vec{R})) = d_{\mathcal{R}}(\vec{R})
\end{equation}$$

where $\mathcal{X}$ is a metric space. Put another way, $\mathcal{X}$ is embedded in $\mathcal{R}$ $g: \mathcal{X} \rightarrow \mathcal{R}$ without distortion. 

## Criticism - Theoretical

* Criticisms regarding the assumptions or formtulation of the technique

re: share information - measured with equal fidelity of code -- compare amplitude averaging for am-noise stimulus-locked cell vs. rate tuned cell.

ignores alternative coding theories, ie. pattern orthogonalization, in favor of some vague evolutionary argument "...would be of adaptive utility..."@Shepard1970 .

** even shepard used multidimensional scaling to comapre similarity matrices -- the basis of multidimensional scaling is the observation that it is impossible to assume that two metric spaces will be the same.

not at all possible to assume that it's directly representing the stimulus as you present and describe it, why not represented as conceptual 

Interpretation cannot be extended to the structure of the neural representation -- that's precisely what you abstracted out of, you can't buy it back at the end. You specifically can't say that the neural representation between x and y is the same, just that they have the same dissimilarity structure. Since there are infinitely many ways to represent a stimulus, there are infinitely many that give the same dissimilarity structure. no free information. related to nontransitivity of correlations

## Criticism - Practical

* Criticisms regarding the particular practice of the technique that have alternatives that don't functionally change the technique.bg
fd
## Lit Review

(table of all the papers and what problematic elements they have used)

# argument

**theoretical**
1. assumption of a meaningfully euclidean neural manifold
** 1-correlation is euclidean distance http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.19.8732&rep=rep1&type=pdf Lemma 1
** The scaling is uncertain - one cannot assume that a stimulus with half the distance from another stimulus is twice as similar. in fact, most examples demonstrate otherwise.
** MDS requires the assumption of ordinality, but there is no reason to assume that for neural data - what if one voxel's activation changes its 'meaning' depending on the state of other voxels? such a circumstance is the rule rather than the exception in nonlinear systems.
** Metric axioms - minimality (others more dissimilar than selves) is treated as an outcome rather than a presupposition, symmetry - transition between states is certainly not symmetrical, triangle inequality - not true if neural manifold is curved at all
2. the second-order isomorphism allows plucking gold from noise by collapsing error at successive levels to means
3. error around 'representation' assumed to be noise around underlying 'real' population average representation == state is not important.
4. multiple types of similarity - association (bread and butter) is different than similarity (red and red-orange)

**statistical**
3. transitivity of correlations
4. omitted variable bias - distance matrices are only meaningful to the degree that they replicate or diverge from the stimulus distance matrix, and that distance matrix is only reasonable to the degree that it is free from omitted variable bias -- that it accurately captures perceptual space. 
5. 

## http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.136.5427&rep=rep1&type=pdf

An important issue in the context of distance functions is the question under which conditions a given dissimilarity space (X,d) can be embedded isometrically into Euclidean spaces H. Here the goal is to find a mapping Φ : X → H such that d(x, y) = ∥Φ(x) − Φ(y)∥ is satisfied for all x, y ∈ X . As distances in vector spaces always satisfy all axioms (D1) - (D5), isometrically embedding a dissimilarity space into a vector space is only possible if the dissimilarity function is a metric. This is a necessary condition, but it is not sufficient. A characterization of met- ric spaces which can be embedded isometrically into Hilbert spaces was given by Schoenberg (1938): A metric space (X,d) can be embedded isometrically into a Hilbert space if and only if the function −d2 is conditionally positive definite, that is − li,j=1 cicjd2(xi,xj) ≥ 0 for all l ∈ N, xi,xj ∈ X, and for all ci,cj ∈ R with  i ci = 0. Such a metric is called a Euclidean metric. Contrary to embeddings into Hilbert spaces, isometric embeddings into certain Banach spaces can be constructed for arbitrary metric spaces. Such constructions will be discussed in detail in Section 2

* neural activations are 'representations' - incl. that measurement variance is noise around some true 'representation'
** "We can think of a brain region’s representation as a multidimensional space. The dimensions of the space correspond to the neurons, and a point corresponds to an activity pattern (i.e., each neuron’s activity provides the coordinate value for one of the dimensions)." - kriegeskorte 2013
* Those represenations are meaningfully compared using 1-correlation, or 1-rank correlation, ie. they are a hilbert space.
* Rather than measure the quality or nature of those represenations themselves, we can measure a 'second-order' isomorphism, or measure the relationship between the dissimilarities of neural representations and those of the stimuli -- which can be estimated using the components of computational models.
* The quality of that second-order isomorphism can be computed by randomizing the condition labels.



* assume that neural activity is some probabilistic function of the stimuli, and compare it to some other function that compares distances. (since the choice of functions mapping stimulus to representational space is arbitrary, subject to infinite researcher degrees of freedom).

Problems:
* It's not clear that neural representations are 'activations' in themselves, ie. that a stimulus reliably evokes a particular pattern of neural activation. Instead it's entirely possible that representation is state dependent.
* It's almost certainly untrue that, with respect to stimulus representation, that each voxel is equivalently 'important' 
* the comparison of computational models to neural data is not as straightforward as it seems, this is confusing the two types of function estimation in vapnik.


# Simulations to run
* comparisons of RSA using raw spiking data, binned spike counts, etc.

# scrap

* `kriegeskorte 2008` - mistakes useful properties of correlation distance with appropriateness of it use.
* `shepard 1962a` - "Clearly, the success of such an undertaking depends upon the selection of the proper distance function; that is, the function that will transforn~ the proximity measures into Euclidean distances."
* "The consequent nonlinearity of the distance function can magnify seemingly negligible statistical fluctuations of small proximity measures into wild swings of the corresponding estimates for the large distances"
* "The preceding tests have indicated that, when the proximity measures are exactly specifiable as a function of the distances in a known Euclidean configuration, both the function and the configuration can be recovered by
the analysis of those proximity measures alone."

* https://pigeon.psy.tufts.edu/avc/dblough/measurement.htm - integral vs. separable dimensions and euclidean vs minkowski measurements, does the brain have a 'preferred axis orientation?' -- if minkowski, need to also determine the relative 'weight' of each of the dimensions.

* http://ramet.elte.hu/~podani/3-Distance,%20similarity.pdf - The distance is meaningful only if the within-group covariances are homogeneous (more precisely, they estimate the same common covariance matrix), and the distribution of variables is multivariate normal. Sneath & Sokal (1973) em- phasize, however, that the distance measure is less sensitive to the violation of these condi- tions (robustness). Note, further, that computation of generalized distance is possible only if the number of objects is not less than the number of variables. Otherwise matrix W is singular (Appendix C) and cannot be inverted. The same problem arises if the correlation of any two variables is –1 or 1, or if the variance of one or more variables is zero.

* Shepard 1970 doesn't really argue for the 2nd-order isomorphism as literal neural representations.

* Vector space qualities pg. 24 https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=4&cad=rja&uact=8&ved=0ahUKEwiVq7aep8_YAhVLzWMKHeYxC2QQFghAMAM&url=http%3A%2F%2Fwww.springer.com%2Fcda%2Fcontent%2Fdocument%2Fcda_downloaddocument%2F9781447140740-c2.pdf%3FSGWID%3D0-0-45-1332402-p174313277&usg=AOvVaw3TKWDlTo_r49F-HBIhWjlN

* relationship between vector spaces and correlation: http://www.pas.rochester.edu/~douglass/papers/Towsley_Pak_Douglass_published_.pdf

* the permutation test is distance correlation: https://en.wikipedia.org/wiki/Distance_correlation


```r
library(ggplot2)

n_stim  <- 92
n_vox   <- 316
n_scans <- 14

# random mean adjustment values for different "codes"
#rep_shunt <- array(rnorm(n_stim))
#rep_shunt <- rnorm(n_stim/23)
rep_shunt <- c(-1,0,1,2)
rep_shunt <- array(rep(rep_shunt, each=23))


# bold means for each stimulus, 

# return vector of mean bold values for each voxel for a stimulus
stim_mean <- function(stim_shunt, scans=n_scans, vox=n_vox){
  s_mean <- colMeans( # mean across presentations
    matrix(nrow=scans, ncol=vox,
      #data=c(rnorm(vox*scans),rnorm(8*vox*scans/9, mean=stim_shunt, sd=0.5)))
      data=rnorm(vox*scans, mean=stim_shunt, sd=0.5))
  )
  return(s_mean)
}

# bold means for each stimulus
subj_rep <- apply(rep_shunt, 1, stim_mean)

# dissim/1-correlation matrix across stim
subj_cor <- cor(subj_rep, method="pearson")
diag(subj_cor) <- 0
subj_cor <- 1-subj_cor

subj_cor_melt <- reshape::melt(subj_cor, varnames=c("stim1", "stim2"))

ggplot(subj_cor_melt, aes(x=stim1, y=stim2, fill=value))+
  geom_raster()+
  scale_fill_distiller(type   = "div", palette="RdGy")
```

<img src="index_files/figure-html/unnamed-chunk-1-1.png" width="672" />

p val estimation from westfall/young p.38-9

```r
# NSIM
nsim <- 10000
nboot <- 1000

counts <- 0
for (i in seq(nsim)){
  if(i%%50 == 0){
    print(i)
  }
  # generate sample data vectors
  v1 <- rnorm(100)
  v2 <- rnorm(100)
  
  r0 <- cor(v1, v2)
  
  # perm test
  countb <- 0
  for (j in seq(nboot)){
    r1 <- cor(v1, sample(v2))
    if(r1>r0){
      countb <- countb+1
    }
  }
  
  if (countb <= 0.05){
    counts <- counts+1
  }
  
}

adj_a <- counts/nsim
```


# Other resources

* https://pigeon.psy.tufts.edu/avc/dblough/measurement.htm
