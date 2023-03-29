cmake_minimum_required(VERSION 3.10)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(CMAKE_CXX_STANDARD 17)

if (APPLE)
    set(CMAKE_CXX_FLAGS "-framework Cocoa -framework IOKit")
    # -framework OpenGL -framework CoreVideo
    add_compile_definitions(GL_SILENCE_DEPRECATION)
endif ()

project(OpenGL)

# include_directories("./glad/include")

add_executable(${CMAKE_PROJECT_NAME} application.cc)

find_package(OpenGL REQUIRED)

find_package(glfw3 3.3 REQUIRED)

target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE OpenGL::GL)

target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE glfw)

find_package(PkgConfig REQUIRED)

pkg_check_modules(glew glew REQUIRED IMPORTED_TARGET)

target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE PkgConfig::glew)

