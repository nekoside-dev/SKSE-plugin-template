cmake_minimum_required(VERSION 4.0.0)


project(plugin VERSION 0.1.0 LANGUAGES CXX)

set(ENABLE_SKYRIM_SE OFF)
set(ENABLE_SKYRIM_VR OFF)
set(BUILD_TESTS OFF)

add_subdirectory(lib/commonlibsse-ng)
include(lib/commonlibsse-ng/cmake/CommonLibSSE.cmake)

add_commonlibsse_plugin(
		${PROJECT_NAME}
		SOURCES
		src/main.cpp
		src/PCH.h
)

target_precompile_headers(${PROJECT_NAME} PRIVATE src/PCH.h)

if (NOT $ENV{SKYRIM_MODS_FOLDER} STREQUAL "")
	message("Found Skyrim mods folder: $ENV{SKYRIM_MODS_FOLDER}")
	add_custom_command(
		TARGET ${PROJECT_NAME}
		POST_BUILD
		COMMAND ${CMAKE_COMMAND} -E make_directory "$ENV{SKYRIM_MODS_FOLDER}/${PROJECT_NAME}/SKSE/Plugins"
		COMMAND ${CMAKE_COMMAND} -E copy_if_different "$<TARGET_FILE:${PROJECT_NAME}>" "$ENV{SKYRIM_MODS_FOLDER}/${PROJECT_NAME}/SKSE/Plugins/$<TARGET_FILE_NAME:${PROJECT_NAME}>"
		VERBATIM
	)

	if (CMAKE_BUILD_TYPE STREQUAL "Debug")
		message("Detected debug mode, copy pdb file")
		add_custom_command(
			TARGET ${PROJECT_NAME}
			POST_BUILD
			COMMAND ${CMAKE_COMMAND} -E copy_if_different "$<TARGET_PDB_FILE:${PROJECT_NAME}>" "$ENV{SKYRIM_MODS_FOLDER}/${PROJECT_NAME}/SKSE/Plugins/$<TARGET_PDB_FILE_NAME:${PROJECT_NAME}>"
			VERBATIM
		)
	endif()
endif()