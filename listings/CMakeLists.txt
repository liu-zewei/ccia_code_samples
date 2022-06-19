cmake_minimum_required(VERSION 3.15)

# set the project name
project(test_concurrency)

set(BUILD_TARGET "listing_1.1" CACHE STRING "Specify the compile target")


# add the executable
#add_executable(listing_1.1 listing_1.1.cpp)

# cllect all cpp files in the current directory
file(GLOB SRC_FILES ./*.cpp)
list(LENGTH SRC_FILES SRC_FILES_COUNT)
MESSAGE(STATUS "SRC_FILES_COUNT = ${SRC_FILES_COUNT}")

#list(TRANSFORM SRC_FILES REPLACE ".cpp" "")

foreach(item ${SRC_FILES})
    #message(STATUS "${item}")
    get_filename_component(file_name ${item} NAME_WLE)
    #message(STATUS "${file_name}")
    list(APPEND FILE_NAME_LIST ${file_name})
endforeach()

list(FIND FILE_NAME_LIST ${BUILD_TARGET} RET)

if(RET MATCHES -1)
    message(FATAL_ERROR "Cannot find this target : ${BUILD_TARGET}")
endif()

add_executable(${BUILD_TARGET}
    ${BUILD_TARGET}.cpp
    )

target_link_libraries(${BUILD_TARGET} PUBLIC pthread)


#message(SEND_ERROR "${FILE_NAME_LIST}")

#MESSAGE(FATAL_ERROR ${SRC_FILES})