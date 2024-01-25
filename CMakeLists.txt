cmake_minimum_required(VERSION 3.20)

project(FreeRtosSimUtills)

add_subdirectory(FreeRtosConfig)

#Add fetch content to the project
include(FetchContent)

# Consume FreeRTOS
FetchContent_Declare(
    freertos_kernel
    GIT_REPOSITORY https://github.com/FreeRTOS/FreeRTOS-Kernel.git
    GIT_TAG        V10.6.0
)
# Select the heap port
message(STATUS "Setting FREERTOS_HEAP=3")
set(FREERTOS_HEAP "3")
# Select the native compile PORT
message(STATUS "UNIX, setting FREERTOS_PORT=GCC_POSIX")
set(FREERTOS_PORT "GCC_POSIX")
# And make it available
FetchContent_MakeAvailable(freertos_kernel)

add_executable(RunUnitTest main.c
                           console.c
                           run-time-stats-utils.c)

target_include_directories(RunUnitTest PRIVATE ${CMAKE_CURRENT_BINARY_DIR})

target_link_libraries(RunUnitTest   PRIVATE UnitTest
                                    PRIVATE freertos_kernel
                                    PRIVATE freertos_config)

set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/.)