cmake_minimum_required(VERSION 3.0 FATAL_ERROR)
project(antivirus-fs VERSION 0.0.1 LANGUAGES C)


set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -D_FILE_OFFSET_BITS=64")
set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -Wall --pedantic -g")

set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/CMake" ${CMAKE_MODULE_PATH})
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

set(CMAKE_EXPORT_COMPILE_COMMANDS 1)


add_executable(antivirus-fs main.c)


find_package(PkgConfig)
if(PKG_CONFIG_FOUND)
    pkg_check_modules(FUSE3 "fuse3")
    if(FUSE3_FOUND)
        include_directories(${FUSE3_INCLUDE_DIR})
        target_link_libraries(antivirus-fs ${FUSE3_LIBRARIES})
        add_definitions(${FUSE3_CFLAGS} ${FUSE3_CFLAGS_OTHER})
    endif()
endif()