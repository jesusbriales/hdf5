cmake_minimum_required (VERSION 2.8.12)
PROJECT (hdfWrap C CXX)
# set(CMAKE_BUILD_TYPE Debug)

message(STATUS "Current BUILD_TYPE: " ${CMAKE_BUILD_TYPE})

# Include own /include directory for this project
INCLUDE_DIRECTORIES( include )

# FIND_PACKAGE (HDF5 NAMES hdf5)
FIND_PACKAGE( HDF5 REQUIRED ) # Find non-cmake built HDF5
INCLUDE_DIRECTORIES( ${HDF5_INCLUDE_DIR} )
SET( H5CPP_LIBS hdf5_cpp )

FIND_PACKAGE( Boost
  COMPONENTS system REQUIRED )

file(GLOB_RECURSE HEADERS
  include/*.h
  include/*.hpp
)

# First application, LSD detector and descriptor with HDF5 storage
add_executable( test
  src/test-hdf.cpp
  ${HEADERS}
)
target_link_libraries( test
  ${HDF5_LIBRARIES}
  ${H5CPP_LIBS}
  ${Boost_LIBRARIES}
)

#ENABLE_TESTING ()
#include (CTest)

#add_test (NAME test_example COMMAND ${example})
