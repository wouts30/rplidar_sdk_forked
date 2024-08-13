cmake_minimum_required(VERSION 2.8)
project(rplidar_sdk)

# Set C++ standard
set(CMAKE_CXX_STANDARD 11)

# Include directories
include_directories(
    ${PROJECT_SOURCE_DIR}/sdk/include
    ${PROJECT_SOURCE_DIR}/sdk/src
)

# Collect all source files
file(GLOB RPLIDAR_SDK_SRC 
    "${PROJECT_SOURCE_DIR}/sdk/src/*.cpp"
    "${PROJECT_SOURCE_DIR}/sdk/src/arch/linux/*.cpp"
    "${PROJECT_SOURCE_DIR}/sdk/src/hal/*.cpp"
)

set(RPLIDAR_SDK_SRC
    ${RPLIDAR_SDK_SRC}
    "${PROJECT_SOURCE_DIR}/sdk/src/dataunpacker/dataunpacker.cpp"
    "${PROJECT_SOURCE_DIR}/sdk/src/sl_lidar_driver.cpp"
)

file(GLOB RPLIDAR_UNPACKER_SRC
    "${PROJECT_SOURCE_DIR}/sdk/src/dataunpacker/*.cpp"
    "${PROJECT_SOURCE_DIR}/sdk/src/dataunpacker/unpacker/*.cpp"
)

set(RPLIDAR_SDK_SRC
    ${RPLIDAR_SDK_SRC}
    ${RPLIDAR_UNPACKER_SRC}
)

# Create library
add_library(rplidar_sdk STATIC ${RPLIDAR_SDK_SRC})

# Set output directory
set_target_properties(rplidar_sdk PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/output"
    LIBRARY_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/output"
)

# Install rules
install(TARGETS rplidar_sdk
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)

install(DIRECTORY sdk/include/
    DESTINATION include
)
