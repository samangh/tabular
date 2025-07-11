#
#      __        ___.         .__
#    _/  |______ \_ |__  __ __|  | _____ _______
#    \   __\__  \ | __ \|  |  \  | \__  \\_  __ \
#     |  |  / __ \| \_\ \  |  /  |__/ __ \|  | \/
#     |__| (____  /___  /____/|____(____  /__|
#               \/    \/                \/
#
#    *  Author: Anas Hamdane
#    *  Github: https://github.com/Anas-Hamdane
#
#

set(EXAMPLES_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/source)
set(EXAMPLES_BIN_DIR ${CMAKE_BINARY_DIR}/bin/examples)

# all header files
file(GLOB HEADER_FILES ${CMAKE_SOURCE_DIR}/include/tabular/*.hpp)

# all examples
file(GLOB EXAMPLE_SOURCES ${EXAMPLES_SOURCE_DIR}/*.cpp)

set(EXAMPLE_TARGETS)

foreach(EXAMPLE_SOURCE ${EXAMPLE_SOURCES})
    get_filename_component(EXAMPLE_NAME ${EXAMPLE_SOURCE} NAME_WE)
    
    add_executable(${EXAMPLE_NAME} ${EXAMPLE_SOURCE} ${HEADER_FILES})

    target_include_directories(${EXAMPLE_NAME} 
        PRIVATE 
        ${CMAKE_SOURCE_DIR}/include 
    )

    set_target_properties(${EXAMPLE_NAME} PROPERTIES
        RUNTIME_OUTPUT_DIRECTORY ${EXAMPLES_BIN_DIR}
    )

    list(APPEND EXAMPLE_TARGETS ${EXAMPLE_NAME})

    message(STATUS "Added example: ${EXAMPLE_NAME}")
endforeach()
