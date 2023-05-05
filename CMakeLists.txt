cmake_minimum_required(VERSION 3.26)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(GIT_URL_BASE "git@github-ikoznov.com:")
if(DEFINED ENV{GITHUB_TOKEN})
    set(GIT_URL_BASE "https://$ENV{GITHUB_TOKEN}@github.com/")
endif()

include(FetchContent)
if(NOT EXISTS "${CMAKE_SOURCE_DIR}/external/lib1/src/CMakeLists.txt")
    FetchContent_Declare(lib1
            SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/external/lib1"
            GIT_REPOSITORY "${GIT_URL_BASE}ikoznov-cross-repo/lib1.git"
            GIT_TAG main)
    FetchContent_GetProperties(lib1)
    if(NOT lib1_POPULATED)
        FetchContent_Populate(lib1)
    endif()
endif()

project(MainProject)

add_subdirectory(src)
