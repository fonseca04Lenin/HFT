cmake_minimum_required(VERSION 3.24)
project(hft_sim LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

include(FetchContent)
FetchContent_Declare(Catch2
  GIT_REPOSITORY https://github.com/catchorg/Catch2.git
  GIT_TAG v3.8.1)
FetchContent_MakeAvailable(Catch2)

add_executable(hft-sim src/main.cpp)
target_include_directories(hft-sim PRIVATE include)
target_compile_options(hft-sim PRIVATE -Wall -Wextra -Wpedantic)

enable_testing()
add_executable(hft-tests tests/test_smoke.cpp)
target_include_directories(hft-tests PRIVATE include)
target_link_libraries(hft-tests PRIVATE Catch2::Catch2WithMain)
include(CTest)
include(Catch)
catch_discover_tests(hft-tests)
