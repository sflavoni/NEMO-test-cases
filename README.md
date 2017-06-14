
# NEMO Demonstration Cases

This repository contains information as to how to run idealized demonstration case with NEMO.


# How to run test cases :

# How to download & compile test cases in NEMO release

## install NEMO from scratch

## PRE-REQUIRED: XIOS needed for input/output for NEMO code

* **download & compile XIOS code : **
> svn co http://forge.ipsl.jussieu.fr/ioserver/svn/XIOS/trunk xios-2.0
<br> cd xios-2.0
<br> ./make_xios --help  (to choice your compiler)
<br> ./make_xios --arch CC_MACOSX --jobs 8


* **download revision 8097 of NEMO : **
> 
mkdir MY_TEST 
<br> cd MY_TEST 
<br> svn --username 'mylogin' co http://forge.ipsl.jussieu.fr/nemo/svn/trunk/NEMOGCM NEMOGCM_r8097 -r 8097


In EXP00 directory there is available some namelists :
These namelists have same blocks of namelist_ref with choice of:
- tracer advection scheme = **FCT2** or **FCT4**
 - FCT2 = COMPACT 2nd order on horizontal and vertical
 - FCT4 = COMPACT 4th order on horizontal and vertical
- form of the momentum advectionvector = **flux** or **form**
- momentum advection scheme = **cen2** or **ubs**
 - cen2 = 2nd order centered scheme
 - ubs = 3rd order UBS scheme
- ln_dynvor_ene = .false. !  enstrophy conserving scheme
- ln_dynvor_ens = .true.  !  energy conserving scheme
- ln_dynvor_mix = .false. !  mixed scheme
- ln_dynvor_een = .false. !  energy & enstrophy scheme