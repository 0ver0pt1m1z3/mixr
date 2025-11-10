project(recorder)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

foreach(CONFIG ${CMAKE_CONFIGURATION_TYPES})
    string(TOUPPER ${CONFIG} CONFIG_UPPER)
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/bin)
endforeach()

file(GLOB PB_SOURCES "./protobuf_v2/*.cpp")
file(GLOB PB_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/protobuf_v2/*.hpp)

file(GLOB PROTO_SOURCES "./protobuf_v2/proto/*.cpp")
file(GLOB PROTO_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/protobuf_v2/proto/*.hpp)

# Combine all sources and headers
set(ALL_SOURCES
    ${PB_SOURCES}
    ${PROTO_SOURCES}
)

set(ALL_HEADERS
    ${PB_HEADERS}
    ${PROTO_HEADERS}
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
source_group("Source Files\\recorder\\protobuf_v2" FILES ${PB_SOURCES})
source_group("Source Files\\recorder\\protobuf_v2\\proto" FILES ${PROTO_SOURCES})

source_group("Header Files\\recorder\\protobuf_v2" FILES ${PB_HEADERS})
source_group("Header Files\\recorder\\protobuf_v2\\proto" FILES ${PROTO_HEADERS})

add_definitions(-DRTI_USES_STD_FSTREAM)
# Optional: Set folder property for the target in Visual Studio
set_target_properties(${PROJECT_NAME} PROPERTIES FOLDER "recorder")