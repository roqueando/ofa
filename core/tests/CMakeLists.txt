file(GLOB TEST_LIST "${ofa_SOURCE_DIR}/tests/*.cpp")

FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://github.com/google/googletest.git
  GIT_TAG v1.14.0
)

FetchContent_MakeAvailable(googletest)

enable_testing()

# Setting up the tests compilation
add_executable(tests ${TEST_LIST})
target_compile_features(tests PRIVATE cxx_std_23)
target_link_libraries(tests PRIVATE ofa GTest::gtest_main)

# important to set fixtures and just test in current directory
add_test(NAME tests COMMAND tests WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}) 

include(GoogleTest)
add_custom_command(
  TARGET tests
  POST_BUILD
  COMMAND ${CMAKE_CTEST_COMMAND} --output-on-failure
  WORKING_DIRECTORY ${CMAKE_BINARY_DIR}
  COMMENT "running tests..."
)
