# Correlation between several cosmological quantities using a machine learning model based on cosmological simulation data

# Yuxuan Cao, Kaile Wang, Saiyang Zhang, Joohyun Lee


## Goals
Study the correlation between SMBH merger history and DM halo merger history, i.e. rebuild SMBH growth history from host halo merger history + their properties

### Models to be used: 
regression (e.g. multi-variate), classification (e.g. random forest), machine learning

### Variables in the problem:
#### Dependent : 
- BH Merger rate (host halo properties, BH properties)
- BH Merger mass ratio (host halo properties, BH properties)
#### Independent: 
- Host halo properties: host merger rate, host merger mass ratio, mass, spin, central density, maximum rotation velocity, …
- BH properties: chirp mass, spin angle, mass, velocity, …


## Links to data
[IllustrisTNG100-1 cosmological simulation](https://www.tng-project.org/data/downloads/TNG100-1/)

[Reduced data on Box](https://utexas.box.com/s/5ke8msfwskzskik3c6oze9e2mlgaw37u)

## Colab Workspace

[Saiyang's Notebook For Data Reduction](https://colab.research.google.com/drive/19lVFtTtRoalElVUE_KS4pIs0btGfIaMR?usp=sharing)


## Description of reduced data
- h = 0.6774, ckpc: comoving kpc (to get physical kpc, multiply by scale factor a)
- `halodata_tng100-1_Nth.npy` (`N*23` array, float32)<br>
Numpy array containing halos' physical properties in the Nth snapshot. The fields of each column are listed. Quantity (Unit)<br>
`SubhaloMass (Msun) halodata[:, 0]` `SubhaloMassType[0,1,4,5] (Msun) halodata[:, 1:5]` `SubhaloPos (3D, kpc) halodata[:, 5:8]` `SubhaloVel (3D, km/s) halodata[:, 8:11]` `SubhaloSpin (3D, kpc*km/s) halodata[:, 11:14]` `SubhaloVmax (km/s) halodata[:, 14]` `SubhaloVmaxRad (kpc) halodata[:, 15]` `SubhaloHalfmassRadType[0,1,4] (kpc) halodata[:, 16:19]` `SubhaloStarMetallicity halodata[:, 19]` `SubhaloGasMetallicity halodata[:, 20]` `SubhaloSFR (Msun/yr) halodata[:, 21]` `SubhaloBHMass (Msun) halodata[:, 22]`<br>
(For `SubhaloMassType`, it is an `N*4` array, with each column meaning the total mass of particle type 0: Gas, 1: DM, 4: Star, 5:BH)<br>
(For `SubhaloHalfmassRadType`, it is an `N*3` array, with each column meaning the total mass of particle type 0: Gas, 1: DM, 4: Star)<br>

- `haloID_tng100-1_Nth.npy` (`N*3` array, int64)<br>
Numpy array containing halos' IDs in the Nth snapshot. The fields of each column are listed. Refer to the `IllustrisTNG` `SubLink` merger tree description to understand the meanings of `NextProgenitorID` and `FirstProgenitorID`.<br>
`SubhaloID` `NextProgenitorID` `FirstProgenitorID` (-1: no NextProgenitor/FirstProgenitor for this halo, otherwise: ID of NextProgenitor/FirstProgenitor)

For a relationship between halo, and its pregenitor, one can refer to https://www.tng-project.org/data/docs/specifications/#parttype1 under section 4. In the cosmic evolution picture, the DM halo grows by eating up other halos (with tractable ID) and surrounding material (untraceable and more diffuse). The halo merger tree is basically a tree-like data structure with halo IDs on the node of the tree, having a total of n = 100 levels, the same as the total snapshot number within the data frame.  It is taking track of how the halo has grown throughout cosmic time, through merging with lighter haloes to a more massive halo we see in the present day. Here, the smaller the level(snapshot) is, which corresponses to higher redshift(earlier epoch in the universe history), the lower the hierarchy within this tree. From i+1 th to i th level, for a node on the i+1 th level, the `FirstProgenitorID` links to the main branch of its child nodes(progenitor halo ID) on the ith level. Then, `NextProgenitorID` is much less important in that it only points to the child node that belongs to the same parent within the same tree level. (More like a deep-first search algorithm to traverse over the tree structure)  

Here, to simplify the problem, we only track the `FirstProgenitorID` of the most massive haloes of our selection within the snapshot 99, to track the growth of halo and SMBH within the halo.



## Data description
- One of the state-of-the-art cosmological hydrodynamic simulations of galaxy formation
- Helps to understand when and how galaxies evolve into the structures that are observed


## References
[https://ui.adsabs.harvard.edu/abs/2023MNRAS.518.2123Z/abstract](https://ui.adsabs.harvard.edu/abs/2023MNRAS.518.2123Z/abstract)<br>
[https://ui.adsabs.harvard.edu/abs/2023MNRAS.523L..69Z/abstract](https://ui.adsabs.harvard.edu/abs/2023MNRAS.523L..69Z/abstract)
