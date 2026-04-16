cmake_minimum_required(VERSION 3.16)
project(lkh3 LANGUAGES C)

find_package(ament_cmake REQUIRED)

file(GLOB LKH_SRC "${CMAKE_CURRENT_SOURCE_DIR}/SRC/*.c")
add_executable(LKH ${LKH_SRC})
target_include_directories(LKH PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/SRC/INCLUDE)
# LKH-3 uses tentative C definitions (globals in multiple TUs).
# GCC 10+ defaults to -fno-common which rejects these; restore legacy behavior.
target_compile_options(LKH PRIVATE -fcommon -w)
target_link_libraries(LKH PRIVATE m)

install(TARGETS LKH DESTINATION bin)

ament_package()
