cmake_minimum_required(VERSION 3.5)
project(XDFBrowser
	LANGUAGES CXX
	VERSION 0.1.0)

# load LSLAppBoilerplate if not done already
if(NOT TARGET LSL::lsl)
	if(NOT LSL_ROOT)
		message(FATAL_ERROR "When building a single app out of tree you need to set LSL_ROOT ( cmake -DLSL_ROOT=/path/to/installed/lsl)")
	endif()
	list(APPEND CMAKE_MODULE_PATH "${LSL_ROOT}/cmake")
	include(LSLAppBoilerplate)
endif()

# GENERAL CONFIG #
set(META_PROJECT_DESCRIPTION "View XDF file contents")

# THIRD PARTY LIBRARIES #

# Qt
find_package(Qt5 COMPONENTS Xml Widgets REQUIRED)
find_package(Boost REQUIRED COMPONENTS filesystem)

# APPLICATION #

# Target name
set(target XDFBrowser)

# Sources
set(sources
	main.cpp
	mainwindow.cpp
	mainwindow.h
	mainwindow.ui
	xdffile.h
	xdffile.cpp
)

# Build executable
add_executable(${target} MACOSX_BUNDLE WIN32 ${sources})

target_link_libraries(${target}
	PRIVATE
	Qt5::Xml
	Qt5::Widgets
	Boost::filesystem
	LSL::lsl
)

installLSLApp(${target})
