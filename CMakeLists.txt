cmake_minimum_required(VERSION 3.23.1)

project(libhello LANGUAGES CXX)

include(GNUInstallDirs)
set(LIBHELLO_INSTALL_CFGDIR ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME})

add_library(libhello libhello.cxx)
set_target_properties(libhello PROPERTIES PREFIX "")
target_sources(libhello
    PUBLIC
        FILE_SET HEADERS FILES libhello.hxx
)

install(TARGETS libhello
        EXPORT libhello-targets
        INCLUDES         DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
        ARCHIVE          DESTINATION ${CMAKE_INSTALL_LIBDIR}
        FILE_SET HEADERS DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)

install(EXPORT libhello-targets
        DESTINATION ${LIBHELLO_INSTALL_CFGDIR}
)

include(CMakePackageConfigHelpers)
configure_package_config_file(
    ${CMAKE_CURRENT_SOURCE_DIR}/cmake/config.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config.cmake
    INSTALL_DESTINATION ${LIBHELLO_INSTALL_CFGDIR}
)

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config.cmake
        DESTINATION ${LIBHELLO_INSTALL_CFGDIR}
)
