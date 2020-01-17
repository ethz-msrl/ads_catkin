cmake_minimum_required(VERSION 2.8.3)
project(ads_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple()

include(ExternalProject)


ExternalProject_Add(ads
    PREFIX ${CATKIN_DEVEL_PREFIX}/ads
    GIT_REPOSITORY https://github.com/Beckhoff/ADS.git
    GIT_TAG 6b3a03009a757cf651fe44d8be7b6df698028f0e
    #GIT_TAG master
    CONFIGURE_COMMAND ""
    UPDATE_COMMAND ""
    BUILD_COMMAND ""
    INSTALL_COMMAND ""
)

ExternalProject_Get_Property(ads source_dir)

#cs_add_library(${PROJECT_NAME}
#    ${source_dir}/AdsLib/AdsDef.cpp
#)

cs_install()
cs_export()