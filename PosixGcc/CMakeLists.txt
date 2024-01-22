add_subdirectory(FreeRtosConfig)

add_executable(RunUnitTest main.c
                           console.c
                           run-time-stats-utils.c)

target_include_directories(RunUnitTest PRIVATE ${CMAKE_CURRENT_BINARY_DIR})

target_link_libraries(RunUnitTest   PRIVATE UnitTest
                                    PRIVATE freertos_kernel
                                    PRIVATE freertos_config)

set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/.)