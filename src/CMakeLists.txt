cmake_minimum_required (VERSION 3.14 FATAL_ERROR)

set(PLLMOD_CFLAGS  "-Wall -Wsign-compare -D_GNU_SOURCE -std=c99 -O3")
if(PLLMOD_DEBUG)
	set(PLLMOD_CFLAGS "${PLLMOD_CFLAGS} -DDEBUG")
endif()

set(CMAKE_SHARED_LINKER_FLAGS  "${CMAKE_SHARED_LINKER_FLAGS} -Wl,-undefined -Wl,dynamic_lookup")
set(PLLMOD_INCLUDE_PATH  ${PLLMODULES_LIBPLL_PATH}/src/ ${PLL_INCLUDE_DIRS} /usr/lib/x86_64-linux-gnu/openmpi/include)

set(PLLMODULES_COMPONENTS "optimize;algorithm;binary;msa;tree;util" CACHE STRING "pll-modules components to build")

foreach(module ${PLLMODULES_COMPONENTS})
  MESSAGE(STATUS "Will compile pll-module ${module}")
  add_subdirectory(${module})
endforeach()

set(PLLMOD_EXPORTED_INCLUDE_PATH ${CMAKE_CURRENT_SOURCE_DIR} "${CMAKE_CURRENT_SOURCE_DIR}/algorithm/" "${CMAKE_CURRENT_SOURCE_DIR}/binary" "${CMAKE_CURRENT_SOURCE_DIR}/msa" "${CMAKE_CURRENT_SOURCE_DIR}/optimize"  "${CMAKE_CURRENT_SOURCE_DIR}/tree" "${CMAKE_CURRENT_SOURCE_DIR}/util" ${LIBPLL_SRC} PARENT_SCOPE)

