project(models)

# Output directories
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

foreach(CONFIG ${CMAKE_CONFIGURATION_TYPES})
    string(TOUPPER ${CONFIG} CONFIG_UPPER)
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/bin)
endforeach()

# Recursively grab all .cpp and .hpp files
file(GLOB_RECURSE ALL_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp")
file(GLOB_RECURSE ALL_HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/*.hpp")

# Create static library
add_library(${PROJECT_NAME} STATIC ${ALL_SOURCES} ${ALL_HEADERS})

# Include directories
target_include_directories(${PROJECT_NAME}
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
        ${CMAKE_SOURCE_DIR}/../mixr-3rdparty/include
	${CMAKE_SOURCE_DIR}/../mixr-3rdparty/include/JSBSim
	${CMAKE_SOURCE_DIR}/../mixr-3rdparty/include/JSBSim/simgear
)

# Organize in Visual Studio solution explorer
source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR} FILES ${ALL_SOURCES} ${ALL_HEADERS})
# Optional: Set folder property for the target in Visual Studio
set_target_properties(${PROJECT_NAME} PROPERTIES 
    FOLDER "Models"
    OUTPUT_NAME "mixr_models"
    OUTPUT_NAME_DEBUG "mixr_models_d"
)