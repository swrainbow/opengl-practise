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
include_directories("/opt/homebrew/Cellar/assimp/5.2.5/include/")

# 添加 GLFW3 预编译库
add_library(glfw SHARED IMPORTED lib/glad.c)

SET_TARGET_PROPERTIES(glfw PROPERTIES IMPORTED_LOCATION "${GLFW_HOME}/lib/libglfw.3.dylib")
#SET_TARGET_PROPERTIES(assimp PROPERTIES IMPORTED_LOCATION "/opt/homebrew/Cellar/assimp/5.2.5/lib/libassimp.5.2.4.dylib")



# 创建可执行文件
add_executable(learnOpengl
#        light_cast.cpp
#        model_import.cpp
#        blending.cpp
#        framebuffer.cpp
#        cube.cpp
#        point.cpp
#        gemotery.cpp
#        instance2.cpp
#        asteroids_instanced.cpp
#        advanced_lighting.cpp
#        gamma.cpp
#        shadow.cpp
#        normal_mapping.cpp
#        hdr.cpp
#        bloom.cpp
        deferred_shading.cpp
        "lib/glad.c"
        shader_s.h
        stb_image.h
        include/camera.h
        include/model.h include/mesh.h)

# 链接 GLFW GLAD OpenGL
target_link_libraries(learnOpengl glfw "-framework OpenGL")
set(CMAKE_LIBRARY_PATH /opt/homebrew/Cellar/assimp/5.2.5/lib)

find_package(assimp REQUIRED) # 添加assimp
target_link_libraries(learnOpengl assimp::assimp)
