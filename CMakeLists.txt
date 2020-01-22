cmake_minimum_required(VERSION 2.8.3)
project(ads_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple()

add_definitions(-std=c++11 -Wall -Wextra)

cs_add_library(${PROJECT_NAME}
	src/AdsDef.cpp
	src/AdsLib.cpp
	src/AmsConnection.cpp
	src/AmsPort.cpp
	src/AmsRouter.cpp
	src/Frame.cpp
	src/Log.cpp
	src/NotificationDispatcher.cpp
	src/Sockets.cpp
)

cs_install()
cs_export()
