# CMS-ECAL_TPGAnalysis (8_0_2)

##This houses the latest version of the Level 1 Ecal TPG analysis of CMS
======================================================================
How to run:

Get the CMSSW release area
```bash
cmsrel CMSSW_8_0_2
cd CMSSW_8_0_2/src
cmsenv
```

Checkout the repository
```
git cms-init
git clone https://github.com/cms-ecal-L1TriggerTeam/CMS-ECAL_TPGAnalysis.git
scram b
``` 


BEFORE YOU RUN, you need to make sure you change the directory/path names to your directories or directories you want results in.

 `cd CMS-ECAL_TPGAnalysis/Scripts/TriggerAnalysis`

In particular the files you need to modify are : `mergeTPGAnalysis.sh; makeTrigPrimPlots.sh ; convertAllPlots.py ;produceplotonCAFqueues.sh `

  `cd ../../TPGPlotting/plots` and also modify path in `makeTPGPlots.sh`
  
  
  ###Running the analysis
  This has been tested on lxplus. After you have changed all the pathnames above:
  
  To run, e.g. on 266423 ZeroBias dataset
  ```./runTPGbatch_AAA.sh lxbatch 266423   /Cosmics/Commissioning2016-v1/RAW  80X_dataRun2_HLT_v6 -1 False```
  
  i.e.```./runTPGbatch_AAA.sh  lxbatch  run_number  das_dataset_path Global_Tag  Num_of_events_to_be_processed(-1 defaults to all events) MC_or_data(False for data)```
  
  This will run the jobs on the queue "cmscaf1nd", If you do not have permissions to run on the queue modify runTPGbatch_AAA.sh and change `queue=cmscaf1nd` appropiately
  
  To locally test if jobs are running:
  `cd log_and_results
  cmsRun runTPG_cfg_2.py`
  
  Once jobs are done, merge the output files.

  ```./mergeTPGAnalysis.sh -r 266423 -m log_and_results/266423-_ZeroBias_Run2015C-v1_RAW-batch/results/ -a testing```
  
  `-a` option is optional if u want run on the same set of data several times and want to call each merged output a different name

  To make plots:`./makeTrigPrimPlots.sh -r 266423 -a testing`

  The plots will be created in the folder: `Scripts/TriggerAnalysis/Commisioning2016`
  
  To make thumbnails: `python convertAllPlots.py  -r 266423 -a testing_eg12`

  Copy it to your html_folder to look at it on the web.
  

       
Somemore plotting options and instructions on this (partially outdated) twiki here:

https://twiki.cern.ch/twiki/bin/viewauth/CMS/EcalPFGCode#Trigger_Primitive_Analysis

