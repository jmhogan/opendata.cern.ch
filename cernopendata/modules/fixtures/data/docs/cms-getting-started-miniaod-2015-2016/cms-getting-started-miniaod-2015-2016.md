1. ["I have installed the CMS open data environment: now what?"](#vm)
2. ["OK! What is in the CMS data?"](#data)
3. ["Nice! But how do I analyse these data?"](#nice)

## <a name="env">"I have installed the CMS open data environment: now what?"</a>

<details>
<summary> 2015 </summary>
<p>
To analyse CMS data collected in 2015, you need <b>version 7.6.7</b> of CMSSW, supported on <b>Scientific Linux 6</b>. If you are unfamiliar with Linux, take a look at <a href="https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookBasicLinux">this short introduction to Linux</a>. Once you have installed the <a href="/docs/cms-guide-docker>CMS open data container</a> or the <a href="/docs/cms-virtual-machine-2015">CMS-specific CERN Virtual Machine (VM)</a>, you need to open a terminal.
</p>
If you are using the VM, always use the "CMS shell" terminal available from the "CMS Shell" icon on the desktop for all CMSSW-specific commands, such as compilation and run. In VM, execute the following command in the terminal if you haven't done so before; it ensures that you have this version of CMSSW running:

```shell
$ cmsrel CMSSW_7_6_7
```
<p>
Note that if you get a warning message about the current OS not being slc6, you are using a wrong terminal ("Outer Shell") which is CERN CentOS 7 (cc7). Open a "CMS Shell" terminal as explained above and execute the cmsrel command there.
</p>
<p>
Both in CMS open data container and in the VM, make sure that you are always in the <b>CMSSW_7_6_7/src/</b> directory (and in the "CMS Shell" terminal in VM).
</p>
In VM, the CMS analysis environment needs to be properly setup by entering the following commands in the terminal (you must do so every time you boot the VM before you can proceed):

```shell
$ cd CMSSW_7_6_7/src/
$ cmsenv # do not execute this command if you are working in the container
```
<br>
</details>


<details>
<summary> 2016 </summary>
<p>
To analyse CMS data collected in 2016, you need <b>version 10.6.30</b> of CMSSW, supported on <b>Scientific Linux 7</b>. If you are unfamiliar with Linux, take a look at <a href="https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookBasicLinux">this short introduction to Linux</a>. Once you have installed the <a href="/docs/cms-guide-docker">CMS open data container</a> or the <a href="/docs/cms-virtual-machine-2015">CMS-specific CERN Virtual Machine (VM)</a>, you need to open a terminal. (MIGHT NEED TO UPDATE VM)
</p>
If you are using the VM, always use the "CMS shell" terminal available from the "CMS Shell" icon on the desktop for all CMSSW-specific commands, such as compilation and run. In VM, execute the following command in the terminal if you haven't done so before; it ensures that you have this version of CMSSW running:

```shell
$ cmsrel CMSSW_10_6_30
```
<p>
Note that if you get a warning message about the current OS not being slc7, you are using a wrong terminal ("Outer Shell") which is CERN CentOS 7 (cc7) (HOW TO EDIT THIS?). Open a "CMS Shell" terminal as explained above and execute the cmsrel command there.
</p>
<p>
Both in CMS open data container and in the VM, make sure that you are always in the <b>CMSSW_10_6_30/src/</b> directory (and in the "CMS Shell" terminal in VM).
</p>
<p>
In VM, the CMS analysis environment needs to be properly setup by entering the following commands in the terminal (you must do so every time you boot the VM before you can proceed):
</p>
```shell
$ cd CMSSW_10_6_30/src/
$ cmsenv # do not execute this command if you are working in the container
```
 
<br>
</details>


## <a name="data">"OK! What is in the CMS data?"</a>

<details>
<summary> 2015 </summary>
<p>
The primary data provided by CMS on the CERN Open Data Portal is in a format called <a href="/docs/cms-physics-objects-2015">Analysis Object Data</a> or AOD for short, and from 2015 onwards, in a slimmer format called MINIAOD. These AOD files are prepared by piecing raw data collected by various sub-detectors of CMS and contain all the information that is needed for analysis. The files cannot be opened and understood as simple data tables but require specific sofware in order to be read.
</p>
So, let's see what a MINIAOD file looks like.
<p>
Make sure that you are in the <b>CMSSW_7_6_7/src/</b> folder, and, in VM, you have executed the `cmsenv` command in your terminal to launch the CMS analysis environment.
</p>
You can select a file from a dataset (a listing is available for each dataset record) and print out it contents with:

```shell
$ edmDumpEventContent root://eospublic.cern.ch//eos/opendata/cms/Run2015D/DoubleEG/MINIAOD/08Jun2016-v1/10000/00387F48-342F-E611-AB5D-0CC47A4D76AC.root
```

The ouput is a list of different objects that the file contains, such as

```shell
Type                                  Module                      Label             Process
----------------------------------------------------------------------------------------------
edm::TriggerResults                   "TriggerResults"            ""                "HLT"
[...]
vector<pat::Electron>                 "slimmedElectrons"          ""                "RECO"
[...]
```
<p>
Documentation of these objects is available in <a href="https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookMiniAOD2015#High_level_physics_objects">the CMS WorkBook 2015 MiniAOD page</a>. The objects are implemented as C++ classes in the CMS software package CMSSW, and detailed reference documentation of all classes is available in <a href="https://cmsdoxygen.web.cern.ch/cmsdoxygen/CMSSW_7_6_7/doc/html/annotated.html">the class list of the CMSSW reference manual</a>. To see the properties of electrons, you would navigate to "pat" and find the entry for "Electron". The <a href="https://cmsdoxygen.web.cern.ch/cmsdoxygen/CMSSW_7_6_7/doc/html/d2/d1f/classpat_1_1Electron.html">pat::Electron Class Reference</a> lists all member functions through which the different properties of reconstructed electron can be accessed. Note that many of the basic propertied are "inherited" from the parent classes, and are listed separately under "Public Member Functions inherited from ... ".
</p>
These objects can be accessed in a software module which can be built with a helper script available in the CMS open data environment. If you are using the VM, this helper scripts does not work out of the box, so skip this part and go directly to <a href="#nice">the next section</a>. If you are using the CMS open data container, you can do the following:

```shell
$ mkdir Test
$ cd Test
$ mkedanlzr MiniAnalyzer
$ cd MiniAnalyzer
```
<p>
This will create several template files in the new MiniAnalyzer directory. For more information, have a look in <a href="https://cms-opendata-guide.web.cern.ch/cmssw/cmsswanalyzers/">the CMS open data guide</a>.
</p>

To access the physics object properties, add <code><use name="DataFormats/PatCandidates"/></code> in <code>plugins/BuildFile.xml</code>. Compile the code with:

```shell
$ scram b
```

To run over the example file, change the input file name <code>file:myfile.root</code> in <code>python/ConfFile_cfg.py</code> to <code>root://eospublic.cern.ch//eos/opendata/cms/Run2015D/DoubleEG/MINIAOD/08Jun2016-v1/10000/00387F48-342F-E611-AB5D-0CC47A4D76AC.root</code>. Change the number of events from <code>-1</code> (runs over all events in the file) to <code>10</code> for testing. You can run this "empty" analyzer to see that the data are accessed properly:

```shell
$ cmsRun python/ConfFile_cfg.py
09-Dec-2021 12:00:35 CET  Initiating request to open file root://eospublic.cern.ch//eos/opendata/cms/Run2015D/DoubleEG/MINIAOD/08Jun2016-v1/10000/00387F48-342F-E611-AB5D-0CC47A4D76AC.root
211209 12:00:35 722 secgsi_InitProxy: cannot access private key file: /home/cmsusr/.globus/userkey.pem
%MSG-w XrdAdaptor:  file_open 09-Dec-2021 12:00:37 CET pre-events
Data is served from cern.ch instead of original site eospublic
%MSG
09-Dec-2021 12:00:38 CET  Successfully opened file root://eospublic.cern.ch//eos/opendata/cms/Run2015D/DoubleEG/MINIAOD/08Jun2016-v1/10000/00387F48-342F-E611-AB5D-0CC47A4D76AC.root
Begin processing the 1st record. Run 258434, Event 269235992, LumiSection 165 at 09-Dec-2021 12:01:10.140 CET
Begin processing the 2nd record. Run 258434, Event 269040066, LumiSection 165 at 09-Dec-2021 12:01:10.141 CET
Begin processing the 3rd record. Run 258434, Event 269567329, LumiSection 165 at 09-Dec-2021 12:01:10.142 CET
Begin processing the 4th record. Run 258434, Event 268674092, LumiSection 165 at 09-Dec-2021 12:01:10.143 CET
Begin processing the 5th record. Run 258434, Event 269416541, LumiSection 165 at 09-Dec-2021 12:01:10.143 CET
Begin processing the 6th record. Run 258434, Event 269251857, LumiSection 165 at 09-Dec-2021 12:01:10.143 CET
Begin processing the 7th record. Run 258434, Event 268739237, LumiSection 165 at 09-Dec-2021 12:01:10.144 CET
Begin processing the 8th record. Run 258434, Event 269456225, LumiSection 165 at 09-Dec-2021 12:01:10.144 CET
Begin processing the 9th record. Run 258434, Event 269845067, LumiSection 165 at 09-Dec-2021 12:01:10.144 CET
Begin processing the 10th record. Run 258434, Event 268437313, LumiSection 165 at 09-Dec-2021 12:01:10.145 CET
09-Dec-2021 12:01:10 CET  Closed file root://eospublic.cern.ch//eos/opendata/cms/Run2015D/DoubleEG/MINIAOD/08Jun2016-v1/10000/00387F48-342F-E611-AB5D-0CC47A4D76AC.root

=============================================

MessageLogger Summary

 type     category        sev    module        subroutine        count    total
 ---- -------------------- -- ---------------- ----------------  -----    -----
    1 XrdAdaptor           -w file_open                              1        1
    2 fileAction           -s file_close                             1        1
    3 fileAction           -s file_open                              2        2

 type    category    Examples: run/evt        run/evt          run/evt
 ---- -------------------- ---------------- ---------------- ----------------
    1 XrdAdaptor           pre-events
    2 fileAction           PostEndRun
    3 fileAction           pre-events       pre-events

Severity    # Occurrences   Total Occurrences
--------    -------------   -----------------
Warning                 1                   1
System                  3                   3
```

To access the physics object information in the code, for example that of electrons, add the following lines in <code>plugins/MiniAnalyzer.cc</code> (the lines before and after of the line to be added are also shown):

```shell
[...]
#include "FWCore/ParameterSet/interface/ParameterSet.h"
#include "DataFormats/PatCandidates/interface/Electron.h" // add this line
//
[...]
      // ----------member data ---------------------------
      edm::EDGetTokenT<pat::ElectronCollection> electronToken_; // add this line
};
[...]
MiniAnalyzer::MiniAnalyzer(const edm::ParameterSet& iConfig): // add the colon to the end of this line
    electronToken_(consumes<pat::ElectronCollection>(iConfig.getParameter<edm::InputTag>("electrons"))) // add this line
{
[...]
using namespace edm;
   edm::Handle<pat::ElectronCollection> electrons; // add from this line
    iEvent.getByToken(electronToken_, electrons);
    for (const pat::Electron &el : *electrons) {
        if (el.pt() < 5) continue;
        printf("electron with pt %4.1f, eta %+5.3f, cluster eta %+5.3f, pass conversion veto %d\n",
                    el.pt(), el.eta(), el.superCluster()->eta(), el.passConversionVeto());
    }                                              // to this line

#ifdef THIS_IS_AN_EVENT_EXAMPLE
[...]
```

Replace the <code>process.demo</code> definition in <code>python/ConfFile_cfg.py</code> with the following:

```shell
process.demo = cms.EDAnalyzer("MiniAnalyzer",
    electrons = cms.InputTag("slimmedElectrons")
)
```
Compile and run again with:

```shell
$ scram b
$ cmsRun python/ConfFile_cfg.py
```

and the output gives information on the electrons in these events:

```shell
Begin processing the 1st record. Run 258434, Event 269235992, LumiSection 165 at 09-Dec-2021 12:11:17.653 CET
electron with pt 94.4, eta -1.959, cluster eta -1.969, pass conversion veto 1
Begin processing the 2nd record. Run 258434, Event 269040066, LumiSection 165 at 09-Dec-2021 12:11:17.748 CET
electron with pt 19.3, eta -0.215, cluster eta -0.236, pass conversion veto 1
electron with pt 18.1, eta -2.271, cluster eta -2.296, pass conversion veto 1
Begin processing the 3rd record. Run 258434, Event 269567329, LumiSection 165 at 09-Dec-2021 12:11:17.749 CET
electron with pt 47.2, eta +0.530, cluster eta +0.548, pass conversion veto 1
electron with pt 42.6, eta +0.362, cluster eta +0.377, pass conversion veto 1
Begin processing the 4th record. Run 258434, Event 268674092, LumiSection 165 at 09-Dec-2021 12:11:17.750 CET
electron with pt 23.3, eta +2.008, cluster eta +2.045, pass conversion veto 0
Begin processing the 5th record. Run 258434, Event 269416541, LumiSection 165 at 09-Dec-2021 12:11:17.751 CET
electron with pt 17.7, eta +2.101, cluster eta +2.081, pass conversion veto 1
Begin processing the 6th record. Run 258434, Event 269251857, LumiSection 165 at 09-Dec-2021 12:11:17.751 CET
Begin processing the 7th record. Run 258434, Event 268739237, LumiSection 165 at 09-Dec-2021 12:11:17.751 CET
Begin processing the 8th record. Run 258434, Event 269456225, LumiSection 165 at 09-Dec-2021 12:11:17.752 CET
electron with pt 23.2, eta +0.491, cluster eta +0.483, pass conversion veto 1
Begin processing the 9th record. Run 258434, Event 269845067, LumiSection 165 at 09-Dec-2021 12:11:17.752 CET
electron with pt 23.0, eta -2.378, cluster eta -2.395, pass conversion veto 1
Begin processing the 10th record. Run 258434, Event 268437313, LumiSection 165 at 09-Dec-2021 12:11:17.752 CET
```

<br>
</details>


<details>
<summary> 2016 </summary>
<p>
The primary data provided by CMS on the CERN Open Data Portal is in a format called <a href="/docs/cms-physics-objects-2016">Analysis Object Data</a> or AOD for short, and from 2016 onwards, in a slimmer format called MINIAOD. These AOD files are prepared by piecing raw data collected by various sub-detectors of CMS and contain all the information that is needed for analysis. The files cannot be opened and understood as simple data tables but require specific sofware in order to be read.
</p>
<p>
So, let's see what a MINIAOD file looks like.
</p>
<p>
Make sure that you are in the <b>CMSSW_10_6_30/src/</b> folder, and, in VM, you have executed the <code>cmsenv</code> command in your terminal to launch the CMS analysis environment.
</p>
<p>
You can select a file from a dataset (a listing is available for each dataset record) and print out it contents with:
</p>
(Now using the 2015 data as a place holder. Will update it to 2016 data, once they are released.)

```shell
$ edmDumpEventContent root://eospublic.cern.ch//eos/opendata/cms/Run2015D/DoubleEG/MINIAOD/08Jun2016-v1/10000/00387F48-342F-E611-AB5D-0CC47A4D76AC.root
```

The ouput is a list of different objects that the file contains, such as

```shell
Type                                  Module                      Label             Process
----------------------------------------------------------------------------------------------
edm::TriggerResults                   "TriggerResults"            ""                "HLT"
[...]
vector<pat::Electron>                 "slimmedElectrons"          ""                "RECO"
[...]
```

Documentation of these objects is available in <a href="https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookMiniAOD2016#High_level_physics_objects">the CMS WorkBook 2016 MiniAOD page</a>. The objects are implemented as C++ classes in the CMS software package CMSSW, and detailed reference documentation of all classes is available in <a href="https://cmsdoxygen.web.cern.ch/cmsdoxygen/CMSSW_10_6_30/doc/html/annotated.html">the class list of the CMSSW reference manual</a>. To see the properties of electrons, you would navigate to "pat" and find the entry for "Electron". The <a href="https://cmsdoxygen.web.cern.ch/cmsdoxygen/CMSSW_10_6_30/doc/html/d2/d1f/classpat_1_1Electron.html">pat::Electron Class Reference</a> lists all member functions through which the different properties of reconstructed electron can be accessed. Note that many of the basic propertied are "inherited" from the parent classes, and are listed separately under "Public Member Functions inherited from ... ".

These objects can be accessed in a software module which can be built with a helper script available in the CMS open data environment. If you are using the VM, this helper scripts does not work out of the box, so skip this part and go directly to <a href="#nice">the next section</a>. If you are using the CMS open data container, you can do the following:

```shell
$ mkdir Test
$ cd Test
$ mkedanlzr MiniAnalyzer
$ cd MiniAnalyzer
```

This will create several template files in the new MiniAnalyzer directory. For more information, have a look in <a href="https://cms-opendata-guide.web.cern.ch/cmssw/cmsswanalyzers/">the CMS open data guide</a>.

To access the physics object properties, add <code><use name="DataFormats/PatCandidates"/></code> in <code>plugins/BuildFile.xml</code>. Compile the code with:

```shell
$ scram b
```

To run over the example file, change the input file name <code>file:myfile.root</code> in <code>python/ConfFile_cfg.py</code> to <code>root://eospublic.cern.ch//eos/opendata/cms/Run2015D/DoubleEG/MINIAOD/08Jun2016-v1/10000/00387F48-342F-E611-AB5D-0CC47A4D76AC.root</code> (UPDATE FILE PATH). Change the number of events from <code>-1</code> (runs over all events in the file) to <code>10</code> for testing. You can run this "empty" analyzer to see that the data are accessed properly:

(PASTE NEW OUTPUTS)
```shell
$ cmsRun python/ConfFile_cfg.py
09-Dec-2021 12:00:35 CET  Initiating request to open file root://eospublic.cern.ch//eos/opendata/cms/Run2015D/DoubleEG/MINIAOD/08Jun2016-v1/10000/00387F48-342F-E611-AB5D-0CC47A4D76AC.root
211209 12:00:35 722 secgsi_InitProxy: cannot access private key file: /home/cmsusr/.globus/userkey.pem
%MSG-w XrdAdaptor:  file_open 09-Dec-2021 12:00:37 CET pre-events
Data is served from cern.ch instead of original site eospublic
%MSG
09-Dec-2021 12:00:38 CET  Successfully opened file root://eospublic.cern.ch//eos/opendata/cms/Run2015D/DoubleEG/MINIAOD/08Jun2016-v1/10000/00387F48-342F-E611-AB5D-0CC47A4D76AC.root
Begin processing the 1st record. Run 258434, Event 269235992, LumiSection 165 at 09-Dec-2021 12:01:10.140 CET
Begin processing the 2nd record. Run 258434, Event 269040066, LumiSection 165 at 09-Dec-2021 12:01:10.141 CET
Begin processing the 3rd record. Run 258434, Event 269567329, LumiSection 165 at 09-Dec-2021 12:01:10.142 CET
Begin processing the 4th record. Run 258434, Event 268674092, LumiSection 165 at 09-Dec-2021 12:01:10.143 CET
Begin processing the 5th record. Run 258434, Event 269416541, LumiSection 165 at 09-Dec-2021 12:01:10.143 CET
Begin processing the 6th record. Run 258434, Event 269251857, LumiSection 165 at 09-Dec-2021 12:01:10.143 CET
Begin processing the 7th record. Run 258434, Event 268739237, LumiSection 165 at 09-Dec-2021 12:01:10.144 CET
Begin processing the 8th record. Run 258434, Event 269456225, LumiSection 165 at 09-Dec-2021 12:01:10.144 CET
Begin processing the 9th record. Run 258434, Event 269845067, LumiSection 165 at 09-Dec-2021 12:01:10.144 CET
Begin processing the 10th record. Run 258434, Event 268437313, LumiSection 165 at 09-Dec-2021 12:01:10.145 CET
09-Dec-2021 12:01:10 CET  Closed file root://eospublic.cern.ch//eos/opendata/cms/Run2015D/DoubleEG/MINIAOD/08Jun2016-v1/10000/00387F48-342F-E611-AB5D-0CC47A4D76AC.root

=============================================

MessageLogger Summary

 type     category        sev    module        subroutine        count    total
 ---- -------------------- -- ---------------- ----------------  -----    -----
    1 XrdAdaptor           -w file_open                              1        1
    2 fileAction           -s file_close                             1        1
    3 fileAction           -s file_open                              2        2

 type    category    Examples: run/evt        run/evt          run/evt
 ---- -------------------- ---------------- ---------------- ----------------
    1 XrdAdaptor           pre-events
    2 fileAction           PostEndRun
    3 fileAction           pre-events       pre-events

Severity    # Occurrences   Total Occurrences
--------    -------------   -----------------
Warning                 1                   1
System                  3                   3
```

To access the physics object information in the code, for example that of electrons, add the following lines in <code>plugins/MiniAnalyzer.cc</code> (the lines before and after of the line to be added are also shown):

```shell
[...]
#include "FWCore/ParameterSet/interface/ParameterSet.h"
#include "DataFormats/PatCandidates/interface/Electron.h" // add this line
//
[...]
      // ----------member data ---------------------------
      edm::EDGetTokenT<pat::ElectronCollection> electronToken_; // add this line
};
[...]
MiniAnalyzer::MiniAnalyzer(const edm::ParameterSet& iConfig): // add the colon to the end of this line
    electronToken_(consumes<pat::ElectronCollection>(iConfig.getParameter<edm::InputTag>("electrons"))) // add this line
{
[...]
using namespace edm;
   edm::Handle<pat::ElectronCollection> electrons; // add from this line
    iEvent.getByToken(electronToken_, electrons);
    for (const pat::Electron &el : *electrons) {
        if (el.pt() < 5) continue;
        printf("electron with pt %4.1f, eta %+5.3f, cluster eta %+5.3f, pass conversion veto %d\n",
                    el.pt(), el.eta(), el.superCluster()->eta(), el.passConversionVeto());
    }                                              // to this line

#ifdef THIS_IS_AN_EVENT_EXAMPLE
[...]
```

Replace the <code>process.demo</code> definition in <code>python/ConfFile_cfg.py</code> with the following:

```shell
process.demo = cms.EDAnalyzer("MiniAnalyzer",
    electrons = cms.InputTag("slimmedElectrons")
)
```
Compile and run again with:

```shell
$ scram b
$ cmsRun python/ConfFile_cfg.py
```

and the output gives information on the electrons in these events:

(PASTE NEW OUTPUTS)

```shell
Begin processing the 1st record. Run 258434, Event 269235992, LumiSection 165 at 09-Dec-2021 12:11:17.653 CET
electron with pt 94.4, eta -1.959, cluster eta -1.969, pass conversion veto 1
Begin processing the 2nd record. Run 258434, Event 269040066, LumiSection 165 at 09-Dec-2021 12:11:17.748 CET
electron with pt 19.3, eta -0.215, cluster eta -0.236, pass conversion veto 1
electron with pt 18.1, eta -2.271, cluster eta -2.296, pass conversion veto 1
Begin processing the 3rd record. Run 258434, Event 269567329, LumiSection 165 at 09-Dec-2021 12:11:17.749 CET
electron with pt 47.2, eta +0.530, cluster eta +0.548, pass conversion veto 1
electron with pt 42.6, eta +0.362, cluster eta +0.377, pass conversion veto 1
Begin processing the 4th record. Run 258434, Event 268674092, LumiSection 165 at 09-Dec-2021 12:11:17.750 CET
electron with pt 23.3, eta +2.008, cluster eta +2.045, pass conversion veto 0
Begin processing the 5th record. Run 258434, Event 269416541, LumiSection 165 at 09-Dec-2021 12:11:17.751 CET
electron with pt 17.7, eta +2.101, cluster eta +2.081, pass conversion veto 1
Begin processing the 6th record. Run 258434, Event 269251857, LumiSection 165 at 09-Dec-2021 12:11:17.751 CET
Begin processing the 7th record. Run 258434, Event 268739237, LumiSection 165 at 09-Dec-2021 12:11:17.751 CET
Begin processing the 8th record. Run 258434, Event 269456225, LumiSection 165 at 09-Dec-2021 12:11:17.752 CET
electron with pt 23.2, eta +0.491, cluster eta +0.483, pass conversion veto 1
Begin processing the 9th record. Run 258434, Event 269845067, LumiSection 165 at 09-Dec-2021 12:11:17.752 CET
electron with pt 23.0, eta -2.378, cluster eta -2.395, pass conversion veto 1
Begin processing the 10th record. Run 258434, Event 268437313, LumiSection 165 at 09-Dec-2021 12:11:17.752 CET
```

<br>
</details>


## <a name="nice">"Nice! But how do I analyse these data?"</a>

<details>
<summary> 2015 </summary>
<p>
We start off with a quick introduction to <b><a href="http://root.cern.ch">ROOT</a></b>. ROOT is the framework used by several particle-physics experiments to work with the collected data. For a quick start on how to write the most common objects and their properties in a root file, use "Physics Object Extractor Tool (POET)" available in <a href="https://github.com/cms-opendata-analyses/PhysObjectExtractorTool/tree/2015MiniAOD">this repository</a>. You can use ROOT to inspect reconstructed particles and the distributions of their properties.
</p>
<p>
Start by getting the code and compiling it. Make sure that you are back in the the <b>CMSSW_7_6_7/src/</b> folder. If you are using the VM, do the next two commands in the "Outer shell" terminal. In the container, keep using the normal container shell.
</p>

 ```shell
$ cd ~/CMSSW_7_6_7/src
$ git clone https://github.com/cms-opendata-analyses/PhysObjectExtractorTool.git
```

If you are using the VM, change now back to the "CMS shell" terminal. Get the 2015 MiniAOD "branch" of the repository and compile the code with:

```
$ cd ~/CMSSW_7_6_7/src
$ cd PhysObjectExtractorTool
$ git checkout 2015MiniAOD
$ scram b
```

Then produce a root file with selected objects by executing:

```shell
$ cd PhysObjectExtractor
$ cmsRun python/poet_cfg.py
```

The configuration file sets it to run over 1000 events in a simulated dataset.

If you are using the CMS open data container with the VNC application installed (see the <a href="/docs/cms-guide-docker">container guide page</a>), open the graphical user interface in the container by typing

```shell
$ start_vnc
```

and then start the graphics window on your browser with the link provided and using the password <code>cms.cern</code>.

You can now open the POET output file in ROOT:

```shell
$ root myoutput.root
```

You will see the ROOT logo appear on screen. You can now open the ROOT GUI by entering:

```shell
TBrowser t
```

and you will see the ROOT browser window:<br>

<img src="/static/docs/cms-getting-started-miniaod-2015-2016/getting_started_with_cms_2015_data_1.png" width="70%"><br>
<p>
Now, let us take a closer look at some collections of physics objects.
</p>
<p>
On the left window of ROOT, double-click on the file name (<code>myoutput.root</code>). You should see a list of names, each corresponding to a collection of reconstructed data.
</p>
Let us take a peek, for example, at the electrons, which are found in <code>myelectrons</code>. Look in there by double-clicking on that line and then double-clicking on <code>Events</code>. Here, you can have a look at various properties of this collection, such as the transverse momentum of the electrons: <code>electron_pt</code>. Double-click on it to draw the distribution.<br>

<img src="/static/docs/cms-getting-started-miniaod-2015-2016/getting_started_with_cms_2015_data_2.png" width="70%"><br>

<p>
You can exit the ROOT browser through the GUI by clicking on <code>Browser</code> on the menu and then clicking on <code>Quit Root</code> or by entering <code>.q</code> in the terminal.
</p>
<p>
<b>NOTE</b>: To analyse the full event content, the analysis job may need access to the "condition data", such as event selection information. You can see how connections to the condition database are established in <a href="/docs/cms-guide-for-condition-database">the guide to the CMS condition database</a> and in <a href="https://cms-opendata-guide.web.cern.ch/">the CMS Open data guide</a>. For simpler analyses, in which only physics objects needing no further data are used, you do not need to connect to the condition database.
</p>
Note also that in your analysis of collision data, you would need to filter only the validated events by downloading <a href="/record/14210">the validated data definition file</a> and adding these lines the job configuration:

```python
import FWCore.ParameterSet.Config as cms
import FWCore.PythonUtilities.LumiList as LumiList
myLumis = LumiList.LumiList(filename='Cert_13TeV_16Dec2015ReReco_Collisions15_25ns_JSON_v2.txt').getCMSSWString().split(',')
```

Add the following statements after the <code>process.source</code> input file definition:

```python
process.source.lumisToProcess = cms.untracked.VLuminosityBlockRange()
process.source.lumisToProcess.extend(myLumis)
```
<p>
This selection must always be applied to any analysis on CMS open data, and to do so you must have the validation file downloaded to your local area.
</p>
<p>
That's it! Hope you enjoyed this exercise. Feel free to play around with the rest of the data and write your own analyzers and analysis code. Learn more in <a href="https://cms-opendata-guide.web.cern.ch/">the CMS Open data guide</a>.
</p>

<br>
</details>

<details>
<summary> 2016 </summary>
<p>
POET is not available for the 2016 MiniAOD data. It is more recommended to work with the NanoAOD format of the 2016 data, which is going to be released soon. NanoAOD data is derived from MiniAOD. Instead of holding C++ classes, it holds tuples that can be directly read or analyzed using ROOT or other ROOT-compatible software. If you would like to analyze the 2016 data in the MiniAOD format, you may refer to the section on EDAnalyzer. You may use it to filter validated runs and apply selection cuts. POET is just a collection of these EDAnalyzers.
</p>
<br>

