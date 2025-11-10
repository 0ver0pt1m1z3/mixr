project(dafif)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

foreach(CONFIG ${CMAKE_CONFIGURATION_TYPES})
    string(TOUPPER ${CONFIG} CONFIG_UPPER)
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/bin)
endforeach()

file(GLOB DAFIF_SOURCES "./*.cpp")
file(GLOB DAFIF_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/dafif/*.hpp)

file(GLOB LOADERS_SOURCES "./loaders/*.cpp")
file(GLOB LOADERS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/dafif/loaders/*.hpp)

file(GLOB RECORDS_SOURCES "./records/*.cpp")
file(GLOB RECORDS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/dafif/records/*.hpp)

# Combine all sources and headers
set(ALL_SOURCES
    ${DAFIF_SOURCES}
    ${LOADERS_SOURCES}
    ${RECORDS_SOURCES}
)

set(ALL_HEADERS
    ${DAFIF_HEADERS}
    ${LOADERS_HEADERS}
    ${RECORDS_HEADERS}
)

# Create the library
add_library(dafif ${ALL_SOURCES} ${ALL_HEADERS})

# Add include directories - fix the path
target_include_directories(dafif
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
)

# Organize files in Visual Studio solution explorer
source_group("Source Files" FILES ${DAFIF_SOURCES})
source_group("Source Files\\loaders" FILES ${LOADERS_SOURCES})
source_group("Source Files\\records" FILES ${RECORDS_SOURCES})

source_group("Header Files" FILES ${DAFIF_HEADERS})
source_group("Header Files\\loaders" FILES ${LOADERS_HEADERS})
source_group("Header Files\\records" FILES ${RECORDS_HEADERS})


# Optional: Set folder property for the target in Visual Studio
set_target_properties(dafif PROPERTIES FOLDER "Dafif")