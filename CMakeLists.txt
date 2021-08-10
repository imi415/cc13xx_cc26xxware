cmake_minimum_required(VERSION 3.15)

set(CMAKE_TRY_COMPILE_TARGET_TYPE "STATIC_LIBRARY")

project(cc13xx_26xxware)

if(CMAKE_C_COMPILER_ID MATCHES "Clang")
    set(COMMON_FLAGS
        "--target=armv7m-none-eabi" "-mcpu=cortex-m3" "-mthumb")
elseif(CMAKE_C_COMPILER_ID MATCHES "GNU")
    set(COMMON_FLAGS
        "-march=armv7-m" "-mcpu=cortex-m3" "-mthumb")
else()
  message(FATAL_ERROR "Not an supported compiler!! ${CMAKE_C_COMPILER_ID}")    
endif()

set(CC26XXWARE_DIR "cc26xxware_2_24_03_17272")
set(CC13XXWARE_DIR "cc13xxware_2_04_03_17272")

file(GLOB_RECURSE CC26XXWARE_SRCS
    "${CC26XXWARE_DIR}/driverlib/*.c"
)

file(GLOB_RECURSE CC13XXWARE_SRCS
    "${CC13XXWARE_DIR}/driverlib/*.c"
)

set(CC26XXWARE_INCS
    "${CC26XXWARE_DIR}"
)

set(CC13XXWARE_INCS
    "${CC13XXWARE_DIR}"
)

add_library(cc26xxware ${CC26XXWARE_SRCS})
add_library(cc13xxware ${CC13XXWARE_SRCS})

target_include_directories(cc26xxware PRIVATE ${CC26XXWARE_INCS})
target_include_directories(cc13xxware PRIVATE ${CC13XXWARE_INCS})

target_compile_options(cc26xxware PRIVATE ${COMMON_FLAGS})
target_compile_options(cc13xxware PRIVATE ${COMMON_FLAGS})

