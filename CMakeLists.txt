cmake_minimum_required(VERSION 3.20.0)
project(ising)

set(CMAKE_CXX_STANDARD 23)

set(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# --- ISING --------------------------------------------------------

# Collect all the code into an executable
add_executable(ising
        src/main.cc
        )

target_include_directories(ising PRIVATE lib)


# --- Unit testing ---------------------------------------------------

include(FetchContent)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/03597a01ee50ed33e9dfd640b249b4be3799d395.zip
)
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

enable_testing()

add_executable(
  hello_test
  test/hello_test.cc
)
target_link_libraries(
  hello_test
  GTest::gtest_main
)

include(GoogleTest)
gtest_discover_tests(hello_test)

