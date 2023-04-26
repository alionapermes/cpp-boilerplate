cmake_minimum_required(VERSION 3.10)
project(name VERSION 0.1.0 LANGUAGES CXX)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_program(MOLD NAMES "mold")
if (NOT DEFINED ${MOLD-NOTFOUND})
    set(CMAKE_CXX_FLAGS "-fuse-ld=mold")
else()
    message(FATAL_ERROR "mold linker not found")
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
#
# add_executable(${EXEC} ${SRC})
# target_link_libraries(${EXEC} ${CONAN_LIBS})

