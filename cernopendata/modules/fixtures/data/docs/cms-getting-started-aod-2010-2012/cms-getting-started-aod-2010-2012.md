1. ["I have installed the CMS open data environment: now what?"](#vm)
2. ["OK! What is in the CMS data?"](#data)
3. ["Nice! But how do I analyze these data?"](#nice)

The CMS primary data for 2010-2012 are provided on the CERN Open Data Portal in the Analysis Object Data (AOD) format. This page provides tutorials on how to access and analyze CMS data in this format for each year.

## <a name="vm">"I have installed the CMS open data environment / virtual machine: now what?"</a>

To analyze CMS data collected in different years, you need different versions of CMSSW (an event processing model). The recommened version for the 2010 data is <b>version 4.2.8</b>, supported only on <b>Scientific Linux 5</b>. The recommended version for the 2011 and 2012 data is <b>version 5.3.32</b>, supported only on <b>Scientific Linux 6</b>. If you are unfamiliar with Linux, take a look at <a href="https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookBasicLinux">this short introduction to Linux</a> or <a href="https://swcarpentry.github.io/shell-novice/">tutorial</a>.

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
If you do not want to work on a virtual machine, you can try to to analyze CMS data in a Docker container, following the <a href="/docs/cms-guide-docker">instruction</a>.
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
If you do not want to work on a virtual machine, you can try to to analyze CMS data in a Docker container, following the <a href="/docs/cms-guide-docker">instruction</a>.
</p>
<br>
</details>

## <a name="data"> "OK! What is in the CMS data?" </a>

<p>
The primary CMS data for 2010 to 2012 on the CERN Open Data Portal are in the format of Analysis Object Data (AOD). The AOD files contain all the information that is needed for physics analysis. These files are prepared by piecing raw data collected by various sub-detectors of CMS. A list of the physics objects contained in the AOD files can be found through the links for <a href="/docs/cms-physics-objects-2010">2010</a> and for <a href="/docs/cms-physics-objects-2011">2011</a>. The AOD files contains physics objects (C++ classes) rather than numbers that you can click on and read.
</p>

<p>
Let's see what physics objects are contained in an AOD file.
</p>

<details>
<summary><h4>2010<h4></summary>

<p>
Make sure that you are in the <b>CMSSW_4_2_8/src/</b> folder (and in the "CMS Shell" terminal, if using the "CMS-OpenData-1.1.2" VM). Also make sure that you have executed the <code>cmsenv</code> command in your terminal to launch the CMS analysis environment.
</p>

<p>
Select a dataset, for example, the <a href="/record/24404">Mu primary dataset</a> from Run2010B. Click the "Download" tab at the bottom of the page to see a list of files contained in this dataset. You can select a file from the list and print out its contents with:

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
</p><br>
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
</p><br>
</details>


## <a name="nice">"Nice! But how do I analyze these data?"</a>

<p>
        You can perform analysis on the AOD dataset directly or on a reduced dataset that is derived from the AOD data. Analyzing on the original AOD dataset can be computationally heavy. Thus, it is recommended to use the reduced dataset, unless you need some information that is only contained in AOD data. 
</p>

<p>
  Let's first see how to perform analysis on the primary AOD dataset. 
</p>

<h3>analyzing the primary AOD dataset using EDAnalyzer</h3>

<p>
As mentioned above, you typically do not perform an analysis directly on the AOD files. However, there might be cases where only the AOD files contain some of the information you need. The objects contained in the AOD files can be accessed through a software module, which can be built with a helper script (EDAnalyzer) available in the CMS open data environment.
</p>

<p>
In CMS environment (after running <code>cmsenv</code> in <a href="#vm">the first section</a>), do the following:

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
Change the file name in the configuration file <code>demoanalyzer_cfg.py</code> in the DemoAnalyzer directory. If we want to check the list of content in he <a href="/record/14">Mu primary dataset</a> from Run2010B, we can replace <code>file:myfile.root</code> with one of the root files in this record, e.g. <code>root://eospublic.cern.ch//eos/opendata/cms/Run2010B/Mu/AOD/Apr21ReReco-v1/0000/00459D48-EB70-E011-AF09-90E6BA19A252.root</code>. If we want to check the list of content in the <a href="/record/24460">SingleMu dataset</a> from Run2012D, we can replace <code>file:myfile.root</code> with one of the root files in this record, e.g. <code>root://eospublic.cern.ch//eos/opendata/cms/Run2012D/SingleMu/AOD/22Jan2013-v1/10000/0015EC7D-EAA7-E211-A9B9-E0CB4E5536A7.root</code>. 
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

<p>
<strong>NOTE</strong>: To analyze the full event content, the analysis job needs access to the "condition data", such as the jet-energy corrections. To see how the connection to the condition database is established, you can check the <a href="/docs/cms-guide-for-condition-database">Guide to the CMS condition database</a>. For simpler analyses, like the example above, where we use only physics objects needing no further data for corrections, you do not need to connect to the condition database.
</p>

<p>
For detailed examples on applying selections and analyzing the full event content of AOD files through EDAnalyzer, refer to <a href="/record/560">this CMS analysis example for 2010 data</a> and <a href="/record/5500">this CMS analysis example for 2011-2012 data</a>. Take a look at the scripts to learn how selections and extractions are done. 
</p><br>

Next, let's see how to analyze the reduced datasets.

<h3> analyzing reduced dataset </h3>

<p>
AOD data can be reduced to simpler formats that hold tuples instead of C++ class and thus can be read directly through ROOT. Within CMS, this type of data is called NanoAOD. For Open Data analyses, we can reduce the AOD data to some NanoAOD-like formats, using one of the two available production tools -- <a href="https://github.com/cms-opendata-analyses/NanoAODRun1ProducerTool">NanoAODRun1 Producer</a> and <a href="https://github.com/cms-opendata-analyses/PhysObjectExtractorTool">POET</a>. One useful otpion of analyzing the reduced dataset is using <b>NanoAODRun1</b> data, which is available for all Run1 data (2010-2012) on Open Data Portal. For 2010 - 2012 data, the NanoAODRun1 Producer can be used to produce NanoAOD files. For 2011 - 2012 data, the Physics Object Extractor Tool (POET) can be used to produce similar files, and is set up so that users could configure the types of physics objects or selected events to include in the files.
</p>
<p>
<a href="https://github.com/cms-opendata-analyses/PhysObjectExtractorTool">Physics Object Extractor Tool (POET)</a> is an example code to extract the physics object information from CMS data. It is essentially a collection of EDAnalyzer that we saw in the <a href="#EDAnalyzer">previous subsection</a>. It is available for <a href="https://github.com/cms-opendata-analyses/PhysObjectExtractorTool/tree/2011">2011</a> and <a href="https://github.com/cms-opendata-analyses/PhysObjectExtractorTool/tree/2012">2012</a> AOD data.
</p><br>


<h4>Reduce the AOD files to NanoAODRun1 tuples</h4>

<p>
The NanoAODRun1 format is a NanoAOD-like ntuple format for CMS Run 1 data, readable with bare ROOT or other ROOT-compatible software. It contains the per-event information that is needed in most generic analyses. The goal is that about 50% of all publishable Open Data analyses can be performed using this simplified and easy-to-access data format without compromise of the quality of the scientific result. A list of variables in NanoAODRun1 MC data can be found <a href="https://twiki.cern.ch/twiki/pub/CMSPublic/WorkBookNanoAODRun1/doc_DYJetsToLL_M-50_7TeV.html">here</a>. Collision data contains the same variables, except for the generator-level information.
</p>

<p>
Note that NanoAODRun1 data format should not be confused with another NanoAOD-like <a href="/record/12353">reduced format created for educational purposes rather than for analysis purposes</a>, which is sometimes also referred to as "NanoAOD" in the Open Data context.
</p>

<p>
Some datasets have already been processed as NanoAODRun1 files (link coming soon), and new datasets can be processed by following the <a href="https://github.com/cms-opendata-analyses/NanoAODRun1ProducerTool">instructions</a>. <b>Note</b>: user customization is not supported for NanoAODRun1, but files can be produced according to this code. 
</p>

<p>
  Here we provide some examples on how to use NanoAODRun1 data to reproduce published results. For more examples and explanations on using NanoAODRun1 datasets, check <a href="https://twiki.cern.ch/twiki/bin/view/CMSPublic/NanoAODRun1Examples">here</a>. The setup and usage of NanoAODRun1 should be the same for all years (2010-2012). 
</p>

<details>
<summary><b>Plot histogram with standard ROOT macro in C++</b></summary>

In this example, we are rerpoducing the plot of invariant mass spectrum of dimuons in a <a href="https://inspirehep.net/literature/1118729">CMS paper</a> that uses the 2010 muon data. 

The only thing we need to do is to write a C++ script and run it with ROOT.

Create a C++ script with the name "MuHistos_eospublic.cxx":
```shell
touch MuHistos_eospublic.cxx
```

Copy and paste the <a href="https://twiki.cern.ch/twiki/pub/CMSPublic/NanoAODRun1Examples/MuHistos_eospublic.cxx">code</a> to the script.

Execute it with 

```shell
root -l MuHistos_eospublic.cxx++
```

<b>Troubleshoot</b>: Make sure you have access to ROOT. It is automatically available if you are in <a href="#vm">CMS environment</a>. To test if you have access to ROOT, execute <code>root -l</code>. This command should start a ROOT session for you, if it is available. If you the job finishes very fast and you get the the output <code>entries = 0</code> (failure of xrootd access, no data read) you might have to source the script described in the FAQ for the next example. 

The output plot looks like this:

<img src="/static/docs/cms-getting-started-with-aod-2010-2012/MuHistos_eospublic_mass.png" width="70%">

<br>
</details>

<details>
<summary><b>Plot histogram with interactive CINT/Cling and/or RDataFrame in C++</b></summary>

<p>
In this example, we will reproduce one plot from a <a href="https://inspirehep.net/literature/1292243">CMS conference report</a> and one plot from <a href="https://inspirehep.net/literature/1485699"> a CMS paper</a>. This example is slightly more complicated than then previous example. It involves trigger selections, muon quality selections, an individually revertexed dimuon system to reduce pileup background, and dealing with two different overlapping datasets. Using this example, we show how to work on NanoAODRun1 data using interactive CINT/Cling or RDataFrame.
</p>

<details>
<summary><h5>CINT/Cling</h5></summary>
<p>
CINT/Cling is the ROOT interactive C++ interpreter, which can be run as a script as well as be run line by line on the command line of an interactive Root session. One does not normally use CINT/Cling for advanced analyses, but it is worthwhile to try out this interactive option before converging to a final analysis strategy. This is the setup that was used for the original development of this example to find the relevant cuts.
</p>
<p>
With NanoAODRun1, the workflow is always the same -- writing an analysis script and execute it in ROOT, regardless of which interface we use it with.
</p>

Create a C++ script with the name "MuHistos_eospublic.cxx":
```shell
touch Dimuon2011_eospublic.C
```

Copy and paste the <a href="https://twiki.cern.ch/twiki/pub/CMSPublic/NanoAODRun1Examples/Dimuon2011_eospublic.C">code</a> to the script.

Execute it with 

```shell
root -l Dimuon2011_eospublic.C
```

It takes at least 30 minutes to run. It might take longer because of your network, because it accesses data remotely from the CERN eospublic disks. If you prefer to download the data to your computer and access it locally, you may use the local data with <a href="https://twiki.cern.ch/twiki/pub/CMSPublic/NanoAODRun1Examples/Dimuon2011_local.C">this script</a>. 

</details>

<details>
<summary><h5>RDataFrame</h5></summary>
<p>
RDataFrame is a powerful interface for data analysis in ROOT. It reads columnar data from a data source and allows easy skimmming  and manipulation of the data in a simple and straightforward way. It also allows multi-threading and other low-level optimizations that may help to speed up the processing time. RDataFrame makes a good choice for analyses with a relatively straightforward cut and analysis flow. 
</p>

Create a C++ script with the name "MuHistos_eospublic.cxx":
```shell
touch Dimuon2011_eospublic_RDF.C
```

Copy and paste the <a href="https://twiki.cern.ch/twiki/pub/CMSPublic/NanoAODRun1Examples/Dimuon2011_eospublic_RDF.C">code</a> to the script. This script plots the dimuon mass spectrum for different trigger paths.

Execute it with 

```shell
root -l Dimuon2011_eospublic_RDF.C
```

If you prefer to download the data (50+80GB) to your computer and access it locally, you may use the local data with <a href="https://twiki.cern.ch/twiki/pub/CMSPublic/NanoAODRun1Examples/Dimuon2011_local_RDF.C">this script</a>.

The output plot looks like this:

<img src="/static/docs/cms-getting-started-with-aod-2010-2012/Dimuon2011_eospublic_RDF.png" width="70%"><br>


If you would like to speed up the processing time through multithreading, try <a href="https://twiki.cern.ch/twiki/pub/CMSPublic/NanoAODRun1Examples/Dimuon2011_eospublic_RDF2.C">this script</a>.

The output plot looks like this:

<img src="/static/docs/cms-getting-started-with-aod-2010-2012/Dimuon2011_eospublic_RDF2.png" width="70%">

<br>
</details>

Exit the ROOT session with <code>.q</code> in the command line, if the session does not automatically end after the execution.

<b>Troubleshoot:</b> If you get the error <code>fatal error: 'Math/Vector4Dfwd.h' file not found</code> with your default ROOT setup, execute

on Centos7:

```shell
  source /cvmfs/sft.cern.ch/lcg/views/LCG_98/x86_64-centos7-gcc8-opt/setup.sh
```

on slc6:

```shell
source /cvmfs/sft.cern.ch/lcg/views/LCG_95/x86_64-slc6-gcc8-opt/setup.sh
```

</details>

<details>
<summary><b>Plot histogram with RDataFrame in python</b></summary>
<p>
In this example, we will reproduce the dimuon spectrum in the <a href="/record/12342">2012 DoubleMuParked outreach example</a>. A much smaller reduced NanoAOD-like ntuples was provided in the outreach example for educational purposes. The analysis scripts from this outreach example can also be used on the larger NanoAODRun1 ntuples. The original <a href="/record/12342">example</a> uses RDataFrame and is available in C++, python and Jupyter notebook. Here we only provide examples in python and Jupyter notebook. For using RDataFrame in C++, please refer to the previous subsection.
</p>
  
Create a C++ script with the name "dimuonSpectrum2012_eospublic.py":
```shell
touch dimuonSpectrum2012_eospublic.py
```

Copy and paste the <a href="https://twiki.cern.ch/twiki/pub/CMSPublic/NanoAODRun1Examples/dimuonSpectrum2012_eospublic.py.txt">code</a> to the script.

Execute it with 

```shell
python dimuonSpectrum2012_eospublic.py
```

The output plot looks like this:

<img src="/static/docs/cms-getting-started-with-aod-2010-2012/dimuonSpectrum2012.png" width="70%"><br>

If you prefer to download the data (80+110GB) to your computer and access it locally, you may use the local data with <a href="https://twiki.cern.ch/twiki/pub/CMSPublic/NanoAODRun1Examples/dimuonSpectrum2012_local.py.txt">this script</a>.

To get a simple demonstration from you web browser without installing ROOT, you can also plug NanoAODRun1 samples into the <a href="/record/12342">original Outreach Jupyter notebook example</a>:

Start the notebook and execute all steps in the order indicated (click on each block and type control enter)

In step \[3\], replace the input file by e.g. <code>root://eospublic.cern.ch//eos/opendata/cms/upload/NanoAODRun1/01-Jul-22/Run2012B_DoubleMuParked/01-Jul-22Run2012B_DoubleMuParked/03C5684F-8BAF-4312-8235-2B0039F2FB93.root</code> (for pasting, use control V).

In step \[12\], change <code>%jsroot</code> on to <code>%jsroot</code> off .

The (low statistics) result (just one file) should pop on on your screen. Note that the notebook might not work on the large merged samples for internal size and memory reasons. Making the usage of Jupyter notebooks possible realistically also for larger samples is currently under investigation.

</details>

<h4>Reduce the AOD files using POET</h4>
<p>
In AOD files, reconstructed physics objects are included without checking their "quality". For example, the reconstructed objects in the muon collection that you printed out in the <a href="#EDAnalyzer">EDAnalyzer example</a> is not guaranteed to be from validated data. In order to analyze only the "good quality" data, you must apply some selection criteria.
</p>
  
<p>
Physics Object Extractor Tool (POET) allows you to filter for validated data, apply selection criteria to select useful events and write out physics objects and their properties to a reduced dataset. For a quick start, check <a href="https://github.com/cms-opendata-analyses/PhysObjectExtractorTool">this repository</a>. Similar to the NanoAODRun1 examples, you can use <a href="http://root.cern.ch">ROOT</a> to inspect reconstructed particles and the distributions of their properties.
</p>

<p>
Start by getting the code and compiling it. Note that POET does not work for the 2010 data, which requires an older version of CMSSW. Make sure that you are back in the <b>CMSSW_5_3_32/src/</b> folder. If you are using the VM, do the git command to get the code in the "Outer shell" terminal. Go to the right folder with <code>cd ~/CMSSW_5_3_32/src</code>. In the container, keep using the normal container shell and go to the right folder with <code>cd $CMSSW_BASE/src</code>.

```shell
$ git clone https://github.com/cms-opendata-analyses/PhysObjectExtractorTool.git
```
</p>

<p>
If you are using the VM, change now back to the "CMS shell" terminal. Get the 2012 (2011) "branch" of the repository for 2012 (2011) data. In the following example, we use the 2012 data, so we checkout the 2012 branch. Make sure that you are always in the <b>CMSSW_5_3_32/src/</b> folder. Checkout the branch and compile the code with:

```shell
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
The configuration file sets it to run over 1000 events in a simulated dataset. The script runs over all the events when the number is set to -1.
</p>

We can check the content of the output ROOT file through command lines or C++ scripts as we did in the previous examples. We can also check the content and make plots through an interactive Graphical User Interface (GUI). We use this example to show how to do so with ROOT GUI.

If you are using the CMS open data container with the VNC application installed (see the <a href="/docs/cms-guide-docker#vnc">container guide page</a>), for opening the graphical user interface, start the VNC application in the container by typing

```shell
$ start_vnc
```

Then start a VNC viewer on your local computer using the password <code>cms.cern</code>. The http option for a GUI in the browser is not guaranteed to work in the container with this CMSSW version.


You can now open the POET output file in ROOT:

```shell
$ root myoutput.root
```

You will see the ROOT logo appear on screen. You can now open the ROOT GUI by entering:

```shell
TBrowser t
```

You will see the ROOT browser window:

<img src="/static/docs/cms-getting-started-with-aod-2010-2012/getting_started_with_cms_2011_2012_data_1.png" width="70%"><br>

Now, let us take a closer look at some collections of the physics objects.

On the left window of ROOT, double-click on the file name (<code>myoutput.root</code>). You should see a list of names, each corresponding to a collection of reconstructed data.

Let us take a peek, for example, at the muons, which are found in <code>mymuons</code>. Look in there by double-clicking on that line and then double-clicking on <code>Events</code>. Here, you can have a look at various properties of this collection, such as the transverse momentum of the muon: <code>muon_pt</code>. Double-click on it to draw the distribution.

<img src="/static/docs/getting-started-with-cms-2011-data/getting_started_with_cms_2011_2012_data_2.png" width="70%"><br>

You can exit the ROOT browser through the GUI by clicking on <code>Browser</code> on the menu and then clicking on <code>Quit Root</code> or by entering <code>.q</code> in the terminal.

<br>

That's it! Hope you enjoyed the exercises. Feel free to play around with the rest of the data and write your own analyzers and analysis code. Learn more in <a href="https://cms-opendata-guide.web.cern.ch/">the CMS Open data guide</a>. Many tutorial lessons can be found in the <a href="https://cms-opendata-guide.web.cern.ch/cmsOpenData/workshops/">CMS Open Data Workshops</a>, particularly from 2020-2021 for AOD data
