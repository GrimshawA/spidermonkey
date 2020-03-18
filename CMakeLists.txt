cmake_minimum_required(VERSION 3.1)
project (SpiderMonkey)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin")

if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
  # using Clang
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
  # using GCC
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -fPIC")
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Intel")
  # using Intel C++
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "MSVC")
  # using Visual Studio C++
endif()

file(GLOB_RECURSE SPIDERMONKEY_SRC
    "js/src/vm/*.cpp"
)

add_library(spidermonkey SHARED ${SPIDERMONKEY_SRC})
target_include_directories(spidermonkey PUBLIC GLOBAL
    "js/src/"
    "${CMAKE_SOURCE_DIR}/include"
)

# Test -----------------------------------------------------------------

add_executable(testsm "test/main.cpp")
target_link_libraries(testsm spidermonkey)
