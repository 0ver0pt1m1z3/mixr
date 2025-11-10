project(graphics)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

foreach(CONFIG ${CMAKE_CONFIGURATION_TYPES})
    string(TOUPPER ${CONFIG} CONFIG_UPPER)
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/bin)
endforeach()

file(GLOB GRAPHICS_SOURCES "./*.cpp")
file(GLOB GRAPHICS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/graphics/*.hpp)

file(GLOB FONTS_SOURCES "./fonts/*.cpp")
file(GLOB FONTS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/graphics/fonts/*.hpp)

file(GLOB READOUTS_SOURCES "./readouts/*.cpp")
file(GLOB READOUTS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/graphics/readouts/*.hpp)

file(GLOB FTGL_SOURCES "./fonts/ftgl/*.cpp")
file(GLOB FTGL_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/graphics/fonts/ftgl/*.hpp)

# Combine all sources and headers
set(ALL_SOURCES
    ${GRAPHICS_SOURCES}
    ${FONTS_SOURCES}
    ${READOUTS_SOURCES}
    ${FTGL_SOURCES}
)

set(ALL_HEADERS
    ${GRAPHICS_HEADERS}
    ${FONTS_HEADERS}
    ${READOUTS_HEADERS}
    ${FTGL_HEADERS}
)

# Create the library
add_library(graphics ${ALL_SOURCES} ${ALL_HEADERS})

# Add include directories - fix the path
target_include_directories(graphics
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
        ${CMAKE_SOURCE_DIR}/dependencies/include
        ${CMAKE_SOURCE_DIR}/dependencies/include/freetype2
)

# Organize files in Visual Studio solution explorer
source_group("Source Files" FILES ${GRAPHICS_SOURCES})
source_group("Source Files\\fonts" FILES ${FONTS_SOURCES})
source_group("Source Files\\fonts\\ftgl" FILES ${FTGL_SOURCES})
source_group("Source Files\\readouts" FILES ${READOUTS_SOURCES})

source_group("Header Files" FILES ${GRAPH_HEADERS})
source_group("Header Files\\fonts" FILES ${FONTS_HEADERS})
source_group("Header Files\\fonts\\ftgl" FILES ${FTGL_HEADERS})
source_group("Header Files\\readouts" FILES ${READOUTS_HEADERS})


# Optional: Set folder property for the target in Visual Studio
set_target_properties(graphics PROPERTIES FOLDER "Graphics")