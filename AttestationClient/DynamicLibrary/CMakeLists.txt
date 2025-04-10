cmake_minimum_required(VERSION 3.5)

#MUST be same as the version in the latest entry in debian/changelog file.

include_directories()

include_directories(
    ${CURL_INCLUDE_DIR}
    ${CRYPTO_INCLUDE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/../../../LinuxTpm/include
    ${CMAKE_CURRENT_SOURCE_DIR}/..
    ${CMAKE_CURRENT_SOURCE_DIR}/../..
    ${CMAKE_CURRENT_SOURCE_DIR}/../include
    ${CMAKE_SOURCE_DIR}/../external/jsoncpp-0.10.7/src
    ${CMAKE_SOURCE_DIR}/../external/SnpVmReport
)

                                           

target_link_libraries(${CMAKE_PROJECT_TARGET} Tpm2)
target_link_libraries(${CMAKE_PROJECT_TARGET} ${CURL_LIB})

set_target_properties(${CMAKE_PROJECT_TARGET} PROPERTIES VERSION ${PROJECT_VERSION})
set_target_properties(${CMAKE_PROJECT_TARGET} PROPERTIES SOVERSION 1)
