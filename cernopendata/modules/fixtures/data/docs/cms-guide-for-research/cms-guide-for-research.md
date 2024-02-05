If you are interested in step-by-step instructions to start working with CMS Open Data, please consult these pages:

* [Install Virtual Machine](https://opendata.cern.ch/search?q=&f=tags%3AVM&f=experiment%3ACMS&l=list&order=desc&p=1&s=10&sort=mostrecent) or [Use a container](/docs/cms-guide-docker)
* [Getting started with CMS AOD Data](/docs/cms-getting-started-aod), for data collected during Run 1 of the LHC.
* Getting started with CMS [MiniAOD Data](/docs/cms-getting-started-miniaod) or [NanoAOD Data](/docs/cms-getting-started-nanoaod), for data collected during Run 2 of the LHC.

This page offers hints, tips and guidance for conducting a research-oriented analysis using CMS Open Data. 

---

### Quick introduction

**I want to get a general introduction into HEP and CMS software and terminology, with a simplified event format.**

* Read the instructions related to [educational content](/docs/cms-guide-for-education) and follow the corresponding exercises.


**I want to learn about the terms under which I can access and use the CMS Open Data, and publish results obtained from them.**

* Go to ["Data preservation and open access policy"](/record/414) (if you are a CMS member, also see the internal document ["Rules for use of open access CMS data by individual members of CMS"](https://cms-docdb.cern.ch/cgi-bin/DocDB/ShowDocument?docid=12242)).


**I want to get inspiration for some potential physics topics.**

* See what others are doing with CMS Open Data! Papers citing DOI [10.7483/OPENDATA.CMS](https://inspirehep.net/literature?sort=mostrecent&size=25&page=1&q=references.reference.dois%3A10.7483%2FOPENDATA.CMS%2A) show a broad scope of usage for Open Data, including physics analyses, data science, and research tool development.
  

**I want to learn about the nature of the CMS physics objects and the corresponding variables and terminology.**

* Check out the ["CMS Open Data Guide"](https://cms-opendata-guide.web.cern.ch/) as well as the pages describing CMS Physics Objects for [2011-2012 data](/docs/cms-physics-objects-2011) and for [2015 data](/docs/cms-physics-objects-2015).


**I want to follow a set of detailed tutorials to learn how to analyze CMS Open Data.**

* Beginning in 2020, CMS has offered workshops targeting research use of Open Data. You can follow the lessons of previous workshops by [visiting this page](https://cms-opendata-guide.web.cern.ch/cmsOpenData/workshops/). 

---

### Deciding which datasets to explore

CMS has released data proton collision data from Run 1 and Run 2, as well as heavy ion collision data from Run 1.

High-energy proton collisions: 

| Collision type and year | Energy (TeV) | Corresponding simulation? | Getting Started page | CMSSW environment |
| ----------------------- | ------------ | ------------------------- | --------------- | ---------------- | 
| proton-proton 2010 | 7            | No                        | [AOD data](/docs/cms-getting-started-aod) | CMSSW_4_2_8 | 
| proton-proton 2011 | 7            | 2011 simulation           | [AOD data](/docs/cms-getting-started-aod) | CMSSW_5_3_32 | 
| proton-proton 2012 | 8            | 2012 simulation           | [AOD data](/docs/cms-getting-started-aod) | CMSSW_5_3_32 | 
| proton-proton 2015 | 13           | 2015 simulation           | [MiniAOD data](/docs/cms-getting-started-miniaod) | CMSSW_7_6_7 | 
| proton-proton 2016 | 13           | 2016 simulation           | [MiniAOD data](/docs/cms-getting-started-aod)<br>[NanoAOD data](/docs/cms-getting-started-nanoaod) | CMSSW_10_6_30<br>Not required | 

Heavy-ion program: 
| Collision type and year | Energy (TeV) | Corresponding simulation? | Getting Started page | CMSSW environment |
| ----------------------- | ------------ | ------------------------- | --------------- | ---------------- | 
| [lead-lead 2010](https://opendata.cern.ch/search?q=&f=experiment%3ACMS&f=collision_energy%3A2.76TeV&f=collision_type%3APbPb&f=type%3ADataset%2Bsubtype%3ACollision&f=year%3A2010&l=list&order=desc&p=1&s=10&sort=mostrecent) | 2.76 | [2010-2011 Pb-Pb simulation](https://opendata.cern.ch/search?q=&f=experiment%3ACMS&f=type%3ADataset%2Bsubtype%3ASimulated&f=year%3A2013&f=collision_type%3APbPb&l=list&order=desc&p=1&s=10&sort=mostrecent) | | CMSSW_3_9_2_patch5\* |
| [lead-lead 2011](https://opendata.cern.ch/search?q=&f=experiment%3ACMS&f=collision_energy%3A2.76TeV&f=collision_type%3APbPb&f=type%3ADataset%2Bsubtype%3ACollision&f=year%3A2011&l=list&order=desc&p=1&s=10&sort=mostrecent) | 2.76 | [2010-2011 Pb-Pb simulation](https://opendata.cern.ch/search?q=&f=experiment%3ACMS&f=type%3ADataset%2Bsubtype%3ASimulated&f=year%3A2013&f=collision_type%3APbPb&l=list&order=desc&p=1&s=10&sort=mostrecent) | | CMSSW_4_4_7\* |
| [proton-proton 2011](https://opendata.cern.ch/search?q=&f=experiment%3ACMS&f=type%3ADataset%2Bsubtype%3ACollision&f=year%3A2011&f=collision_energy%3A2.76TeV&f=collision_type%3App&l=list&order=desc&p=1&s=10&sort=mostrecent) | 2.76 | No | | CMSSW_4_4_7
| [proton-proton 2013](https://opendata.cern.ch/search?q=&f=experiment%3ACMS&f=type%3ADataset%2Bsubtype%3ACollision&f=collision_energy%3A2.76TeV&f=collision_type%3App&f=year%3A2013&l=list&order=desc&p=1&s=10&sort=mostrecent) | 2.76 | [2013 p-p simulation](https://opendata.cern.ch/search?q=&f=experiment%3ACMS&f=type%3ADataset%2Bsubtype%3ASimulated&f=year%3A2013&f=collision_type%3App&l=list&order=desc&p=1&s=10&sort=mostrecent) | [Heavy Ion data](/docs/cms-getting-started-hi-2013-2015) | CMSSW_5_3_20 |
| [proton-lead 2013](https://opendata.cern.ch/search?q=&f=experiment%3ACMS&f=type%3ADataset%2Bsubtype%3ACollision&f=collision_energy%3A5.02TeV&f=collision_type%3ApPb&l=list&order=desc&p=1&s=10&sort=mostrecent) | 5.02 | [2013 p-Pb simulation](https://opendata.cern.ch/search?q=&f=experiment%3ACMS&f=type%3ADataset%2Bsubtype%3ASimulated&f=year%3A2013&f=collision_type%3ApPb&l=list&order=desc&p=1&s=10&sort=mostrecent) | [Heavy Ion data](/docs/cms-getting-started-hi-2013-2015) | CMSSW_5_3_20 |
| [proton-proton 2015](https://opendata.cern.ch/search?q=&f=experiment%3ACMS&f=type%3ADataset%2Bsubtype%3ACollision&f=collision_type%3App&f=collision_energy%3A5.02TeV&l=list&order=desc&p=1&s=10&sort=mostrecent) | 5.02 | No  | [Heavy Ion data](/docs/cms-getting-started-hi-2013-2015) | CMSSW_7_5_8_patch3 |

\* The Pb-Pb simulation linked in these rows is analyzed using CMSSW_5_3_20. 

**I want to find out whether I should go for data from 2010 or 2011 (both are pp data at 7 TeV) or from 2012 (pp data at 8 TeV).**

* The 2010 data have been released first; have fewer, smaller datasets with better low-p<sub>T</sub> tracking, low trigger thresholds, low pile-up and more/simpler analysis/validation examples; but have no MC. If you do not need MC or maximal statistics, you might want to try 2010 data first.
* The 2011/2012 data have more statistics, more diverse datasets, many associated MC sets, and a slightly more advanced VM environment. If you are immediately interested in maximal statistics and/or MC acceptance corrections you should go for 2011/2012 data.
* Information on the respective luminosities and pile-up rates vs time can be found in [public CMS luminosity information](https://twiki.cern.ch/twiki/bin/view/CMSPublic/LumiPublicResults#Multi_year_Collisions_Plots).
* If you want to try both datasets, you will need to use [the appropriate VMs](/search?page=1&size=20&tags=VM&experiment=CMS).


**I want to install the CMS software environment needed for access to and analysis of CMS Research level data.**

* Install the appropriate virtual machine, [2010 VM](/record/250) for 2010 data, and [2011 VM](/record/252) for 2011/2012 data.
* As an alternative to a virtual machine you can try running the CMS software environment in a container by following [these instructions](/docs/cms-guide-docker).
* Go to ["Getting started with CMS 2010 open data"](/docs/cms-getting-started-2010) for 2010 or ["Getting started with CMS 2011 open data"](/docs/cms-getting-started-2011) for 2011/2012 data.

**Note**: The 2010 (SL5) virtual machine will only work on 2010 data with CMSSW 4-2-8 (and other SLC5-based CMSSW releases). The 2011 (SL6) virtual machine will only work on 2011/2012 data and MC with CMSSW 5-3-32 (and other SLC6-based CMSSW releases).


**I want to produce some example physics distributions.**

* Install the CMS software as in the previous item (for 2010 or 2011).
* Follow options A (inclusive di-muon spectrum analysis example directly from AOD) or B (two-/four-lepton analysis example with intermediate ntuples) in ["Getting started with CMS 2010 open data"](/docs/cms-getting-started-2010) or ["Getting started with CMS 2011 open data"](/docs/cms-getting-started-2011).

---

### Exploring the 2010 datasets

**I want to find out which 2010 datasets exist, and how to get a feel for their content.**

* Go to [2010 CMS primary datasets](/search?page=1&size=20&q=&type=Dataset&subtype=Collision&experiment=CMS&year=2010),
* choose a dataset, and read the comments.


**I also want to view some corresponding event displays.**

* Go to [2010 CMS derived datasets of event display ("ig") type](/search?page=1&size=20&q=&type=Dataset&subtype=Derived&experiment=CMS&year=2010&file_type=ig),
* choose `Event display file derived from`… + the name of the CMS primary dataset you want (ZeroBias is known to be essentially empty).

or, alternatively:

* Load the [CMS event display](/visualise/events/cms),
* choose `Open File` &rarr; `Open Files from Web` &rarr; `2010`, and
* choose your dataset.


**I want to find out which 2010 dataset and/or analysis/validation example is most useful for my purpose.**

* To learn how to do a muon analysis, follow "*I want to produce some example physics distributions*," (above) with either option A (recommended) or B, or try one of the relevant "*I want to run the examples used for validation of the 2010 datasets*," (further below).
- To learn how to do an electron analysis, follow "*I want to produce some first physics distributions*," (above) with option B, or try one of the relevant "*I want to run the examples used for validation of the 2010 datasets*," (below).
- To learn how to do a minimum-bias track analysis, try the MinimumBias example on "*I want to run the examples used for validation of the 2010 datasets*," (below).
- [More to come…]

---

### Exploring the 2011-2012 datasets

**I want to find out which 2011-2012 data and MC sets exist, and how to get a feel for their content.**

* For collision data, go to [2011 CMS primary datasets](/search?page=1&size=20&q=&subtype=Collision&experiment=CMS&year=2011) or [2012 CMS primary datasets](/search?page=1&size=20&q=&subtype=Collision&experiment=CMS&year=2012)
* For MC, go to [2011 CMS simulated datasets](/search?page=1&size=20&q=&subtype=Simulated&experiment=CMS&year=2011) or [2012 CMS simulated datasets](/search?page=1&size=20&q=&subtype=Simulated&experiment=CMS&year=2012)
* choose a dataset, read the comments, and read also about [simulated dataset names](/docs/cms-simulated-dataset-names).


**I also want to  to view some corresponding event displays.**

* These are available for data only for the time being.
* Go to CMS derived datasets of event display ("ig") type for the [2011 data](/search?page=1&size=20&q=&subtype=Derived&experiment=CMS&year=2011&file_type=ig) or the [2012 data](/search?page=1&size=20&q=&subtype=Derived&experiment=CMS&year=2012&file_type=ig) ,
* choose `Event display file derived from`… + the name of the CMS primary dataset you want (ZeroBias is known to be essentially empty).

or, alternatively:

* Load the [CMS event display](/visualise/events/cms),
* choose `Open File` &rarr; `Open Files from Web` &rarr; `2011` or `2012`, and
* choose your dataset.


**I want to find out which 2011 or 2012 dataset and/or analysis/validation example is most useful for my purpose.**

* Dedicated examples beyond those available in "Getting Started" can be found in [software](/search?page=1&size=20&type=Software&subtype=Analysis&experiment=CMS&year=2011&year=2011-2012), including Higgs-to-four-lepton analysis, jet tuple production and top cross-sections. Alternatively, start from a 2010 example and adjust to run on 2011 or 2012 data (see [the CMS troubleshooting guide](/docs/cms-guide-troubleshooting) for instructions).


* For more information on Monte Carlo, see below.

---

### Trigger information, condition data, luminosity

**I want to find out how to use the trigger and trigger prescale information in the dataset I am interested in.**

* Go to [the guide to CMS trigger system](/docs/cms-guide-trigger-system).


**I want to find out how to access the luminosity information for the dataset I am interested in and how to select "good data" only.**

* Check the [CMS luminosity information](/search?page=1&size=20&q=luminosity&type=Supplementaries&subtype=Luminosity), and
* check the [list of validated runs](/search?page=1&size=20&q=%22CMS%20list%20of%20validated%20runs%22).


**I want to find out whether I need condition data base information, and if so, how to access it.**

* Condition data are needed on examples using e.g. jet energy corrections and trigger configuration information, many of the simpler analysis/validation examples do not need any additional corrections from condition database.
* Using condition data slows down data access, so use them only if really needed. If so:
    * see the instructions in ["The Guide to the CMS condition database"](/docs/cms-guide-for-condition-database).


**I want to find the luminosity of my dataset, possibly constrained by using specific triggers.**

* Please check [CMS luminosity information](/search?page=1&size=20&q=luminosity&type=Supplementaries&subtype=Luminosity),
* decide on the triggers you want to use,
* find out the runs/lumi sections in which these triggers were active and whether they were prescaled,
* overlap with the available CMS Open Data samples (run range) and with the selection in the list of validated runs.
    * If not prescaled, sum up the luminosity for the surviving runs/lumi sections.
    * If prescaled, life is more complicated. Find the prescales as in [the trigger example code](/record/5004)

---

### Performing an analysis

**I want to find more CMS software and data format documentation from public sources.**

* This is strongly recommended for serious analysis, but is hard to navigate!
* Check the [CMS public Twiki](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WebHome) or the CMS Fermilab website or use your favourite web-search engine.


**I want to learn about the published jet-analysis papers by the MIT group.**

* See *Jet Substructure Studies with CMS Open Data*, A. Tripathee et al., Apr 19, 2017, MIT-CTP-4890, [arXiv:1704.05842](https://inspirehep.net/record/1593756),
* and *Exposing the QCD Splitting Function with CMS Open Data*, A. Larkoski et al., Apr 17, 2017, MIT-CTP-4891, [arXiv:1704.05066](https://inspirehep.net/record/1591972).


**I want to run the examples used for validation of the 2010 datasets within my setup…**

* … for the MinimumBias, Commissioning, Mu or MuMonitor datasets:
    * Go to [Validation software](/search?page=1&size=20&q=&subtype=Validation&type=Software&year=2010)
    * choose and execute the corresponding Validation code.
* … for the Multijet dataset (see also [here](http://hep.caltech.edu/cms/opendata/)):
    * choose and execute ["Razor filter and analyzer for SUSY searches"](/record/553).
* … for the Electron (or Mu) dataset:
    * choose and execute ["Software to preprocess the CMS 2010 Muon and Electron datasets for the two-lepton/four-lepton analysis example of CMS open data"](/record/200), then
    * choose ["Two-lepton/four-lepton analysis example of CMS 2010 open data"](/record/101) and compare PAT-tuples from the previous to those linked therein, or execute it on your new PAT tuples.
* … for the ZeroBias dataset:
    * Not useful, no validation needed.
* … for the Jet, MuOnia, BTau, Photon, JetMETTaumonitor, METFwd datasets:
    - Validation not yet available (partially in preparation).


**I want to backup my code, or import some external code.**

* You can use `scp` from and to your host from within the VM.

---

### Monte Carlo

**How do I interpret the MC set names?**

* Check [CMS Simulated Dataset Names](/docs/cms-simulated-dataset-names).


**I want to find the effective luminosity of my MC set.**

* Information will be added to the portal.
* Generically: divide MC cross-section (next item) times matching efficiency times filter efficiency by the number of events.

**I want to find the generator cross section of a particular MC set.**

* To be documented.
* On some MC sets, the following might work (reliability of information not guaranteed): open the ROOT file, create TBrowser and navigate to `Runs` &rarr; `GenRunInfoProduct_generator__SIM.` &rarr; `GenRunInfoProduct_generator__SIM.obj` &rarr; `InternalXSec` &rarr; `value_`.

---

### Further information / Contact us

**I want information that is not documented here and elsewhere on the [CERN Open Data portal](http://opendata.cern.ch/).**

* Kindly contact &lt;[opendata-support@cern.ch](mailto:opendata-support@cern.ch)&gt;

**I ran into a problem and need help!**

* Please check [our page related to known errors](/docs/cms-guide-troubleshooting).
