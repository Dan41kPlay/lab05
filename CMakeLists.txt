cmake_minimum_required(VERSION 3.10)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

option(BUILD_TEST "Build tests" OFF)

project(banking)

add_library(banking STATIC banking/Account.cpp banking/Transaction.cpp)
target_include_directories(banking PUBLIC banking)

if(BUILD_TESTS)
	# partially source: https://google.github.io/googletest/quickstart-cmake.html
	include(FetchContent)
	FetchContent_Declare(
		googletest
		URL https://github.com
	)
	# For Windows compatibility, set gtest_force_shared_crt
	set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
	FetchContent_MakeAvailable(googletest)
	enable_testing()
	add_executable(check tests/test.cpp)
	target_link_libraries(check banking GTest::gtest_main GTest::gmock_main)
	include(GoogleTest)
	gtest_discover_tests(check)
endif()
