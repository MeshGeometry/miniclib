# Set minimum version
cmake_minimum_required (VERSION 2.8.6)

if (UNIX)
    find_package (Threads REQUIRED)
endif ()

# Define target name
set (TARGET_NAME Tests)

add_executable(Tests main.cpp)

#needs some wrangling to get urho source to work
add_definitions(-DMINI_URHO -DURHO3D_LOGGING -DURHO3D_IS_BUILDING)

#include dirs
include_directories("../Source")
include_directories("./googletest/include" "./googletest")

#link the lib
target_link_libraries(Tests miniclib)

#change linker settings on windows
if (MSVC)
    target_link_libraries(Tests winmm.lib)
    SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /MD")
    SET(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /MDd")
endif()

if (UNIX)
    target_link_libraries (Tests ${CMAKE_THREAD_LIBS_INIT})
endif ()