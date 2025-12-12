# CME distribution toy model

This notebook accompagnied the paper "From sphere to disk
Effects of spherical geometry on coronal mass ejection detection" by 
A.G.M. Pietrow1, M. De Wilde , and et al. 

Coronal Mass Ejections expel large quantities of charged plasma into space.
High resolution solar images revealed many CMEs that create geomagnetic storms.
Stellar CMEs are detected using Doppler shifts. But they are vary rarely seen, even on Sun-like stars.
There are lots of theories that explain this paucity in CMEs.
We use a toy model to demonstrate that the typical distribution of CMEs over the solar surface,
combined with a randomised viewing angle, dramatically reduces the chance of a detection via a Doppler shift.
This underlying geometrical bias has strong implications for our theories of magnetism and habitability around Sun like stars.

This notebook provide the walk trough to calculate for any input 3D distribution of flares/AR the 2D viewing angle distribution for CME's and flares.

Scheme:

    1. We fit a rice distribution to the experimental flare distribution (see experimental_flare_distribution.ipynb)

    2. We calculate the general distribution of flares in viewing angle mu (see flare_viewing_angle_distribution.ipynb)

    3. We calculate the overal distribution of CMEs in viewing angle beta. 
    Because of efficiency we explored with a monte carlo integral (see CME_distribution_mc.ipynb)
    However, the accuracy around $\beta = 0$ was not reached, and the exact integral was numerically calculated (see CME_distribution_ni.ipynb)

    4. We repeated in both notebooks (see CME_distribution_mc.ipynb, CME_distribution_ni.ipynb)
    the procedure for other active region distribution on stars, e.g. a polar flares star with 
    a normal distribution of flares around both poles, or a normal distribution around the equator.
    We also considered a step function around the equator as a posibility, which has as a curiosity
    sharp edges showing up in its subsequent distributions as well.

The important take-away, is that given a known distribution of active regions/flares and the orientation of the star, this codes gives a quick calculation of the distribution of expected flares for different redshifts. However, when averaged over orientation a sine distribution is 
obviously the correct mean.