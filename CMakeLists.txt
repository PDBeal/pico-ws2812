add_library(pico_ws2812
        ws2812.cpp)

target_link_libraries(pico_ws2812
        pico_stdlib
        hardware_pio
        )

target_include_directories (pico_ws2812 PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})