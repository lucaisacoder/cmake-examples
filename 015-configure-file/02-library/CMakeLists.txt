cmake_minimum_required(VERSION 2.8)

# Project
project(015-configure-file-02)

# Directories
set(example_BIN_DIR bin)
set(example_INC_DIR include)
set(example_LIB_DIR lib)
set(example_SRC_DIR src)

# Version
set(example_VERSION_MAJOR 1)
set(example_VERSION_MINOR 2)
set(example_VERSION_PATCH 3)
set(example_VERSION "${example_VERSION_MAJOR}.${example_VERSION_MINOR}.${example_VERSION_PATCH}")

# Version File
configure_file(${example_INC_DIR}/version.h.in ${CMAKE_CURRENT_BINARY_DIR}/version.h)

# Library files
set(library_SOURCES ${example_SRC_DIR}/library.cpp)
set(library_HEADERS ${example_INC_DIR}/library.h)
set(executable_SOURCES ${example_SRC_DIR}/main.cpp)

# Add library to project
add_library(library STATIC ${library_SOURCES})

# Include directories
target_include_directories(library PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/${example_INC_DIR})
target_include_directories(library PUBLIC ${CMAKE_CURRENT_BINARY_DIR})

# Add executable to project
add_executable(executable ${executable_SOURCES})

# Linking
target_link_libraries(executable library)


# Install
install(TARGETS executable DESTINATION ${example_BIN_DIR})
install(TARGETS library DESTINATION ${example_LIB_DIR})
install(FILES ${library_HEADERS} DESTINATION ${example_INC_DIR})
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/version.h DESTINATION ${example_INC_DIR})
