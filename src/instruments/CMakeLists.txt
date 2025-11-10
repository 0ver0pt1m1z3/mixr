project(instruments)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

foreach(CONFIG ${CMAKE_CONFIGURATION_TYPES})
    string(TOUPPER ${CONFIG} CONFIG_UPPER)
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/bin)
endforeach()

file(GLOB INSTR_SOURCES "./*.cpp")
file(GLOB INSTR_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/*.hpp)

file(GLOB ADI_SOURCES "./adi/*.cpp")
file(GLOB ADI_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/adi/*.hpp)

file(GLOB BUTTONS_SOURCES "./buttons/*.cpp")
file(GLOB BUTTONS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/buttons/*.hpp)

file(GLOB DIALS_SOURCES "./dials/*.cpp")
file(GLOB DIALS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/dials/*.hpp)

file(GLOB EADI3D_SOURCES "./eadi3d/*.cpp")
file(GLOB EADI3D_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/eadi3d/*.hpp)

file(GLOB ENGINES_SOURCES "./engines/*.cpp")
file(GLOB ENGINES_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/engines/*.hpp)

file(GLOB GUAGES_SOURCES "./guages/*.cpp")
file(GLOB GUAGES_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/guages/*.hpp)

file(GLOB GEAR_SOURCES "./landinggear/*.cpp")
file(GLOB GEAR_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/landinggear/*.hpp)

file(GLOB MAPS_SOURCES "./maps/*.cpp")
file(GLOB MAPS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/maps/*.hpp)

# Combine all sources and headers
set(ALL_SOURCES
    ${INSTR_SOURCES}
    ${ADI_SOURCES}
    ${BUTTONS_SOURCES}
    ${DIALS_SOURCES}
    ${EADI3D_SOURCES}
    ${ENGINES_SOURCES}
    ${GUAGES_SOURCES}
    ${GEAR_SOURCES}
    ${MAPS_SOURCES}
)

set(ALL_HEADERS
    ${INSTR_HEADERS}
    ${ADI_HEADERS}
    ${BUTTONS_HEADERS}
    ${DIALS_HEADERS}
    ${EADI3D_HEADERS}
    ${ENGINES_HEADERS}
    ${GUAGES_HEADERS}
    ${GEAR_HEADERS}
    ${MAPS_HEADERS}
)

# Create the library
add_library(${PROJECT_NAME} ${ALL_SOURCES} ${ALL_HEADERS})

# Add include directories - fix the path
target_include_directories(${PROJECT_NAME}
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
)

# Organize files in Visual Studio solution explorer
source_group("Source Files" FILES ${INSTR_SOURCES})
source_group("Source Files\\adi" FILES ${ADI_SOURCES})
source_group("Source Files\\buttons" FILES ${BUTTONS_SOURCES})
source_group("Source Files\\dials" FILES ${DIALS_SOURCES})
source_group("Source Files\\eadi3d" FILES ${EADI3D_SOURCES})
source_group("Source Files\\engines" FILES ${ENGINES_SOURCES})
source_group("Source Files\\guages" FILES ${GUAGES_SOURCES})
source_group("Source Files\\landinggear" FILES ${GEAR_SOURCES})
source_group("Source Files\\maps" FILES ${MAPS_SOURCES})

source_group("Header Files" FILES ${INSTR_HEADERS})
source_group("Header Files\\adi" FILES ${ADI_HEADERS})
source_group("Header Files\\buttons" FILES ${BUTTONS_HEADERS})
source_group("Header Files\\dials" FILES ${DIALS_HEADERS})
source_group("Header Files\\eadi3d" FILES ${EADI3D_HEADERS})
source_group("Header Files\\engines" FILES ${ENGINES_HEADERS})
source_group("Header Files\\guages" FILES ${GUAGES_HEADERS})
source_group("Header Files\\gear" FILES ${GEAR_HEADERS})
source_group("Header Files\\maps" FILES ${MAPS_HEADERS})

# Optional: Set folder property for the target in Visual Studio
set_target_properties(${PROJECT_NAME} PROPERTIES FOLDER "Instruments")