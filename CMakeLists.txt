cmake_minimum_required(VERSION 3.6)
project(counter)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_BUILD_TYPE Debug)

set(SOURCE_FILES src/counter.cpp src/u32word.cpp src/word-counter.cpp src/checksum-counter.cpp)

add_library(counter ${SOURCE_FILES})

add_executable(prog src/main.cpp)
target_link_libraries(prog counter)

add_library(Catch2 INTERFACE)
target_include_directories(Catch2 INTERFACE "third-party/catch2")

enable_testing()
add_executable(tests tests/test.cpp tests/catch-main.cpp tests/test-wordcounter.cpp)
target_include_directories(tests PRIVATE "src")
target_link_libraries(tests Catch2)
target_link_libraries(tests counter)
add_test(tests tests)
