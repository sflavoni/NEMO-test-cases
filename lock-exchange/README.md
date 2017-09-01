# Lock Exchange demonstration case

Here a description of the test case + link toward the src and notebooks. 
<br>
We here provide a physical description of this experiment and additional details as to how to run this experiment within NEMO. This experiment is **created and tested** for NEMO **code at revision 8097**. 

A ipython notebook is also provided as a demonstration of possible analysis. If you have already run the NEMO experiment and want to analyse the resulting output, you can directly look at the notebook : [here](https://github.com/lesommer/unofficial-nemo-test-cases-repository/blob/master/lock-exchange/notebook/lock-notebook.ipynb).

## Objectives

The LOCK EXCHANGE experiment is a classical fluid dynamics experiment that has been adapted by Haidvogel and Beckmann (1999) for testing advection schemes in ocean circulation models. It has been used by several authors including Burchard and Bolding (2002) and Ilıcak et al. (2012). The LOCK EXCHANGE experiment can in particulart illustrate the impact of different choices of numerical schemes and/or subgrid closures on spurious interior mixing. 

## Physical description

NEMO LOCK EXCHANGE demonstration case follows the specifications of Illicak et al. (2012).<br>
For the lock exchange test case, a closed two-dimensional vertical domain with a constant depth of H = 20 m and a length of L = 64 km is considered. Initially, the left half of the domain (x < 32 km) has a density of σt = 5 kg m−3 and the right half of the domain (x ⩾ 32 km) has a density of σt = 0 kg m−3, separated by a vertical line (here salinity is constant = 35 psu). Initial surface elevation and velocity are zero.<br>
At t = 0, the separation is removed such that the dense water is forced under the fresh water, and the system evolves for 17 hours. <br>
Earth rotation, bed friction and mixing are neglected, such that the effective density mixing is only due to advection of density. 
<br>
In the notebook numerical mixing of the second-order FCT2 and fortht-order FCT4 schemes will be assessed.

 <img src="./figures/start-lock-exchange.001.jpeg"><br>
 
## References

Ilıcak, Mehmet, et al. "Spurious dianeutral mixing and the role of momentum closure." Ocean Modelling 45 (2012): 37-58.<br>
Haidvogel, Dale B., and Aike Beckmann. Numerical ocean circulation modeling. Vol. 2. World Scientific, 1999. <br>


## How to set experiment
NEMO code needs : 

* <b>namelist_ref</b> : namelist of reference in which ALL parameters are declared
* <b>namelist_cfg</b> : blocks of namelist of the specific configuration, in which you can set specific parameters. It need to be used to overwrite namelist\_ref blocks 

In EXP00 directory there are available also some pre-set namelist\_cfg with some choices already done. To activate one of this namelist\_xxx\_cfg just rename or do a link to namelist_cfg.

<b> choice is done for ALL experiments for next parameters :</b>

- **laplacian lateral diffusion on momentum** (see namelist block: "namdyn_ldf")
- **horizontal direction** (see namelist block: "namdyn_ldf" ln_dynldf_hor=.true.)
- **with coefficient 0.01** (see namelist block: "namdyn_ldf" coefficient rn_ahm_0)

## Experiment:
* Set of LOCK EXCHANGE run : <br>
*  Choice of : FCT4 advection scheme, vector invariant form, energy conservation

```
ln -sf namelist_FCT4_vect_ens_cfg namelist_cfg
```
### Description of namelist\_FCT4\_vect\_ens\_cfg :
- **FCT4** Advection scheme: FCT (flux-corrected transport scheme) 4th order on horizontal and vertical
- **vect** Vector formulation of the momentum advection
- **ens** Vorticity energy conserving scheme

Run the executable :
``` mpirun -np 1 ./opa ```

Output files : <br>
LOCK\_FCT4\_vect\_ens\_grid\_T.nc, <br>
LOCK\_FCT4\_vect\_ens\_grid\_U.nc, <br>
LOCK\_FCT4\_vect\_ens\_grid\_V.nc, <br>
LOCK\_FCT4\_vect\_ens\_grid\_W.nc

<pre>
NOTA: output file name is set into EXP00/<b>file_def_nemo-opa.xml</b>
in variable <b>name="@expname@"</b>
</pre>

When output files are created see the notebook to start some analysis.