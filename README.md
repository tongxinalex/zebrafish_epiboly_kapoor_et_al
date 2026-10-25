# Zebrafish epiboly analysis

Custom Python scripts for image processing, analysis, quantification and data handling used in the manuscript (not publicly accessible yet):

> Kapoor T., Tong X., …, Heisenberg C.-P. Apico-basal polarisation sets the basis for epiboly movements during zebrafish gastrulation.

## Contents

| Notebook | Purpose |
| --- | --- |
| [`piv_kymograph_front_aligned.ipynb`](#piv-kymographs-aligned-to-the-epiboly-front) | Build PIV kymographs along the animal–vegetal (A–V) axis, align them to the epiboly front and extract average velocity profiles |
| [`piv_profiles_compare_conditions.ipynb`](#velocity-profiles-across-conditions) | Overlay A–V velocity profiles from different experimental conditions |
| [`front_velocity_stitched.ipynb`](#epiboly-front-displacement-and-instantaneous-velocity) | Track the epiboly front, correct for 3D embryo shape, stitch consecutive movies and compute instantaneous velocities |
| [`plot_replicates_mean_sd.ipynb`](#combining-replicates) | Interpolate replicates onto a common x-axis to plot, average and compute SD/SEM |

## Requirements

- **Python 3** with NumPy, SciPy, scikit-image, scikit-learn, statsmodels, pandas, Matplotlib and Seaborn
- **Jupyter** to run the notebooks
- **MATLAB** with **PIVlab** for particle image velocimetry (PIV)

Exact package versions are listed in the Methods section of the manuscript.

## Workflow

### PIV kymographs aligned to the epiboly front

`piv_kymograph_front_aligned.ipynb`

**Input:** a kymograph made along the A–V axis and the corresponding PIV velocity fields (from PIVlab).

1. Segment the kymograph to obtain the epiboly front position over time.
2. Convert the PIV data into a kymograph over time, with the colour map showing the distribution of the y-component of velocity along the A–V axis.
3. Align the PIV kymograph to the epiboly front.
4. Average the velocity distribution along the A–V axis and plot it as a line profile.

### Velocity profiles across conditions

`piv_profiles_compare_conditions.ipynb`

**Input:** the A–V velocity profiles produced by the previous notebook.

1. Overlay the velocity profiles from different conditions (e.g. wild-type, DMSO-treated, drug-treated) in a single plot.

### Epiboly front displacement and instantaneous velocity

`front_velocity_stitched.ipynb`

**Input:** kymographs drawn along the A–V axis from one or more consecutive movies, and the embryo surface profile sketched from a sectional view.

1. **Segment the kymograph** to obtain the epiboly front position over time.
2. **Correct the displacement for 3D embryo shape.**
   Embryos were imaged as 3D volumetric time-lapses, so kymographs made from maximum-intensity projections systematically underestimate the true displacement of the epiboly front. The displacements are therefore corrected using the 3D embryo surface profile, sketched manually from the sectional view.
3. **Stitch displacements from consecutive movies.**
   At high magnification the epiboly front eventually moves out of the field of view. To follow it, imaging was paused and the stage moved to re-centre the front before starting the next movie. To reconstruct the full trajectory, kymographs from consecutive movies are concatenated by overlapping the front position in the last frame of one movie with that in the first frame of the next.
   Because the displacement during each repositioning gap cannot be measured, each gap is assumed to last one frame, with a displacement equal to that of the final frame of the preceding movie.
4. **Calculate the instantaneous velocity** of the epiboly front from the corrected, stitched displacement.

### Combining replicates

`plot_replicates_mean_sd.ipynb`

Replicates are often sampled at different x-axis intervals, which makes them awkward to plot together, average, or summarise (SD/SEM) in tools such as Origin or Excel. This notebook linearly interpolates each replicate onto a common x-axis so that replicates of the same condition can be plotted in one graph and averaged directly.

## Citation

If you find this code useful, a citation to the manuscript is appreciated but not required.