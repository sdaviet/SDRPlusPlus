cmake_minimum_required(VERSION 3.13)
project(demo)

if (MSVC)
    set(CMAKE_CXX_FLAGS "-O2 /std:c++17 /EHsc")
elseif (CMAKE_CXX_COMPILER_ID MATCHES "Clang")
    set(CMAKE_CXX_FLAGS "-O3 -std=c++17 -Wno-unused-command-line-argument -undefined dynamic_lookup -fPIC")
else ()
    set(CMAKE_CXX_FLAGS "-O3 -std=c++17 -fPIC")
endif ()

file(GLOB SRC "src/*.cpp")
include_directories("src/")

add_library(demo SHARED ${SRC})
set_target_properties(demo PROPERTIES PREFIX "")

# Install directives
install(TARGETS demo DESTINATION lib/sdrpp/plugins)