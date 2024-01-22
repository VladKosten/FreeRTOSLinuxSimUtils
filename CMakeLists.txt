cmake_minimum_required(VERSION 3.20)

project(FreeRtosSimUtills)

if(WIN32)
    message(STATUS "WINDOWS")
    add_subdirectory(Win32MiniGw)
else()
    message(STATUS "UNIX")
    add_subdirectory(PosixGcc)
endif()

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
set( FREERTOS_HEAP "3")
# Select the native compile PORT
if(WIN32)
    message(STATUS "Windows, setting FREERTOS_PORT=MSVC_MINIGW")
    set(FREERTOS_PORT "MSVC_MINGW")
else()
    message(STATUS "UNIX, setting FREERTOS_PORT=GCC_POSIX")
    set(FREERTOS_PORT "GCC_POSIX")
endif()
# And make it available
FetchContent_MakeAvailable(freertos_kernel)