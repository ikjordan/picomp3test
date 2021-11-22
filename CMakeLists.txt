# Generated Cmake Pico project file

cmake_minimum_required(VERSION 3.13)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# initalize pico_sdk from installed location
# (note this can come from environment, CMake cache etc)
# set(PICO_SDK_PATH "/YOUR_PICO_SDK_PATH/pico-sdk")

# Pull in Pico SDK (must be before project)
include(pico_sdk_import.cmake)

project(picomp3test C CXX ASM)

set(PICO_CXX_ENABLE_EXCEPTIONS 1)

set(PICO_CXX_ENABLE_RTTI 1)

# Initialise the Pico SDK
pico_sdk_init()

# Add executable. Default name is the project name, version 0.1

add_executable(picomp3test ${CMAKE_CURRENT_LIST_DIR}/hw_config.c
                           ${CMAKE_CURRENT_LIST_DIR}/picomp3lib/test/convert.c 
                           ${CMAKE_CURRENT_LIST_DIR}/picomp3lib/test/wave.c 
                           ${CMAKE_CURRENT_LIST_DIR}/picomp3lib/test/timing.c 
                           ${CMAKE_CURRENT_LIST_DIR}/fs_mount.c
                           ${CMAKE_CURRENT_LIST_DIR}/picomp3lib/interface/music_file.c
               )

pico_set_program_name(picomp3test "picomp3test")
pico_set_program_version(picomp3test "0.1")

pico_enable_stdio_uart(picomp3test 1)
pico_enable_stdio_usb(picomp3test 0)

# Needed to access fs_mount.h
target_include_directories(picomp3test PUBLIC
                          ${CMAKE_CURRENT_LIST_DIR}/
)

add_subdirectory(no-OS-FatFS-SD-SPI-RPi-Pico/FatFs_SPI build)
add_subdirectory(picomp3lib/src)

# Add the standard library to the build
target_link_libraries(picomp3test pico_stdlib)

# Add any user requested libraries
target_link_libraries(picomp3test
#                      hardware_dma
#                      hardware_pio
                      hardware_timer
                      hardware_clocks
#                      hardware_pwm
                      FatFs_SPI 
                      picomp3lib
                     )

pico_add_extra_outputs(picomp3test)

