cmake_minimum_required(VERSION 2.8)

# Project
project(002-static-library)

# Directories
set(example_BIN_DIR bin)
set(example_INC_DIR include)
set(example_LIB_DIR lib)
set(example_SRC_DIR src)

# Library files
set(library_SOURCES ${example_SRC_DIR}/library.cpp)
set(library_HEADERS ${example_INC_DIR}/library.h)

# Add library to project
add_library(library STATIC ${library_SOURCES})

# Include directories
target_include_directories(library PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/${example_INC_DIR})

# Install
install(TARGETS library DESTINATION ${example_LIB_DIR})
install(FILES ${library_HEADERS} DESTINATION ${example_INC_DIR})
