cmake_minimum_required(VERSION 3.27)
project(OpenGL)

set(CMAKE_CXX_STANDARD 20)

set(GLEW_DIR ${CMAKE_SOURCE_DIR}/Dependencies/glew)
set(GLFW_DIR ${CMAKE_SOURCE_DIR}/Dependencies/glfw)

file(COPY ${GLEW_DIR}/lib/Release/x64/ DESTINATION ${CMAKE_BINARY_DIR})
file(COPY ${GLFW_DIR}/x64/lib-vc2022/ DESTINATION ${CMAKE_BINARY_DIR})

#define .h files
include_directories(${CMAKE_SOURCE_DIR}/OpenGL/Headers)
include_directories(${GLEW_DIR}/include)
include_directories(${GLFW_DIR}/x64/include)

#define .cpp files
file(GLOB SOURCES ${CMAKE_SOURCE_DIR}/OpenGL/Source/*.cpp)

# define .cpp files as executable
add_executable(${PROJECT_NAME} ${SOURCES})
add_definitions(-DGLEW_STATIC)
target_link_libraries(${PROJECT_NAME}
    ${GLEW_DIR}/lib/Release/x64/glew32s.lib
    ${GLFW_DIR}/x64/lib-vc2022/glfw3.lib
    opengl32.lib)
