


project (pystring CXX)
cmake_minimum_required (VERSION 3.10)


set (HEADERS pystring.h )
set (SOURCES pystring.cpp )
set (TEST_SOURCE test.cpp )

add_executable (${PROJECT_NAME}-test ${TEST_SOURCE} ${SOURCES} ${HEADERS})

# Run tests before building the library
add_custom_target(test_run ALL
  COMMAND pystring-test
  WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMENT "Run tests in ${CMAKE_CURRENT_SOURCE_DIR}"
  SOURCES ${pystring-test_SOURCES}
)


add_library (${PROJECT_NAME} SHARED ${HEADERS} ${SOURCES})

# Original Sony Makefile specified gcc options, which wouldn't apply to MSVC, etc.
if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
    set (CXXFLAGS --std=c++14 -g -O3 -Wall -Wextra -Wshadow -Wconversion -Wcast-qual -Wformat=2 )
    target_compile_options( ${PROJECT_NAME} PUBLIC ${CXXFLAGS} )

endif()


