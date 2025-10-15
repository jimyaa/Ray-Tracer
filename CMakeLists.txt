cmake_minimum_required(VERSION 3.16)
project(RayTracer)
set(CMAKE_CXX_STANDARD 17)

# Find dependencies
find_package(PNG REQUIRED)
find_package(imgui CONFIG REQUIRED)
find_package(glfw3 CONFIG REQUIRED)
find_package(glad  CONFIG REQUIRED)

# Pick up all .cpp sources (auto-detect new ones)
file(GLOB_RECURSE SOURCES CONFIGURE_DEPENDS src/*.cpp)

# (Optional) Include headers for IDE visibility
file(GLOB_RECURSE HEADERS CONFIGURE_DEPENDS src/*.h)

# Define executable first!
add_executable(RayTracer
    ${SOURCES}
    ${HEADERS}
)

# Include directories (so your includes like "camera.h" work)
target_include_directories(RayTracer PRIVATE
    $<TARGET_PROPERTY:imgui::imgui,INTERFACE_INCLUDE_DIRECTORIES>
    $<TARGET_PROPERTY:glad::glad,INTERFACE_INCLUDE_DIRECTORIES>
    ${VCPKG_INSTALLED_DIR}/${VCPKG_TARGET_TRIPLET}/include
    ${CMAKE_CURRENT_SOURCE_DIR}/src
    ${CMAKE_CURRENT_SOURCE_DIR}/src/core
    ${CMAKE_CURRENT_SOURCE_DIR}/src/image
    ${CMAKE_CURRENT_SOURCE_DIR}/src/image/external
    ${CMAKE_CURRENT_SOURCE_DIR}/src/materials
    ${CMAKE_CURRENT_SOURCE_DIR}/src/materials/textures
    ${CMAKE_CURRENT_SOURCE_DIR}/src/materials/volumes
    ${CMAKE_CURRENT_SOURCE_DIR}/src/objects/primatives
    ${CMAKE_CURRENT_SOURCE_DIR}/src/objects
    ${CMAKE_CURRENT_SOURCE_DIR}/src/acceleration
)

# Link libraries (AFTER defining the target)
target_link_libraries(RayTracer PRIVATE imgui::imgui PNG::PNG)

target_compile_definitions(RayTracer PRIVATE IMGUI_IMPL_OPENGL_LOADER_GLAD)

target_link_libraries(RayTracer PRIVATE
  imgui::imgui
  glfw
  glad::glad
  PNG::PNG
  opengl32
)