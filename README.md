# CME distribution model

This repository accompanies the paper "Geometric suppression of stellar CME Doppler
signatures" by 
A.G.M. Pietrow, M. De Wilde, M. Druett, H. Eklund,
J. D. Alvarado-Gomez, V. Fedun. 

Coronal Mass Ejections expel large quantities of charged plasma into space.
High resolution solar images revealed many CMEs that create geomagnetic storms.
Stellar CMEs are detected using Doppler shifts. But they are very rarely seen, even on Sun-like stars.
There are lots of theories that explain this paucity in CMEs.
We use a toy model to demonstrate that the typical distribution of CMEs over the solar surface,
combined with a randomised viewing angle, dramatically reduces the chance of a detection via a Doppler shift.
This underlying geometrical bias has strong implications for our theories of magnetism and habitability around Sun like stars.

The notebooks below provide the walk through to calculate, for any input 3D distribution of flares/AR, the 2D viewing angle distribution for CME's and flares.

## Requirements

Python 3.9+ with the packages listed in [`requirements.txt`](requirements.txt) (`numpy`, `scipy`, `matplotlib`,
`pillow`, `jupyter`):

```
pip install -r requirements.txt
```

Each notebook is self-contained and can be run independently with "Run All", in the order listed below.
Notebooks that repeat an expensive numerical integration cache their result as a `.npy` file under
`calculations/` (or `<folder>/calculations/` for the notebooks in `Fast rotators/`); delete the relevant
file there to force a recompute.

## Scheme

    1. We fit a rice distribution to the experimental flare distribution (see experimental_flare_distribution.ipynb)

    2. We calculate the general distribution of flares in viewing angle mu (see flare_viewing_angle_distribution.ipynb)

    3. We calculate the overall distribution of CMEs in viewing angle beta. The integral was numerically calculated (see CME_distribution.ipynb)

    4. We repeated in  CME_distribution.ipynb the procedure for other flare distribution on stars, e.g. a polar flares star with a normal distribution of flares around both poles, or a normal distribution around the equator. We also considered a step function around the equator as a possibility, which has as a curiosity sharp edges showing up in its subsequent distributions as well.

    5. Stars with rotational velocities in the same order of magnitude as the CME velocity are considered fast rotators in this study. For them we need to calculate the distortion of their rotation on the distribution of projected velocities. This is done in CME_distribution_rotation.ipynb. 

    6. The calculated CME distributions are true distributions of flares that originate from their base location. However, experimentally a flare seen is not assigned to its base location if by projection effects the flare appears to be closer to the limb. The projection also allows behind the limb flares to be misclassified as on the limb, causing an artificial bump there. This projection is only needed for flare location data originating from spacially resolved observation, not from Doppler shift methods. We have incorporated this in flare_viewing_height_correction.ipynb to test our model on solar flares. 

    7. We test how changing the CME ejection angle distribution changes the overall distribution in CME_dist_multiple_output_angles.ipynb. The angle of ejection compared to the zenith is still an active topic of study and might be different on different stars. For solar flares this is assumed to be in the range of 20 to 30 degrees. But for completeness we examine 20, 23, 60 and 90 degrees.

    8. One of the most studied stars concerning CMEs is EK Draconis, which counted 2 CMEs associated to 11 flares. We calculated the expected percentage of captured CME per flare our model predict for the star EK Draconis (See EK_Draconis_CME_observation_ratio.ipynb). 

    9. We investigated the effect of Spörer's law (equatortowards migration of AR) over the solar cycle on the change in distribution for the sun. This was done in flare_latitude_solar_cycle_fourier.ipynb.

The important take-away, is that given a known distribution of active regions/flares and the orientation of the star, this codes gives a quick calculation of the distribution of expected flares for different redshifts. However, when averaged over orientation of the rotation axis of the star a sine distribution is obviously the correct mean.

## Repository layout

Beyond the seven notebooks above:

- `calculations/` — cached `.npy` results for the expensive numerical integrals in `CME_distribution.ipynb`
  and `CME_dist_multiple_output_angles.ipynb`, keyed by scenario name. Safe to delete; notebooks recompute
  and repopulate the cache automatically (this can take a while, see the note under Requirements).
- `RGO_NOAA1874_2013/` — the raw Royal Greenwich Observatory / USAF-NOAA sunspot-group data
  (1874-2013, one file per year) used to fit the active-region latitude distribution in
  `experimental_flare_distribution.ipynb`.
- `Figures/` — notebooks used to produce the figures in the paper (`coordinateplot.ipynb` for the
  coordinate-system schematic, `Figures_CME_distribution_AND_bands.ipynb` for the CME-distribution plots),
  plus the exported PDFs.

## Notation

The symbols below are used consistently across all notebooks and follow the associated paper:

| Symbol | Code | Meaning |
| --- | --- | --- |
| α | `alpha` | Colatitude of an active region/flare, measured from the star's rotation pole |
| θ, φ | `theta`, `phi` | Colatitude/azimuth of a point on the star, measured from the observer's line of sight |
| τ | `tau` | Stellar orientation (inclination): 0 is pole-on, π/2 is equator-on |
| θ' | `theta2` | CME ejection angle, measured from the local zenith |
| β | `beta` | Angle between a CME's direction and the line of sight (β=0 ⇒ maximal Doppler shift) |
| μ | `mu` | cos(θ): line-of-sight-projected latitude of a flare |
| ρ(α) | `rho` | Active-region/flare distribution over the stellar surface |
| ρ<sup>CME</sup>(θ') | `rho_CME` | CME ejection-angle distribution |

All the angles can be seen visually in Figures/coordinate_plot.pdf

## License

MIT — see [`LICENSE`](LICENSE).
