project(interop)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

foreach(CONFIG ${CMAKE_CONFIGURATION_TYPES})
    string(TOUPPER ${CONFIG} CONFIG_UPPER)
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/bin)
endforeach()

file(GLOB INTEROP_SOURCES "./*.cpp")
file(GLOB INTEROP_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/*.hpp)

file(GLOB HLA_SOURCES "./hla/*.cpp")
file(GLOB HLA_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/hla/*.hpp)

file(GLOB DIS_SOURCES "./dis/*.cpp")
file(GLOB DIS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/dis/*.hpp)

file(GLOB RPRFOM_SOURCES "./hla/rprfom/*.cpp")
file(GLOB RPRFOM_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/hla/rprfom/*.hpp)

# Combine all sources and headers
set(ALL_SOURCES
    ${INTEROP_SOURCES}
    ${HLA_SOURCES}
    ${DIS_SOURCES}
    ${RPRFOM_SOURCES}
)

set(ALL_HEADERS
    ${INTEROP_HEADERS}
    ${HLA_HEADERS}
    ${DIS_HEADERS}
    ${RPRFOM_HEADERS}
)

# Create the library
add_library(${PROJECT_NAME} ${ALL_SOURCES} ${ALL_HEADERS})

# Add include directories - fix the path
target_include_directories(${PROJECT_NAME}
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
        ${CMAKE_SOURCE_DIR}/dependencies/include
        ${CMAKE_SOURCE_DIR}/dependencies/include/portico/hla13
)

# Organize files in Visual Studio solution explorer
source_group("Source Files" FILES ${INTEROP_SOURCES})
source_group("Source Files\\hla" FILES ${HLA_SOURCES})
source_group("Source Files\\hla\\rprfom" FILES ${RPRFOM_SOURCES})
source_group("Source Files\\dis" FILES ${DIS_SOURCES})

source_group("Header Files" FILES ${INTEROP_HEADERS})
source_group("Header Files\\hla" FILES ${HLA_HEADERS})
source_group("Header Files\\hla\\rprfom" FILES ${RPRFOM_HEADERS})
source_group("Header Files\\dis" FILES ${DIS_HEADERS})

add_definitions(-DRTI_USES_STD_FSTREAM)
# Optional: Set folder property for the target in Visual Studio
set_target_properties(${PROJECT_NAME} PROPERTIES FOLDER "Interop")