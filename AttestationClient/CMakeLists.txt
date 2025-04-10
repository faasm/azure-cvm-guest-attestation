cmake_minimum_required(VERSION 3.5)

find_package(Tss2 REQUIRED)
include_directories(${TSS2_INCLUDE_DIRS})

find_path(CURL_INCLUDE_DIR 
	  NAMES curl 
	  PATHS /usr/local/attestationcurl/include NO_DEFAULT_PATH)
find_path(CRYPTO_INCLUDE_DIR 
	  NAMES openssl 
	  PATHS /usr/local/attestationssl/include NO_DEFAULT_PATH)
find_library(CURL_LIB 
	     NAMES curl 
	     PATHS /usr/local/attestationcurl/lib NO_DEFAULT_PATH)

set(CMAKE_PROJECT_TARGET azguestattestation)
add_library(${CMAKE_PROJECT_TARGET} SHARED 
  	    AttestationClientImpl.cpp
  	    AttestationClient.cpp
	    AttestationHelper.cpp
  	    AttestationLibTelemetry.cpp
  	    AttestationLibUtils.cpp
  	    AttestationParameters.cpp
  	    HclReportParser.cpp
  	    HttpClient.cpp
  	    ImdsClient.cpp
  	    ImdsOperations.cpp
  	    IsolationInfo.cpp
  	    Logging.cpp
  	    NativeConverter.cpp
  	    TpmCertOperations.cpp
  	    TpmInfo.cpp
  	    TpmUnseal.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/../external/jsoncpp-0.10.7/src/jsoncpp.cpp)

target_compile_options(${CMAKE_PROJECT_TARGET} PRIVATE -Wno-narrowing -Wno-dev -Wno-conversion-null)
target_include_directories(${CMAKE_PROJECT_TARGET} PUBLIC
    ${CURL_INCLUDE_DIR}
    ${CRYPTO_INCLUDE_DIR}
    ${CMAKE_CURRENT_LIST_DIR}/../LinuxTpm/include
    ${CMAKE_CURRENT_LIST_DIR}/include
    ${CMAKE_CURRENT_LIST_DIR}/../external/jsoncpp-0.10.7/src
    ${CMAKE_CURRENT_LIST_DIR}/../external/SnpVmReport
)
target_link_libraries(${CMAKE_PROJECT_TARGET} Tpm2 ${CURL_LIB})
