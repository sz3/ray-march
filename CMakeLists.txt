cmake_minimum_required(VERSION 2.6)

project(raymarch)
add_subdirectory(glload)
add_subdirectory(data)

set (SOURCES
	src/main.cpp

	src/fileio.cpp
	src/fileio.h
	src/opengl.cpp
	src/opengl.h
)

include_directories(
	${geeel_SOURCE_DIR}
	${geeel_SOURCE_DIR}/glload/include
)

link_directories(
	${geeel_SOURCE_DIR}/glload
)

add_executable (
	raymarch
	${SOURCES}
)

target_link_libraries(raymarch
	glfw
	
	glload
)

