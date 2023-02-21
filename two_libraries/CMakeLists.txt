cmake_minimum_required(VERSION 3.26)
project(two_libraries CXX C ASM)

set(CMAKE_EXPERIMENTAL_CXX_MODULE_CMAKE_API "2182bf5c-ef0d-489a-91da-49dbc3090d2a")

include(../cxx_modules_rules_clang.cmake)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

add_library(a)
target_sources(a
  PUBLIC
    FILE_SET cxx_modules TYPE CXX_MODULES FILES
    a.cppm
)

add_library(b)
target_sources(b
  PUBLIC
    FILE_SET cxx_modules TYPE CXX_MODULES FILES
    b.cppm
)

# The compiler won't find module 'a' if we delete the following
# line.
target_link_libraries(b PUBLIC a)
