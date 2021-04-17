cmake_minimum_required(VERSION 3.10)

set(CMAKE_TOOLCHAIN_FILE Toolchain-arm-gcc.cmake)

# Allow assembler
enable_language(ASM)

project(example-cmake)

set(INCLUDE_DIRS

)

set(C_SRCS

)

set(ASM_SRCS

)

set(GLOBAL_DEFINES

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
