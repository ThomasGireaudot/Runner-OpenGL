cmake_minimum_required(VERSION 3.10)

# Set the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Add include directory
include_directories(include)

# Set the project name
project(Runner_OpenGL)

# Add the source files
file(GLOB_RECURSE SOURCES "src/*.cpp")

# Add executable
add_executable(${PROJECT_NAME} ${SOURCES})

# Find OpenGL
find_package(OpenGL REQUIRED)
target_link_libraries(${PROJECT_NAME} OpenGL::GL)

# Link GLFW (Window and Input Handling)
add_subdirectory(external/glfw)
target_link_libraries(${PROJECT_NAME} glfw)

# Link GLAD (OpenGL Function Loader)
add_subdirectory(external/glad)
target_link_libraries(${PROJECT_NAME} glad)

# Link GLM (Math library)
add_subdirectory(external/glm)
target_link_libraries(${PROJECT_NAME} glm)

if(WIN32)
    # Windows-specific configuration
    target_compile_definitions(${PROJECT_NAME} PRIVATE PLATFORM_WINDOWS)
elseif(UNIX)
    # Linux-specific configuration
    target_compile_definitions(${PROJECT_NAME} PRIVATE PLATFORM_LINUX)
endif()

