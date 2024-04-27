cmake_minimum_required(VERSION 3.14)

set(OFA_PROJECT_NAME ofa)
set(OFA_SOURCE_DIR src)
set(OFA_SOURCE ${OFA_SOURCE_DIR}/main.cpp)
set(OFA_PROJECT_VERSION 0.0.1)

# CMake CXX Standards
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(
  ${OFA_PROJECT_NAME}
  VERSION ${OFA_PROJECT_VERSION}
  DESCRIPTION "Powerful data pipelines based on Drain algorithm for logs"
  LANGUAGES CXX
  )

if (CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)
  set(CMAKE_CXX_EXTENSIONS OFF)
  set_property(GLOBAL PROPERTY USE_FOLDERS ON)
endif()

include(FetchContent)

add_subdirectory(src)

if(CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME AND BUILD_TESTING)
  add_subdirectory(tests)
endif()
