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

    To analyse CMS data collected in 2011 and 2012, you need **version 5.3.32** of CMSSW, supported only on **Scientific Linux 6**. If you are unfamiliar with Linux, take a look at [this short introduction to Linux](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookBasicLinux) or [tutorial](https://swcarpentry.github.io/shell-novice/). Once you have installed the [CMS open data container](/docs/cms-guide-docker) or the [CMS-specific CERN Virtual Machine](/docs/cms-virtual-machine-2011), you need to open a terminal.

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
