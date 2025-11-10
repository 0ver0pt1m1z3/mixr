project(models)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

foreach(CONFIG ${CMAKE_CONFIGURATION_TYPES})
    string(TOUPPER ${CONFIG} CONFIG_UPPER)
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/lib)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/bin)
endforeach()

file(GLOB MODELS_SOURCES "./*.cpp")
file(GLOB MODELS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/*.hpp)

file(GLOB ACTION_SOURCES "./action/*.cpp")
file(GLOB ACTION_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/action/*.hpp)

file(GLOB DYNAMICS_SOURCES "./dynamics/*.cpp")
file(GLOB DYNAMICS_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/dynamics/*.hpp)

file(GLOB JSBSIM_SOURCES "./dynamics/jsbsim/*.cpp")
file(GLOB JSBSIM_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/dynamics/jsbsim/*.hpp)

file(GLOB ENV_SOURCES "./environment/*.cpp")
file(GLOB ENV_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/environment/*.hpp)

file(GLOB NAV_SOURCES "./navigation/*.cpp")
file(GLOB NAV_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/navigation/*.hpp)

file(GLOB AIR_SOURCES "./player/air/*.cpp")
file(GLOB AIR_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/player/air/*.hpp)

file(GLOB EFFECT_SOURCES "./player/effect/*.cpp")
file(GLOB EFFECT_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/player/effect/*.hpp)

file(GLOB GROUND_SOURCES "./player/ground/*.cpp")
file(GLOB GROUND_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/player/ground/*.hpp)

file(GLOB SPACE_SOURCES "./player/space/*.cpp")
file(GLOB SPACE_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/player/space/*.hpp)

file(GLOB WAEPON_SOURCES "./player/weapon/*.cpp")
file(GLOB WEAPON_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/player/weapon/*.hpp)

file(GLOB PLAYER_SOURCES "./player/*.cpp")
file(GLOB PLAYER_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/player/*.hpp)

file(GLOB SENSOR_SOURCES "./sensor/*.cpp")
file(GLOB SENSOR_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/sensor/*.hpp)

file(GLOB SIG_SOURCES "./signature/*.cpp")
file(GLOB SIG_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/signature/*.hpp)

file(GLOB SYSTEM_SOURCES "./system/*.cpp")
file(GLOB SYSTEM_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/system/*.hpp)

file(GLOB TRKMGR_SOURCES "./system/trackmanager/*.cpp")
file(GLOB TRKMGR_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/system/trackmanager/*.hpp)

file(GLOB TRACK_SOURCES "./track/*.cpp")
file(GLOB TRACK_HEADERS ${CMAKE_SOURCE_DIR}/include/mixr/${PROJECT_NAME}/track/*.hpp)

# Combine all sources and headers
set(ALL_SOURCES
    ${MODELS_SOURCES}
    ${ACTION_SOURCES}
    ${DYNAMICS_SOURCES}
    ${JSBSIM_SOURCES}
    ${ENV_SOURCES}
    ${NAV_SOURCES}
    ${AIR_SOURCES}
    ${EFFECT_SOURCES}
    ${GROUND_SOURCES}
    ${SPACE_SOURCES}
    ${WAEPON_SOURCES}
    ${PLAYER_SOURCES}
    ${SENSOR_SOURCES}
    ${SIG_SOURCES}
    ${SYSTEM_SOURCES}
    ${TRKMGR_SOURCES}
    ${TRACK_SOURCES}
)

set(ALL_HEADERS
    ${MODELS_HEADERS}
    ${ACTION_HEADERS}
    ${DYNAMICS_HEADERS}
    ${JSBSIM_HEADERS}
    ${ENV_HEADERS}
    ${NAV_HEADERS}
    ${AIR_HEADERS}
    ${EFFECT_HEADERS}
    ${GROUND_HEADERS}
    ${SPACE_HEADERS}
    ${WEAPON_HEADERS}
    ${PLAYER_HEADERS}
    ${SENSOR_HEADERS}
    ${SIG_HEADERS}
    ${SYSTEM_HEADERS}
    ${TRKMGR_HEADERS}
    ${TRACK_HEADERS}
)

# Create the library
add_library(${PROJECT_NAME} ${ALL_SOURCES} ${ALL_HEADERS})

# Add include directories - fix the path
target_include_directories(${PROJECT_NAME}
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
        ${CMAKE_SOURCE_DIR}/dependencies/include
        ${CMAKE_SOURCE_DIR}/dependencies/include/jsbSim
)

# Organize files in Visual Studio solution explorer
source_group("Source Files" FILES ${MODELS_SOURCES})
source_group("Source Files\\action" FILES ${ACTION_SOURCES})
source_group("Source Files\\dynamics" FILES ${DYNAMICS_SOURCES})
source_group("Source Files\\jsbsim" FILES ${JSBSIM_SOURCES})
source_group("Source Files\\environment" FILES ${ENV_SOURCES})
source_group("Source Files\\navigation" FILES ${NAV_SOURCES})
source_group("Source Files\\player\\air" FILES ${AIR_SOURCES})
source_group("Source Files\\player\\effect" FILES ${EFFECT_SOURCES})
source_group("Source Files\\player\\ground" FILES ${GROUND_SOURCES})
source_group("Source Files\\player\\space" FILES ${SPACE_SOURCES})
source_group("Source Files\\player\\weapon" FILES ${WEAPON_SOURCES})
source_group("Source Files\\player" FILES ${PLAYER_SOURCES})
source_group("Source Files\\sensor" FILES ${SENSOR_SOURCES})
source_group("Source Files\\signature" FILES ${SIG_SOURCES})
source_group("Source Files\\system" FILES ${SYSTEM_SOURCES})
source_group("Source Files\\system\\trackmanager" FILES ${TRKMGR_SOURCES})
source_group("Source Files\\track" FILES ${TRACK_SOURCES})

source_group("Header Files" FILES ${MODELS_SOURCES})
source_group("Header Files\\action" FILES ${ACTION_SOURCES})
source_group("Header Files\\dynamics" FILES ${DYNAMICS_SOURCES})
source_group("Header Files\\jsbsim" FILES ${JSBSIM_SOURCES})
source_group("Header Files\\environment" FILES ${ENV_SOURCES})
source_group("Header Files\\navigation" FILES ${NAV_SOURCES})
source_group("Header Files\\player\\air" FILES ${AIR_SOURCES})
source_group("Header Files\\player\\effect" FILES ${EFFECT_SOURCES})
source_group("Header Files\\player\\ground" FILES ${GROUND_SOURCES})
source_group("Header Files\\player\\space" FILES ${SPACE_SOURCES})
source_group("Header Files\\player\\weapon" FILES ${WEAPON_SOURCES})
source_group("Header Files\\player" FILES ${PLAYER_SOURCES})
source_group("Header Files\\sensor" FILES ${SENSOR_SOURCES})
source_group("Header Files\\signature" FILES ${SIG_SOURCES})
source_group("Header Files\\system" FILES ${SYSTEM_SOURCES})
source_group("Header Files\\system\\trackmanager" FILES ${TRKMGR_SOURCES})
source_group("Header Files\\track" FILES ${TRACK_SOURCES})

# Optional: Set folder property for the target in Visual Studio
set_target_properties(${PROJECT_NAME} PROPERTIES FOLDER "Models")