cmake_minimum_required(VERSION 3.13)
set(LibName al2o3_miniz)
project(${LibName})

include(FetchContent)
FetchContent_Declare( al2o3 GIT_REPOSITORY https://github.com/DeanoC/al2o3 GIT_TAG master )
FetchContent_GetProperties(al2o3)
if(NOT al2o3_POPULATED)
	FetchContent_Populate(al2o3)
	add_subdirectory(${al2o3_SOURCE_DIR} ${al2o3_BINARY_DIR})
endif()

option( AL2O3_ORIGINAL_MINIZ_API "provide original miniz/libz api" OFF)

set(Interface
		miniz.h
		)
set(Src
		miniz.c
		lib/miniz.c
		)

set(Deps
		al2o3_platform
		)

ADD_LIB(${LibName} "${Interface}" "${Src}" "${Deps}")
if(AL2O3_ORIGINAL_MINIZ_API)
	target_include_directories(${LibName} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src)
endif()

