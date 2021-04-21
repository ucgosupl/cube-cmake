cmake_minimum_required(VERSION 3.10)

set(CMAKE_TOOLCHAIN_FILE Toolchain-arm-gcc.cmake)

# Allow assembler
enable_language(ASM)

project(example-cmake)

set(SRC_DIR src)

set(INCLUDE_DIRS
    ${SRC_DIR}/Core/Inc
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Inc 
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Inc/Legacy 
    ${SRC_DIR}/Drivers/CMSIS/Device/ST/STM32F4xx/Include 
    ${SRC_DIR}/Drivers/CMSIS/Include
    ${SRC_DIR}/Middlewares/Third_Party/FreeRTOS/Source/include 
    ${SRC_DIR}/Middlewares/Third_Party/FreeRTOS/Source/CMSIS_RTOS_V2
    ${SRC_DIR}/Middlewares/Third_Party/FreeRTOS/Source/portable/GCC/ARM_CM4F
)

set(C_SRCS
    ${SRC_DIR}/Core/Src/dma.c
    ${SRC_DIR}/Core/Src/freertos.c
    ${SRC_DIR}/Core/Src/gpio.c
    ${SRC_DIR}/Core/Src/main.c
    ${SRC_DIR}/Core/Src/stm32f4xx_hal_msp.c
    ${SRC_DIR}/Core/Src/stm32f4xx_hal_timebase_tim.c
    ${SRC_DIR}/Core/Src/stm32f4xx_it.c
    ${SRC_DIR}/Core/Src/syscalls.c
    ${SRC_DIR}/Core/Src/sysmem.c
    ${SRC_DIR}/Core/Src/system_stm32f4xx.c
    ${SRC_DIR}/Core/Src/tim.c
    ${SRC_DIR}/Core/Src/usart.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_cortex.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_dma.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_dma_ex.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_exti.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_flash.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_flash_ex.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_flash_ramfunc.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_gpio.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_pwr.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_pwr_ex.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_rcc.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_rcc_ex.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_tim.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_tim_ex.c
    ${SRC_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_uart.c
    ${SRC_DIR}/Middlewares/Third_Party/FreeRTOS/Source/CMSIS_RTOS_V2/cmsis_os2.c
    ${SRC_DIR}/Middlewares/Third_Party/FreeRTOS/Source/croutine.c
    ${SRC_DIR}/Middlewares/Third_Party/FreeRTOS/Source/event_groups.c
    ${SRC_DIR}/Middlewares/Third_Party/FreeRTOS/Source/list.c
    ${SRC_DIR}/Middlewares/Third_Party/FreeRTOS/Source/queue.c
    ${SRC_DIR}/Middlewares/Third_Party/FreeRTOS/Source/stream_buffer.c
    ${SRC_DIR}/Middlewares/Third_Party/FreeRTOS/Source/tasks.c
    ${SRC_DIR}/Middlewares/Third_Party/FreeRTOS/Source/timers.c
    ${SRC_DIR}/Middlewares/Third_Party/FreeRTOS/Source/portable/GCC/ARM_CM4F/port.c
    ${SRC_DIR}/Middlewares/Third_Party/FreeRTOS/Source/portable/MemMang/heap_4.c
)

set(ASM_SRCS
    ${SRC_DIR}/Core/Startup/startup_stm32f407vgtx.s
)

set(GLOBAL_DEFINES
    #-DDEBUG
    -DUSE_HAL_DRIVER
    -DSTM32F407xx
)

set(LINKED_LIBS

)

link_directories(

)

include_directories(${INCLUDE_DIRS})
add_definitions(${GLOBAL_DEFINES})

include(compiler_flags.cmake)

add_arm_executable(${CMAKE_PROJECT_NAME} ${CPP_SRCS} ${C_SRCS} ${ASM_SRCS})

arm_link_libraries(${CMAKE_PROJECT_NAME} ${LINKED_LIBS})
