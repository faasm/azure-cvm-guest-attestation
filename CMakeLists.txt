cmake_minimum_required(VERSION 3.5)
project(azguestattestation VERSION 1.0.5)

set(CMAKE_MODULE_PATH "${MODULE_PATH};${CMAKE_CURRENT_SOURCE_DIR}/LinuxTpm/tools/cmake")

add_definitions (-DPLATFORM_UNIX)

add_subdirectory(AttestationClient)
add_subdirectory(LinuxTpm)
