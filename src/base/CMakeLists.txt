project(base)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

foreach(CONFIG ${CMAKE_CONFIGURATION_TYPES})
    string(TOUPPER ${CONFIG} CONFIG_UPPER)
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/bin)
endforeach()

file(GLOB BASE_SOURCES "./*.cpp")
file(GLOB BASE_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/*.hpp)

file(GLOB COLORS_SOURCES "./colors/*.cpp")
file(GLOB COLORS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/colors/*.hpp)

file(GLOB CONCEPTS_SOURCES "./concepts/*.cpp")
file(GLOB CONCEPTS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/concepts/*.hpp)

file(GLOB EDL_SOURCES "./edl/*.cpp")
file(GLOB EDL_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/edl/*.hpp)

file(GLOB LINEAR_SOURCES "./linearsystem/*.cpp")
file(GLOB LINEAR_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/linearsystem/*.hpp)

file(GLOB NETWORK_SOURCES "./network/*.cpp")
file(GLOB NETWORK_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/network/*.hpp)

file(GLOB NUMERIC_SOURCES "./numeric/*.cpp")
file(GLOB NUMERIC_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/numeric/*.hpp)

#file(GLOB OSG_SOURCES "./osg/*.cpp")
set(OSG_SOURCES
    "./osg/math.cpp"
    "./osg/Matrixd.cpp"
    "./osg/MatrixDecomposition.cpp"
    "./osg/Matrixf.cpp"
    "./osg/Quat.cpp"
)
file(GLOB OSG_HEADERS 
    ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/osg/*.hpp
    ${CMAKE_SOURCE_DIR}/include/mixr/b${PROJECT_NAME}/osg/*
)

file(GLOB QTY_SOURCES "./qty/*.cpp")
file(GLOB QTY_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/qty/*.hpp)

file(GLOB RELATIONS_SOURCES "./relations/*.cpp")
file(GLOB RELATIONS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/realtions/*.hpp)

file(GLOB THREADS_SOURCES "./threads/*.cpp")
file(GLOB THREADS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/threads/*.hpp)

file(GLOB TIMERS_SOURCES "./timers/*.cpp")
file(GLOB TIMERS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/timers/*.hpp)

file(GLOB TRANS_SOURCES "./transformations/*.cpp")
file(GLOB TRANS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/transformations/*.hpp)

file(GLOB UBF_SOURCES "./ubf/*.cpp")
file(GLOB UBF_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/ubf/*.hpp)

file(GLOB UTIL_SOURCES "./util/*.cpp")
file(GLOB UTIL_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/util/*.hpp)

# Combine all sources and headers
set(ALL_SOURCES
    ${BASE_SOURCES}
    ${COLORS_SOURCES}
    ${CONCEPTS_SOURCES}
    ${EDL_SOURCES}
    ${LINEAR_SOURCES}
    ${NETWORK_SOURCES}
    ${NUMERIC_SOURCES}
    ${OSG_SOURCES}
    ${QTY_SOURCES}
    ${RELATIONS_SOURCES}
    ${THREADS_SOURCES}
    ${TIMERS_SOURCES}
    ${TRANS_SOURCES}
    ${UBF_SOURCES}
    ${UTIL_SOURCES}
)

set(ALL_HEADERS
    ${BASE_HEADERS}
    ${COLORS_HEADERS}
    ${CONCEPTS_HEADERS}
    ${EDL_HEADERS}
    ${LINEAR_HEADERS}
    ${NETWORK_HEADERS}
    ${NUMERIC_HEADERS}
    ${OSG_HEADERS}
    ${QTY_HEADERS}
    ${RELATIONS_HEADERS}
    ${THREADS_HEADERS}
    ${TIMERS_HEADERS}
    ${TRANS_HEADERS}
    ${UBF_HEADERS}
    ${UTIL_HEADERS}
)

# Create the library
add_library(${PROJECT_NAME} ${ALL_SOURCES} ${ALL_HEADERS})

# Add include directories - fix the path
target_include_directories(${PROJECT_NAME}
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
)

# Organize files in Visual Studio solution explorer
source_group("Source Files" FILES ${BASE_SOURCES})
source_group("Source Files\\colors" FILES ${COLORS_SOURCES})
source_group("Source Files\\concepts" FILES ${CONCEPTS_SOURCES})
source_group("Source Files\\edl" FILES ${EDL_SOURCES})
source_group("Source Files\\linearsystem" FILES ${LINEAR_SOURCES})
source_group("Source Files\\network" FILES ${NETWORK_SOURCES})
source_group("Source Files\\numeric" FILES ${NUMERIC_SOURCES})
source_group("Source Files\\osg" FILES ${OSG_SOURCES})
source_group("Source Files\\qty" FILES ${QTY_SOURCES})
source_group("Source Files\\relations" FILES ${RELATIONS_SOURCES})
source_group("Source Files\\threads" FILES ${THREADS_SOURCES})
source_group("Source Files\\timers" FILES ${TIMERS_SOURCES})
source_group("Source Files\\transformations" FILES ${TRANS_SOURCES})
source_group("Source Files\\ubf" FILES ${UBF_SOURCES})
source_group("Source Files\\util" FILES ${UTIL_SOURCES})

source_group("Header Files" FILES ${BASE_HEADERS})
source_group("Header Files\\colors" FILES ${COLORS_HEADERS})
source_group("Header Files\\concepts" FILES ${CONCEPTS_HEADERS})
source_group("Header Files\\edl" FILES ${EDL_HEADERS})
source_group("Header Files\\linearsystem" FILES ${LINEAR_HEADERS})
source_group("Header Files\\network" FILES ${NETWORK_HEADERS})
source_group("Header Files\\numeric" FILES ${NUMERIC_HEADERS})
source_group("Header Files\\osg" FILES ${OSG_HEADERS})
source_group("Header Files\\qty" FILES ${QTY_HEADERS})
source_group("Header Files\\relations" FILES ${RELATIONS_HEADERS})
source_group("Header Files\\threads" FILES ${THREADS_HEADERS})
source_group("Header Files\\timers" FILES ${TIMERS_HEADERS})
source_group("Header Files\\transformations" FILES ${TRANS_HEADERS})
source_group("Header Files\\ubf" FILES ${UBF_HEADERS})
source_group("Header Files\\util" FILES ${UTIL_HEADERS})

# Optional: Set folder property for the target in Visual Studio
set_target_properties(${PROJECT_NAME} PROPERTIES FOLDER "Base")