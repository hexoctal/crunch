# Set the minimum version required of CMake
cmake_minimum_required(VERSION 3.20.0)

# Export compile commands for clangd (Code Completion)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON CACHE INTERNAL "" FORCE)

# Build type
set(CMAKE_BUILD_TYPE "Release" CACHE STRING "" FORCE)

# Debug mode (GDB) + Disable optimization (for debugging) + Warnings
set(CMAKE_CXX_FLAGS_DEBUG "-ggdb -O0 -Wall -Wpedantic -Wextra" CACHE STRING "" FORCE)

# Release mode
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -DNDEBUG" CACHE STRING "" FORCE)

# Set up the project
project(
	"crunch"
	VERSION 1.0.0
	LANGUAGES CXX
	)

# Source files
set(crunch_SRCS
	crunch/binary.cpp
	crunch/bitmap.cpp
	crunch/GuillotineBinPack.cpp
	crunch/hash.cpp
	crunch/lodepng.cpp
	crunch/main.cpp
	crunch/MaxRectsBinPack.cpp
	crunch/packer.cpp
	crunch/Rect.cpp
	crunch/str.cpp
	)

# Create the library
add_executable(${PROJECT_NAME}
	${crunch_SRCS}
	)

# Require C++14
target_compile_features(${PROJECT_NAME}
	PUBLIC cxx_std_14
	)

# Impose the use of C++ for the linker
set_target_properties(${PROJECT_NAME}
	PROPERTIES LINKER_LANGUAGE CXX
	)
