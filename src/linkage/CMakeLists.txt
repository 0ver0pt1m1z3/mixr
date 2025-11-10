project(linkage)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

foreach(CONFIG ${CMAKE_CONFIGURATION_TYPES})
    string(TOUPPER ${CONFIG} CONFIG_UPPER)
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/bin)
endforeach()

file(GLOB LINKAGE_SOURCES "./*.cpp")
file(GLOB LINKAGE_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/*.hpp)

file(GLOB ADAPTERS_SOURCES "./adapters/*.cpp")
file(GLOB ADAPTERS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/adapters/*.hpp)

file(GLOB GENERATORS_SOURCES "./generators/*.cpp")
file(GLOB GENERATORS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/generators/*.hpp)

file(GLOB PLATFORM_SOURCES "./paltforms/*.cpp")
file(GLOB PLATFORM_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/platforms/*.hpp)

# Combine all sources and headers
set(ALL_SOURCES
    ${LINKAGE_SOURCES}
    ${ADAPTERS_SOURCES}
    ${GENERATORS_SOURCES}
    ${PLATFORM_SOURCES}
)

set(ALL_HEADERS
    ${LINKAGE_HEADERS}
    ${ADAPTERS_HEADERS}
    ${GENERATORS_HEADERS}
    ${PLATFORM_HEADERS}
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
source_group("Source Files" FILES ${LINKAGE_SOURCES})
source_group("Source Files\\adapters" FILES ${ADAPTERS_SOURCES})
source_group("Source Files\\generators" FILES ${GENERATORS_SOURCES})
source_group("Source Files\\platform" FILES ${PLATFORM_SOURCES})

source_group("Header Files" FILES ${LINKAGE_HEADERS})
source_group("Header Files\\adapters" FILES ${ADAPTERS_HEADERS})
source_group("Header Files\\generators" FILES ${GENERATORS_HEADERS})
source_group("Header Files\\platform" FILES ${PLATFORM_HEADERS})

# Optional: Set folder property for the target in Visual Studio
set_target_properties(${PROJECT_NAME} PROPERTIES FOLDER "Linkage")