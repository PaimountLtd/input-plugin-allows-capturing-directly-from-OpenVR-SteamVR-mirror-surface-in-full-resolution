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


add_library(win-openvr MODULE)
add_library(OBS::openvr ALIAS win-openvr)

target_sources(win-openvr PRIVATE win-openvr.cpp)

target_link_libraries(win-openvr PRIVATE OBS::libobs OBS::w32-pthreads)

setup_plugin_target(win-openvr)

install(FILES "${CMAKE_BINARY_DIR}/plugins/obs-openvr/openvrsdk-prefix/src/openvrsdk/bin/win64/openvr_api.dll" DESTINATION "${OBS_EXECUTABLE_DESTINATION}")
