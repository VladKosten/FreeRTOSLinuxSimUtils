add_subdirectory(FreeRTOSConfig)

add_library(freeRtosPortUtils STATIC ${CMAKE_CURRENT_SOURCE_DIR}/console.c)

target_include_directories(freeRtosPortUtils PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})