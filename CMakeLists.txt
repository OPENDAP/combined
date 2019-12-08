
# CMakeLists.txt file for use with CLion's code discovery, etc., modes.
# Use the autotools configure, Makefiles, etc., for building the code.
# jhrg 12/5/19

cmake_minimum_required(VERSION 3.15)

project(hyrax_git)

# Edited. set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD 11)

add_subdirectory(libdap4)
add_subdirectory(bes)

include_directories(bes)
include_directories(libdap4)

include_directories(/usr/local/include)
include_directories(/usr/local/include/c++)

# Added.
include_directories(/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/include/libxml2)
include_directories(/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/include/curl)

# Added for the sql handler and its use of unixODBC
include_directories(/usr/local/Cellar/openssl/1.0.2r/include/)

# The Hyrax dependencies directories
include_directories(build/deps/include)

include_directories(build/deps/include/gridfields)
include_directories(build/deps/include/openjpeg-2.1)
include_directories(build/deps/include/unicode)
