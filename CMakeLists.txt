cmake_minimum_required(VERSION 3.16)
project(Chip8 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(SDL2 CONFIG REQUIRED)

add_executable(chip8 main.cpp)
target_link_libraries(chip8 PRIVATE SDL2::SDL2)

if(WIN32)
    add_custom_command(TARGET chip8 POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_if_different
            "$<TARGET_FILE:SDL2::SDL2>"
            "$<TARGET_FILE_DIR:chip8>"
    )
endif()