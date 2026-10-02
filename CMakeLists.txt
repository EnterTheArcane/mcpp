#
# Copyright (c) Contributors to the Open 3D Engine Project.
# For complete copyright and license terms please see the LICENSE at the root of this distribution.
#
# SPDX-License-Identifier: Apache-2.0 OR MIT
#

cmake_minimum_required(VERSION 3.20)
project(mcpp VERSION 2.7.2 LANGUAGES C)

include(GNUInstallDirs)

option(BUILD_SHARED_LIBS "Build shared libraries" OFF)

add_library(mcpp
    include/mcpp_lib.h
    include/mcpp_out.h
    include/mcpp.h
    src/directive.c
    src/eval.c
    src/expand.c
    src/internal.h
    src/main.c
    src/mbchar.c
    src/noconfig.h
    src/support.c
    src/system.c
    src/system.h
)

add_library(mcpp::mcpp ALIAS mcpp)

target_include_directories(mcpp PUBLIC
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>"
    "$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>"
)

target_compile_definitions(mcpp
    PRIVATE
        MCPP_LIB=1
        DLL_EXPORT=$<BOOL:${BUILD_SHARED_LIBS}>
    INTERFACE
        MCPP_DLL_IMPORT=$<BOOL:${BUILD_SHARED_LIBS}>
)

target_compile_features(mcpp PRIVATE c_std_99)

set_target_properties(mcpp PROPERTIES
    POSITION_INDEPENDENT_CODE ON
    UNITY_BUILD OFF
)

install(
    TARGETS mcpp
    EXPORT mcpp-targets
)
install(
    DIRECTORY include/
    DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)
install(
    EXPORT mcpp-targets
    FILE mcpp-config.cmake
    NAMESPACE mcpp::
    DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/mcpp"
)
install(
    FILES LICENSE.txt LICENSE_APACHE2.txt LICENSE_MIT.txt
    DESTINATION "${CMAKE_INSTALL_DATADIR}/licenses/mcpp"
)
