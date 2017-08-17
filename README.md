
# NEMO Demonstration Cases
<!---
COMMENT ON STYLE: 
this is useful sintax to have nice grey box
[comment]: <

 ```
cd TEST\_CASES\_NEMO
mkdir MY\_TEST 
cd MY\_TEST 
svn --username 'mylogin' co http://forge.ipsl.jussieu.fr/nemo/svn/trunk/NEMOGCM NEMOGCM_r8097 -r 
8097
```
>
-->

<!--
equivalent commands:
<pre> </pre>
or
````

-->

<!--
comment:
can choise:
    type of font 
    dimension in points
    and color

<code>
<span style="color:red; font-family: 'Courier'; font-size: 18pt;"> memo for style
 : prova</span>
</code>
-->

This repository contains information as to how to run demonstration case  <b> WITHIN </b> NEMO.

--
NEMO Example Experiments   (
<span style="color:red"> 
copied by MITgcm page: https://github.com/altMITgcm/MITgcm66h/blob/master/docs/examples/examples.rst ) 
</style>


<span style="color:red"> To re-adapt better : </style>

<span style="color:red">
The full NEMO distribution comes with a set of pre-configured numerical experiments. Some of these example experiments are tests of individual parts of the model code, but many are fully fledged numerical simulations. Full tutorials exist for a few of the examples, and are documented in sections :xxxxxx.
The other examples follow the same general structure as the tutorial examples. However, they only include brief instructions in a text file called  <i> README </i>.
The examples are located in subdirectories under the directory <i> CONFIG/TEST_CASES </i>. 
Each example is briefly described below. Full list of model examples.....
Once you have chosen the example you want to run, you are ready to compile the code.
</span>

--

## This is a tutorial for NEMO release 8097
### In NEMO official repository (revision 8097) there are 4 demonstration cases : 

The list of these 5 cases is available in NEMOGCM/CONFIG/TEST_CASES directory :

- LOCK_EXCHANGE
- OVERFLOW
- ISOMIP
- WAD (Wetting & Dry)
- SAS_BIPER

# How to run demonstration cases in NEMO 

### Here a description on How To Download/Compile/Run NEMO (you can skip this part if you already know it)


* Create your own directory in which you want to download & compile NEMO

```
mkdir my_TEST 
```

## XIOS needed for input/output for NEMO code: download and compile xios
 
XIOS is tool for NEMO Inputs/Outputs, developped outside NEMO. 

* create directory in which you want to download & compile XIOS
 
```
 mkdir ~/XIOS; cd ~/XIOS
```
  
* download & compile **XIOS** code : 
 
```
svn co http://forge.ipsl.jussieu.fr/ioserver/svn/XIOS/trunk xios-2.0
cd xios-2.0
./make_xios --help  (to choice your compiler)
example: ./make_xios --arch CC_MACOSX --jobs 8
```
  
<b> N.B. </b> Into the xios-2.0/arch directory there is a list of files created for some architectures, that can be used like example, to create your own. Check version and PATH of compilers on your machine

<b> NOW XIOS is installed and compiled. </b>

## Install NEMO from scratch
### Download NEMO
<i> You need to have a login to download NEMO code. If you need one go to the NEMO web site</i>

* download revision 8097 of **NEMO** : 

<pre>
cd my_TEST 
svn --username 'mylogin' co http://forge.ipsl.jussieu.fr/nemo/svn/trunk/NEMOGCM NEMOGCM_r8097 -r <b>8097</b>
</pre>

### Compile NEMO
<pre>
cd NEMOGCM_r8097/CONFIG
./makenemo -a TEST_CASES -n my_TEST_CASE -n <i>TEST_CASE_EXAMPLE</i> -m <i>your_ARCH_FILE</i>
</pre>

### Set of NEMO runs
If you want to run one of these test cases you can read README instructions in each corrisponding directory.