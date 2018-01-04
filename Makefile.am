
AUTOMAKE_OPTIONS = foreign

SUBDIRS = . olfs 
# libdap4 bes

# This 'local' all target is here in case the user did not use the
# --recursive option with clone or submodule. Not sure this will 
# work in all cases since configure might depend on libdap4 being
# present. jhrg 1/2/18
all-local:
	git submodule update --init --recursive --jobs=9
