cmake_minimum_required(VERSION 3.10.0)

set(CMAKE_TOOLCHAIN_FILE "${CMAKE_CURRENT_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake")

project(gravity-sim VERSION 0.1.0 LANGUAGES C CXX)


file(GLOB_RECURSE SOURCE_FILES ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp)

add_executable(gravity-sim ${SOURCE_FILES})

function(set_output_dirs target)
set_target_properties(${target} PROPERTIES
RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/out/bin
LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/out/lib
ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/out/lib
)
endfunction()

find_package(glfw3 CONFIG REQUIRED)
find_package(GLEW CONFIG REQUIRED)
find_package(imgui CONFIG REQUIRED)

target_link_libraries(gravity-sim PRIVATE 
    GLEW::GLEW
    glfw
    imgui::imgui
)

set_output_dirs(gravity-sim)