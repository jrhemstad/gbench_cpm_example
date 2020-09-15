cmake_minimum_required(VERSION 3.14 FATAL_ERROR)

project(CPMExampleBenchmark)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# ---- Dependencies ----

include(./cmake/CPM.cmake)

CPMAddPackage(
  NAME fibonacci
  GITLAB_REPOSITORY TheLartians/Fibonacci
  VERSION 2.0
)

CPMAddPackage(
  NAME benchmark
  GITHUB_REPOSITORY google/benchmark
  VERSION 1.4.1
  OPTIONS
    "BENCHMARK_ENABLE_TESTING Off"
)

if (benchmark_ADDED)
  # patch google benchmark target
  set_target_properties(benchmark PROPERTIES CXX_STANDARD 14)
endif()

# ---- Executable ----

add_executable(CPMExampleBenchmark "main.cpp")
set_target_properties(CPMExampleBenchmark PROPERTIES CXX_STANDARD 14)        
target_link_libraries(CPMExampleBenchmark fibonacci benchmark)
