cmake_minimum_required(VERSION 2.8.3)
project(ads_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple()

# From Cmake version 3.11 on, there is the module FetchContent which can be used instead of DownloadProject
include(DownloadProject.cmake)


# This file uses the module DownloadProject to download the source files from the Beckhoff ADS library. DownloadProject can
# be replaced by FetchContent (which is only available for Cmake >3.10). DownloadProject can build targets and makes them 
# available before building this file. However, here we just use it to download the source files without building them.
# The files are placed to the CATKIN_DEVEL_PREFIX because the include files should only be placed in source or devel space.
# The libraries are linked to these include files and, therefore, they can not be moved. To keep the devel space clean, 
# unnecessary files are deleted in the end. However, since Cmake files are not processed in chronological order, we need
# to keep the .cpp files.
# The library is installed to include/AdsLib both in devel space, as well as in install space. It can be included by 
# "include <AdsLib/AdsLib.h>.

download_project(
    PROJ    ads
    PREFIX ${CATKIN_DEVEL_PREFIX}/ads
    GIT_REPOSITORY https://github.com/Beckhoff/ADS.git
    GIT_TAG 6b3a03009a757cf651fe44d8be7b6df698028f0e
    # GIT_TAG master
)

include_directories(
    ${ads_SOURCE_DIR}
)

cs_add_library(AdsLib
    ${ads_SOURCE_DIR}/AdsLib/AdsDef.cpp
    ${ads_SOURCE_DIR}/AdsLib/AdsLib.cpp
    ${ads_SOURCE_DIR}/AdsLib/AmsConnection.cpp
    ${ads_SOURCE_DIR}/AdsLib/AmsPort.cpp
    ${ads_SOURCE_DIR}/AdsLib/AmsRouter.cpp
    ${ads_SOURCE_DIR}/AdsLib/Frame.cpp
    ${ads_SOURCE_DIR}/AdsLib/Log.cpp
    ${ads_SOURCE_DIR}/AdsLib/NotificationDispatcher.cpp
    ${ads_SOURCE_DIR}/AdsLib/Sockets.cpp
)

cs_install()

install(DIRECTORY ${ads_SOURCE_DIR}/AdsLib/
        DESTINATION ${CATKIN_GLOBAL_INCLUDE_DESTINATION}/AdsLib
        FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp"  
)

cs_export(
    INCLUDE_DIRS ${ads_SOURCE_DIR}
)

# Removing almost all files which do not belong to devel space
set(DELETE_FILES
    ${CATKIN_DEVEL_PREFIX}/ads/ads-build
    ${CATKIN_DEVEL_PREFIX}/ads/ads-download
    ${CATKIN_DEVEL_PREFIX}/ads/ads-src/AdsLibTest
    ${CATKIN_DEVEL_PREFIX}/ads/ads-src/AdsLibTestRef
    ${CATKIN_DEVEL_PREFIX}/ads/ads-src/docs
    ${CATKIN_DEVEL_PREFIX}/ads/ads-src/example
    ${CATKIN_DEVEL_PREFIX}/ads/ads-src/PLC-TestProject
    ${CATKIN_DEVEL_PREFIX}/ads/ads-src/tools
    ${CATKIN_DEVEL_PREFIX}/ads/ads-src/AdsLibTest
    ${CATKIN_DEVEL_PREFIX}/ads/ads-src/AdsLib.sln
    ${CATKIN_DEVEL_PREFIX}/ads/ads-src/LICENSE
    ${CATKIN_DEVEL_PREFIX}/ads/ads-src/Makefile
    ${CATKIN_DEVEL_PREFIX}/ads/ads-src/README
)

file(REMOVE_RECURSE ${DELETE_FILES})
