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
	${raymarch_SOURCE_DIR}
	${raymarch_SOURCE_DIR}/glload/include
)

link_directories(
	${raymarch_SOURCE_DIR}/glload
)

add_executable (
	raymarch
	${SOURCES}
)

target_link_libraries(raymarch
-Wl,--start-group
	GL
	glfw
	
	glload
-Wl,--end-group
)

