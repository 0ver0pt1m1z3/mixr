project(map)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

foreach(CONFIG ${CMAKE_CONFIGURATION_TYPES})
    string(TOUPPER ${CONFIG} CONFIG_UPPER)
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/bin)
endforeach()

file(GLOB RPF_SOURCES "./rpf/*.cpp")
file(GLOB RPF_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/rpf/*.hpp)

file(GLOB VPF_SOURCES "./vpf/*.cpp")
file(GLOB VPF_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/vpf/*.hpp)

# Combine all sources and headers
set(ALL_SOURCES
    ${RPF_SOURCES}
    ${VPF_SOURCES}
)

set(ALL_HEADERS
    ${RPF_HEADERS}
    ${VPF_HEADERS}
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
source_group("Source Files\\map\\rpf" FILES ${RPRFOM_SOURCES})
source_group("Source Files\\map\\vpf" FILES ${RPRFOM_SOURCES})

source_group("Header Files\\map\\rpf" FILES ${RPRFOM_HEADERS})
source_group("Header Files\\map\\vpf" FILES ${RPRFOM_HEADERS})

add_definitions(-DRTI_USES_STD_FSTREAM)
# Optional: Set folder property for the target in Visual Studio
set_target_properties(${PROJECT_NAME} PROPERTIES FOLDER "Map")