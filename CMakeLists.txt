cmake_minimum_required (VERSION 2.8) 
project (WSLAY) 


OPTION(DEBUG_MODE          "Enable debug output [default: ON]"      ON)

#
# Compiler SETtings
#
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wpointer-arith")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-long-long")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-unused-parameter")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-unused-function")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wunused-variable")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pedantic")

IF(DEBUG_MODE MATCHES "ON")
    MESSAGE ("Setting debug flags")
    SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g")
    SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O0")
    SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fno-optimize-sibling-calls")
ELSE()
    MESSAGE("Setting release flags")
    SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3")
ENDIF(DEBUG_MODE MATCHES "ON")
#
# Libraries
#

INCLUDE_DIRECTORIES (${WSLAY_SOURCE_DIR}/lib/includes)

set (PACKAGE_VERSION 0.1.1)
 
# configure a header file to pass some of the CMake settings
# to the source code
configure_file (
    "${WSLAY_SOURCE_DIR}/lib/includes/wslay/wslayver.h.in"
    "${WSLAY_SOURCE_DIR}/lib/includes/wslay/wslayver.h")

ADD_LIBRARY (wslay lib/wslay_event.c lib/wslay_frame.c lib/wslay_net.c lib/wslay_queue.c lib/wslay_stack.c)

