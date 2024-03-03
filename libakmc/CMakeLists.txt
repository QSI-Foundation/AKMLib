# # #

CMAKE_MINIMUM_REQUIRED (VERSION 3.25.1)

PROJECT (
    akm
    VERSION       0.0.0.0
    DESCRIPTION   "AKM C Language Library"
    HOMEPAGE_URL  "https://github.com/QSI-Foundation/libakm"
    LANGUAGES     C CXX
)


# # #

SET (CMAKE_C_STANDARD 11)
SET (CMAKE_C_STANDARD_REQUIRED True)
SET (CMAKE_CXX_STANDARD 11)
SET (CMAKE_CXX_STANDARD_REQUIRED True)

CONFIGURE_FILE (
    inc/akm.h.in akm.h
    ESCAPE_QUOTES
)


# # #

ADD_LIBRARY ("${PROJECT_NAME}" SHARED)

TARGET_SOURCES (
    "${PROJECT_NAME}" PRIVATE
    src/addr_list.c
    src/akm.c
    src/akm_core.c
    src/bytevector.c
    src/endianness.c
    src/flagset.c
    src/sha256.c
    src/utilities.c
)

TARGET_INCLUDE_DIRECTORIES (
    "${PROJECT_NAME}" PUBLIC
    "${PROJECT_BINARY_DIR}"
    inc
)


# # #

ADD_EXECUTABLE ("${PROJECT_NAME}_testn")

TARGET_SOURCES (
    "${PROJECT_NAME}_testn" PRIVATE
    test/testn.cpp
)

TARGET_LINK_LIBRARIES (
    "${PROJECT_NAME}_testn" PRIVATE
    "${PROJECT_NAME}"
)


# # #

ENABLE_TESTING ()

ADD_TEST (
    NAME     "${PROJECT_NAME}_testn"
    COMMAND  "${PROJECT_NAME}_testn"
)

SET_TESTS_PROPERTIES (
    "${PROJECT_NAME}_testn"
    PROPERTIES
        FAIL_REGULAR_EXPRESSION  "."
)


# # #

INSTALL (
    TARGETS "${PROJECT_NAME}"
    DESTINATION lib
)

INSTALL (
    FILES "${PROJECT_BINARY_DIR}/akm.h"
    DESTINATION include
)


# # #
