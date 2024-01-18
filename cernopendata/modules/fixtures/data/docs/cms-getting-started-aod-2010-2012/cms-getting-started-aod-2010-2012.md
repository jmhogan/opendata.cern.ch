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


## <a name="nice">"Nice! But how do I analyse these data?"</a>

<p>
        You can perform analysis on the AOD dataset directly or on a reduced dataset that is derived from the AOD data. Analyzing on the original AOD dataset can be computationally heavy. Thus, it is recommended to use the reduced dataset, unless you need some information that is only contained in AOD data. 
</p>

<p>
        Below we provide examples of how to perfom analysis on both the primary AOD data and the reduced data. 
</p>

<details>
<summary><a name="EDAnalyzer"><h3>Analysing the primary AOD dataset using EDAnalyzer</h3></a></summary>

<p>
As mentioned above, you typically do not perform an analysis directly on the AOD files. However, there might be cases where only the AOD files contain some of the information you need. The objects contained in the AOD files can be accessed through a software module, which can be built with a helper script (EDAnalyzer) available in the CMS open data environment. Here we provide a simple example on how to use EDAnalyzer. 
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
Change the file name in the configuration file <code>demoanalyzer_cfg.py</code> in the DemoAnalyzer directory. Take the <a href="/record/14">Mu primary dataset</a> from Run2010B (<a href="/record/24460">SingleMu dataset</a> from Run2012D) as an example. Replace <code>file:myfile.root</code> with <code>file:myfile.root</code> with <code>root://eospublic.cern.ch//eos/opendata/cms/Run2010B/Mu/AOD/Apr21ReReco-v1/0000/00459D48-EB70-E011-AF09-90E6BA19A252.root</code (<code>root://eospublic.cern.ch//eos/opendata/cms/Run2012D/SingleMu/AOD/22Jan2013-v1/10000/0015EC7D-EAA7-E211-A9B9-E0CB4E5536A7.root</code>). 
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
<strong>NOTE</strong>: To analyse the full event content, the analysis job needs access to the "condition data", such as the jet-energy corrections. To see how the connection to the condition database is established, you can check the <a href="/docs/cms-guide-for-condition-database">Guide to the CMS condition database</a>. For simpler analyses, like the example above, where we use only physics objects needing no further data for corrections, you do not need to connect to the condition database.
</p>

<p>
For detailed examples on applying selections and analyzing the full event content of AOD files through EDAnalyzer, refer to <a href="/record/560">this CMS analysis example for 2010 data</a> and <a href="/record/5500">this CMS analysis example for 2011-2012 data</a>. Take a look at the scripts to learn how selections and extractions are done. 
</p><br>

</details>


<p>
        Physics Object Extractor Tool (POET) is an example code to extract the physics object information from CMS data. It is available for <a href="https://github.com/cms-opendata-analyses/PhysObjectExtractorTool/tree/2011">2011</a> and <a href="https://github.com/cms-opendata-analyses/PhysObjectExtractorTool/tree/2012">2012</a> AOD data. It is not available for the 2010 data, but we can perform selection and extraction directly with EDAnalyzer. POET is just a collection of Event Data Analyzer (EDAnalyzer). 
</p><br>

<details>
<summary><h3> Analysing reduced dataset </h3></summary>
  
  <p>
  AOD data can be reduced to NanoAOD-like data formats, which hold tuples instead of C++ class and thus can be read directly through ROOT. One useful otpion of analyzing the reduced dataset is using <b>NanoAODRun1</b> data, which is available for all Run1 data (2010-2012) on Open Data Portal. The <a href="https://github.com/cms-opendata-analyses/NanoAODRun1ProducerTool">production code</a> is available but not intended to be used by non-expert users. Users who wish to produce reduced dataset by themselves should refer to the other option -- <a href="https://github.com/cms-opendata-analyses/PhysObjectExtractorTool"><b>Physics Object Extractor Tool (POET)</b></a>, which extracts information of different physics objects into a ROOT file and produces NanoAOD-like tuples from AOD files. It is in essence a collection of EDAnalyzer that we saw in the <a href="#EDAnalyzer">previous subsection</a>. Note that POET is only avaialble for 2011 and 2012 data. Users should refer back to the <a href="#EDAnalyzer">EDAnalyzer</a>, if they need more information from the 2010 data than what is already in NanoAODRun1. Examples on how to use NanoAODRun1 and POET are provided respectively. 
  </p><br>
  
  <details>
  <summary><h4>Reduce the AOD files to NanoAODRun1 tuples</h4></summary>
    
  <p>
  The NanoAODRun1 format is a NanoAOD-like ntuple format for CMS Run 1 data, readable with bare ROOT or other ROOT-compatible software. It contains the per-event information that is needed in most generic analyses. The goal is that about 50% of all publishable Open Data analyses can be performed using this simplified and easy-to-access data format without compromise of the quality of the scientific result. 
  </p>

  <p>
  Note that NanoAODRun1 dfata format should not be confused with another NanoAOD-like <a href="/record/12353">reduced format created for educational purposes rather than for analysis purposes</a>, which is sometimes also referred to as "NanoAOD" in the Open Data context.
  </p>
  
  <p>
    Here we provide examples on how to use NanoAODRun1 data to reproduce published results. The setup and usage of NanoAODRun1 are the same for all years (2010-2012).
  </p>

  <details>
  <summary><b>Plot histogram with standard ROOT macro in C++</b></summary>

  In this example, we are rerpoducing the plot of invariant mass spectrum of dimuons in a <a href="https://inspirehep.net/literature/1118729">CMS paper</a> that uses the 2010 muon data. 

  The only thing we need to do is to write a C++ script and run it with ROOT.

  Create a C++ script with the name "MuHistos_eospublic.cxx":
  ```shell
  touch MuHistos_eospublic.cxx
  ```

  Copy and paste the code to the script:
  <pre>
    <code>
      {
      // the opening parenthesis is important!
      // the following code can also be typed by hand on the root command line 
      // (or copy-pasted into it one by one or in blocks).
      // To run it as a script, start interactive root and type .x Dimuon2011_public.C
      // (takes about 10 minutes locally from interactive DESY workgroup server)
      // if access to eospublic doesn't work, try 
      // source /cvmfs/sft.cern.ch/lcg/views/LCG_98/x86_64-centos7-gcc8-opt/setup.sh
      //
      // enable implicit multithreading
      //ROOT::EnableImplicitMT();
      //
      // chain t1 is 2011 DoubleMu Run A in NanoAODRun1 format
      TChain *t1 = new TChain("Events");
      t1->Add("root://eospublic.cern.ch//eos/opendata/cms/derived-data/NanoAODRun1/01-Jul-22/Run2011A_DoubleMu_merged.root");
      //
      // define a canvas with log y scale
      TCanvas *c1=new TCanvas("c1","c1",1);
      c1->SetLogy();                                                // set log scale
      gStyle->SetOptStat(0);                                        // remove box
      
      // book the histogram
      TH1D *h_dimulog = new TH1D("h_dimulog", "h_dimulog", 620,-0.4, 2.7);
      gROOT->cd();
      cout << "high pt dimuon" << endl;
      // fill the histogram from the ntuple ("high pt" = 13/8 or larger, see threshold "bump")
      // the factor in the second argument acts as a weight
      t1->Draw("log10(Dimu_mass)>>h_dimulog","2./log(10.)/Dimu_mass*(run<170000 && Trig_DoubleMuThresh>12 && Dimu_charge==0 && Muon_pt[Dimu_t1muIdx]>6. && Muon_pt[Dimu_t2muIdx]>6. && Muon_mediumId[Dimu_t1muIdx] && Muon_mediumId[Dimu_t2muIdx])");
      // clone the histogram and set to no directory such that it does not get deleted
      TH1D *h_dimulog1 = (TH1D*)h_dimulog->Clone(); 
      h_dimulog1->SetDirectory(0);
      //
      // chain t2 is 2011 MuOnia Run A in NanoAODRun1 format
      TChain *t2 = new TChain("Events");
      t2->Add("root://eospublic.cern.ch//eos/opendata/cms/derived-data/NanoAODRun1/01-Jul-22/Run2011A_MuOnia_merged.root");
      //
      // explicit rebooking is necessary for name labels to be picked up by Draw
      TH1D *h_dimulog2 = new TH1D("h_dimulog2", "h_dimulog2", 620,-0.4, 2.7);
      TH1D *h_dimulog4 = new TH1D("h_dimulog4", "h_dimulog4", 620,-0.4, 2.7);
      TH1D *h_dimulog6 = new TH1D("h_dimulog6", "h_dimulog6", 620,-0.4, 2.7);
      TH1D *h_dimulog7 = new TH1D("h_dimulog7", "h_dimulog7", 620,-0.4, 2.7);
      TH1D *h_dimulog8 = new TH1D("h_dimulog8", "h_dimulog8", 620,-0.4, 2.7);
      TH1D *h_dimulog12 = new TH1D("h_dimulog12", "h_dimulog12", 620,-0.4, 2.7);
      TH1D *h_dimulog3 = (TH1D*)h_dimulog2->Clone(); 
      TH1D *h_dimulog5 = (TH1D*)h_dimulog4->Clone(); 
      TH1D *h_dimulog9 = (TH1D*)h_dimulog4->Clone(); 
      TH1D *h_dimulog10 = (TH1D*)h_dimulog4->Clone(); 
      TH1D *h_dimulog11 = (TH1D*)h_dimulog4->Clone(); 
      TH1D *h_dimulog13 = (TH1D*)h_dimulog4->Clone(); 
      cout << "all MuOnia" << endl;
      // all except displaced, trimuon, and 0 threshold triggers (and events already treated from DoubleMuon)
      t2->Draw("log10(Dimu_mass)>>h_dimulog4","2./log(10.)/Dimu_mass*(run<170000 && !(Alsoon_DoubleMu && Trig_DoubleMuThresh>12) && Trig_JpsiThresh !=0 && (!HLT_DoubleMu4_LowMass_Displaced && !HLT_DoubleMu4p5_LowMass_Displaced && !HLT_DoubleMu5_LowMass_Displaced && !HLT_Dimuon6p5_LowMass_Displaced && !HLT_Dimuon7_LowMass_Displaced) && (!HLT_DoubleMu4_Jpsi_Displaced && !HLT_DoubleMu5_Jpsi_Displaced && !HLT_Dimuon6p5_Jpsi_Displaced && !HLT_Dimuon7_Jpsi_Displaced) && !HLT_Mu5_L2Mu2 && Dimu_mass>2. && Dimu_charge==0 && Muon_pt[Dimu_t1muIdx]>3. && Muon_pt[Dimu_t2muIdx]>3. && Muon_mediumId[Dimu_t1muIdx] && Muon_mediumId[Dimu_t2muIdx])");
      // early 2011A Quarkonium trigger only
      cout << "Quarkonium/Low pT dimuon only" << endl;
      // was cut offline at m>2
      t2->Draw("log10(Dimu_mass)>>h_dimulog2","2./log(10.)/Dimu_mass*(run<170000 && !(Alsoon_DoubleMu && Trig_DoubleMuThresh>12) && HLT_DoubleMu3_Quarkonium && Dimu_mass>2. && Dimu_charge==0 && Muon_pt[Dimu_t1muIdx]>2. && Muon_pt[Dimu_t2muIdx]>2. && Muon_mediumId[Dimu_t1muIdx] && Muon_mediumId[Dimu_t2muIdx])");
      // early quarkonium and Upsilon
      cout << "Quarkonium and Upsilon" << endl;
      // to take care of the tails, Upsilon should have cuts 7<m<14
      t2->Draw("log10(Dimu_mass)>>h_dimulog6","2./log(10.)/Dimu_mass*(run<170000 && !(Alsoon_DoubleMu && Trig_DoubleMuThresh>12) && (HLT_DoubleMu3_Quarkonium || ((HLT_Dimuon0_Upsilon || HLT_Dimuon0_Barrel_Upsilon || HLT_DoubleMu3_Upsilon || HLT_Dimuon5_Upsilon_Barrel || HLT_Dimuon7_Upsilon_Barrel) && Dimu_mass>7. && Dimu_mass<14.)) && Dimu_mass>2. && Dimu_charge==0 && Muon_pt[Dimu_t1muIdx]>2. && Muon_pt[Dimu_t2muIdx]>2. && Muon_mediumId[Dimu_t1muIdx] && Muon_mediumId[Dimu_t2muIdx])");
      // early quarkonium and B0
      cout << "Quarkonium and B0" << endl;
      // to take care of the tails, B0 should have cuts 4<m<7
       t2->Draw("log10(Dimu_mass)>>h_dimulog7","2./log(10.)/Dimu_mass*(run<170000 && !(Alsoon_DoubleMu && Trig_DoubleMuThresh>12) && ((HLT_DoubleMu3_Quarkonium && Muon_pt[Dimu_t1muIdx]>2. && Muon_pt[Dimu_t2muIdx]>2.) || ((HLT_Dimuon6_Bs || HLT_Dimuon4_Bs_Barrel || HLT_DoubleMu4_Dimuon6_Bs || HLT_DoubleMu4_Dimuon4_Bs_Barrel || HLT_DoubleMu3_Bs || HLT_DoubleMu2_Bs) && Dimu_mass>4. && Dimu_mass<7.)) && Dimu_mass>2. && Dimu_charge==0 && Muon_pt[Dimu_t1muIdx]>2. && Muon_pt[Dimu_t2muIdx]>2. && Muon_mediumId[Dimu_t1muIdx] && Muon_mediumId[Dimu_t2muIdx])"); // 
      // early quarkonium and Jpsi
      cout << "Quarkonium and Jpsi" << endl;
      // to take care of the tails, Dimuon0 and Dimuon6p5 should have cuts 2.8<m<3.4, Dimuon10/13 should have cuts 2.5<m<4.3
      t2->Draw("log10(Dimu_mass)>>h_dimulog8","2./log(10.)/Dimu_mass*(run<170000 && !(Alsoon_DoubleMu && Trig_DoubleMuThresh>12) && ((HLT_DoubleMu3_Quarkonium && Muon_pt[Dimu_t1muIdx]>3. && Muon_pt[Dimu_t2muIdx]>3.) || ((HLT_Dimuon6p5_Jpsi || HLT_Dimuon6p5_Barrel_Jpsi) && Dimu_mass>2.5 && Dimu_mass<4.3) || ((HLT_Dimuon0_Jpsi || HLT_Dimuon13_Jpsi_Barrel || HLT_Dimuon10_Jpsi_Barrel) && Dimu_mass>2.8 && Dimu_mass<3.4)) && Dimu_mass>2. && Dimu_charge==0 && Muon_pt[Dimu_t1muIdx]>1.5 && Muon_pt[Dimu_t2muIdx]>1.5 && Muon_mediumId[Dimu_t1muIdx] && Muon_mediumId[Dimu_t2muIdx])"); // HLT_Dimuon0_Jpsi? -> not culprit for tail, HLT_Dimuon10/13_Jpsi_Barrel is?
      // early quarkonium and Jpsi/psiprime
      cout << "Quarkonium and Jpsi/psiprime" << endl;
      // to take care of the tails, the psiprime triggers should have cuts 3.4<m<4.3
      t2->Draw("log10(Dimu_mass)>>h_dimulog12","2./log(10.)/Dimu_mass*(run<170000 && !(Alsoon_DoubleMu && Trig_DoubleMuThresh>12) && ((HLT_DoubleMu3_Quarkonium && Muon_pt[Dimu_t1muIdx]>3. && Muon_pt[Dimu_t2muIdx]>3.) || ((HLT_Dimuon6p5_Jpsi || HLT_Dimuon6p5_Barrel_Jpsi) && Dimu_mass>2.5 && Dimu_mass<4.3) || ((HLT_Dimuon0_Jpsi || HLT_Dimuon13_Jpsi_Barrel || HLT_Dimuon10_Jpsi_Barrel) && Dimu_mass>2.8 && Dimu_mass<3.4) || ((HLT_Dimuon11_PsiPrime || HLT_Dimuon9_PsiPrime || HLT_Dimuon7_PsiPrime) && Dimu_mass>3.4 && Dimu_mass<4.3)) && Dimu_mass>2. && Dimu_charge==0 && Muon_pt[Dimu_t1muIdx]>1.5 && Muon_pt[Dimu_t2muIdx]>1.5 && Muon_mediumId[Dimu_t1muIdx] && Muon_mediumId[Dimu_t2muIdx])"); 
      h_dimulog3->Add(h_dimulog1,h_dimulog2,1,1);
      h_dimulog5->Add(h_dimulog1,h_dimulog4,1,1);
      h_dimulog9->Add(h_dimulog1,h_dimulog6,1,1);
      h_dimulog10->Add(h_dimulog1,h_dimulog7,1,1);
      h_dimulog11->Add(h_dimulog1,h_dimulog8,1,1);
      h_dimulog13->Add(h_dimulog1,h_dimulog12,1,1);
      // draw histogram
      //h_dimulog5->SetFillColor(5); // yellow
      //h_dimulog5->GetXaxis()->SetTitle("Invariant Log10(Mass) for Nmuon>=2 (in log10(m/GeV/c^2))");
      //h_dimulog5->GetYaxis()->SetTitle("Number of Events/10 MeV");
      //h_dimulog5->SetMinimum(0.02);
      //h_dimulog5->SetMaximum(3.E6);
      //h_dimulog5->Draw("hist");
      h_dimulog9->SetTitle("Dimuon mass spectrum 2011 7 TeV (1.2 fb-1)");  // set histogram title
      h_dimulog9->SetFillColor(8); // Green
      h_dimulog9->GetXaxis()->SetTitle("Invariant Log10(Mass) for Nmuon>=2 (in log10(m/GeV/c^2))");
      h_dimulog9->GetYaxis()->SetTitle("Number of Events/10 MeV");
      h_dimulog9->SetMinimum(0.02);
      h_dimulog9->SetMaximum(3.E6);
      h_dimulog9->Draw("hist");
      // draw others on top
      //h_dimulog9->Draw("hist same");
      h_dimulog10->SetFillColor(29); // blue_green
      h_dimulog10->Draw("hist same");
      h_dimulog13->SetFillColor(9); // dark blue
      h_dimulog13->Draw("hist same");
      h_dimulog11->SetFillColor(2); // red
      h_dimulog11->Draw("hist same");
      h_dimulog3->SetFillColor(38); // dark grey
      h_dimulog3->Draw("hist same");
      h_dimulog1->SetFillColor(18); // light grey
      h_dimulog1->Draw("hist same");
      // regenerate ticks 
      gPad->RedrawAxis();
      //
      // produce output picture file 
      c1->Print("Dimuon2011_eospublic.png");
      // write out histograms (will delete previous file, if any!)
      TFile Dimuon2011("Dimuon2011_eospublic.root","RECREATE"); 
      h_dimulog1->Write();
      h_dimulog2->Write();
      h_dimulog3->Write();
      h_dimulog4->Write();
      h_dimulog5->Write();
      h_dimulog6->Write();
      h_dimulog7->Write();
      h_dimulog8->Write();
      h_dimulog9->Write();
      h_dimulog10->Write();
      h_dimulog11->Write();
      h_dimulog12->Write();
      h_dimulog13->Write();
      // output root file will be closed automatically when session is closed
      //
      // the closing parenthesis is important!
      }
    </code>
  </pre>

  Execute it with 
  
  ```shell
  root -l MuHistos_eospublic.cxx++
  ```

  <b>Troubleshoot</b>: Make sure you have access to ROOT. It is automatically available if you are in <a href="#vm">CMS environment</a>. You may also install ROOT locally, following <a href="https://root.cern/install/">the instructions here</a>. To test if you have access to ROOT, execute <code>root -l</code>. This command should start a ROOT session for you, if it is installed.

  The output plot looks like this:
  
  <img src="/static/docs/cms-getting-started-aod-2010-2012/MuHistos_eospublic_mass.png" width="70%">

  <br>
  </details>

  <details>
  <summary><b>Plot histogram with interactive CINT/Cling and/or RDataFrame</b></summary>
    
    <p>
  In this example, we will reproduce simultaneously one plot from a <a href="https://inspirehep.net/literature/1292243">CMS conference report</a> and one plot from <a href="https://inspirehep.net/literature/1485699"> a CMS paper</a>. This example is slightly more complicated than then previous example. It involves trigger selections, muon quality selections, an individually revertexed dimuon system to reduce pileup background, and dealing with two different overlapping datasets. Using this example, we show how to work on NanoAODRun1 data using interactive CINT/Cling or RDataFrame.
    </p>

    <details>
    <summary><h5>CINT/Cling</h5></summary>
    </details>
  
    <details>
      <summary><h5>RDataFrame</h5></summary>
    </details>
  
  </details>
    
  </details>

  <details>
  <summary><h4>Reduce the AOD files using POET</h4></summary>
    D
  </details>
  
</details>

<!-- Tab links -->
<div class="tab">
  <button class="tablinks" onclick="openCity(event, 'London')">London</button>
  <button class="tablinks" onclick="openCity(event, 'Paris')">Paris</button>
  <button class="tablinks" onclick="openCity(event, 'Tokyo')">Tokyo</button>
</div>

<!-- Tab content -->
<div id="London" class="tabcontent">
  <h3>London</h3>
  <p>London is the capital city of England.</p>
</div>

<div id="Paris" class="tabcontent">
  <h3>Paris</h3>
  <p>Paris is the capital of France.</p> 
</div>

<div id="Tokyo" class="tabcontent">
  <h3>Tokyo</h3>
  <p>Tokyo is the capital of Japan.</p>
</div>
