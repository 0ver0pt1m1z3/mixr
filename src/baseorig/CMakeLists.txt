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

file(GLOB EDL_SOURCES "./edl_parser/*.cpp")
file(GLOB EDL_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/edl_parser/*.hpp)

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

file(GLOB THREADS_SOURCES "./threads/*.cpp")
file(GLOB THREADS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/threads/*.hpp)

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
    ${NETWORK_SOURCES}
    ${NUMERIC_SOURCES}
    ${OSG_SOURCES}
    ${THREADS_SOURCES}
    ${UBF_SOURCES}
    ${UTIL_SOURCES}
)

set(ALL_HEADERS
    ${BASE_HEADERS}
    ${COLORS_HEADERS}
    ${CONCEPTS_HEADERS}
    ${EDL_HEADERS}
    ${NETWORK_HEADERS}
    ${NUMERIC_HEADERS}
    ${OSG_HEADERS}
    ${THREADS_HEADERS}
    ${UBF_HEADERS}
    ${UTIL_HEADERS}
)
message(STATUS "Compiling the following source files for ${PROJECT_NAME}:")
foreach(src ${ALL_SOURCES})
    message(STATUS "  ${src}")
endforeach()

message(STATUS "Including headers for ${PROJECT_NAME}:")
foreach(hdr ${ALL_HEADERS})
    message(STATUS "  ${hdr}")
endforeach()
# Create the library
add_library(${PROJECT_NAME} ${ALL_SOURCES} ${ALL_HEADERS})

# Add include directories - fix the path
target_include_directories(${PROJECT_NAME}
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
	${CMAKE_SOURCE_DIR}/../mixr-3rdparty/include
)

# Organize files in Visual Studio solution explorer
source_group("src\\${PROJECT_NAME}" FILES ${BASE_SOURCES})
source_group("src\\${PROJECT_NAME}\\colors" FILES ${COLORS_SOURCES})
source_group("src\\${PROJECT_NAME}\\concepts" FILES ${CONCEPTS_SOURCES})
source_group("src\\${PROJECT_NAME}\\edl_parser" FILES ${EDL_SOURCES})
source_group("src\\${PROJECT_NAME}\\network" FILES ${NETWORK_SOURCES})
source_group("src\\${PROJECT_NAME}\\numeric" FILES ${NUMERIC_SOURCES})
source_group("src\\${PROJECT_NAME}\\osg" FILES ${OSG_SOURCES})
source_group("src\\${PROJECT_NAME}\\threads" FILES ${THREADS_SOURCES})
source_group("src\\${PROJECT_NAME}\\ubf" FILES ${UBF_SOURCES})
source_group("src\\${PROJECT_NAME}\\util" FILES ${UTIL_SOURCES})

source_group("include\\mixr\\${PROJECT_NAME}" FILES ${BASE_HEADERS})
source_group("include\\mixr\\${PROJECT_NAME}\\colors" FILES ${COLORS_HEADERS})
source_group("include\\mixr\\${PROJECT_NAME}\\concepts" FILES ${CONCEPTS_HEADERS})
source_group("include\\mixr\\${PROJECT_NAME}\\edl_parser" FILES ${EDL_HEADERS})
source_group("include\\mixr\\${PROJECT_NAME}\\network" FILES ${NETWORK_HEADERS})
source_group("include\\mixr\\${PROJECT_NAME}\\numeric" FILES ${NUMERIC_HEADERS})
source_group("include\\mixr\\${PROJECT_NAME}\\osg" FILES ${OSG_HEADERS})
source_group("include\\mixr\\${PROJECT_NAME}\\threads" FILES ${THREADS_HEADERS})
source_group("include\\mixr\\${PROJECT_NAME}\\ubf" FILES ${UBF_HEADERS})
source_group("include\\mixr\\${PROJECT_NAME}\\util" FILES ${UTIL_HEADERS})

# Optional: Set folder property for the target in Visual Studio
set_target_properties(${PROJECT_NAME} PROPERTIES 
    FOLDER "Base"
    OUTPUT_NAME "mixr_base"
    OUTPUT_NAME_DEBUG "mixr_base_d"
)