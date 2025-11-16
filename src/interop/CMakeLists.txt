
project(interop VERSION 1.0.0 LANGUAGES CXX)

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
set(INC_BASE ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME})

#─────────────────────────────────────────────────────────────────────────────
# COMMON (mixr_interop)
#─────────────────────────────────────────────────────────────────────────────
file(GLOB COMMON_SOURCES "${SRC_BASE}/common/*.cpp")
file(GLOB COMMON_HEADERS "${INC_BASE}/*.hpp" "${SRC_BASE}/common/*.hpp")

add_library(mixr_${PROJECT_NAME} STATIC ${COMMON_SOURCES} ${COMMON_HEADERS})

target_include_directories(mixr_${PROJECT_NAME}
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
        ${CMAKE_SOURCE_DIR}/../mixr-3rdparty/include
)

source_group(TREE ${CMAKE_SOURCE_DIR} FILES ${COMMON_SOURCES} ${COMMON_HEADERS})

set_target_properties(mixr_${PROJECT_NAME} PROPERTIES
    FOLDER "Interop"
    OUTPUT_NAME "mixr_interop"
    OUTPUT_NAME_DEBUG "mixr_interop_d"
)

#─────────────────────────────────────────────────────────────────────────────
# DIS (mixr_interop_dis)
#─────────────────────────────────────────────────────────────────────────────
file(GLOB DIS_SOURCES "${SRC_BASE}/dis/*.cpp")
file(GLOB DIS_HEADERS "${INC_BASE}/dis/*.hpp" "${SRC_BASE}/dis/*.hpp")

add_library(mixr_${PROJECT_NAME}_dis STATIC ${DIS_SOURCES} ${DIS_HEADERS})

target_include_directories(mixr_${PROJECT_NAME}_dis
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
        ${CMAKE_SOURCE_DIR}/../mixr-3rdparty/include
)

source_group(TREE ${CMAKE_SOURCE_DIR} FILES ${DIS_SOURCES} ${DIS_HEADERS})

set_target_properties(mixr_${PROJECT_NAME}_dis PROPERTIES
    FOLDER "Interop"
    OUTPUT_NAME "mixr_interop_dis"
    OUTPUT_NAME_DEBUG "mixr_interop_dis_d"
)

#─────────────────────────────────────────────────────────────────────────────
# HLA (mixr_interop_hla)
#─────────────────────────────────────────────────────────────────────────────
file(GLOB HLA_SOURCES "${SRC_BASE}/hla/*.cpp")
file(GLOB HLA_HEADERS "${INC_BASE}/hla/*.hpp" "${SRC_BASE}/hla/*.hpp")

add_library(mixr_${PROJECT_NAME}_hla STATIC ${HLA_SOURCES} ${HLA_HEADERS})

target_include_directories(mixr_${PROJECT_NAME}_hla
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
        ${CMAKE_SOURCE_DIR}/../mixr-3rdparty/include
        ${CMAKE_SOURCE_DIR}/../mixr-3rdparty/include/portico/hla13
)

source_group(TREE ${CMAKE_SOURCE_DIR} FILES ${HLA_SOURCES} ${HLA_HEADERS})

set_target_properties(mixr_${PROJECT_NAME}_hla PROPERTIES
    FOLDER "Interop"
    OUTPUT_NAME "mixr_interop_hla"
    OUTPUT_NAME_DEBUG "mixr_interop_hla_d"
)

#─────────────────────────────────────────────────────────────────────────────
# RPRFOM (mixr_interop_rprfom)
#─────────────────────────────────────────────────────────────────────────────
file(GLOB RPR_SOURCES "${SRC_BASE}/rprfom/*.cpp")
file(GLOB RPR_HEADERS "${INC_BASE}/hla/rprfom/*.hpp" "${SRC_BASE}/rprfom/*.hpp")

add_library(mixr_${PROJECT_NAME}_rprfom STATIC ${RPR_SOURCES} ${RPR_HEADERS})

target_include_directories(mixr_${PROJECT_NAME}_rprfom
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
        ${CMAKE_SOURCE_DIR}/../mixr-3rdparty/include
        ${CMAKE_SOURCE_DIR}/../mixr-3rdparty/include/portico/hla13
)

source_group(TREE ${CMAKE_SOURCE_DIR} FILES ${RPR_SOURCES} ${RPR_HEADERS})

set_target_properties(mixr_${PROJECT_NAME}_rprfom PROPERTIES
    FOLDER "Interop"
    OUTPUT_NAME "mixr_interop_rprfom"
    OUTPUT_NAME_DEBUG "mixr_interop_rprfom_d"
)

# Global define used in all
add_definitions(-DRTI_USES_STD_FSTREAM)
