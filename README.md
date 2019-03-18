[![Documentation Status](https://readthedocs.org/projects/pyhht/badge/?version=latest)](https://readthedocs.org/projects/pyhht/?badge=latest)
[![Build Status](https://travis-ci.org/jaidevd/pyhht.svg?branch=dev)](https://travis-ci.org/jaidevd/pyhht)
[![Coverage Status](https://coveralls.io/repos/github/jaidevd/pyhht/badge.svg?branch=dev)](https://coveralls.io/github/jaidevd/pyhht?branch=dev)
[![Code Health](https://landscape.io/github/jaidevd/pyhht/dev/landscape.svg?style=flat)](https://landscape.io/github/jaidevd/pyhht/dev)

GPHHT (work in progress ...)
=====

Common implementations of the Hilbert Huang Transform are known to be affected by a finite-size effect known as "edge problem". Namely, in order to find the signal envelope, the usual approach is to interpolate local extrema with a spline polynomial, which in turn raises the following dilemma: is it better to
A) crop the signal to the region where both the lower and upper envelopes formally exist, which at low frequencies can reduce data by a considerable ammount; or
B) exploit features of the signal itself in order to mimic the correct behavior of the evelopes in the edges' neighbourhood, at the cost of introducing a prior knowledge (in Bayesian language) on the underlying process.

While A) is more accurate for signal analysis, it is virtually useless for predictions, as it forbids one to avail on the last portion of the signal. Practitioners therefore ofter chose the B) option. A common work-around is to mirror the signal across the edges in order to extend the envelope splines. Nonetheless this creates "leakage" issues -- the splines do not trace perfectly local extrema, but go reasonably near them. Moreover mirroring is a rather strong prior assumption. 

I attack the problem in a different way -- I use a Gaussian Process Regression to compute the envelopes of local extrema rather than interpolating splines. This has the following advantages: allows to explit the autoregressive features of the signal itself, thus introducing a much weaker prior; incorporates the notion of an observational error, minimises leakage effects. Cleary, it comes at the cost of being a much more computationally intensive.

**Based on @jaidevd pyhht module**

Dependencies
------------
The module has been tested to work on Python 2.7 and Python 3.6. It requires NumPy, SciPy and
matplotlib.

pytftb is required to run some examples. It can be found at:

http://github.com/scikit-signal/pytftb
