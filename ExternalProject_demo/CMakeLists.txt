cmake_minimum_required(VERSION 3.24)
project(untitled)

set(CMAKE_CXX_STANDARD 20)

add_executable(untitled main.cpp)


include(ExternalProject)
ExternalProject_Add(libspdlog
        GIT_REPOSITORY    git@github.com:gabime/spdlog.git
        GIT_TAG           v1.11.0
        PREFIX ${CMAKE_BINARY_DIR}/3rdparty/spdlog/prefix
        LOG_DIR ${CMAKE_BINARY_DIR}/3rdparty/spdlog/log_dir
        DOWNLOAD_DIR ${CMAKE_BINARY_DIR}/3rdparty/spdlog/download_dir
        INSTALL_DIR ${CMAKE_BINARY_DIR}/3rdparty/spdlog/install_dir
        CMAKE_ARGS "-DCMAKE_INSTALL_PREFIX=${CMAKE_BINARY_DIR}/3rdparty/spdlog/install_prefix"
        )
add_dependencies(untitled libspdlog)

target_include_directories(untitled PRIVATE
        ${CMAKE_BINARY_DIR}/3rdparty/spdlog/install_prefix/include
        )
