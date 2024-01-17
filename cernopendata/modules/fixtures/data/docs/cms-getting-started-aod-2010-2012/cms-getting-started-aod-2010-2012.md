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
</p><br>

<details>
<summary><h3>Analysing the primary AOD dataset using EDAnalyzer</h3></summary>
  
        <p>
        As mentioned above, you typically do not perform an analysis directly on the AOD files. However, there might be cases where only the AOD files contain some of the information you need. The objects contained in the AOD files can be accessed through a software module, which can be built with a helper script (EDAnalyzer) available in the CMS open data environment. Here we provide a simple example on how to use EDAnalyzer. 
        </p>

        
</details>

