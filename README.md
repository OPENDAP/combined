
# The new Hyrax Project

## Under construction

The _combined_ project is similar to the _hyrax_ project in that it
contains all the code OPeNDAP has written that is currently in the
the production release of the Hyrax Data Server. However, unlike 'hyrax,'
this project uses git submodules and a single configure/Makefile to
build the code.

## What's here

This meta-project contains the libdap4, bes, hyrax-dependencies and olfs
repositories along with autotools builds scripts (configure, make, et c.)
to build them. You can work within one of the repos as if it was independently
cloned as well as build the whole server.

#### _OLFS_

This software implements the web API of the Data Access Protocol (DAP) and 
other web interfaces for Hyrax. Most of the 'web functionality' is here. Written 
in Java.

#### _libdap4_

The DAP2 and 4 implementations. C++

#### BES

A Unix Daemon that is the dat processing engine at the heart of the Hyrax server.
C++

#### _hyrax dependencies_

There is a GitHub project called _hyrax-dependencies_ that holds all of the
odd dependencies that hyrax needs - not the stuff you can get easily from _yum_.
The code included in hyrax-dependencies includes, new(er) versins of HDF5, 
netCDF, ..., as well as more unusual things like _gridfields_.

## Details

### Linux/OSX

You need a Linux/OSX/Unix computer that can compile C, C++ and Java.
Most of the requirements are fairly plain, with the exception that
you'll need a recent copy of bison and flex. Since CentOS/RedHat comes
with 'yum' and the yum command syntax is fairly concise, I'll use it
as shorthand for the packages you need (with the advantage that some
users can cut and paste in a plain machine and get the packages
installed very quickly):

    yum install java-1.7.0-openjdk java-1.7.0-openjdk-devel ant git \
        gcc-c++ flex bison autoconf automake libtool emacs openssl-devel \
        libuuid-devel readline-devel zlib-devel bzip2 bzip2-devel \
        libjpeg-devel libxml2-devel curl-devel libicu-devel

### Clone

Use a reccursive clone operation to get all the submodules that are
part of this repository:

    git clone --recursive --jos=9 https://github.com/opendap/combined

or, if you used a simple _git clone_ already

    git submodule update --init --recursive --jobs=9

### Configure the build environment

Set up the _prefix_ and _PATH_ environment variables in the shell
you're using. Use _source spath.sh_ to do this. This will set the
_prefix_ environment variable to `pwd`/build and add `pwd`/build/bin
to the front of PATH so that libdap, BES and the various
modules/handlers for the BES can find the dependencies once they are
built.

    source spath.sh

### Build it

    autoreconf --force --include --verbose
    configure --prefix=$prefix --with-dependencies=$prefix/deps --enable-developer \
   	     --with-libdap=`pwd`/libdap4
    make -j9
    make -j9 install

See the _TOMCAT_ section below if you want a running server (and not just the 
BES daemon.

### Comveniences

I have defined an alias _update_ that will pull and recursively update all the 
child repos. To use this, run _git update_ in this directory. The alias is defined
as:

    git config --global alias.update '!git pull && git submodule update --init --recursive

### Caveat Emptor

The BES repository has submodules of its own. Currently (Jan 2018) those are the HDF4 
and HDF5 handlers and the SQL handler. If you work with those, you must commit, push, et c., 
from within those directories. Then, make sure to update the BES too, so that the correct
commit hashes are recorded in the _.gitsubmodules_ file.

The repository URLs all use the HTTPS protocol. On older versions of git, you cannot
push commits and will need to switch the repos to use ssh.

### Tomcat

Get the Tomcat distribution from _hyrax-dependencies/extra_downloads_ and unpack it in
the _build_ directory. Use _make install_ in the _olfs_ or top level direcotry to 
install the _oepndap.war_ file (that implements the web interface for Hyrax.

For a real deployment of Hyrax, using the Tomcat from a RPM or DEB packages is better,
but for development, using a local Tomcat will simply testing.

### Test

TBD
