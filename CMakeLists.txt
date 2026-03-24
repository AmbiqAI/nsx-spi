if(NOT DEFINED NSX_BOARD_FLAGS_TARGET)
    message(FATAL_ERROR "Board must define NSX_BOARD_FLAGS_TARGET before ns-spi is added.")
endif()

add_library(nsx_spi STATIC
    ${CMAKE_CURRENT_LIST_DIR}/src/ns_spi.c
)
set_target_properties(nsx_spi PROPERTIES EXPORT_NAME spi)
add_library(nsx::spi ALIAS nsx_spi)

target_link_libraries(nsx_spi PUBLIC
    ${NSX_BOARD_FLAGS_TARGET}
    nsx_soc_hal
    nsx_harness
)

target_include_directories(nsx_spi PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/includes-api>
    $<BUILD_INTERFACE:${NSX_ROOT}/modules/nsx-harness/includes-api>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/nsx/modules/nsx-spi/includes-api>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/nsx/modules/nsx-harness/includes-api>
)

install(DIRECTORY
    ${CMAKE_CURRENT_LIST_DIR}/includes-api
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/nsx/modules/nsx-spi
)

install(TARGETS
    nsx_spi
    EXPORT nsxTargets
)
