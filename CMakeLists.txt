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
    BUILD_BYPRODUCTS 
        <SOURCE_DIR>/AdsLib/AdsDef.cpp
        <SOURCE_DIR>/AdsLib/AdsLib.cpp
        <SOURCE_DIR>/AdsLib/AmsConnection.cpp
        <SOURCE_DIR>/AdsLib/AmsPort.cpp
        <SOURCE_DIR>/AdsLib/AmsRouter.cpp
        <SOURCE_DIR>/AdsLib/Frame.cpp
        <SOURCE_DIR>/AdsLib/Log.cpp
        <SOURCE_DIR>/AdsLib/NotificationDispatcher.cpp
        <SOURCE_DIR>/AdsLib/Sockets.cpp
        <SOURCE_DIR>/AdsLib/AdsDef.h
        <SOURCE_DIR>/AdsLib/AdsLib.h
        <SOURCE_DIR>/AdsLib/AdsNotification.h
        <SOURCE_DIR>/AdsLib/AmsConnection.h
        <SOURCE_DIR>/AdsLib/AmsHeader.h
        <SOURCE_DIR>/AdsLib/AmsPort.h
        <SOURCE_DIR>/AdsLib/AmsRouter.h
        <SOURCE_DIR>/AdsLib/Frame.h
        <SOURCE_DIR>/AdsLib/Log.h
        <SOURCE_DIR>/AdsLib/NotificationDispatcher.h
        <SOURCE_DIR>/AdsLib/RingBuffer.h
        <SOURCE_DIR>/AdsLib/Router.h
        <SOURCE_DIR>/AdsLib/Semaphore.h
        <SOURCE_DIR>/AdsLib/Sockets.h
        <SOURCE_DIR>/AdsLib/wrap_endian.h
        <SOURCE_DIR>/AdsLib/wrap_socket.h
)

ExternalProject_Get_Property(ads SOURCE_DIR)


include_directories(
    ${SOURCE_DIR}/AdsLib
)

cs_add_library(${PROJECT_NAME}
    ${SOURCE_DIR}/AdsLib/AdsDef.cpp
    ${SOURCE_DIR}/AdsLib/AdsLib.cpp
    ${SOURCE_DIR}/AdsLib/AmsConnection.cpp
    ${SOURCE_DIR}/AdsLib/AmsPort.cpp
    ${SOURCE_DIR}/AdsLib/AmsRouter.cpp
    ${SOURCE_DIR}/AdsLib/Frame.cpp
    ${SOURCE_DIR}/AdsLib/Log.cpp
    ${SOURCE_DIR}/AdsLib/NotificationDispatcher.cpp
    ${SOURCE_DIR}/AdsLib/Sockets.cpp
)
add_dependencies(${PROJECT_NAME} ads)


cs_install()
cs_export()