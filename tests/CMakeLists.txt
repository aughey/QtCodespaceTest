cmake_minimum_required(VERSION 3.14)
project(my_project)

add_compile_options(-Wall -Wextra -pedantic -Werror)

# GoogleTest requires at least C++11
set(CMAKE_CXX_STANDARD 11)

include(FetchContent)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/609281088cfefc76f9d0ce82e1ff6c30cc3591e5.zip
)
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

FILE(GLOB TEST_SRCS *.cpp)

include_directories("${CMAKE_CURRENT_SOURCE_DIR}/../lib")

add_executable(
  all_tests
  ${TEST_SRCS}
)
target_link_libraries(
  all_tests
  gtest_main
)

include(GoogleTest)


gtest_discover_tests(all_tests)
