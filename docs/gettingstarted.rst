Getting started
===============

System requirements
-------------------

**Osprey** requires
`MATLAB <https://www.mathworks.com/products/matlab.html>`__ version 2019a and newer for full functionality.

.. warning::

   MATLAB has substantially re-built its GUI functions starting with version 2026a. 
   We have not yet tested Osprey with the new GUI functions. We have received reports of errors and warning occurring in these situations,
   and cannot currently guarantee that Osprey will work properly with MATLAB 2026a and later.


The following toolboxes are required for full functionality:

-  Optimization
-  Statistics and Machine Learning

.. note::

   You may need to ask your system administrator for a separate license
   for missing toolboxes.

You can check your current MATLAB version and the available toolboxes
with the following command at the MATLAB prompt:

::

   > ver

   -----------------------------------------------------------------------------------------------------
   MATLAB Version: 9.12.0.2170939 (R2022a) Update 6
   MATLAB License Number: 703789
   Operating System: Microsoft Windows 11 Enterprise Version 10.0 (Build 26100)
   Java Version: Java 1.8.0_202-b08 with Oracle Corporation Java HotSpot(TM) 64-Bit Server VM mixed mode
   -----------------------------------------------------------------------------------------------------
   MATLAB                                                Version 9.12        (R2022a)
   Curve Fitting Toolbox                                 Version 3.7         (R2022a)
   GUI Layout Toolbox                                    Version 2.3.6       (R2023a)
   Global Optimization Toolbox                           Version 4.7         (R2022a)
   Image Processing Toolbox                              Version 11.5        (R2022a)
   MATLAB Compiler                                       Version 8.4         (R2022a)
   MATLAB Compiler SDK                                   Version 7.0         (R2022a)
   Optimization Toolbox                                  Version 9.3         (R2022a)
   Parallel Computing Toolbox                            Version 7.6         (R2022a)
   Signal Processing Toolbox                             Version 9.0         (R2022a)
   Statistics and Machine Learning Toolbox               Version 12.3        (R2022a)
   Widgets Toolbox - Compatibility Support               Version 1.5.1       (R2023a)

.. note::

   The available toolboxes (including SPM) are checked at the initial
   call of the Osprey GUI, and missing toolboxes are reported back to
   the user.

Installing Osprey and necessary dependencies
--------------------------------------------

Osprey package
~~~~~~~~~~~~~~

Get the latest **Osprey** code from our `GitHub
repository <https://github.com/schorschinho/osprey>`__:

-  Clone the repository, or download and extract the contents of the
   .ZIP file to a directory on your drive.

.. figure:: img/02-installing-osprey-download-clone.png

   Cloning Osprey from GitHub.

-  Add the entire ``osprey`` directory (with subfolders) to your MATLAB
   path.

   -  Make sure to regularly check the repository for updates, as we
      frequently commit new features, bug fixes, and improved functions.

SPM package
~~~~~~~~~~~

To perform voxel co-registration and tissue segmentation, download
**SPM12** `from the University College London
website <http://www.fil.ion.ucl.ac.uk/spm/software/spm12/>`__. You will
need to provide the SPM team with some information before you can access
the download link.

.. note::

   If you run an Apple Silicon processor (M1 and later), please download
   the `SPM development version from
   GitHub <https://github.com/spm/spm>`__. The SPM12 package behind the
   official download link above likely does not contain pre-compiled C
   binaries for Silicon.

-  Extract the downloaded archive so that the ``spm12`` folder is on the
   same directory level as the ``osprey`` folder:

.. figure:: img/02-installing-osprey-spm-folder.png

   Make sure that the SPM12 and Osprey folders are in the same
   directory.

-  Add the ``spm12`` folder to your MATLAB path, but **without**
   subfolders.

.. warning::

   During testing, we have found that adding SPM subfolders to the
   MATLAB path can cause functions to fail. Add the top-level directory
   to your path, but not subfolders.

GUI Toolboxes
~~~~~~~~~~~~~

If you want to use the **Osprey** Graphical User Interface (GUI), please
download the following toolboxes from the MATLAB File Exchange:

-  `GUI Layout
   Toolbox <https://www.mathworks.com/matlabcentral/fileexchange/47982-gui-layout-toolbox>`__
   (David Sampson)

-  `Widget
   Toolbox <https://www.mathworks.com/matlabcentral/fileexchange/66235-widgets-toolbox>`__
   (Robin Jackey)

Download both toolboxes in the MATLAB toolbox format (.mltbx). You can
double-click to install. MATLAB will automatically add the toolboxes to
its path.

How to organize your raw data
-----------------------------

Raw MRS data come in an overwhelming variety of formats, each producing
different numbers of files. **Osprey** does not make a lot of
assumptions with regard to your folder structure, since you specify the
exact location for each file in a job file prior to each analysis. It is
**highly** recommended, however, that you store different acquisitions
in separate folders. Organizing your raw data in a consistent and
meaningful way will save you a lot of time and nerves.

To ensure optimal functioning of **Osprey**, we suggest adapting the
folder hierarchy `proposed by the BIDS (Brain Imaging Data Structure)
initiative <https://github.com/bids-standard/bids-starter-kit/wiki/The-BIDS-folder-hierarchy>`__:

   There are four main levels of the folder hierarchy, these are:

::

   project/
   └── subject
       └── session
           └── acquisition

..

   With the exception of the top-level ``project`` folder, all
   sub-folders have a specific structure to their name (described
   below). Here’s an example of how this hierarchy looks:

::

   myProject/
   └── sub-01
       └── ses-01
           └── anat

An example adaptation of this hierarchy for Philips MRS data could look
like this:

::

   myProject/
   ├── sub-01
   │   └── ses-01
   │       ├── anat
   │       │   └── sub-01_T1w.nii
   │       └── mrs
   │           ├── sub-01_mega-press_act
   │           │   ├── sub-01_mega-press_act.sdat
   │           │   └── sub-01_mega-press_act.spar
   │           ├── sub-01_mega-press_ref
   │           │   ├── sub-01_mega-press_ref.sdat
   │           │   └── sub-01_mega-press_ref.spar
   │           └── sub-01_press-water
   │               ├── sub-01_press-water_act.sdat
   │               └── sub-01_press-water_act.spar
   ├── sub-02
   │   └── ses-01
   │       ├── anat
   │       │   └── sub-02_T1w.nii
   │       └── mrs
   │           ├── sub-02_mega-press_act
   │           │   ├── sub-02_mega-press_act.sdat
   │           │   └── sub-02_mega-press_act.spar
   │           ├── sub-02_mega-press_ref
   │           │   ├── sub-02_mega-press_ref.sdat
   │           │   └── sub-02_mega-press_ref.spar
   │           └── sub-02_press-water
   │               ├── sub-02_press-water_act.sdat
   │               └── sub-02_press-water_act.spar
   ...
   ...

While adhering to the BIDS standard is strongly recommended, it is by no
means binding for most file formats. You can, for example, keep Siemens
TWIX files (``.dat``) all in the same folder, and **Osprey** will be
able to handle them, if you define their paths in the job file
accordingly.

.. warning::

   There is one exception: For data stored in single-average DICOM
   (``*.IMA``, ``*.DCM``) or single-average Siemens RDA format, it is
   **absolutely necessary** to keep every scan in a separate folder.


