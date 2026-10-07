# LINUX PACKAGE MANAGEMENT

## What is a Package

  - Its an archive containing software files and metadata needed to install and managge a paricular software.
  - Commonly contains;

    ''''bash
 
      compiled binaries or executable code: actual program files
      configuration files: default settings of the software
      Metadata: info about the software 
      Installation script: instructions on how and where to install and place the file, and how to setup the permission and services.

    ''''
  - Common Package formats are:

    ''''bash
      LINUX - .deb (Debian/Ubuntu)
              .rpm (Fedora/RedHat)
              .pkg.tar.zst (Arch package files)

      PROGRAMMING Languages - .whl/.tar.gz (PythonPyPI)
                              npm (javascript/Node.js packages)

    ''''

## What is a Package Manager and what does it do

   - A package manager is an automated software tool used to automate installation, updating, configuring, and removal of software packages in a OS or in a development enviroment.
   - The key responsiblities of a package manager tool are:

     ''''bash
       1 Dependency Resolution;
         - Checks for required dependancies, automatically downloads, and installs them in correct order
       2 Repository Management;
         - Package manager tools usually connect directly to central, verified online servers,
         - This allows users to download and install software with simple commands than serching for installer files.
       3 Installation & Removal:
         - Unpacks the files places them in the appropriate system directories, runs the setup scripts, and neatly removes all associated filesduring uninstall.
       4 Updates & Upgrades:
         - It tracks the whole installed packages and its version.
         - it also checks the repos for newer versions and upgrade the software or the whole OS securely.
       5 System Consistency & Integrity Verification:
         - It maintains a local database for every installed files to prevent software conflicts, track files ownership, and verify digital signatures for non tampering.

    ''''

   - Common Package Manager Examples:

    ''''bash
 
         SCOPE                         PACKAGE-MANAGER                       COMMON-COMMANDS

      Ubuntu/Debian                         apt                           sudo apt install <package>
      Fedora/RHEL Linux                     dnf                           sudo dnf install <package>
         macOS                         Homebrew(brew)                     brew install <package>
        Python                              pip                           pip install <package>
     JavaScript/Node.js                     npm                           npm install <package>

    ''''


## APT Package-Manager

   - 'apt' uses package indexes containing metadata about packages available from configured repositories defined in '/etc/apt/source.list.d directory.
   - The Ubuntu repositores are usually defined in '/etc/apt/sources.list.d/ubuntu.sources' file.
   - Hence to doanload and refresh the package index with latest changes made in the repositories to access the up-to-date version of the packages,
   - running;

     ''''bash

             sudo apt update

     ''''

  - running;

    ''''bash

           sudo apt upgrade

    ''''

  - will use the downloaded information to upgrade the installed packages.

## Repositories, Package indexes, Dependacies

   ### Repositories. 
           - these are sources containing packages and metadata.
           - usually defined in '/etc/apt/source.list'(main repo list) and '/etc/apt/source.list.d/ (extra sources).

   ### Package Indexes.
           - This are the metadata files downloaded with 'apt update' which contains details of the program like version,dependancies,size, but not the actual program files.
           - Usually stored in '/var/lib/apt/lists/'.

   ### Dependancies.
           - These are the rules that specify what other packages are needed to be installed for the softwareto work.

  ### Installed package info.
           - database of installed packages which is located at '/var/lib/dpkg/'

## Package Operations

   ### packages installation,
       - running;

                 ''''bash

                      sudo apt install <packagename>

                 ''''

  ### package removal,
      - running;

                ''''bash

                     sudo apt remove <packagename>

                ''''

      - adding "--purge" option to "apt remove" will result to the removal of package configuration files. needs to be used with caution.
 
  ### package Upgrading,
      - running;

                ''''bash

                     sudo apt update
                     sudo apt upgrade

               ''''

     - this updates your system by updating the package index the upgrades.
     - this updates are usually available from the package repositories.

  ### cache management
      - running;

                ''''bash

                     sudo apt clean
                     sudo apt autoclean
                     sudo apt autoremove

               ''''

      - will clear the unused files and dependancies

## dpkg

  - a package manager used for debian-based systems,
  - can install, remove & build packages.
  - cannot automatically download and install packeages or their dependancies.


## Using dpkg to manage locally installed packages

  - to list the packages known to the dpkg database, including different packages state. (installed & un-installed),
  - you run;

           ''''bash

               dpkg -l

          ''''

   - depending on the number of packages on the system it can generate a large output.
   - piping the output with grep will help you see if a specific or required package is installed.
   - like running;

                 ''''bash

                     dpkg -l | grep <package>

                 ''''

   - to list the files installed by a package,
   - run;

         ''''bash

             dpkg -L <package>

        ''''

   - if you dont know which package has installed a file,
   - running;

            ''''bash

                dpkg -S /usr/bin/zip

            ''''

   - may tell you which package the file belongs to.

## Installing a '.deb' file

  - to install a .deb file in a system;
  - running;

           ''''bash

               sudo dpkg -i <.deb-file>

          ''''

   - will install the local file that you need to install.
   - running:

            ''''bash

                sudo dpkg -r zip

           ''''

   - will remove a package but does not automatically resolve dependancies.
   - uninstalling packages using 'dpkg' is not used in most casses, APT is preferable for normal package management.
   - it will remove the package but any installed packages that depended on it will sieze to function correctly.


## N.B

   - all the actions/logs of the 'apt' command like the installation and removal of packages are logged in,

              /var/log/dpkg.log 
