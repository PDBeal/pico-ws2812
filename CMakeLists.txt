
cmake_minimum_required(VERSION 3.12)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

project(pico-ws2812
    VERSION 1.0.0
    DESCRIPTION "RP2040 library for controlling strips/pixels using WS2812 (NeoPixel) LEDs using PIO and pico-sdk"
)

add_library(pico-ws2812 INTERFACE)

target_sources(pico-ws2812 INTERFACE
        ${CMAKE_CURRENT_LIST_DIR}/ws2812.cpp
)

target_include_directories(pico-ws2812 INTERFACE ${CMAKE_CURRENT_LIST_DIR})

if(PICO_SDK)
    pico_generate_pio_header(pico-ws2812 ${CMAKE_CURRENT_LIST_DIR}/ws2812.pio)
endif(PICO_SDK)

# Link to pico_stdlib (gpio, time, etc. functions)
target_link_libraries(${PROJECT_NAME} INTERFACE
    pico_stdlib
    hardware_pio
)
