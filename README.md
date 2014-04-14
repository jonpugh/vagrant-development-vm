# Zivtech

## About

This repository manages Zivtech's development virtual server. It has a number of
tools that Zivtech uses to help build Drupal sites. Drush is included as well as
Drush Fetcher which is a tool used to sync copies of Drupal sites between
environments. There are also other useful features such as a solr server for
Drupal search integration.

## Installation

You must have [Vagrant](http://vagrantup.com) and [VirtualBox](https://www.virtualbox.org/) installed first.

This repository has several git submodules that you will need before the
installation will complete. Run "git submodule update --init" from within this
directory to get the required sub-projects.

Once the repositories have been downloaded run "vagrant up" from within this
directory. This will build the virtual server and provision it. You can change
some settings such as the IP address of the server and the server's name in the
VagrantFile.

After the server has been built it is a good idea to update the packages. Log in
to the server over SSH. The username and password are both "vagrant". Run
"sudo apt-get update && sudo apt-get upgrade" to update the server's packages.
When this is completed back on the command line in this directory run
"vagrant provision" to finish the build.

You should now have a working Virtual Server.

The default server hostname is `local` and the default IP is `33.33.33.40`.

## Installation Instructions

<em>I am walking through and testing the instructions and am going to provide exact commands 
in an attempt to make this as simple as possible. -@jonpugh</em>

0. Install [Virtualbox](https://www.virtualbox.org/wiki/Downloads) and [Vagrant](http://www.vagrantup.com/downloads.html).

  0.1 Install NFS.

  This Vagrantfile uses NFS to mount your Host folder in the Guest. MacOSX comes with it built in.
  To install in ubuntu:

    ```sh
    you@host ~ $ sudo apt-get install nfs-kernel-server nfs-common portmap
    ```
    
1. Get this repo and all sub-repos. You can do this in one command using the `--recursive` option.

    ```sh
    you@host ~ $ git clone git@github.com:jonpugh/vagrant-development-vm.git --recursive
    ```

2. Change Directory and Vagrant Up

    ```sh
    you@host ~ $ cd vagrant-development-vm.git
    you@host ~ $ vagrant up
    ```

    The first time you do this it will download the [precise-vbox-4.2.18.2](http://fattony.zivtech.com/files/precise-vbox-4.2.18.2.box) 
    Vagrant box from Zivtech's Server. This may take a while depending on your bandwidth.
    
    Once that's done, it will provision the server according to the puppet modules. This will also take a long time.
    
3. Coming soon... 
  Vagrant still doesn't see nsfd so I'm rebooting to see if that fixes it.


## Issues

Vagrant tries to mount a shared NFS directory to the host machine (the physical
computer). This has been known to fail in some cases. If you receive errors
about a failed mount remove the virtual machine with "vagrant destroy" then
comment out the line that sets this up in the VagrantFile by placing a # at the
beginning of the line:

    #config.vm.share_folder("web", "/var/www", "www", :nfs => true)
