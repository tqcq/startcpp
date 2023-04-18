cmake_minimum_required(VERSION 3.18)
project(startcpp LANGUAGES C CXX VERSION 0.1.0)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED true)
set(CMAKE_CXX_EXTENSIONS false)

include_directories("${CMAKE_CURRENT_SOURCE_DIR}/third_party/rxcpp/Rx/v2/src")
include_directories("${CMAKE_CURRENT_SOURCE_DIR}/third_party/imgui")
include_directories("${CMAKE_CURRENT_SOURCE_DIR}/third_party/imgui/backends")
include_directories("${CMAKE_CURRENT_SOURCE_DIR}/third_party/glfw/include")

add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/third_party/glfw/")
# add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/third_party/libuv/")

add_library(imgui STATIC
    "${CMAKE_CURRENT_SOURCE_DIR}/third_party/imgui/imgui.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/third_party/imgui/imgui_demo.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/third_party/imgui/imgui_draw.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/third_party/imgui/imgui_tables.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/third_party/imgui/imgui_widgets.cpp"
)

target_include_directories(imgui
    PUBLIC
        "${CMAKE_CURRENT_SOURCE_DIR}/third_party/imgui/"
        "${CMAKE_CURRENT_SOURCE_DIR}/third_party/imgui/backends"
)
target_link_libraries(imgui
    PRIVATE
        glfw
        "-framework OpenGL"
)

if (APPLE)
target_sources(imgui 
    PRIVATE
        "${CMAKE_CURRENT_SOURCE_DIR}/third_party/imgui/backends/imgui_impl_opengl3.cpp"
        "${CMAKE_CURRENT_SOURCE_DIR}/third_party/imgui/backends/imgui_impl_glfw.cpp"
)

target_link_libraries(imgui
    PRIVATE
        "-framework OpenGL"
)
endif(APPLE)

add_executable(startcpp "")
target_include_directories(startcpp
    PRIVATE
        include)
target_sources(startcpp
    PRIVATE
        src/main.cpp
)
target_link_libraries(startcpp
    PRIVATE
        imgui
)