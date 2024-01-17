1. ["I have installed the CMS open data environment: now what?"](#vm)
2. ["OK! What is in the CMS data?"](#data)
3. ["Nice! But how do I analyse these data?"](#nice)

The CMS primary data for 2010-2012 are provided on the CERN Open Data Portal in the Analysis Object Data (AOD) format. This page provides tutorials on how to access and analyse CMS data in this format for each year.

## <a name="vm">"I have installed the CMS open data environment / virtual machine: now what?" </a>

To analyse CMS data collected in different years, you need different versions of CMSSW (an event processing model). The recommened version for the 2010 data is <b>version 4.2.8</b>, supported only on <b>Scientific Linux 5</b>. The recommended version for the 2011 and 2012 data is <b>version 5.3.32</b>, supported only on <b>Scientific Linux 6</b>. If you are unfamiliar with Linux, take a look at <a href="https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookBasicLinux">this short introduction to Linux</a> or <a href="https://swcarpentry.github.io/shell-novice/">tutorial</a>.

<details>
<summary><h4>2010</h4></summary>
  
  <header>
    <h3>Using virtual machine</h3>
  </header>

<p>
Once you have installed the <a href="/docs/cms-virtual-machine-2010"> CMS-specific CERN Virtual Machine </a>, you need to open a terminal. In the "CMS-OpenData-1.1.2" VM, always use the "CMS shell" terminal available from the "CMS Shell" icon on the desktop (only if using the VM version "CMS-OpenData-1.0.0-rc7". Open a terminal with the X terminal emulator from an icon bottom-left of the VM screen). Execute the following command in the terminal if you haven't done so yet. It downloads for you the correct version of CMSSW:

```shell
$ cmsrel CMSSW_4_2_8
```
</p>

<p>
Then, make sure that you are always in the <b>CMSSW_4_2_8/src/</b> directory and that the CMS analysis environment is properly setup by entering the following commands in the terminal (you must do so every time you boot the VM before you can proceed):

```shell
$ cd CMSSW_4_2_8/src/
$ cmsenv
```
</p>

<header>
  <h3>Using Docker container</h3>
</header>

<p>
If you do not want to work on a virtual machine, you can try to to analyse CMS data in a Docker container, following the <a href="/docs/cms-guide-docker">instruction</a>.
</p>
<br>
</details>


<details>
<summary><h4>2011-2012</h4></summary>
<br>

<header>
  <h3>Using virtual machine</h3>
</header>

<p>
Once you have installed the <a href="/docs/cms-guide-docker">CMS open data container</a> or the <a href="/docs/cms-virtual-machine-2011">CMS-specific CERN Virtual Machine</a>, you need to open a terminal. If you are using the VM, always use the "CMS shell" terminal for all CMSSW-specific commands. It is available from the "CMS Shell" icon on the desktop. In the VM "CMS Shell", execute the following command in the terminal if you haven't done so yet. It downloads for you the correct version of CMSSW:

```shell
$ cmsrel CMSSW_5_3_32
```
</p>

<p>
Note that if you get a warning message about the current OS not being slc6, you are using a wrong terminal ("Outer Shell") which is CERN CentOS 7 (cc7). Open a "CMS Shell" terminal as explained above and execute the cmsrel command there.
</p>

<p>
In the VM, the CMS analysis environment needs to be properly setup by entering the following commands in the terminal (you must do so every time you boot the VM before you can proceed):

```shell
$ cd CMSSW_5_3_32/src/
$ cmsenv # do not execute this command if you are working in the container
```
</p>

<p>
Make sure that you are always in the <b>CMSSW_5_3_32/src/</b> directory, both in the CMS open data container and in the VM (and in the "CMS Shell" terminal in VM).
</p>

<header>
  <h3>Using Docker container</h3>
</header>

<p>
If you do not want to work on a virtual machine, you can try to to analyse CMS data in a Docker container, following the <a href="/docs/cms-guide-docker">instruction</a>.
</p>
<br>
</details>



## <a name="data"> "OK! What is in the CMS data?" </a>

<p>
The primary CMS data for 2010 to 2012 on the CERN Open Data Portal are in the format of Analysis Object Data (AOD). The AOD files contain all the information that is needed for physics analysis. These files are prepared by piecing raw data collected by various sub-detectors of CMS. A list of the physics objects contained in the AOD files can be found through the links for <a href="/docs/cms-physics-objects-2010">2010</a> and for <a href="/docs/cms-physics-objects-2011">2011</a>. The AOD files contains physics objects (C++ classes) rather than numbers that you can click on and read. Follow the instructions below for a peak at these files.

<details>
<summary><h4>2010<h4></summary>

<p>
Let's first see what physics objects are contained in an AOD file.
</p>

<p>
Make sure that you are in the <b>CMSSW_4_2_8/src/</b> folder (and in the "CMS Shell" terminal, if using the "CMS-OpenData-1.1.2" VM). Also make sure that you have executed the <code>cmsenv</code> command in your terminal to launch the CMS analysis environment.
</p>

<p>
Select a dataset, for example, the <a href="/record/24404">Mu primary dataset</a> from Run2012A. Click the "Download" tab at the bottom of the page to see a list of files contained in this dataset. You can select a file from the list and print out its contents with:

```shell
$ edmDumpEventContent root://eospublic.cern.ch//eos/opendata/cms/Run2010B/Mu/AOD/Apr21ReReco-v1/0000/00459D48-EB70-E011-AF09-90E6BA19A252.root
```
</p>

<p>
The ouput is a list of objects that the file contains, such as
        
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
</p>

<p>
Documentation of the objects of main interest to physics analysis is available in <a href="https://cms-opendata-guide.web.cern.ch/analysis/selection/objects/objects/">the CMS Open Data guide</a>. The objects are implemented as C++ classes in the CMS software package <a href="https://github.com/cms-sw/cmssw">CMSSW</a>, and detailed reference documentation of all classes is available in <a href="https://cmsdoxygen.web.cern.ch/cmsdoxygen/CMSSW_4_2_8/doc/html/annotated.html">the class list of the CMSSW reference manual</a>. To see the properties of electrons, you would navigate to the <a href="https://cmsdoxygen.web.cern.ch/cmsdoxygen/CMSSW_4_2_8/doc/html/d1/d57/namespacereco.html">namespace "reco"</a> and find the entry for <code>GsfElectron</code>. The <a href="https://cmsdoxygen.web.cern.ch/cmsdoxygen/CMSSW_4_2_8/doc/html/d0/d6d/classreco_1_1GsfElectron.html">reco::GsfElectron Class Reference</a> lists all member functions through which the different properties of a reconstructed electron can be accessed. Note that many of the basic properties are "inherited" from the parent classes and are listed separately under "Public Member Functions inherited from ... ". You can find more information about each object in the CMS Open Data guide (e.g. <a href="https://cms-opendata-guide.web.cern.ch/analysis/selection/objects/electrons/">electrons</a>).
</p>

<p>
The objects contained in the AOD files can be accessed through a software module, which can be built with Event Data Analyzer (EDAnalyzer). EDAnalyzer is a helper script available in the CMS open data environment. Do the following:

```shell
$ mkdir Demo
$ cd Demo
$ mkedanlzr DemoAnalyzer
$ cd DemoAnalyzer
```
</p>

<p>
This will create several template files in the new DemoAnalyzer directory. For more information about CMSSW analyzer modules, have a look in <a href="https://cms-opendata-guide.web.cern.ch/cmssw/cmsswanalyzers/">the CMS open data guide</a>.
</p>

<p>
Compile the code with:

```shell
$ scram b
```
</p>

<p>
You can ignore the message

```
    ****WARNING: No need to export library once you have declared your library as plugin.
            Please cleanup src/Demo/DemoAnalyzer/BuildFile by removing the <export></export> section.
```

or take action and remove the indicated section from <code>BuildFile.xml</code>.
</p>

<p>
Change the file name in the configuration file <code>demoanalyzer_cfg.py</code> in the DemoAnalyzer directory. Take, for example, the <a href="/record/14">Mu primary dataset</a> from Run2010B i.e. replace <code>file:myfile.root</code> with <code>root://eospublic.cern.ch//eos/opendata/cms/Run2010B/Mu/AOD/Apr21ReReco-v1/0000/00459D48-EB70-E011-AF09-90E6BA19A252.root</code>.
</p>

<p>
Change the max number of events to 10 (i.e change -1 to 10 in <code>process.maxEvents = cms.untracked.PSet( input = cms.untracked.int32(-1)</code>).
</p>

<p>
Run the code with:

```shell
$ cmsRun demoanalyzer_cfg.py
```
</p>

<p>
You will get an output like (UPDATE OUTPUT):

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
</p>

<p>
This is a simple loop over the first 10 events in the file. To access the physics object information, for example, of muons, add the following lines in <code>src/DemoAnalyzer.cc</code> (the lines before and after of the lines to be added are also shown):
        
(UPDATE THE CODE)

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

Modify the <code>BuildFile.xml</code> to include <code>DataFormats/MuonReco</code> dependencies so that it becomes:

```shell
<use name="FWCore/Framework"/>
<use name="FWCore/PluginManager"/>
<use name="DataFormats/MuonReco"/>
<use name="FWCore/ParameterSet"/>
<flags EDM_PLUGIN="1"/>
```
</p>

<p>
Compile and run again with:

```shell
$ scram b
$ cmsRun demoanalyzer_cfg.py
```
</p>

<p>
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
</p>
</details>


<details>
<summary><h4>2011-2012</h4></summary>
<p>
Make sure that you are in the <b>CMSSW_5_3_32/src/</b> folder (and, in VM, you have executed the <code>cmsenv</code> command in your terminal).
</p>
<p>
Select a dataset, for example, the <a href="/record/24404">ElectronHad dataset</a> from Run2012A. Click the "Download" tab at the bottom of the page to see a list of files contained in this dataset. You can select a file from the list and print out its contents with:

```shell
$ edmDumpEventContent root://eospublic.cern.ch//eos/opendata/cms/Run2012A/ElectronHad/AOD/22Jan2013-v1/20000/FEE9E03A-F581-E211-8758-002618943901.root
```
</p>

<p>
The ouput is a list of objects that the file contains, such as

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
</p>

<p>
Documentation of the objects of main interest to physics analysis is available in <a href="https://cms-opendata-guide.web.cern.ch/analysis/selection/objects/objects/">the CMS Open Data guide</a>. The objects are implemented as C++ classes in the CMS software package <a href="https://github.com/cms-sw/cmssw">CMSSW</a>, and detailed reference documentation of all classes is available in <a href="https://cmsdoxygen.web.cern.ch/cmsdoxygen/CMSSW_5_3_30/doc/html/annotated.html">the class list of the CMSSW reference manual</a>. To see the properties of electrons, you would navigate to the <a href="https://cmsdoxygen.web.cern.ch/cmsdoxygen/CMSSW_5_3_30/doc/html/d1/d57/namespacereco.html">namespace "reco"</a> and find the entry for <code>GsfElectron</code>. The <a href="https://cmsdoxygen.web.cern.ch/cmsdoxygen/CMSSW_5_3_30/doc/html/d0/d6d/classreco_1_1GsfElectron.html">reco::GsfElectron Class Reference</a> lists all member functions through which the different properties of a reconstructed electron can be accessed. Note that many of the basic properties are "inherited" from the parent classes and are listed separately under "Public Member Functions inherited from ... ". You can find more information about each object in the CMS Open Data guide (e.g. <a href="https://cms-opendata-guide.web.cern.ch/analysis/selection/objects/electrons/">electrons</a>).
</p>

<p>
The objects contained in the AOD files can be accessed through a software module, which can be built with a helper script available in the CMS open data environment. Do the following:

```shell
$ mkdir Demo
$ cd Demo
$ mkedanlzr DemoAnalyzer
$ cd DemoAnalyzer
```
</p>

<p>
This will create several template files in the new DemoAnalyzer directory. For more information about CMSSW analyzer modules, have a look in <a href="https://cms-opendata-guide.web.cern.ch/cmssw/cmsswanalyzers/">the CMS open data guide</a>.
</p>

<p>
Compile the code with:

```shell
$ scram b
```
</p>

<p>
You can ignore the message

```
    ****WARNING: No need to export library once you have declared your library as plugin.
            Please cleanup src/Demo/DemoAnalyzer/BuildFile by removing the <export></export> section.
```

or take action and remove the indicated section from <code>BuildFile.xml</code>.
</p>

<p>
Change the file name in the configuration file <code>demoanalyzer_cfg.py</code> in the DemoAnalyzer directory. Take, for example, the <a href="/record/24460">SingleMu dataset</a> from Run2012D i.e. replace <code>file:myfile.root</code> with <code>root://eospublic.cern.ch//eos/opendata/cms/Run2012D/SingleMu/AOD/22Jan2013-v1/10000/0015EC7D-EAA7-E211-A9B9-E0CB4E5536A7.root</code>.
</p>
<p>
Change the max number of events to 10 (i.e change -1 to 10 in <code>process.maxEvents = cms.untracked.PSet( input = cms.untracked.int32(-1)</code>).
</p>

<p>
Run the code with:

```shell
$ cmsRun demoanalyzer_cfg.py
```
</p>

<p>
You will get an output like:

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
</p>

<p>
This is a simple loop over the first 10 events in the file. To access the physics object information, for example, of muons, add the following lines in <code>src/DemoAnalyzer.cc</code> (the lines before and after of the lines to be added are also shown):

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
</p>

<p>
Modify the <code>BuildFile.xml</code> to include <code>DataFormats/MuonReco</code> dependencies so that it becomes:

```shell
<use name="FWCore/Framework"/>
<use name="FWCore/PluginManager"/>
<use name="DataFormats/MuonReco"/>
<use name="FWCore/ParameterSet"/>
<flags EDM_PLUGIN="1"/>
```
</p>

<p>
Compile and run again with:

```shell
$ scram b
$ cmsRun demoanalyzer_cfg.py
```
</p>

<p>
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
</p>
<br>
</details>

## <a name="nice">"Nice! But how do I analyse these data?"</a>
<p>
        You can perform analysis on the AOD dataset directly or on a reduced dataset that is derived from the AOD data. Analyzing on the original AOD dataset can be computationally heavy. Usually, it is recommended to use the reduced dataset, unless you need some information that is only contained in AOD data. 
</p>
<p>
        In AOD files, reconstructed physics objects are included without checking their "quality". For example, the reconstructed objects in the electron collection / muon collection that you printed out are not guaranteed to be from validated data. In order to analyse only the "good quality" data, you must apply some selection criteria.
</p>
<p>
        Below we provide examples of how to perfom selection and analysis on both the primary AOD data and the reduced data. Two common formats of reduced data are NanoAODRun1 tuples and PAT tuples. Examples of producing both data formats are provided. Using NanoAODRun1 format is favored, because it is available on Open Data Portal, and the example code is more up-to-date. Non-expert users do not need to produce NanoAODRun1 by themselves.
</p>

<p>
        Physics Object Extractor Tool (POET) is an example code to extract the physics object information from CMS data. It is available for <a href="https://github.com/cms-opendata-analyses/PhysObjectExtractorTool/tree/2011">2011</a> and <a href="https://github.com/cms-opendata-analyses/PhysObjectExtractorTool/tree/2012">2012</a> AOD data. It is not available for the 2010 data, but we can perform selection and extraction directly with EDAnalyzer. POET is just a collection of Event Data Analyzer (EDAnalyzer). 
</p>

<br>
<details>
<summary><h4>Analysing the primary AOD dataset</h4></summary>

        <details>
        <summary><h3>2010</h3></summary>
        <br>
        <p>
                As mentioned above, you typically do not perform an analysis directly on the AOD files. However, there might be cases where only the AOD files contain some of the information you need. <a href="/record/560">This CMS analysis example</a> takes you through the steps of analyzing the AOD files directly.
        </p>
        <p>
                Take a look at the scripts to see how the selections are applied and how the information are extracted for analysis.
        </p>
        <p>
                Your final analysis is done using a software module called an "analyzer". If you followed the validation step for the virtual machine setup, you have already produced and run a simple analyzer. You can specify your initial selection criteria within the analyzer to perform your analysis directly on the AOD files, or further elaborate the selections and other operations needed for analysing the reduced dataset. To learn more about configuring analyzers, follow <a href="https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookWriteFrameworkModule">these instructions in the CMSSW WorkBook</a>. Make sure, though, that you replace the release version (CMSSW_nnn) with the release that you are using, i.e. one that is compatible with the CMS open data.
        </p>
        <p>
                You can also pass the selection criteria through the configuration file. This file activates existing tools within CMSSW in order to perform the desired selections. If you have followed the validation step for the virtual machine setup, you have already seen a configuration file, which is used to give the parameters to the <code>cmsRun</code> executable. You can see how this is done in our analysis example.
        </p>
        <p>
                <strong>NOTE</strong>: To analyse the full event content, the analysis job needs access to the "condition data", such as the jet-energy corrections. To see how the connection to the condition database is established, you can check the <a href="/docs/cms-guide-for-condition-database">Guide to the CMS condition database</a>. For simpler analyses, where we use only physics objects needing no further data for corrections, you do not need to connect to the condition database. This is the case for the examples for analysing the primary datasets below.
        </p><br>
        </details>

</details>

<details>
<summary><h3> Analysing reduced dataset </h3></summary>
        <details>
        <head>
                <h4>Option A: Reduce the AOD files to NanoAODRun1 tuples</h4>
        </head>
                <p>
                        The NanoAODRun1 format is a NanoAOD-like Ntuple format for CMS Run 1 data, readable with bare ROOT or other ROOT-compatible software, and containing the per-event information that is needed in most generic analyses. It is a reduced dataset made available for convenient access and physics analysis. The goal is that about 50% of all publishable Open Data analyses done by external users can use this simplified NanoAODRun1 data format without compromise on the quality of the scientific result.
                </p>
                <p>
                        Note that NanoAODRun1 dfata format should not be confused with a NanoAOD-like educational <a href="/record/12353">reduced NanoAOD format</a>, which is sometimes also plainly referred to as "NanoAOD" in the Open Data context. Tha latter is a partially compatible but much more reduced content, aiming to be used in specific educational/pedagogical exercises rather than in general full physics analysis.
                </p> 
                <p>
                        NanoAODRun1 ntuples for relevant Open Data and MC sets are being/will be produced and made available by the DPOA group, so normal users should not need to deal with the ntuple production code except for reference purposes. The <a href="https://github.com/cms-opendata-analyses/NanoAODRun1ProducerTool">code</a> that produces them from AOD is provided for reference, but not meant to be pedagogical and not intended to be used by non-expert users. Users interested in pedagogical code at AOD level are referred to the <a href="https://github.com/cms-opendata-analyses/PhysObjectExtractorTool">POET</a> setup (for CMSSW_5_3_32 and 7_6_7 only).
                </p>
                <p>
                        A list of variables in NanoAODRun1 MC data can be found <a href="https://twiki.cern.ch/twiki/pub/CMSPublic/WorkBookNanoAODRun1/doc_DYJetsToLL_M-50_7TeV.html">here</a>. Collision data contains the same variables, except for the generator-level information.
                </p>
                <p>
                        Users who need information beyond the <a href="https://twiki.cern.ch/twiki/pub/CMSPublic/WorkBookNanoAODRun1/doc_DYJetsToLL_M-50_7TeV.html">list</a> should directly use the AOD data, following the example provided in the previous section. 
                </p>
                <p>
                        Let's take a look at how to perform analysis using the NanoAODRun1 tuples.
                </p>

                <details>
                        <h5>2010</h5>
                <br>
                </details>
                <details>
                        <h5>2011-2012</h5>
                <br>
                </details>
        <br>
        </details>
        
        <details>
        <head>
                <h4>Option B: Reduce the AOD files to PAT tuples</h4>
                <details>
                        <h5>2010</h5>
                <br>
                </details>
                <details>
                        <h5>2011-2012</h5>
                <br>
        </head>
        <br>
        </details>
</details>

<details>
<summary><h4>2011-2012</h4></summary>

<details>
<summary><h3>Option A: Analysing primary datasets</h3> </summary>
<p>
As mentioned above, you do not typically perform an analysis directly on the AOD files. However, there may be cases when you want to do so. Therefore, we have provided an example analysis to take you through the steps that you may need on the occassions that you want to analyse the AOD files directly. You can find the files and instructions in <a href="/record/5001">this CMS analysis example</a>.  
</p>

<p>
<b>NOTE</b>: To analyse the full event content, the analysis job needs access to the "condition data", such as trigger information or jet-energy corrections. In the VM, the condition database is made available through the <code>cvmfs</code> file system, and in the container, the condition data can be read from predefined condition data servers. In both cases, reading the condition data for the first time can take very long. For the 2011 and 2012 collision and simulated data, a selection of condition databases is provided locally in the <code>cmssw_5_3_32-slc6_amd64_gcc472</code> container, and the access is much faster. Comment or uncomment the lines related to condition data depending of your environment following the instructions in the configuration file <code>PhysObjectExtractor/python/poet_cfg.py</code>. See detailed instructions for the use of condition data for different data-taking years in <a href="/docs/cms-guide-for-condition-database">the guide to the CMS condition database</a>.
</p>
</details>

<details>
<summary><h3>Option B: Analysing reduced datasets</h3></summary>

<p>
First of all, you will need to apply a filter for validated data. Then, you will want to apply some identification and selection criteria (e.g. whether the objects in your analysis are isolated from or close to other particles in the same collision).
</p>

<p>
For a quick start on how to do this and to write out the most common objects and their properties, use the "Physics Object Extractor Tool (POET)" available in <a href="https://github.com/cms-opendata-analyses/PhysObjectExtractorTool/tree/2012">this repository</a>. You can use <a href="http://root.cern.ch">ROOT</a> to inspect reconstructed particles and the distributions of their properties.
</p>

<p>
Start by getting the code and compiling it. Make sure that you are back in the <b>CMSSW_5_3_32/src/</b> folder. If you are using the VM, do the git command to get the code in the "Outer shell" terminal. Go to the right folder with <code>cd ~/CMSSW_5_3_32/src</code>. In the container, keep using the normal container shell and go to the right folder with <code>cd $CMSSW_BASE/src</code>.

```shell
$ git clone https://github.com/cms-opendata-analyses/PhysObjectExtractorTool.git
```
</p>

<p>
If you are using the VM, change now back to the "CMS shell" terminal. Get the 2012 "branch" of the repository and, always in the **CMSSW_5_3_32/src/** folder, compile the code with:

```
$ cd PhysObjectExtractorTool
$ git checkout 2012
$ scram b
```
</p>

<p>
Note how only the validated runs are selected in the configuration file. The relevant lines are:

```python
    import FWCore.ParameterSet.Config as cms
    import FWCore.PythonUtilities.LumiList as LumiList

    [...]

	goodJSON = "data/Cert_190456-208686_8TeV_22Jan2013ReReco_Collisions12_JSON.txt"
	myLumis = LumiList.LumiList(filename=goodJSON).getCMSSWString().split(",")
	process.source.lumisToProcess = CfgTypes.untracked(
	    	CfgTypes.VLuminosityBlockRange())
	process.source.lumisToProcess.extend(myLumis)
```
</p>

<p>
This selection must always be applied to any analysis on CMS open data, and to do so you must have the validation file downloaded to your local area.
</p>

<p>
To produce a root file with selected objects, do the following:

```shell
$ cd PhysObjectExtractor
$ cmsRun python/poet_cfg.py
```
</p>

<p>
The configuration file sets it to run over 1000 events in a simulated dataset.
</p>


If you are using the CMS open data container with the VNC application installed (see the <a href="/docs/cms-guide-docker#vnc">container guide page</a>), for opening the graphical user interface, start the VNC application in the container by typing

```shell
$ start_vnc
```


and then start a VNC viewer on your local computer using the password <code>cms.cern</code>. The http option for a GUI in the browser is not guaranteed to work in the container with this CMSSW version.

You can now open the POET output file in ROOT:

```shell
$ root myoutput.root
```

You will see the ROOT logo appear on screen. You can now open the ROOT GUI by entering:

```shell
TBrowser t
```

and you will see the ROOT browser window:<br>

<img src="/static/docs/getting-started-with-cms-2011-data/getting_started_with_cms_2011_2012_data_1.png" width="70%">

Now, let us take a closer look at some collections of physics objects.

On the left window of ROOT, double-click on the file name (<code>myoutput.root</code>). You should see a list of names, each corresponding to a collection of reconstructed data.

Let us take a peek, for example, at the muons, which are found in <code>mymuons</code>. Look in there by double-clicking on that line and then double-clicking on <code>Events</code>. Here, you can have a look at various properties of this collection, such as the transverse momentum of the muon: <code>muon_pt</code>. Double-click on it to draw the distribution.

<img src="/static/docs/getting-started-with-cms-2011-data/getting_started_with_cms_2011_2012_data_2.png" width="70%">

You can exit the ROOT browser through the GUI by clicking on <code>Browser</code> on the menu and then clicking on <code>Quit Root</code> or by entering <code>.q</code> in the terminal.

That's it! Hope you enjoyed this exercise. Feel free to play around with the rest of the data and write your own analyzers and analysis code. Learn more in <a href="https://cms-opendata-guide.web.cern.ch/">the CMS Open data guide</a> and have a look at the other example analysis workflows such as the <a href="/record/12340">tool to produce reduced "NanoAOD" format for outreach and education</a> and the example analyses on its output implemented in python for the <a href="/record/1234)">di-muon spectrum</a> or the <a href="/record/12350">Higgs boson decay to two tau leptons</a>, or the Higgs decay to four leptons implemented in <a href="/record/5500">C++</a> or using <a href="/record/12360">ROOT's RDataFrame</a>, or the <a href="/record/22350">di-muon spectrum analysis using Julia</a>.
<br>
</details>
</details>
