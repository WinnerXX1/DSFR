cmake_minimum_required(VERSION 3.13 FATAL_ERROR)

set(PROJECT_NAME DairyShoresFertileRivers)
project(${PROJECT_NAME})

set( SDL_STATIC ON CACHE BOOL "" FORCE )
set( SDL_SHARED OFF CACHE BOOL "" FORCE )

add_executable(${PROJECT_NAME} 
    src/ENGINE.c
)

set(SDL2_IMAGE_INCLUDE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/external/SDL2_image")
set(SDL2_IMAGE_LIB_DIR     "${CMAKE_CURRENT_SOURCE_DIR}/build/external/SDL2_image/Debug")

set(SDL2_TTF_INCLUDE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/external/SDL2_ttf")
set(SDL2_TTF_LIB_DIR     "${CMAKE_CURRENT_SOURCE_DIR}/build/external/SDL2_ttf/Debug")

set(SDL2_NET_INCLUDE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/external/SDL2_net")
set(SDL2_NET_LIB_DIR     "${CMAKE_CURRENT_SOURCE_DIR}/build/external/SDL2_net/Debug")

set(SDL2_MIXER_INCLUDE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/external/SDL2_mixer/include")
set(SDL2_MIXER_LIB_DIR     "${CMAKE_CURRENT_SOURCE_DIR}/build/external/SDL2_mixer/Debug")

add_subdirectory(external/SDL2)
target_link_libraries(${PROJECT_NAME} SDL2main SDL2-static SDL2_test)
add_definitions(-Dmain=SDL_main)

add_subdirectory(external/SDL2_image)
target_link_libraries(${PROJECT_NAME} SDL2_image)
INCLUDE_DIRECTORIES(${PROJECT_NAME}/external/SDL2_image)

set( BUILD_SHARED_LIBS OFF CACHE BOOL "" FORCE )
set( SDL2TTF_HARFBUZZ ON CACHE BOOL "" FORCE )
set( SDL2TTF_SAMPLES OFF CACHE BOOL "" FORCE )
set( SDL2TTF_VENDORED ON CACHE BOOL "" FORCE )
add_subdirectory(external/SDL2_ttf)
target_link_libraries(${PROJECT_NAME} SDL2_ttf)

set( BUILD_SHARED_LIBS OFF CACHE BOOL "" FORCE )
set( SDL2MIXER_SAMPLES OFF CACHE BOOL "" FORCE )
set( SDL2MIXER_VENDORED ON CACHE BOOL "" FORCE )
add_subdirectory(external/SDL2_mixer)
INCLUDE_DIRECTORIES(${PROJECT_NAME}/external/SDL2_mixer/external/opusfile/include)
target_link_libraries(${PROJECT_NAME} SDL2_mixer)

add_subdirectory(external/SDL2_net)
target_link_libraries(${PROJECT_NAME} SDL2_net)

set_target_properties(${PROJECT_NAME} PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin/)







