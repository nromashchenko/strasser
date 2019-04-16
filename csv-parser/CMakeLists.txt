cmake_minimum_required(VERSION 3.10 FATAL_ERROR)

# It is possible to define CSV_IO_NO_THREAD here and disable thread support.
# See include/csv-parser/csv.h
find_package(Threads REQUIRED)

add_library(csv_parser INTERFACE)
add_library(strasser::csv_parser ALIAS csv_parser)

target_include_directories(csv_parser
        INTERFACE
        $<INSTALL_INTERFACE:include>
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        )

target_link_libraries(csv_parser
        INTERFACE
            Threads::Threads
)

###################################################################################################
# Installation instructions

include(GNUInstallDirs)
set(INSTALL_CONFIGDIR ${CMAKE_INSTALL_LIBDIR}/cmake/strasser)

install(TARGETS csv_parser
        EXPORT strasser-targets
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
        )

install(DIRECTORY include/
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

# Export the target
install(EXPORT strasser-targets
        FILE strasserTargets.cmake
        NAMESPACE strasser::
        DESTINATION ${INSTALL_CONFIGDIR}
        )

export(EXPORT strasser-targets
        FILE ${CMAKE_CURRENT_BINARY_DIR}/strasserTargets.cmake
        NAMESPACE strasser::)

export(PACKAGE strasser)