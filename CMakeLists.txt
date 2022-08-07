cmake_minimum_required(VERSION 3.5)
project(AKFSFSimulation)

set(CMAKE_CXX_STANDARD 11)

find_package (Eigen3 3.3 REQUIRED NO_MODULE)

find_library(SDL2Fwk SDL2 REQUIRED)
find_library(SDL2TTfFwk SDL2_ttf REQUIRED)
message(STATUS "found SDL2TTfFwk=${SDL2TTfFwk}")

set(SRC_CPP
    src/main.cpp
    src/display.cpp
    src/beacons.cpp
    src/sensors.cpp
    src/simulation.cpp
    src/utils.cpp
    src/kalmanfilter.cpp
)

add_executable(${PROJECT_NAME}
        ${SRC_CPP}
        )

include_directories(${PROJECT_NAME} ${SDL2_INCLUDE_DIRS})

target_link_libraries(${PROJECT_NAME}
        ${SDL2Fwk}
        ${SDL2TTfFwk}
        Eigen3::Eigen
        )

add_custom_command(TARGET ${PROJECT_NAME} PRE_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
    ${CMAKE_SOURCE_DIR}/data/ $<TARGET_FILE_DIR:${PROJECT_NAME}>)

