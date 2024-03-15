# Correlation between several cosmological quantities using a machine learning model based on cosmological simulation data

# Yuxuan Cao, Kaile Wang, Saiyang Zhang, Joohyun Lee


## Goals
Study the correlation between SMBH merger history and DM halo merger history, i.e. rebuild SMBH growth history from host halo merger history + their properties

### Models to be used: 
regression(e.g. multi-variate), classification (e.g. random forest), machine learning

### Variables in the problem:
#### Dependent : 
- BH Merger rate(host halo properties, BH properties)
- BH Merger mass ratio(host halo properties, BH properties)
#### Independent: 
- Host halo properties: host merger rate, host merger mass ratio, mass, spin, central density, maximum rotation velocity, …
- BH properties: chirp mass, spin angle, mass, velocity, …


## Links to data
[IllustrisTNG100-1 cosmological simulation](https://www.tng-project.org/data/downloads/TNG100-1/)

[Reduced data on Box](https://utexas.box.com/s/5ke8msfwskzskik3c6oze9e2mlgaw37u)


## Description of reduced data
- h = 0.6774, ckpc: comoving kpc (to get physical kpc, multiply by scale factor a)
- `halodata_tng100-1_Nth.npy` (`N*16` array, float32)<br>
Numpy array containing halos' physical properties in the Nth snapshot. The fields of each column are listed. Quantity (Unit)<br>
`SubhaloMass (Msun)` `SubhaloMassType[0,1,4,5] (Msun)` `SubhaloPos (3D, kpc)` `SubhaloVel (3D, km/s)` `SubhaloSpin (3D, kpc*km/s)` `SubhaloVmax (km/s)` `SubhaloVmaxRad (kpc)`
<br>
(For `SubhaloMassType`, it is an `N*4` array, with each column meaning the total mass of particle type 0: Gas, 1: DM, 4: Star, 5:BH)
- `haloID_tng100-1_Nth.npy` (`N*3` array, int64)<br>
Numpy array containing halos' IDs in the Nth snapshot. The fields of each column are listed. Refer to the `IllustrisTNG` `SubLink` merger tree description to understand the meanings of `NextProgenitorID` and `FirstProgenitorID`.<br>
`SubhaloID` `NextProgenitorID` `FirstProgenitorID`


## Data description
- One of the state-of-the-art cosmological hydrodynamic simulations of galaxy formation
- Helps to understand when and how galaxies evolve into the structures that are observed


## References
[https://ui.adsabs.harvard.edu/abs/2023MNRAS.518.2123Z/abstract](https://ui.adsabs.harvard.edu/abs/2023MNRAS.518.2123Z/abstract)<br>
[https://ui.adsabs.harvard.edu/abs/2023MNRAS.523L..69Z/abstract](https://ui.adsabs.harvard.edu/abs/2023MNRAS.523L..69Z/abstract)
