
file(GLOB OPTIMIZE_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/*.c 
  ${CMAKE_CURRENT_SOURCE_DIR}/lbfgsb/*.c
  ${CMAKE_CURRENT_SOURCE_DIR}/../pllmod_common.c)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${PLLMOD_CFLAGS}")

add_pllmodules_lib(pllmodoptimize "${OPTIMIZE_SOURCES}")
