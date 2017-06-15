
# NEMO Demonstration Cases

This repository contains information as to how to run idealized demonstration case within NEMO.


# How to run test cases in NEMO release 8097 :

* create your own directory in which you want to download & compile NEMO

> mkdir TEST\_CASES_NEMO 

## XIOS needed for input/output for NEMO code: download and compile xios :
 
XIOS is tool for NEMO Inputs/Outputs, developped outside NEMO. 

* create directory in which you want to download & compile XIOS
 
> mkdir ~/XIOS; cd ~/XIOS
  
* download & compile **XIOS** code : 
 
> svn co http://forge.ipsl.jussieu.fr/ioserver/svn/XIOS/trunk xios-2.0
<br> cd xios-2.0
<br> ./make\_xios --help  (to choice your compiler)
<br> example: ./make\_xios --arch CC_MACOSX --jobs 8
  
<i> N.B. Into the xios-2.0/arch directory there is a list of files created for some architectures, that can be used like example, to create your own. Check version and PATH of compilers on your machine</i>

NOW XIOS is installed and compiled.

## Install NEMO from scratch
<i> You need to have a login to download NEMO code. If you need one go to the NEMO web site</i>

* download revision 8097 of **NEMO** : 

  > cd TEST\_CASES\_NEMO
 <br> mkdir MY\_TEST 
 <br> cd MY\_TEST 
 <br> svn --username 'mylogin' co http://forge.ipsl.jussieu.fr/nemo/svn/trunk/NEMOGCM NEMOGCM_r8097 -r 8097


<b>In NEMO official repository there are 4 demonstration cases : </b>

The list of these 4 cases is available in NEMOGCM/CONFIG/TEST_CASES directory :

- ISOMIP
- LOCK_EXCHANGE
- OVERFLOW
- WAD (Wetting&Dry)
 
 
###COMPILE TEST CASES 
 
* compile TEST\_CASES (example here the LOCK_EXCHANGE) : 

 > cd MY\_TEST/NEMOGCM/CONFIG
 <br> ./makenemo -a TEST_CASES -n my\_LOCK\_EXCHANGE -r LOCK\_EXCHANGE -m your\_arch\_file
  

Now TEST CAS "LOCK_EXCHANGE" code is installed and compiled. 