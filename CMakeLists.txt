#---------------------------------------------------------------------------------------------------
# Basic Configuration
#---------------------------------------------------------------------------------------------------
cmake_minimum_required(VERSION 3.14)
project(explore)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(SRC_DIR ${PROJECT_SOURCE_DIR}/src)
set(INC_DIR ${PROJECT_SOURCE_DIR}/inc)
set(TEST_DIR ${PROJECT_SOURCE_DIR}/tests)

#---------------------------------------------------------------------------------------------------
# Included Libraries
#---------------------------------------------------------------------------------------------------
include (FetchContent)

#---------------------------------------------------------------------------------------------------
FetchContent_Declare(
    googletest
    URL https://github.com/google/googletest/archive/03597a01ee50ed33e9dfd640b249b4be3799d395.zip
)
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

#---------------------------------------------------------------------------------------------------
FetchContent_Declare(
    SFML
    GIT_REPOSITORY https://github.com/SFML/SFML.git
    GIT_TAG 2.6.x
    GIT_SHALLOW ON
    EXCLUDE_FROM_ALL
    SYSTEM
)
FetchContent_MakeAvailable(SFML)

#---------------------------------------------------------------------------------------------------
# Source(s)
#---------------------------------------------------------------------------------------------------
file(GLOB WINDOW_SRCS ${SRC_DIR}/Components/window/*.cpp)

add_executable(${PROJECT_NAME} 
    ${SRC_DIR}/main.cpp
    ${SRC_DIR}/Components/game.cpp
    ${WINDOW_SRCS}
)
target_link_libraries(${PROJECT_NAME} PRIVATE
      sfml-graphics
)

# Uncomment if external libraries are present.
# target_include_directories(${PROJECT_NAME} PRIVATE
#     #${<external_library>_SOURCE_DIR}/inc
# )

#---------------------------------------------------------------------------------------------------
# Test(s)
#---------------------------------------------------------------------------------------------------
# Uncomment if testing is present.

# enable_testing()

# set(TESTS
#     # ${TEST_DIR}/ex_test.cpp
# )

# add_executable(${PROJECT_NAME}_tests ${TESTS})

# target_link_libraries(${PROJECT_NAME}_tests
#     GTest::gtest_main
#     ${PROJECT_NAME}_lib
# )

# include(GoogleTest)
# gtest_discover_tests(${PROJECT_NAME}_tests)
