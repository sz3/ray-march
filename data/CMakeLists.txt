cmake_minimum_required(VERSION 2.6)

set(SOURCES
	default.fs
	default.vs
	raymarch.fs
	raymarch.vs
)

add_custom_target(shaders SOURCES ${SOURCES})

