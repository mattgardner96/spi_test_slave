cmake_minimum_required(VERSION 3.13)

include(pico_sdk_import.cmake)

project(multi_spi)

pico_sdk_init()

if (TARGET tinyusb_device)
    add_executable(multi_spi
            main.cpp
            )

        add_subdirectory(pico-ssd1306)

        target_link_libraries(multi_spi
                hardware_i2c
                pico_ssd1306
                hardware_spi
                pico_printf)

        # enable usb output, disable uart output
        pico_enable_stdio_usb(multi_spi 1)
        pico_enable_stdio_uart(multi_spi 0)

        pico_add_extra_outputs(multi_spi)

elseif(PICO_ON_DEVICE)
        message(WARNING "not building multi_spi because TinyUSB submodule is not initialized in the SDK")
    endif()