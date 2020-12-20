cmake_minimum_required (VERSION 3.7.2)

project(CPP_SDL2_BASE)
set(CMAKE_CXX_STANDARD 11)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")

set(BIN_DIR ${CPP_SDL2_BASE_SOURCE_DIR}/bin)

IF (WIN32)
  set(SDL2_PATH "D:/CodeLibraries/SDL/SDL2-2.0.12")
ENDIF()

find_package(SDL2 REQUIRED)
include_directories(${SDL2_INCLUDE_DIR})

set(SOURCE_FILES "src/main.cpp")

add_executable(CPP_SDL2_BASE 
	${SOURCE_FILES}
)

target_link_libraries(CPP_SDL2_BASE 
	${SDL2_LIBRARY}
)

install(TARGETS CPP_SDL2_BASE RUNTIME DESTINATION ${BIN_DIR}/)
set_target_properties(CPP_SDL2_BASE PROPERTIES 
	RUNTIME_OUTPUT_DIRECTORY_DEBUG ${BIN_DIR}/debug/
	RUNTIME_OUTPUT_DIRECTORY_RELEASE ${BIN_DIR}/release/ )


# Copy SDL2.dll to bin/debug
IF(WIN32)
	add_custom_command( TARGET CPP_SDL2_BASE POST_BUILD COMMAND ${CMAKE_COMMAND} -E copy_if_different 
		${SDL2_PATH}/bin/SDL2.dll 
		${BIN_DIR}/debug/SDL2.dll  )
ENDIF()