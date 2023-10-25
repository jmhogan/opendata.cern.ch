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

Don't panic if you do not have any exeprience with ROOT. The following instructions will walk you through the steps of checking the content of AOD files with ROOT. 

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


