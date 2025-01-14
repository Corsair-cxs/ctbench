cmake_minimum_required(VERSION 3.25)
project(ctbench VERSION 1.0.0)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

if(${CTBENCH_ENABLE_CLANG_TIDY})
  set(CMAKE_CXX_CLANG_TIDY clang-tidy -checks=-*,readability-*)
endif()

include(cmake/dependencies.cmake)
include(cmake/ctbench-compile-opts.cmake)

# Docs
if(${CTBENCH_ENABLE_DOCS})
  add_subdirectory(cmake-doc-extractor)
  include(cmake/docs.cmake)
endif()

if(${CTBENCH_ENABLE_TESTS})
  # Dummy target for all tests
  add_custom_target(test-all)
endif()

add_subdirectory(ttw)
add_subdirectory(grapher)

include(cmake/ctbench-api.cmake)
include(cmake/install.cmake)
