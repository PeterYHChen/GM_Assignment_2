cmake_minimum_required(VERSION 3.1)
project(ex2)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

# libigl options: choose between header only and compiled static library
# Header-only is preferred for small projects. For larger projects the static build
# considerably reduces the compilation times
option(LIBIGL_USE_STATIC_LIBRARY "Use LibIGL as static library" OFF)

# add a customizable menu bar
option(LIBIGL_WITH_NANOGUI     "Use Nanogui menu"   ON)

# libigl options: choose your dependencies (by default everything is OFF except opengl) 
option(LIBIGL_WITH_VIEWER      "Use OpenGL viewer"  ON)
option(LIBIGL_WITH_OPENGL      "Use OpenGL"         ON)
option(LIBIGL_WITH_OPENGL_GLFW "Use GLFW"           ON)
option(LIBIGL_WITH_BBW         "Use BBW"            OFF)
option(LIBIGL_WITH_EMBREE      "Use Embree"         OFF)
option(LIBIGL_WITH_PNG         "Use PNG"            OFF)
option(LIBIGL_WITH_TETGEN      "Use Tetgen"         OFF)
option(LIBIGL_WITH_TRIANGLE    "Use Triangle"       OFF)
option(LIBIGL_WITH_XML         "Use XML"            OFF)
option(LIBIGL_WITH_LIM         "Use LIM"            OFF)
option(LIBIGL_WITH_COMISO      "Use CoMiso"         OFF)
option(LIBIGL_WITH_MATLAB      "Use Matlab"         OFF) # This option is not supported yet
option(LIBIGL_WITH_MOSEK       "Use MOSEK"          OFF) # This option is not supported yet
option(LIBIGL_WITH_CGAL        "Use CGAL"           OFF)


find_package(LIBIGL QUIET)


# Prepare the build environment

# Add your project files
# Note: we need some stubs for building to succeed on TravisCI.
if (TRAVISCI_BUILD)
    FILE(GLOB SOURCES src/*.cpp src_travisci/*.cpp)
else (TRAVISCI_BUILD)
    FILE(GLOB SOURCES src/*.cpp)
endif (TRAVISCI_BUILD)

add_executable(${PROJECT_NAME}_bin ${SOURCES} ${LIBIGL_EXTRA_SOURCES})
target_link_libraries(${PROJECT_NAME}_bin igl::core igl::viewer)
