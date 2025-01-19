cmake_minimum_required(VERSION 3.28)
set (project turbovnc)

set(${project}_SOURCES
	${CMAKE_CURRENT_SOURCE_DIR}/tight.c
	${CMAKE_CURRENT_SOURCE_DIR}/turbojpeg.h
)
add_library(${project} STATIC ${${project}_SOURCES} )