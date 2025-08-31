# ----------------------------------------------------------------------------------------
#  CMAKE File
#  Copyright (C) 2025 - 2025  Helmut Fieres
# ----------------------------------------------------------------------------------------
cmake_minimum_required(VERSION 3.29)

project(ELF-File-Viewer C CXX ASM)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_C_EXTENSIONS ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

# ---- Bring in ELFIO with FetchContent ----
include(FetchContent)

FetchContent_Declare(
  ELFIO
  GIT_REPOSITORY https://github.com/serge1/ELFIO.git
  GIT_TAG        main   # or pin to a release, e.g. v3.12
)

FetchContent_MakeAvailable(ELFIO)

# ---- Build the example elfdump ----
# The source file is inside the fetched ELFIO directory
add_executable(ELF-File-Viewer
    ${elfio_SOURCE_DIR}/examples/elfdump/elfdump.cpp
)

target_link_libraries(ELF-File-Viewer PRIVATE elfio::elfio)