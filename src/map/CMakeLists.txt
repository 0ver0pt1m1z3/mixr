cmake_minimum_required(VERSION 3.15)
project(map VERSION 1.0.0 LANGUAGES CXX)

# Output directories
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

foreach(CONFIG ${CMAKE_CONFIGURATION_TYPES})
    string(TOUPPER ${CONFIG} CONFIG_UPPER)
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/bin)
endforeach()

set(SRC_BASE ${CMAKE_CURRENT_SOURCE_DIR})

# ──────────────────────────────────────────────────────────────
# RPF LIBRARY
# ──────────────────────────────────────────────────────────────
file(GLOB RPF_SOURCES "${SRC_BASE}/rpf/*.cpp")
file(GLOB RPF_HEADERS "${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/rpf/*.hpp"
                      "${SRC_BASE}/rpf/*.hpp")

add_library(${PROJECT_NAME}_rpf STATIC ${RPF_SOURCES} ${RPF_HEADERS})

target_include_directories(${PROJECT_NAME}_rpf
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
        ${CMAKE_SOURCE_DIR}/../mixr-3rdparty/include
    PRIVATE
        ${SRC_BASE}
)

source_group(TREE ${CMAKE_SOURCE_DIR} FILES ${RPF_SOURCES} ${RPF_HEADERS})

set_target_properties(${PROJECT_NAME}_rpf PROPERTIES
    FOLDER "Map"
    OUTPUT_NAME "mixr_map_rpf"
    OUTPUT_NAME_DEBUG "mixr_map_rpf_d"
)

# ──────────────────────────────────────────────────────────────
# VPF LIBRARY
# ──────────────────────────────────────────────────────────────
file(GLOB VPF_SOURCES "${SRC_BASE}/vpf/*.cpp")
file(GLOB VPF_HEADERS "${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/vpf/*.hpp"
                      "${SRC_BASE}/vpf/*.hpp")

add_library(${PROJECT_NAME}_vpf STATIC ${VPF_SOURCES} ${VPF_HEADERS})

target_include_directories(${PROJECT_NAME}_vpf
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
        ${CMAKE_SOURCE_DIR}/../mixr-3rdparty/include
    PRIVATE
        ${SRC_BASE}
)

source_group(TREE ${CMAKE_SOURCE_DIR} FILES ${VPF_SOURCES} ${VPF_HEADERS})

set_target_properties(${PROJECT_NAME}_vpf PROPERTIES
    FOLDER "Map"
    OUTPUT_NAME "mixr_map_vpf"
    OUTPUT_NAME_DEBUG "mixr_map_vpf_d"
)

# Optional: Required compiler flag
add_definitions(-DRTI_USES_STD_FSTREAM)
