project (hdr_histogram)

cmake_minimum_required (VERSION 2.8)

set(CMAKE_MACOSX_RPATH 1)

include(${WORKSPACE}/WORKSPACE.cmake)

include_directories("." "./src")

set(CMAKE_C_FLAGS "-Wall -Wno-unknown-pragmas -Wextra -Wshadow -Winit-self -Wmissing-prototypes -D_GNU_SOURCE")
set(CMAKE_C_FLAGS_DEBUG "-O0 -g")
set(CMAKE_C_FLAGS_RELEASE "-O3 -g")
add_compile_options(-DBAZEL=1)

FILE(GLOB CPP_FILES "${PROJECT_SOURCE_DIR}/src/*.c")
FILE(GLOB H_FILES "${PROJECT_SOURCE_DIR}/src/*.h")

SET( SOURCE_FILES ${CPP_FILES} ${H_FILES})

SET(BUILD_FILES
${PROJECT_SOURCE_DIR}/BUILD
${PROJECT_SOURCE_DIR}/PACKAGE.cmake
)

include(${PROJECT_SOURCE_DIR}/PACKAGE.cmake)

add_library(hdr_histogram ${SOURCE_FILES} ${BUILD_FILES})
target_link_libraries(hdr_histogram ${ZLIB_LIB})

add_executable(perftest ${PROJECT_SOURCE_DIR}/test/hdr_histogram_perf.c ${BUILD_FILES})
target_link_libraries(perftest ${HDR_HISTOGRAM_LIB})

add_executable(hdr_histogram_test ${PROJECT_SOURCE_DIR}/test/hdr_histogram_test.c ${BUILD_FILES})
target_link_libraries(hdr_histogram_test ${HDR_HISTOGRAM_LIB})

add_executable(hdr_histogram_log_test ${PROJECT_SOURCE_DIR}/test/hdr_histogram_log_test.c ${BUILD_FILES})
target_link_libraries(hdr_histogram_log_test ${HDR_HISTOGRAM_LIB} ${ZLIB_LIB})

add_custom_target (FORMAT ALL
/usr/local/bin/clang-format -style=Google -i ${SOURCE_FILES} ${PROJECT_SOURCE_DIR}/test/hdr_histogram_perf.c ${PROJECT_SOURCE_DIR}/test/hdr_histogram_log_test.c ${PROJECT_SOURCE_DIR}/test/hdr_histogram_test.c
)
