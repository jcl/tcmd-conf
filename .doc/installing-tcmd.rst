============================
 Installing Total Commander
============================


These are my notes on how I install `Total Commander`_ x64 in a reproducable,
and mostly automated (aka. `unattended`), fashon.

.. _`Total Commander`: https://www.ghisler.com/

.. contents::


Procedure: Install Total Commander
==================================

The following steps reproduce a GUI driven install as described in
`Appendix: The Total Commander GUI install process reproduced`_.

#. Start new cmd.exe shell with `Administrators` privileges *and* _elevated_:

   Execute in non-Administrator cmd.exe shell OR WSL 1 shell::

       powershell.exe -Command "Start-Process cmd.exe -Verb Runas"

   A `User Account Control` window is shown:
   `Do you want to allow this app to make changes to your device?`.
   In the `User name` field, enter the username of a user account that is a
   member of the local ``Administrators`` group (remember to include the
   ``.\`` prefix for local user accounts), enter password, and click `Yes`.

   This will spawn a cmd.exe shell running with Administrators privileges
   (with `Administrator:` prefix in window title) in a new window.

#. Execute installer, and do some housekeeping afterwards:

   In the spawned `Administrator:` cmd.exe shell, execute::

       ::  all this specific path to the tcmd installer .exe stuff can just
       ::  be ignored; it is specific to my environment and just added here to
       ::  make my life easier.

       set fslib_root=C:\Users\username\fs\libmirror

       ::  this command returns before completing,
       ::  so wait 7 seconds before proceeding.
       %fslib_root%\dl-tcmd\tcmd-10.52\root\tcmd1052x64.exe /A1H1L1M0G1D0U1FN"*"

       ::  don't want to leave these per-user defaults around for the user
       ::  account executing the install (if needed, follow the README.rst for
       ::  this account as well)
       rmdir /s /q "%APPDATA%\GHISLER"
       reg.exe delete "HKCU\SOFTWARE\Ghisler" /f

   Learned the installer command line parameters from
   https://www.ghisler.ch/wiki/index.php?title=Installer .


Procedure: Uninstall Total Commander and purge configuration etc. left behind
=============================================================================

#. Start new cmd.exe shell with `Administrators` privileges *and* _elevated_:

   Execute in non-Administrator cmd.exe shell OR WSL 1 shell::

       powershell.exe -Command "Start-Process cmd.exe -Verb Runas"

   A `User Account Control` window is shown:
   `Do you want to allow this app to make changes to your device?`.
   In the `User name` field, enter the username of a user account that is a
   member of the local ``Administrators`` group (remember to include the
   ``.\`` prefix for local user accounts), enter password, and click `Yes`.

   This will spawn a cmd.exe shell running with Administrators privileges
   (with `Administrator:` prefix in window title) in a new window.

#. Execute Total Commander uninstaller:

   In the spawned `Administrator:` cmd.exe shell, execute::

       ::  This .EXE is the target of the .lnk shortcut
       ::      "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Total Commander\Uninstall or Repair Total Commander.lnk"
       ::  (what the shortcut executes):
       ::      "C:\Program Files\totalcmd\TCUNIN64.EXE"
       ::  Executing it with argument for "silent uninstall"
       ::  (learned from https://www.ghisler.ch/board/viewtopic.php?t=8169 ):
       "C:\Program Files\totalcmd\TCUNIN64.EXE" /7

#. Purge configuration etc. left behind:

   In the spawned `Administrator:` cmd.exe shell, execute::

       reg.exe delete "HKLM\SOFTWARE\Ghisler" /f

       ::  the Total Commander installer is adding this for the user account
       ::  that executes the installer:
       ::      %APPDATA%\GHISLER\
       ::      %APPDATA%\GHISLER\wincmd.ini
       rmdir /s /q "%APPDATA%\GHISLER"

       reg.exe delete "HKCU\SOFTWARE\Ghisler" /f

.. admonition:: Purging per-user configuration for other user accounts:

   Consider also purging the Total Commander configuration left heind for each
   user account outside of the installer user account.  This essentially boils
   down to executing this as each user account (in a cmd.exe shell)::

       rmdir /s /q "%APPDATA%\GHISLER"
       rmdir /s /q "%APPDATA%\tcmd"
       reg.exe delete "HKCU\SOFTWARE\Ghisler" /f


Appendix: The Total Commander GUI install process reproduced
============================================================

#. Start new cmd.exe shell with `Administrators` privileges *and* _elevated_:

   Execute in non-Administrator cmd.exe shell OR WSL 1 shell::

       powershell.exe -Command "Start-Process cmd.exe -Verb Runas"

   A `User Account Control` window is shown:
   `Do you want to allow this app to make changes to your device?`.
   In the `User name` field, enter the username of a user account that is a
   member of the local ``Administrators`` group (remember to include the
   ``.\`` prefix for local user accounts), enter password, and click `Yes`.

   This will spawn a cmd.exe shell running with Administrators privileges
   (with `Administrator:` prefix in window title) in a new window.

#. Execute Total Commander installer:

   In the spawned `Administrator:` cmd.exe shell, execute::

       set fslib_root=C:\Users\username\fs\libmirror

       %fslib_root%\dl-tcmd\tcmd-10.52\root\tcmd1052x64.exe

#. Follow the GUI installer dialogs, and respond according to the following::

       * Please select a language:                           English  [default]
       * Do you also want to install all other languages?    ( ) Yes  [default]
                                                             (*) No
       * Please enter target directory for installation:     C:\Program Files\totalcmd  [default]

       * Change ini file location:

             (*) Application data (user-specific application data)  [default]
             ( ) Documents and Settings (user-specific documents)
             ( ) User-defined directory

             [ ] Set this location for all users on this system  [default: unchecked]

       * Create shortcut icons (lnk files):

             [x] In the Windows Start menu  [default: checked]
             [ ] On the Desktop  [default: checked]

         Create for:

             ( ) This user: [drop-down with all usernames]  [default]
             (*) All users

Observations: the parts installed by above process:

    [file system] **System-wide**::

        $ dir /a /on /b /s "C:\Program Files\totalcmd" "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Total Commander"
        C:\Program Files\totalcmd\BLAKEX64.DLL
        C:\Program Files\totalcmd\CGLPT64.SYS
        C:\Program Files\totalcmd\DEFAULT.BAR
        C:\Program Files\totalcmd\DESCRIPT.ION
        C:\Program Files\totalcmd\FILTER64
        C:\Program Files\totalcmd\HISTORY.TXT
        C:\Program Files\totalcmd\KEYBOARD.TXT
        C:\Program Files\totalcmd\LANGUAGE
        C:\Program Files\totalcmd\NO.BAR
        C:\Program Files\totalcmd\NOCLOSE64.EXE
        C:\Program Files\totalcmd\SFXHEAD.SFX
        C:\Program Files\totalcmd\SIZE!.TXT
        C:\Program Files\totalcmd\TC7Z64.DLL
        C:\Program Files\totalcmd\TCLZMA64.DLL
        C:\Program Files\totalcmd\TCMADM64.EXE
        C:\Program Files\totalcmd\TCMDX32.EXE
        C:\Program Files\totalcmd\TCshareWin10x64.dll
        C:\Program Files\totalcmd\TCUNIN64.EXE
        C:\Program Files\totalcmd\TCUNIN64.WUL
        C:\Program Files\totalcmd\TCUNINST.WUL
        C:\Program Files\totalcmd\TCUNZL64.DLL
        C:\Program Files\totalcmd\TcUsbRun.exe
        C:\Program Files\totalcmd\TOTALCMD.CHM
        C:\Program Files\totalcmd\TOTALCMD.INC
        C:\Program Files\totalcmd\TOTALCMD64.EXE
        C:\Program Files\totalcmd\TOTALCMD64.EXE.MANIFEST
        C:\Program Files\totalcmd\UNRAR64.DLL
        C:\Program Files\totalcmd\VERTICAL.BAR
        C:\Program Files\totalcmd\WCMICON2.DLL
        C:\Program Files\totalcmd\WCMICONS.DLL
        C:\Program Files\totalcmd\WCMICONS.INC
        C:\Program Files\totalcmd\WCMZIP64.DLL
        C:\Program Files\totalcmd\WCUNINST.WUL
        C:\Program Files\totalcmd\FILTER64\AutoPitch.dll
        C:\Program Files\totalcmd\FILTER64\SoundTouchDLL_License.txt
        C:\Program Files\totalcmd\FILTER64\SoundTouchDLL_x64.dll
        C:\Program Files\totalcmd\FILTER64\vmr9rotator.dll
        C:\Program Files\totalcmd\LANGUAGE\WCMD_ENG.MNU
        C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Total Commander\Total Commander 64 bit.lnk
        C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Total Commander\Total Commander Help.lnk
        C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Total Commander\Uninstall or Repair Total Commander.lnk

    [registry] **System-wide**:

        No changes observed.

        .. Note::

           If this option in the `Change ini file location` dialog had been
           checked::

               [ ] Set this location for all users on this system  [default: unchecked]

           then these keys/values would have been added to the registry
           [REGEDIT4 .reg format]::

               [HKEY_LOCAL_MACHINE\SOFTWARE\Ghisler\Total Commander]
               "IniFileName"="%APPDATA%\\GHISLER\\wincmd.ini"
               "FtpIniName"="%APPDATA%\\GHISLER\\wcx_ftp.ini"
               "InstallDir"="C:\\Program Files\\totalcmd"

    [file system] User account executing installer::

        %APPDATA%\GHISLER
        %APPDATA%\GHISLER\wincmd.ini

    [file system] ... contents of ``%APPDATA%\GHISLER\wincmd.ini``::

        [Configuration]
        InstallDir=C:\Program Files\totalcmd

    [registry] User account executing installer [REGEDIT4 .reg format]::

        [HKEY_CURRENT_USER\SOFTWARE\Ghisler\Total Commander]
        "IniFileName"="%APPDATA%\\GHISLER\\wincmd.ini"
        "FtpIniName"="%APPDATA%\\GHISLER\\wcx_ftp.ini"
        "InstallDir"="C:\\Program Files\\totalcmd"
