
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
hyrax:	bes-stamp

bes-stamp: libdap4-stamp
	test -n $$prefix
	(cd bes && $(MAKE) $(MFLAGS))
	(cd bes && $(MAKE) $(MFLAGS) check)
	(cd bes && $(MAKE) $(MFLAGS) install)
	touch bes-stamp

libdap4-stamp: run-configure-stamp
	test -n $$prefix
	(cd libdap4 && $(MAKE) $(MFLAGS))
	(cd libdap4 && $(MAKE) $(MFLAGS) check)
	(cd libdap4 && $(MAKE) $(MFLAGS) install)
	touch libdap4-stamp

run-configure-stamp:
	test -n $$prefix
	./configure --prefix=$$prefix --with-dependencies=$$prefix/deps \
		--with-libdap=`pwd`/libdap4 --enable-developer
	touch run-configure-stamp

clean-local:
	-rm run-configure-stamp
	-rm libdap4-stamp

# make this a function/program that can be called from the actions.
# adding it a target dep makes the targets from all the time
env-check:
	test -n $$prefix

build-hyrax-dependencies:
	(cd hyrax-dependencies && $(MAKE) $(MFLAGS) skinny)

