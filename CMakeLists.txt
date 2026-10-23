
cmake_minimum_required(VERSION 3.10)

project(Marston)

if(NOT DEFINED ENV{VITASDK})
    message(FATAL_ERROR "VITASDK is not set")
endif()

include("$ENV{VITASDK}/share/vita.cmake" REQUIRED)

set(VITA_APP_NAME "Marston")
set(VITA_TITLEID "MRST00001")
set(VITA_VERSION "01.00")

add_executable(marston
    main.c
)

target_link_libraries(marston
    SceDisplay_stub
    SceCtrl_stub
)

vita_create_self(eboot.bin marston)
vita_create_vpk(Marston.vpk ${VITA_TITLEID} eboot.bin
    VERSION ${VITA_VERSION}
)
