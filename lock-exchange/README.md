# Lock Exchange demonstration case

Here a description of the test case + link toward the src and notebooks. 
<br>
We here provide a physical description of this experiment and additional details as to how to run this experiment within NEMO. This experiment is **created and tested** for NEMO **code at revision 8097**. 

A ipython notebook is also provided as a demonstration of possible analysis. If you have already run the NEMO experiment and want to analyse the resulting output, you can directly look at the notebook : [here](https://github.com/lesommer/unofficial-nemo-test-cases-repository/blob/master/lock-exchange/notebook/lock-notebook.ipynb).

## Objectives

The LOCK EXCHANGE experiment is a classical fluid dynamics experiment that has been adapted by Haidvogel and Beckmann (1999) for testing advection schemes in ocean circulation models. It has been used by several authors including Burchard and Bolding (2002) and Ilıcak et al. (2012). The LOCK EXCHANGE experiment can in particulart illustrate the impact of different choices of numerical schemes and/or subgrid closures on spurious interior mixing. 

## Physical description

NEMO LOCK EXCHANGE demonstration case follows the specifications of Illicak et al. (2012): 
"A vertical density front separates two density classes. Adjustment occurs in which lighter water moves above heavier water". <br>
For the lock exchange test case, a closed two-dimensional vertical domain with a constant depth of H = 20 m and a length of L = 64 km is considered. Initially, the left half of the domain (x < 32 km) has a density of σt = 5 kg m−3 and the right half of the domain (x ⩾ 32 km) has a density of σt = 30 kg m−3, separated by a vertical line (here salinity is constant = 35 psu). Initial surface elevation and velocity are zero.<br>
At t = 0, the separation is removed such that the dense water is forced under the fresh water, and the system evolves for 17 hours. <br>
Earth rotation, bottom friction and mixing are neglected, such that the effective density mixing is only due to advection of tracers.  <br>

 <img src="./figures/start-lock-exchange.001.jpeg"><br>
 

## Experiments
_The namelists read by the code are the reference namelists "namelist\_ref" overwritten by the configuration namelists "namelist\_cfg"_

* <b>namelist_ref</b> : namelist of reference in which ALL parameters are declared
* <b>namelist_cfg</b> : blocks of namelist of the specific configuration, in which you can set specific parameters.  

For LOCK\_EXCHANGE test case some namelists are available, in which some physical choices already done. To activate one of this namelists just copy it into namelist\_cfg or do a symbolic link to namelist\_cfg.  <br>
In these namelists : <br>
for **lateral diffusion on momentum : (namelist block: "namdyn_ldf")** 

- is applied with a laplacian operator 
- in horizontal direction (ln\_dynldf\_hor=.true.)
- with coefficient 0.01 (coefficient rn\_ahm\_0)

### How to set up a simulation  
```
ln -sf namelist_FCT4_vect_ens_cfg namelist_cfg
```

* Here there is an exemple of simulation with FCT4 advection scheme, vector invariant form, energy conservation : namelist\_FCT4\_vect\_ens\_cfg <br>

Tracer advection scheme: **FCT** (flux-corrected transport scheme) **4th order** on horizontal and vertical <br>

~~~fortran
!-----------------------------------------------------------------------
&namtra_adv    !   advection scheme for tracer
!-----------------------------------------------------------------------
   ln_traadv_fct = .true. !  FCT scheme
      nn_fct_h   =  4            !  =2/4, horizontal 2nd / 4th order
      nn_fct_v   =  4            !  =2/4, vertical   2nd / COMPACT 4th order
      nn_fct_zts =  0            !  >=1, 
~~~

Momentum advection formulation : <br>

~~~fortran
!-----------------------------------------------------------------------
&namdyn_adv    !   formulation of the momentum advection
!-----------------------------------------------------------------------
   ln_dynadv_vec = .true.  !  vector form (T) or flux form (F)
~~~

Vorticity enstrophy conserving scheme : <br>

~~~fortran
!-----------------------------------------------------------------------
&namdyn_vor    !   option of physics/algorithm
!-----------------------------------------------------------------------
   ln_dynvor_ene = .false. !  enstrophy conserving scheme
   ln_dynvor_ens = .true.  !  energy conserving scheme
   ln_dynvor_mix = .false. !  mixed scheme
   ln_dynvor_een = .false. !  energy & enstrophy scheme
~~~

Run the executable : 

``` 
 mpirun -np 1 ./opa 
```

Output files : <br>
LOCK\_FCT4\_vect\_ens\_grid\_T.nc, <br>
LOCK\_FCT4\_vect\_ens\_grid\_U.nc, <br>
LOCK\_FCT4\_vect\_ens\_grid\_V.nc, <br>
LOCK\_FCT4\_vect\_ens\_grid\_W.nc

``` 
N.B. : output file name is set into file_def_nemo-opa.xml in variable name="@expname@"
``` 
In the notebook numerical mixing of the second-order FCT2 and fortht-order FCT4 schemes will be assessed. <br>
When output files are created see the notebook to start some analysis.

## References

Ilıcak, Mehmet, et al. "Spurious dianeutral mixing and the role of momentum closure." Ocean Modelling 45 (2012): 37-58.<br>
Haidvogel, Dale B., and Aike Beckmann. Numerical ocean circulation modeling. Vol. 2. World Scientific, 1999. <br>

