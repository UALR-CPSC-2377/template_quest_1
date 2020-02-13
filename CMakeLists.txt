cmake_minimum_required(VERSION 3.10)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")

project(castlevania)

find_package(SDL2 REQUIRED)
find_package(SDL2_image REQUIRED)

set(CMAKE_CXX_FLAGS "-ggdb")

include_directories(
    ${PROJECT_SOURCE_DIR}/include
    ${SDL2_INCLUDE_DIRS}
    ${SDL2_IMAGE_INCLUDE_DIRS}
)

add_executable(castlevania
    ${PROJECT_SOURCE_DIR}/source/main.cpp
    ${PROJECT_SOURCE_DIR}/source/engine.cpp
    ${PROJECT_SOURCE_DIR}/source/GUI.cpp
    ${PROJECT_SOURCE_DIR}/source/Texture.cpp
)

target_link_libraries(castlevania
    ${SDL2_LIBRARIES}
    ${SDL2_IMAGE_LIBRARIES}
)

add_custom_command(
    TARGET castlevania
    POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
                ${CMAKE_SOURCE_DIR}/assets/
                ${CMAKE_CURRENT_BINARY_DIR}/Assets/
    COMMAND ${CMAKE_COMMAND} -E echo "Finished Copying Assets"
)
