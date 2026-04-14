FAQs
====

If you encounter any issues using Osprey, we encourage you to check the
following frequently asked questions. If you are still having
difficulties, please reach out to us at
`MRSHub <https://forum.mrshub.org/c/mrs-software/osprey/>`__ or on
`GitHub <https://github.com/schorschinho/osprey/issues/>`__.

**Osprey crashes with "Unrecognized function or variable lgamma":**

   Make sure that you have added SPM12 to the MATLAB path **without** subfolders (see
   `Installation
   instructions <https://schorschinho.github.io/osprey/getting-started.html#installing-osprey>`__).

**Osprey crashes during the "Osprey" GUI call:**

   Make sure that you have downloaded and installed both external
   toolboxes from the MATLAB File Exchange (see `system
   requirements <https://schorschinho.github.io/osprey/getting-started.html#system-requirements>`__).

**Osprey crashes during the OspreyLoad call:**

   Check whether you have picked the right ``seqType`` in the job file. Are
   the path definitions in the struct right, e.g., files correspond to
   metabolite data? If the the problem persists after careful inspection
   of the job file you can reach out to us. It is quite possible that
   your specific sequence is not implemented into Osprey yet.

**Osprey crashes with "There is no appropriate basis set to model your
data…":**

   You have to provide a matching basis set for the LCM. You can visit
   our `MRSCloud tool <https://braingps.anatomyworks.org/home>`__ to
   generate a matching basis set yourself. Or, if a matching option is
   not available, you can reach out to us.

**Osprey crashes with "Unrecognized function or variable 'spm_vol'":**

   Make sure to add SPM12 to the MATLAB path (see `system
   requirements <https://schorschinho.github.io/osprey/getting-started.html#system-requirements>`__).
   You can also write a startup.m script with the following lines and
   add this to your MATLAB folder. This will automatically set the path
   right during the MATLAB startup.

::

   addpath(genpath('/Users/Documents/GitHub/osprey'));
   addpath('/Users/Documents/GitHub/spm12');

**Osprey crashes with "Unrecognized function or variable 'osp_platform'":**

   Make sure to add SPM12 to the MATLAB path (see `system
   requirements <https://schorschinho.github.io/osprey/getting-started.html#system-requirements>`__).
   You can also write a ``startup.m`` script with the following lines and
   add this to your MATLAB folder. This will automatically set the path
   right during the MATLAB startup:

::

   addpath(genpath('/Users/Documents/GitHub/osprey'));
   addpath('/Users/Documents/GitHub/spm12');

