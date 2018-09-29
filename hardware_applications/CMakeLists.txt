cmake_minimum_required(VERSION 3.5.1)
project(hardware_applications)

set(CMAKE_CXX_STANDARD 17)

include(ExternalProject)

ExternalProject_Add(STSL
        GIT_REPOSITORY https://github.com/RoboJackets/stsl.git
        INSTALL_DIR ${PROJECT_BINARY_DIR}
        CMAKE_ARGS -DCMAKE_INSTALL_PREFIX:PATH=<INSTALL_DIR> -DCMAKE_C_COMPILER=${CMAKE_C_COMPILER} -DCMAKE_CXX_COMPILER=${CMAKE_CXX_COMPILER} -DCMAKE_CXX_FLAGS=${CMAKE_CXX_FLAGS} -DCMAKE_C_FLAGS=${CMAKE_C_FLAGS}
        UPDATE_COMMAND "")

set(STSL_LIBS ${PROJECT_BINARY_DIR}/lib/libSTSL.a)

if(WIN32)
    set(STSL_LIBS ${STSL_LIBS} ws2_32)
endif()

include_directories(${PROJECT_BINARY_DIR}/include)

SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake/modules)

add_subdirectory(spin_in_place)

add_subdirectory(drive_in_square)
add_subdirectory(drive_in_square_solution)

add_subdirectory(line_follow)
add_subdirectory(line_follow_solution)

add_subdirectory(median_line)
add_subdirectory(median_line_solution)
