cmake_minimum_required(VERSION 3.12)
project(Skeleton)

# LLVM uses C++17.
set(CMAKE_CXX_STANDARD 17)

# Load LLVMConfig.cmake. If this fails, consider setting `LLVM_DIR` to point
# to your LLVM installation's `lib/cmake/llvm` directory.
find_package(LLVM REQUIRED CONFIG)
include_directories(${LLVM_INCLUDE_DIRS}
    "$(brew --prefix llvm)/include/c++/v1"
    "$(brew --prefix)/include"
    "$(brew --prefix)/include"
)

# Include the part of LLVM's CMake libraries that defines
# `add_llvm_pass_plugin`.
include(AddLLVM)

# Use LLVM's preprocessor defini`tions, include directories, and library search
# paths.
add_definitions(${LLVM_DEFINITIONS})
include_directories(${LLVM_INCLUDE_DIRS})
link_directories(${LLVM_LIBRARY_DIRS})

# Our pass lives in this subdirectory.
add_subdirectory(skeleton)

set(CMAKE_CXX_COMPILER "$(brew --prefix llvm)/bin/clang++")
