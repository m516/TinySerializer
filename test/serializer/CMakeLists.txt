# Based on the official GoogleTest CMake tutorial, available here:
# https://google.github.io/googletest/quickstart-cmake.html
cmake_minimum_required(VERSION 3.14)
# GoogleTest requires at least C++14
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Fetch GoogleTest
include(FetchContent)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/03597a01ee50ed33e9dfd640b249b4be3799d395.zip
)

# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

# Create the test executable
add_executable(
  ${PROJECT_NAME}_tests
  test_serializer.cc
)

# Link with this library and GoogleTest
target_link_libraries(
  ${PROJECT_NAME}_tests
  GTest::gtest_main
  ${PROJECT_NAME}
)

# Discover all tests
include(GoogleTest)
gtest_discover_tests(${PROJECT_NAME}_tests)
