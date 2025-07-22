
cmake_minimum_required( VERSION 3.15 )

project( epitran-c
    VERSION 0.0.1
    LANGUAGES C
)

set(CMAKE_C_STANDARD 99)

set(EPITRANC_BUILD)

option(EPITRANC_SHARED "Shared build" ON)
option(EPITRANC_STATIC "Static build" OFF)

if(CMAKE_SYSTEM_NAME STREQUAL WASI)
  set(EPITRANC_STATIC ON CACHE BOOL "Static option" FORCE)
  set(EPITRANC_SHARED OFF CACHE BOOL "Shared option" FORCE)
endif()

if(NOT EPITRANC_STATIC AND EPITRANC_SHARED)
  set(EPITRANC_BUILD SHARED)
else(EPITRANC_STATIC)
  set(EPITRANC_BUILD STATIC)
endif()

add_library(${PROJECT_NAME}
    ${EPITRANC_BUILD}
    )
    
