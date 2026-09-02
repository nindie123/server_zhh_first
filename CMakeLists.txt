cmake_minimum_required(VERSION 3.10)
project(WebServer)

# 修复Makefile下CMAKE_BUILD_TYPE不生效的坑
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Debug CACHE STRING "build type" FORCE)
endif()
set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release" "RelWithDebInfo")

# C++标准，优先使用官方变量，不要写死在flags
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 全局警告选项，所有模式共用
add_compile_options(-Wall -Werror)
# 增加 compile_commands.json，保证格式不会产生报错，舒服
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)


# Debug模式：关闭优化
set(CMAKE_CXX_FLAGS_DEBUG "-O0")
# Release模式：开启O2优化（CMake默认自带，这里显式写出方便查看）
set(CMAKE_CXX_FLAGS_RELEASE "-O2 -DNDEBUG")

# 可执行文件输出目录，新版CMake变量
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/build/test/)

# 头文件搜索路径
include_directories(
    base
    tcp
    log
    http
    timer
)

# 多线程
find_package(Threads REQUIRED)

# jsoncpp
find_package(PkgConfig REQUIRED)
pkg_check_modules(JSONCPP jsoncpp)

aux_source_directory(base SRC_LIST1)
aux_source_directory(tcp SRC_LIST2)
aux_source_directory(http SRC_LIST3)
aux_source_directory(timer SRC_LIST4)
aux_source_directory(log SRC_LIST5)

add_executable(webserver test/http_server.cpp
    ${SRC_LIST1}
    ${SRC_LIST2}
    ${SRC_LIST3}
    ${SRC_LIST4}
    ${SRC_LIST5}
)

# 目标专属链接，不要用全局link_libraries
target_link_libraries(webserver
    ${CMAKE_THREAD_LIBS_INIT}
    ${JSONCPP_LIBRARIES}
)

