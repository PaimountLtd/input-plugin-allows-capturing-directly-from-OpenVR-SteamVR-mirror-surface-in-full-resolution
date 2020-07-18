project(win-openvr)

include(ExternalProject)

ExternalProject_Add(openvrsdk
 	GIT_REPOSITORY https://github.com/ValveSoftware/openvr.git
 	GIT_SHALLOW 1
	GIT_TAG master
 	CONFIGURE_COMMAND  ""
 	BUILD_COMMAND ""
 	INSTALL_COMMAND ""
 )

if(MSVC)
    include_directories(${CMAKE_BINARY_DIR}/plugins/obs-openvr/openvrsdk-prefix/src/openvrsdk/)
	link_directories(${CMAKE_BINARY_DIR}/plugins/obs-openvr/openvrsdk-prefix/src/openvrsdk/)
endif()

set(win-openvr_SOURCES
	win-openvr.cpp)

add_library(win-openvr MODULE
	${win-openvr_SOURCES})
target_link_libraries(win-openvr
	libobs)

install_obs_plugin_with_data(win-openvr data)

install(FILES "${CMAKE_BINARY_DIR}/plugins/obs-openvr/openvrsdk-prefix/src/openvrsdk/bin/win64/openvr_api.dll" DESTINATION "${OBS_EXECUTABLE_DESTINATION}")
