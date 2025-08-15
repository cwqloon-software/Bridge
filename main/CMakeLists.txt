set(SRCS
        main.c
        tcp_server.c
        msp_ltm_serial.c
        http_server.c
        db_esp32_control.c
        db_crc.c
        db_esp_now.c
        db_serial.c
        db_mavlink_msgs.c
        db_parameters.c
        usbip_server.c
        usb_desc.c
        usb_cdc_handler.c
        cdc_uart.c
        DAP_handle.c
        msc_disk.c
        )

if(CONFIG_BT_ENABLED)
    list(APPEND SRCS db_ble.c)
endif()

idf_component_register(SRCS ${SRCS}
        INCLUDE_DIRS ".")


if(CONFIG_WEB_DEPLOY_SF)
    set(WEB_SRC_DIR "${CMAKE_BINARY_DIR}/frontend")
    spiffs_create_partition_image(www ${WEB_SRC_DIR} FLASH_IN_PROJECT DEPENDS frontend)
endif()

# 添加以下行来启用 C++ 支持
set(COMPONENT_REQUIRES "${COMPONENT_REQUIRES}" esp_common)
set(COMPONENT_PRIV_REQUIRES "")

# 设置 C++ 标准版本（如 11、14 或 17）
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
