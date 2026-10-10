cmake_minimum_required(VERSION 3.16)
project(NewChip8 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(SDL2_ROOT
    "C:/Users/georg/Downloads/SDL2-devel-2.32.10-mingw/SDL2-2.32.10/x86_64-w64-mingw32"
)

add_executable(chip8 main.cpp)

target_include_directories(chip8 PRIVATE "${SDL2_ROOT}/include")
target_link_libraries(chip8 PRIVATE "${SDL2_ROOT}/lib/libSDL2.dll.a")

add_custom_command(TARGET chip8 POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
        "${SDL2_ROOT}/bin/SDL2.dll"
        "$<TARGET_FILE_DIR:chip8>"
)