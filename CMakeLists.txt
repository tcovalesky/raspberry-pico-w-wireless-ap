cmake_minimum_required(VERSION 3.13)

set(PICO_BOARD pico_w)

# initialize the SDK based on PICO_SDK_PATH
# note: this must happen before project()
include(pico_sdk_import.cmake)
include(pico_extras_import_optional.cmake)

project(wireless_access_point)

set(LIB_PICO_CYW43_ARCH 1)
set(CYW43_LWIP 1)
set(PICO_CYW43_ARCH_POL 1)

# initialize the Raspberry Pi Pico SDK
pico_sdk_init()

add_executable(wireless_access_point
    wireless_access_point.c
    dhcpserver/dhcpserver.c
    dnsserver/dnsserver.c
    )

target_include_directories(wireless_access_point PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}
    ${CMAKE_CURRENT_LIST_DIR}/dhcpserver
    ${CMAKE_CURRENT_LIST_DIR}/dnsserver
    )

target_link_libraries(wireless_access_point
    pico_stdlib              # for core functionality
    pico_cyw43_arch_lwip_threadsafe_background
    )

pico_add_extra_outputs(wireless_access_point)

