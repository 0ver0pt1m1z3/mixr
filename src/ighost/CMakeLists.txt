cmake_minimum_required(VERSION 3.15)
project(ighost VERSION 1.0.0 LANGUAGES CXX)

# C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

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

# Base source folder for convenience
set(SRC_BASE ${CMAKE_CURRENT_SOURCE_DIR})

# ──────────────────────────────────────────────────────────────
# CIGI LIBRARY FILES
# ──────────────────────────────────────────────────────────────

# Non-session sources (top folder only)
file(GLOB CIGI_SOURCES_NO_SESSION "${SRC_BASE}/cigi/*.cpp")
file(GLOB CIGI_HEADERS_NO_SESSION "${CMAKE_SOURCE_DIR}/include/mixr/ighost/cigi/*.hpp")

# Session files (explicit because recursive must include .hpp in src)
file(GLOB SESSION_SOURCES "${SRC_BASE}/cigi/session/*.cpp")
file(GLOB SESSION_HEADERS 
    "${CMAKE_SOURCE_DIR}/include/mixr/ighost/cigi/session/*.hpp"
    "${SRC_BASE}/cigi/session/*.hpp"
)

set(ALL_CIGI_SOURCES ${CIGI_SOURCES_NO_SESSION} ${SESSION_SOURCES})
set(ALL_CIGI_HEADERS ${CIGI_HEADERS_NO_SESSION} ${SESSION_HEADERS})

add_library(ighost_cigi STATIC ${ALL_CIGI_SOURCES} ${ALL_CIGI_HEADERS})

target_include_directories(ighost_cigi
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
        ${CMAKE_SOURCE_DIR}/../mixr-3rdparty/include
    PRIVATE
        ${SRC_BASE}
)

# Automatic VS folder layout
source_group(TREE ${CMAKE_SOURCE_DIR} FILES ${ALL_CIGI_SOURCES} ${ALL_CIGI_HEADERS})

set_target_properties(ighost_cigi PROPERTIES 
    FOLDER "IGhost"
    OUTPUT_NAME "mixr_ighost_cigi"
    OUTPUT_NAME_DEBUG "mixr_ighost_cigi_d"
)

# ──────────────────────────────────────────────────────────────
# POV LIBRARY FILES
# ──────────────────────────────────────────────────────────────

file(GLOB_RECURSE POV_SOURCES "${SRC_BASE}/pov/*.cpp")
file(GLOB_RECURSE POV_HEADERS
    "${CMAKE_SOURCE_DIR}/include/mixr/ighost/pov/*.hpp"
    "${SRC_BASE}/pov/*.hpp"
)

add_library(ighost_pov STATIC ${POV_SOURCES} ${POV_HEADERS})

target_include_directories(ighost_pov
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
        ${CMAKE_SOURCE_DIR}/../mixr-3rdparty/include
    PRIVATE
        ${SRC_BASE}
)

# Link CIGI if required
# target_link_libraries(ighost_pov PUBLIC ighost_cigi)

# Automatic VS folder layout
source_group(TREE ${CMAKE_SOURCE_DIR} FILES ${POV_SOURCES} ${POV_HEADERS})

set_target_properties(ighost_pov PROPERTIES 
    FOLDER "IGhost"
    OUTPUT_NAME "mixr_ighost_pov"
    OUTPUT_NAME_DEBUG "mixr_ighost_pov_d"
)
