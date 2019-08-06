cmake_minimum_required(VERSION 2.8)
project(minivmac C)
set(CMAKE_C_STANDARD 11)

# Uncomment or pass -DCMAKE_RUNTIME_OUTPUT_DIRECTORY="${CMAKE_SOURCE_DIR}" to output the executable to the same directory as the source files.
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/../bld")

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wmissing-prototypes -Wno-uninitialized -Wundef -Wstrict-prototypes")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS} -O2 -mwindows -s")
set(CMAKE_C_FLAGS_MINSIZEREL "${CMAKE_C_FLAGS} -Os -mwindows -s")

include_directories(PRIVATE "../cfg" ".")

add_executable(tool ../setup/tool.c)
set_target_properties(tool PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/..)


add_executable(minivmac
		MINEM68K.c OSGLUWIN.c GLOBGLUE.c M68KITAB.c DISAM68K.c VIAEMDEV.c VIA2EMDV.c IWMEMDEV.c SCCEMDEV.c RTCEMDEV.c
		ROMEMDEV.c SCSIEMDV.c SONYEMDV.c SCRNEMDV.c VIDEMDEV.c MOUSEMDV.c ADBEMDEV.c ASCEMDEV.c PROGMAIN.c
		../cfg/main.rc)

target_link_libraries(minivmac winmm ole32 uuid)

