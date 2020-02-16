
AUTOMAKE_OPTIONS = foreign

SUBDIRS = . hyrax-dependencies libdap4 bes

# This 'local' all target is here in case the user did not use the
# --recursive option with clone or submodule. Not sure this will 
# work in all cases since configure might depend on libdap4 being
# present. jhrg 1/2/18
all-local: submodule-update hyrax

all:
	echo "Override the default automake rule for all"

submodule-update:
	git submodule update --init --recursive --jobs=9

# This set of rules rule will build and install the components in the
# correct order
hyrax:	bes

bes: libdap4
	(cd bes && $(MAKE) $(MFLAGS))
	(cd bes && $(MAKE) $(MFLAGS) check)
	(cd bes && $(MAKE) $(MFLAGS) install)

libdap4: build-hyrax-dependencies # run-configure
	(cd libdap4 && $(MAKE) $(MFLAGS))
	(cd libdap4 && $(MAKE) $(MFLAGS) check)
	(cd libdap4 && $(MAKE) $(MFLAGS) install)

run-configure: # build-hyrax-dependencies
	./configure --prefix=$$prefix --with-dependencies=$$prefix/deps \
		--with-libdap=`pwd`/libdap4 --enable-developer 

build-hyrax-dependencies:
	(cd hyrax-dependencies && $(MAKE) $(MFLAGS))

