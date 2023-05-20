cmake_minimum_required(VERSION 3.24)
project(learnOpengl)

set(CMAKE_CXX_STANDARD 17)
# 检查环境变量
if (NOT DEFINED ENV{GLFW_HOME})
message(FATAL_ERROR "found no env named GLFW_HOME")
endif()
if (NOT DEFINED ENV{GLAD_HOME})
message(FATAL_ERROR "found no env named GLAD_HOME")
endif()

# 暂存环境变量
set(GLFW_HOME $ENV{GLFW_HOME})
set(GLAD_HOME $ENV{GLAD_HOME})

# 设置头文件目录
include_directories("${GLFW_HOME}/include")
include_directories("${GLAD_HOME}/include")
include_directories("/opt/homebrew/Cellar/glm/0.9.9.8/include")

# 添加 GLFW3 预编译库
add_library(glfw SHARED IMPORTED lib/glad.c)
SET_TARGET_PROPERTIES(glfw PROPERTIES IMPORTED_LOCATION "${GLFW_HOME}/lib/libglfw.3.dylib")


# 创建可执行文件
add_executable(learnOpengl light_maps.cpp "lib/glad.c" shader_s.h stb_image.h include/camera.h)

# 链接 GLFW GLAD OpenGL
target_link_libraries(learnOpengl glfw "-framework OpenGL")