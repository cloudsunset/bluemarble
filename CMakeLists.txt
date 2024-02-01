
cmake_minimum_required(VERSION 3.12)

project(BlueMarble)

add_executable(${CMAKE_PROJECT_NAME} "main.cpp" "Camera.cpp" "Camera.h")

find_package(OpenGL REQUIRED)
find_package(glfw3 CONFIG REQUIRED)
find_package(GLEW CONFIG REQUIRED)
find_package(glm CONFIG REQUIRED)

target_include_directories(${CMAKE_PROJECT_NAME} PRIVATE deps/stb)

target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE OpenGL::GL)
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE glfw)
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE GLEW::GLEW)
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE glm::glm)


add_custom_command(TARGET BlueMarble POST_BUILD
                   COMMAND ${CMAKE_COMMAND} -E create_symlink "${CMAKE_SOURCE_DIR}/shaders" "${CMAKE_BINARY_DIR}/shaders"
                   COMMAND ${CMAKE_COMMAND} -E create_symlink "${CMAKE_SOURCE_DIR}/textures" "${CMAKE_BINARY_DIR}/textures")