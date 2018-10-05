


project (pystring CXX)
cmake_minimum_required (VERSION 3.12)


set (HEADERS pystring.h )
set (SOURCES pystring.cpp )
set (TEST_SOURCE test.cpp )

# Original Sony Makefile specified gcc options, which wouldn't apply to MSVC, etc.
if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
    set (CXXFLAGS --std=c++14 -g -O3 -Wall -Wextra -Wshadow -Wconversion -Wcast-qual -Wformat=2 )
    target_compile_options( ${PROJECT_NAME} PUBLIC ${CXXFLAGS} )

endif()


add_library (${PROJECT_NAME} SHARED ${HEADERS} ${SOURCES})

add_executable (${PROJECT_NAME}-test ${TEST_SOURCE} ${SOURCES} ${HEADERS})
