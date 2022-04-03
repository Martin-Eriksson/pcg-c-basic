cmake_minimum_required(VERSION 3.23.0)
project(pcg-c-basic DESCRIPTION "pcg-c-basic"
                    LANGUAGES C)

add_library(${PROJECT_NAME} STATIC)
target_sources(${PROJECT_NAME} PUBLIC
    pcg_basic.c
)
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
set_target_properties(${PROJECT_NAME} PROPERTIES C_STANDARD 11 C_STANDARD_REQUIRED ON C_EXTENSIONS OFF)
if(MSVC AND NOT (CMAKE_C_COMPILER_FRONTEND_VARIANT STREQUAL "GNU"))
    target_compile_options(${PROJECT_NAME} PRIVATE /W4 /wd4456)
else()
    target_compile_options(${PROJECT_NAME} PRIVATE -Wall -pedantic -Werror=vla)
endif()
