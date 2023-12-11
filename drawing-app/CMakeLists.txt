cmake_minimum_required(VERSION 3.28)

project(drawing-app LANGUAGES CXX)

# Default to C++ extensions being off. Clang's modules support have trouble
# with extensions right now and it is not required for any other compiler

set(CMAKE_CXX_STANDARD 20)

add_library(std_lib)

target_sources(std_lib
  PUBLIC
    FILE_SET CXX_MODULES FILES
    std.cxx
)

add_library(singleton_lib)

target_sources(singleton_lib
  PUBLIC
    FILE_SET CXX_MODULES FILES
    Singleton.cxx
)

add_library(factory_lib)

target_sources(factory_lib
  PUBLIC
    FILE_SET CXX_MODULES FILES
    Factory.cxx
)

target_link_libraries(factory_lib PUBLIC std_lib singleton_lib)

add_library(drawing_lib)

target_sources(drawing_lib
  PUBLIC
    FILE_SET CXX_MODULES FILES
    Shapes.cxx
    Shape-Factory.cxx
    Shapes-Point.cxx
    Shapes-Base.cxx
    Shapes-Square.cxx
    Shapes-Rectangle.cxx
)

target_link_libraries(drawing_lib PUBLIC std_lib factory_lib)

add_executable(drawing_app DrawingApp.cpp)
target_link_libraries(drawing_app PRIVATE drawing_lib)