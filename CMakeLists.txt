cmake_minimum_required(VERSION 3.10)
project(name VERSION 0.1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_program(MOLD "mold")
if (NOT DEFINED MOLD)
    message(FATAL_ERROR "mold linker not found")
else()
    set(CMAKE_CXX_FLAGS "-fuse-ld=mold")
    message(STATUS "linker: mold")
endif()

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

if (DEBUG)
    add_compile_options(-g3 -ggdb)
    add_compile_definitions(DEBUG)
endif()

if (DOCS)
    add_subdirectory(docs)
endif()

# set(EXEC exec_name)
# set(SRC main.cpp)

# add_executable(${EXEC} ${SRC})
# target_link_libraries(${EXEC} ${CONAN_LIBS})
