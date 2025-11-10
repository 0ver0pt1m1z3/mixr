project(ighost)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

foreach(CONFIG ${CMAKE_CONFIGURATION_TYPES})
    string(TOUPPER ${CONFIG} CONFIG_UPPER)
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/bin)
endforeach()

file(GLOB IGHOST_SOURCES "./*.cpp")
file(GLOB IGHOST_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/ighost/*.hpp)

file(GLOB CIGI_SOURCES "./cigi/*.cpp")
file(GLOB CIGI_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/ighost/cigi/*.hpp)

file(GLOB SESSION_SOURCES "./cigi/session/*.cpp")
file(GLOB SESSION_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/ighost/cigi/session/*.hpp)

file(GLOB FLIGHTGEAR_SOURCES "./flightgear/*.cpp")
file(GLOB FLIGHTGEAR_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/ighost/flightgear/*.hpp)

file(GLOB POV_SOURCES "./pov/*.cpp")
file(GLOB POV_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/ighost/pov/*.hpp)

# Combine all sources and headers
set(ALL_SOURCES
    ${IGHOST_SOURCES}
    ${CIGI_SOURCES}
    ${SESSION_SOURCES}
    ${FLIGHTGEAR_SOURCES}
    ${POV_SOURCES}
)

set(ALL_HEADERS
    ${IGHOST_HEADERS}
    ${CIGI_HEADERS}
    ${SESSION_HEADERS}
    ${FLIGHTGEAR_HEADERS}
    ${POV_HEADERS}
)

# Create the library
add_library(ighost ${ALL_SOURCES} ${ALL_HEADERS})

# Add include directories - fix the path
target_include_directories(ighost
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
        ${CMAKE_SOURCE_DIR}/dependencies/include
)

# Organize files in Visual Studio solution explorer
source_group("Source Files" FILES ${IGHOST_SOURCES})
source_group("Source Files\\cigi" FILES ${CIGI_SOURCES})
source_group("Source Files\\cigi\\session" FILES ${SESSION_SOURCES})
source_group("Source Files\\flightgear" FILES ${FLIGHTGEAR_SOURCES})
source_group("Source Files\\pov" FILES ${POV_SOURCES})

source_group("Header Files" FILES ${IGHOST_HEADERS})
source_group("Header Files\\cigi" FILES ${CIGI_HEADERS})
source_group("Header Files\\cigi\\session" FILES ${SESSION_HEADERS})
source_group("Header Files\\flightgear" FILES ${FLIGHTGEAR_HEADERS})
source_group("Header Files\\pov" FILES ${POV_HEADERS})

# Optional: Set folder property for the target in Visual Studio
set_target_properties(ighost PROPERTIES FOLDER "IGhost")