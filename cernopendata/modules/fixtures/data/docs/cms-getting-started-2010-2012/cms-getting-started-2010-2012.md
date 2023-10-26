1. ["I have installed the CMS open data environment: now what?"](#vm)
2. ["OK! What is in the CMS data?"](#data)
3. ["Nice! But how do I analyse these data?"](#nice)

## <a name="vm">"I have installed the CMS open data environment / virtual machine: now what?"</a>

=== "2010"

    ### Using virtual machine
    
    To analyse CMS data collected in 2010, you need **version 4.2.8** of CMSSW, supported only on **Scientific Linux 5**. If you are unfamiliar with Linux, take a look at [this short introduction to Linux](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookBasicLinux) or try this interactive [command-line bootcamp](http://rik.smith-unna.com/command_line_bootcamp/). Once you have installed the [CMS-specific CERN Virtual Machine](/docs/cms-virtual-machine-2010), you need to open a terminal. In the "CMS-OpenData-1.1.2" VM, always use the "CMS shell" terminal available from the "CMS Shell" icon on the desktop (only if using the VM version "CMS-OpenData-1.0.0-rc7", open a terminal with the X terminal emulator from an icon bottom-left of the VM screen). Execute the following command in the terminal if you haven't done so before; it ensures that you have this version of CMSSW running:

    ```shell
    $ cmsrel CMSSW_4_2_8
    ```

    Then, make sure that you are always in the **CMSSW_4_2_8/src/** directory and the CMS analysis environment is properly setup by entering the following commands in the terminal (you must do so every time you boot the VM before you can proceed):

    ```shell
    $ cd CMSSW_4_2_8/src/
    $ cmsenv
    ```

    ### Using Docker container

    If you do not want to work on a virtual machine, you can try to to analyse CMS data in a Docker container, following the [instruction](/docs/cms-guide-docker).
    
=== "2011/2012"

    ### Using Docker container
    
    To analyse CMS data collected in 2011 and 2012, you need **version 5.3.32** of CMSSW, supported only on **Scientific Linux 6**. If you are unfamiliar with Linux, take a look at [this short introduction to Linux](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookBasicLinux) or [tutorial](https://swcarpentry.github.io/shell-novice/). Once you have installed the [CMS open data container](/docs/cms-guide-docker) or the [CMS-specific CERN Virtual Machine](/docs/cms-virtual-machine-2011), you need to open a terminal.
    
    ### Using virtual machine
    
    If you are using the VM, always use the "CMS shell" terminal available from the "CMS Shell" icon on the desktop for all CMSSW-specific commands, such as compilation and run. In the VM "CMS Shell", execute the following command in the terminal if you haven't done so before; it ensures that you have this version of CMSSW running:

    ```shell
    $ cmsrel CMSSW_5_3_32
    ```

    Note that if you get a warning message about the current OS not being slc6, you are using a wrong terminal ("Outer Shell") which is CERN CentOS 7 (cc7). Open a "CMS Shell" terminal as explained above and execute the cmsrel command there.

    In the VM, the CMS analysis environment needs to be properly setup by entering the following commands in the terminal (you must do so every time you boot the VM before you can proceed):

    ```shell
    $ cd CMSSW_5_3_32/src/
    $ cmsenv # do not execute this command if you are working in the container
    ```

    <a name="container">Make sure that you are always in the **CMSSW_5_3_32/src/** directory, both in the CMS open data container</a> and in the VM (and in the "CMS Shell" terminal in VM).

## <a name="data">"What is in the CMS data?"</a>

The primary data provided by CMS on the CERN Open Data Portal are in a format called "Analysis Object Data“ or AOD for short. These AOD files are prepared by piecing raw data collected by various sub-detectors of CMS and contain all the information that is needed for analysis. The list and the description of the physics objects contained in the AOD files can be found through the links for [2010](/docs/cms-physics-objects-2010) and for [2011](/docs/cms-physics-objects-2011). The AOD files cannot be opened and understood as simple data tables. To read these files, you would need [ROOT](http://root.cern.ch), a framework used by several particle-physics experiments to work with the collected data.

The following instructions will walk you through the steps of checking the content of AOD files. 

=== "2010"

Make sure that you are in the **CMSSW_4_2_8/src/** folder (and in the "CMS Shell" terminal, if using the "CMS-OpenData-1.1.2" VM). Also make sure that you have executed the `cmsenv` command in your terminal to launch the CMS analysis environment.

You can now open a CMS AOD file in ROOT. Let us open one of the files from the CERN Open Data Portal by entering the following command:

```shell
$ root root://eospublic.cern.ch//eos/opendata/cms/Run2010B/Mu/AOD/Apr21ReReco-v1/0000/00459D48-EB70-E011-AF09-90E6BA19A252.root
```

You will see the ROOT logo appear on screen. You can now open the ROOT GUI by entering:

```shell
TBrowser t
```

Excellent! You have successfully opened a CMS AOD file in ROOT. If this was the first time you've done so, pat yourself on the back. Now, to see what is inside this file, let us take a closer look at some collections of [physics objects](/docs/cms-physics-objects-2010#cms-data).

On the left window of ROOT (see the screenshot below), double-click on the file name (`root://eospublic.cern.ch//eos/opendata/...`). You should see a list of entries under `Events`, each corresponding to a collection of reconstructed data. We are interested in the collections containing information about reconstructed physics objects.

<img src="/static/docs/getting-started-with-cms-2010-data/cms_tbrowser.png" width="70%">

Let us take a peek, for example, at the electrons, which are found in `recoGsfElectrons_gsfElectrons__RECO`, as shown on the list of [physics objects](/docs/cms-physics-objects-2010). Look in there by double-clicking on that line and then double-clicking on `recoGsfElectrons_gsfElectrons__RECO.obj`. Here, you can have a look at various properties of this collection, such as the plot for the transverse momentum of the electrons: `recoGsfElectrons_gsfElectrons__RECO.obj.pt_`.

You can exit the ROOT browser through the GUI by clicking on `Browser` on the menu and then clicking on `Quit Root` or by entering `.q` in the terminal.

=== "2011/2012"
Make sure that you are in the **CMSSW_5_3_32/src/** folder (and, in VM, you have executed the `cmsenv` command in your terminal).

Select a dataset, for example, the [ElectronHad dataset](/record/24404) from Run2012A. You can select a file, (a listing is available for each dataset record) and print out it contents with:

```shell
$ edmDumpEventContent root://eospublic.cern.ch//eos/opendata/cms/Run2012A/ElectronHad/AOD/22Jan2013-v1/20000/FEE9E03A-F581-E211-8758-002618943901.root
```

The ouput is a list of different objects that the file contains, such as

```shell
    Type                                  Module                      Label             Process
    ----------------------------------------------------------------------------------------------
    edm::TriggerResults                   "TriggerResults"            ""                "HLT"
    trigger::TriggerEvent                 "hltTriggerSummaryAOD"      ""                "HLT"
    [...]
    vector<reco::GsfElectron>             "gsfElectrons"              ""                "RECO"
    [...]
    vector<reco::Muon>                    "muons"                     ""                "RECO"
    [...]
```

Documentation of the objects of main interest to physics analysis is available in [the CMS Open Data guide](https://cms-opendata-guide.web.cern.ch/analysis/selection/objects/objects/). The objects are implemented as C++ classes in the CMS software package [CMSSW](https://github.com/cms-sw/cmssw), and detailed reference documentation of all classes is available in [the class list of the CMSSW reference manual](https://cmsdoxygen.web.cern.ch/cmsdoxygen/CMSSW_5_3_30/doc/html/annotated.html). To see the properties of electrons, you would navigate to the [namespace "reco"](https://cmsdoxygen.web.cern.ch/cmsdoxygen/CMSSW_5_3_30/doc/html/d1/d57/namespacereco.html) and find the entry for `GsfElectron`. The [reco::GsfElectron Class Reference](https://cmsdoxygen.web.cern.ch/cmsdoxygen/CMSSW_5_3_30/doc/html/d0/d6d/classreco_1_1GsfElectron.html) lists all member functions through which the different properties of a reconstructed electron can be accessed. Note that many of the basic properties are "inherited" from the parent classes, and are listed separately under "Public Member Functions inherited from ... ". You can find more information on each object in the CMS Open Data guide (e.g. [electrons](https://cms-opendata-guide.web.cern.ch/analysis/selection/objects/electrons/)).

These objects can be accessed in a software module which can be built with a helper script available in the CMS open data environment. Do the following:

```shell
$ mkdir Demo
$ cd Demo
$ mkedanlzr DemoAnalyzer
$ cd DemoAnalyzer
```

This will create several template files in the new DemoAnalyzer directory. For more information about CMSSW analyzer modules, have a look in [the CMS open data guide](https://cms-opendata-guide.web.cern.ch/cmssw/cmsswanalyzers/).

Compile the code with:

```shell
$ scram b
```

You can ignore the message

```
    ****WARNING: No need to export library once you have declared your library as plugin.
            Please cleanup src/Demo/DemoAnalyzer/BuildFile by removing the <export></export> section.
```

or take action and remove the indicated section from ```BuildFile.xml```.

Change the file name in the configuration file ```demoanalyzer_cfg.py``` in the DemoAnalyzer directory. Take, for example, the [SingleMu dataset](/record/24460) from Run2012D i.e. replace ```file:myfile.root``` with ```root://eospublic.cern.ch//eos/opendata/cms/Run2012D/SingleMu/AOD/22Jan2013-v1/10000/0015EC7D-EAA7-E211-A9B9-E0CB4E5536A7.root```.
Change the max number of events to 10 (i.e change -1 to 10 in ```process.maxEvents = cms.untracked.PSet( input = cms.untracked.int32(-1)```).

Run the code with:

```shell
$ cmsRun demoanalyzer_cfg.py
```

and you will get an output like:

```
    221119 18:53:23 1032 Xrd: XrdClientConn: Error resolving this host's domain name.
    221119 18:53:23 1032 secgsi_InitProxy: cannot access private key file: /home/cmsusr/.globus/userkey.pem
    221119 18:53:23 1032 Xrd: CheckErrorStatus: Server [eospublic.cern.ch] declared: (error code: 3005)
    19-Nov-2022 18:53:23 CET  Initiating request to open file root://eospublic.cern.ch//eos/opendata/cms/Run2012D/SingleMu/AOD/22Jan2013-v1/10000/0015EC7D-EAA7-E211-A9B9-E0CB4E5536A7.root
    19-Nov-2022 18:53:26 CET  Successfully opened file root://eospublic.cern.ch//eos/opendata/cms/Run2012D/SingleMu/AOD/22Jan2013-v1/10000/0015EC7D-EAA7-E211-A9B9-E0CB4E5536A7.root
    Begin processing the 1st record. Run 206401, Event 240060474, LumiSection 178 at 19-Nov-2022 18:54:37.199 CET
    Begin processing the 2nd record. Run 206401, Event 240069594, LumiSection 178 at 19-Nov-2022 18:54:37.227 CET
    Begin processing the 3rd record. Run 206401, Event 240049754, LumiSection 178 at 19-Nov-2022 18:54:37.228 CET
    Begin processing the 4th record. Run 206401, Event 240115594, LumiSection 178 at 19-Nov-2022 18:54:37.228 CET
    Begin processing the 5th record. Run 206401, Event 240154770, LumiSection 178 at 19-Nov-2022 18:54:37.229 CET
    Begin processing the 6th record. Run 206401, Event 240103386, LumiSection 178 at 19-Nov-2022 18:54:37.229 CET
    Begin processing the 7th record. Run 206401, Event 240173338, LumiSection 178 at 19-Nov-2022 18:54:37.230 CET
    Begin processing the 8th record. Run 206401, Event 240127898, LumiSection 178 at 19-Nov-2022 18:54:37.230 CET
    Begin processing the 9th record. Run 206401, Event 240103970, LumiSection 178 at 19-Nov-2022 18:54:37.231 CET
    Begin processing the 10th record. Run 206401, Event 240129066, LumiSection 178 at 19-Nov-2022 18:54:37.231 CET
    19-Nov-2022 18:54:37 CET  Closed file root://eospublic.cern.ch//eos/opendata/cms/Run2012D/SingleMu/AOD/22Jan2013-v1/10000/0015EC7D-EAA7-E211-A9B9-E0CB4E5536A7.root

    =============================================

    MessageLogger Summary

    type     category        sev    module        subroutine        count    total
    ---- -------------------- -- ---------------- ----------------  -----    -----
        1 fileAction           -s file_close                             1        1
        2 fileAction           -s file_open                              2        2

    type    category    Examples: run/evt        run/evt          run/evt
    ---- -------------------- ---------------- ---------------- ----------------
        1 fileAction           PostEndRun
        2 fileAction           pre-events       pre-events

    Severity    # Occurrences   Total Occurrences
    --------    -------------   -----------------
    System                  3                   3
```

This is a simple loop over the first 10 events in the file. To access the physics object information, for example that of muons, add the following lines in `src/DemoAnalyzer.cc` (the lines before and after of the lines to be added are also shown):

```shell
[...]
#include "FWCore/ParameterSet/interface/ParameterSet.h"

//classes to extract Muon information
#include "DataFormats/MuonReco/interface/Muon.h"
#include "DataFormats/MuonReco/interface/MuonFwd.h"
#include<vector>
//
// class declaration
[...]

      // ----------member data ---------------------------
      std::vector<float> muon_e; //energy values for muons in the event
};
[...]
   using namespace edm;

    //clean the container
    muon_e.clear();

    //define the handler and get by label
    Handle<reco::MuonCollection> mymuons;
    iEvent.getByLabel("muons", mymuons);

    //if collection is valid, loop over muons in event
    if(mymuons.isValid()){
        for (reco::MuonCollection::const_iterator itmuon=mymuons->begin(); itmuon!=mymuons->end(); ++itmuon){
            muon_e.push_back(itmuon->energy());
        }
    }

    //print the vector
    for(unsigned int i=0; i < muon_e.size(); i++){
        std::cout <<"Muon # "<<i<<" with E = "<<muon_e.at(i)<<" GeV."<<std::endl;
    }

#ifdef THIS_IS_AN_EVENT_EXAMPLE
[...]
```

Modify the `BuildFile.xml` to include `DataFormats/MuonReco` dependencies so that it becomes:

```shell
<use name="FWCore/Framework"/>
<use name="FWCore/PluginManager"/>
<use name="DataFormats/MuonReco"/>
<use name="FWCore/ParameterSet"/>
<flags EDM_PLUGIN="1"/>
```

Compile and run again with:

```shell
$ scram b
$ cmsRun demoanalyzer_cfg.py
```

The output gives the energy of muons in these events:

```
    19-Nov-2022 19:53:08 CET  Initiating request to open file root://eospublic.cern.ch//eos/opendata/cms/Run2012D/SingleMu/AOD/22Jan2013-v1/10000/0015EC7D-EAA7-E211-A9B9-E0CB4E5536A7.root
    19-Nov-2022 19:53:10 CET  Successfully opened file root://eospublic.cern.ch//eos/opendata/cms/Run2012D/SingleMu/AOD/22Jan2013-v1/10000/0015EC7D-EAA7-E211-A9B9-E0CB4E5536A7.root
    Begin processing the 1st record. Run 206401, Event 240060474, LumiSection 178 at 19-Nov-2022 19:53:50.971 CET
    Muon # 0 with E = 31.2151 GeV.
    Begin processing the 2nd record. Run 206401, Event 240069594, LumiSection 178 at 19-Nov-2022 19:53:51.000 CET
    Muon # 0 with E = 62.6309 GeV.
    Begin processing the 3rd record. Run 206401, Event 240049754, LumiSection 178 at 19-Nov-2022 19:53:51.001 CET
    Muon # 0 with E = 71.6465 GeV.
    Muon # 1 with E = 3.99535 GeV.
    Begin processing the 4th record. Run 206401, Event 240115594, LumiSection 178 at 19-Nov-2022 19:53:51.001 CET
    Muon # 0 with E = 137.55 GeV.
    Muon # 1 with E = 2.70864 GeV.
    Muon # 2 with E = 4.33524 GeV.
    Begin processing the 5th record. Run 206401, Event 240154770, LumiSection 178 at 19-Nov-2022 19:53:51.002 CET
    Muon # 0 with E = 87.9848 GeV.
    Muon # 1 with E = 4.34456 GeV.
    Begin processing the 6th record. Run 206401, Event 240103386, LumiSection 178 at 19-Nov-2022 19:53:51.002 CET
    Muon # 0 with E = 30.2197 GeV.
    Muon # 1 with E = 11.064 GeV.
    Muon # 2 with E = 10.8193 GeV.
    Begin processing the 7th record. Run 206401, Event 240173338, LumiSection 178 at 19-Nov-2022 19:53:51.003 CET
    Muon # 0 with E = 6.84971 GeV.
    Muon # 1 with E = 12.0909 GeV.
    Muon # 2 with E = 3.20224 GeV.
    Muon # 3 with E = 7.04104 GeV.
    Muon # 4 with E = 7.90646 GeV.
    Muon # 5 with E = 6.20379 GeV.
    Begin processing the 8th record. Run 206401, Event 240127898, LumiSection 178 at 19-Nov-2022 19:53:51.003 CET
    Muon # 0 with E = 42.8793 GeV.
    Muon # 1 with E = 3.31122 GeV.
    Muon # 2 with E = 3.85927 GeV.
    Muon # 3 with E = 3.0424 GeV.
    Begin processing the 9th record. Run 206401, Event 240103970, LumiSection 178 at 19-Nov-2022 19:53:51.003 CET
    Muon # 0 with E = 55.7221 GeV.
    Muon # 1 with E = 2.80195 GeV.
    Begin processing the 10th record. Run 206401, Event 240129066, LumiSection 178 at 19-Nov-2022 19:53:51.004 CET
    Muon # 0 with E = 33.7197 GeV.
    Muon # 1 with E = 4.90223 GeV.
    Muon # 2 with E = 5.61441 GeV.
    19-Nov-2022 19:53:51 CET  Closed file root://eospublic.cern.ch//eos/opendata/cms/Run2012D/SingleMu/AOD/22Jan2013-v1/10000/0015EC7D-EAA7-E211-A9B9-E0CB4E5536A7.root
```
