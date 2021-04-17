cmake_minimum_required(VERSION 3.10)

set(CMAKE_TOOLCHAIN_FILE Toolchain-arm-gcc.cmake)

# Allow assembler
enable_language(ASM)

project(audio-cmake)

set(SRC_DIR src)

set(INCLUDE_DIRS
-I${SRC_DIR}/Inc
-I${SRC_DIR}/Drivers/CMSIS/Device/ST/STM32F4xx/Include
-I${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Inc
-I${SRC_DIR}/Drivers/BSP/STM32F4-Discovery
-I${SRC_DIR}/Middlewares/ST/STM32_USB_Device_Library/Core/Inc
-I${SRC_DIR}/Middlewares/ST/STM32_USB_Host_Library/Class/MSC/Inc
-I${SRC_DIR}/Middlewares/ST/STM32_USB_Host_Library/Core/Inc
-I${SRC_DIR}/Middlewares/ST/STM32_Audio/Addons/PDM/Inc
-I${SRC_DIR}/Middlewares/Third_Party/FatFs/src
-I${SRC_DIR}/Drivers/CMSIS/Include
)

set(C_SRCS
    ${SRC_DIR}/Src/main.c
    ${SRC_DIR}/Src/stm32f4xx_it.c
    ${SRC_DIR}/Src/usbh_conf.c
    ${SRC_DIR}/Src/waveplayer.c
    ${SRC_DIR}/Src/waverecorder.c
    ${SRC_DIR}/Drivers/BSP/Components/cs43l22/cs43l22.c
    ${SRC_DIR}/Drivers/BSP/Components/lis302dl/lis302dl.c
    ${SRC_DIR}/Drivers/BSP/Components/lis3dsh/lis3dsh.c
    ${SRC_DIR}/Drivers/BSP/STM32F4-Discovery/stm32f4_discovery.c
    ${SRC_DIR}/Drivers/BSP/STM32F4-Discovery/stm32f4_discovery_accelerometer.c
    ${SRC_DIR}/Drivers/BSP/STM32F4-Discovery/stm32f4_discovery_audio.c
    ${SRC_DIR}/Src/system_stm32f4xx.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_cortex.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_dma.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_flash.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_flash_ex.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_gpio.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_hcd.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_i2c.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_i2c_ex.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_i2s.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_i2s_ex.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_pwr.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_pwr_ex.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_rcc.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_rcc_ex.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_rtc.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_spi.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_tim.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_tim_ex.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_ll_fmc.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_ll_usb.c
    ${SRC_DIR}/Middlewares/Third_Party/FatFs/src/diskio.c
    ${SRC_DIR}/Middlewares/Third_Party/FatFs/src/ff.c
    ${SRC_DIR}/Middlewares/Third_Party/FatFs/src/ff_gen_drv.c
    ${SRC_DIR}/Src/usbh_diskio_dma.c
    ${SRC_DIR}/Middlewares/Third_Party/FatFs/src/option/syscall.c
    ${SRC_DIR}/Middlewares/Third_Party/FatFs/src/option/unicode.c
    ${SRC_DIR}/Middlewares/ST/STM32_USB_Host_Library/Class/MSC/Src/usbh_msc.c
    ${SRC_DIR}/Middlewares/ST/STM32_USB_Host_Library/Class/MSC/Src/usbh_msc_bot.c
    ${SRC_DIR}/Middlewares/ST/STM32_USB_Host_Library/Class/MSC/Src/usbh_msc_scsi.c
    ${SRC_DIR}/Middlewares/ST/STM32_USB_Host_Library/Core/Src/usbh_core.c
    ${SRC_DIR}/Middlewares/ST/STM32_USB_Host_Library/Core/Src/usbh_ctlreq.c
    ${SRC_DIR}/Middlewares/ST/STM32_USB_Host_Library/Core/Src/usbh_ioreq.c
    ${SRC_DIR}/Middlewares/ST/STM32_USB_Host_Library/Core/Src/usbh_pipes.c
)

set(ASM_SRCS
    ${SRC_DIR}/SW4STM32/startup_stm32f407xx.s
)

set(GLOBAL_DEFINES
    -DUSE_HAL_DRIVER
    -DSTM32F407xx
    -DUSE_STM32F4_DISCO
)

set(LINKED_LIBS
    PDMFilter_CM4_GCC_wc32
)

link_directories(
    ${SRC_DIR}/Middlewares/ST/STM32_Audio/Addons/PDM/Lib
)

include_directories(${INCLUDE_DIRS})
add_definitions(${GLOBAL_DEFINES})

include(compiler_flags.cmake)

add_arm_executable(${CMAKE_PROJECT_NAME} ${CPP_SRCS} ${C_SRCS} ${ASM_SRCS})

arm_link_libraries(${CMAKE_PROJECT_NAME} ${LINKED_LIBS})
