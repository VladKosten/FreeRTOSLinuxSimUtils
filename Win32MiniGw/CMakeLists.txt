add_subdirectory(FreeRtosConfig)

add_executable(RunUnitTest  main.c
                            run-time-stats-utils.c)

target_link_libraries(RunUnitTest   PRIVATE UnitTest
                                    PUBLIC freertos_kernel)
