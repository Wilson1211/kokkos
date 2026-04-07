cmake_minimum_required(VERSION 3.16)
project(tutorial_01_hello_world LANGUAGES CXX)

if(COMMAND kokkos_include_directories AND COMMAND kokkos_add_executable)
	# In-tree Kokkos tutorial build path.
	kokkos_include_directories(${CMAKE_CURRENT_BINARY_DIR})
	kokkos_include_directories(${CMAKE_CURRENT_SOURCE_DIR})

	# This is a tutorial, not a test, so we don't ask CTest to run it.
	kokkos_add_executable(tutorial_01_hello_world SOURCES hello_world.cpp)
else()
	# Standalone build path (e.g., running CMake directly in this directory).
	find_package(Kokkos REQUIRED CONFIG)

	add_executable(tutorial_01_hello_world hello_world.cpp)
	target_link_libraries(tutorial_01_hello_world PRIVATE Kokkos::kokkos)
endif()
