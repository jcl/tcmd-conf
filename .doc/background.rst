============
 Background
============


Some observations
=================

* Registry key::

      HKEY_CURRENT_USER\SOFTWARE\Ghisler\Total Commander

  will take precedence over::

      HKEY_LOCAL_MACHINE\SOFTWARE\Ghisler\Total Commander

* The ``InstallDir`` value(s) does not seem to matter; can be deleted
  [REGEDIT4 .reg format]::

      [HKEY_LOCAL_MACHINE\SOFTWARE\Ghisler\Total Commander]
      "InstallDir"="C:\\Program Files\\totalcmd"

      [HKEY_CURRENT_USER\SOFTWARE\Ghisler\Total Commander]
      "InstallDir"="C:\\Program Files\\totalcmd"
