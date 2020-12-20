cmake_minimum_required (VERSION 3.7.2)

project(SDL_cmake_template)
set(CMAKE_CXX_STANDARD 11)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")

set(BIN_DIR ${SDL_cmake_template_SOURCE_DIR}/bin)

# This path is used by FindSDL2 module. 
# It will find include and lib folders under this directory.
# This is because find command doesn't include any path for Windows.
# So it can't find anything using default paths.
# SDL2_PATH is already expected in module file. I'm using the same variable.
IF (WIN32)
  set(SDL2_PATH "D:/CodeLibraries/SDL/SDL2-2.0.12")
ENDIF()

find_package(SDL2 REQUIRED)
include_directories(${SDL2_INCLUDE_DIR})

set(SOURCE_FILES "src/main.cpp")

add_executable(SDL_cmake_template 
	${SOURCE_FILES}
)

target_link_libraries(SDL_cmake_template 
	${SDL2_LIBRARY}
)

install(TARGETS SDL_cmake_template RUNTIME DESTINATION ${BIN_DIR}/)
set_target_properties(SDL_cmake_template PROPERTIES 
	RUNTIME_OUTPUT_DIRECTORY_DEBUG ${BIN_DIR}/debug/
	RUNTIME_OUTPUT_DIRECTORY_RELEASE ${BIN_DIR}/release/ )

# Copy SDL2.dll to bin/debug
add_custom_command( TARGET SDL_cmake_template POST_BUILD COMMAND ${CMAKE_COMMAND} -E copy_if_different 
	${SDL2_PATH}/bin/SDL2.dll 
	${BIN_DIR}/debug/SDL2.dll  )