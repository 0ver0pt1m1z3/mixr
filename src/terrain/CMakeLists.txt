project(terrain)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

foreach(CONFIG ${CMAKE_CONFIGURATION_TYPES})
    string(TOUPPER ${CONFIG} CONFIG_UPPER)
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/bin)
endforeach()

file(GLOB TERRAIN_SOURCES "./*.cpp")
file(GLOB TERRAIN_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/*.hpp)

file(GLOB DED_SOURCES "./ded/*.cpp")
file(GLOB DED_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/ded/*.hpp)

file(GLOB DTED_SOURCES "./dted/*.cpp")
file(GLOB DTED_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/dted/*.hpp)

file(GLOB SRTM_SOURCES "./srtm/*.cpp")
file(GLOB SRTM_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/srtm/*.hpp)

# Combine all sources and headers
set(ALL_SOURCES
    ${TERRAIN_SOURCES}
    ${DED_SOURCES}
    ${DTED_SOURCES}
    ${SRTM_SOURCES}
)

set(ALL_HEADERS
    ${TERRAIN_HEADERS}
    ${DED_HEADERS}
    ${DTED_HEADERS}
    ${SRTM_HEADERS}
)

# Create the library
add_library(${PROJECT_NAME} ${ALL_SOURCES} ${ALL_HEADERS})

# Add include directories - fix the path
target_include_directories(${PROJECT_NAME}
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
        ${CMAKE_SOURCE_DIR}/dependencies/include
)

# Organize files in Visual Studio solution explorer
source_group("Source Files" FILES ${TERRAIN_SOURCES})
source_group("Source Files\\ded" FILES ${DED_SOURCES})
source_group("Source Files\\dted" FILES ${DTED_SOURCES})
source_group("Source Files\\srtm" FILES ${SRTM_SOURCES})

source_group("Header Files" FILES ${TERRAIN_SOURCES})
source_group("Header Files\\ded" FILES ${DED_SOURCES})
source_group("Header Files\\dted" FILES ${DTED_SOURCES})
source_group("Header Files\\srtm" FILES ${SRTM_SOURCES})

# Optional: Set folder property for the target in Visual Studio
set_target_properties(${PROJECT_NAME} PROPERTIES FOLDER "Terrain")