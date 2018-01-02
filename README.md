
# The new Hyrax Project

## Under construction

The _combined_ project is similar to teh _hyrax_ project in that it
contains all the code OPeNDAP has written that is currently in the
the production release of the Hyrax Data Server. However, unlike 'hyrax,'
this project uses git submodules and a single configure/Makefile to
build the code.

## Details

### Linux/OSX

You need a Linux/OSX/Unix computer that can compile C, C++ and Java.
Most of the requirements are fairly plain, with the exception that
you'll need a recent copy of bison and flex and newer versions of the
autotools software. Since CentOS/RedHat comes with 'yum' and the yum
command syntax is fairly concise, I'll use it as shorthand for the
packages you need (with the advantage that some users can cut and
paste in a plain machine and get the packages installed very quickly):

yum install java-1.7.0-openjdk java-1.7.0-openjdk-devel ant git \
 gcc-c++ flex bison openssl-devel libuuid-devel readline-devel \
 zlib-devel libjpeg-devel libxml2-devel curl-devel ant-junit

Then download and build the latest versions of autoconf, automake and
libtool. Those can be found at:

    http://ftp.gnu.org/gnu/autoconf/autoconf-2.69.tar.gz
    http://ftp.gnu.org/gnu/automake/automake-1.14.1.tar.gz
    http://ftp.gnu.org/gnu/libtool/libtool-2.4.2.tar.gz

and are very easy to build.

### Configure the build environment

Set up the 'prefix' and 'PATH' environment variables in the shell
you're using. Use 'source spath.sh' to do this. This will set the
'prefix' environment variable to `pwd`/build and add `pwd`/build/bin
to the front of PATH so that libdap, BES and the various
modules/handlers for the BES can find the dependencies once they are
built.

    source spath.sh

### Get the source code

   git submodule update --init
   
### Build it

   autoreconf
   configure --prefix=$prefix --with-dependencies=$prefix/deps --enable-developer
   make -j9

### Tomcat

TBD

### Test

TBD