#/*************************************************************************************************
# * Copyright (c) 2021 Calypso Networks Association https://calypsonet.org/                       *
# *                                                                                               *
# * See the NOTICE file(s) distributed with this work for additional information regarding        *
# * copyright ownership.                                                                          *
# *                                                                                               *
# * This program and the accompanying materials are made available under the terms of the Eclipse *
# * Public License 2.0 which is available at http://www.eclipse.org/legal/epl-2.0                 *
# *                                                                                               *
# * SPDX-License-Identifier: EPL-2.0                                                              *
# *************************************************************************************************/

PROJECT(KeypleCardGenericCppLib C CXX)
CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

SET(VERSION_MAJOR "2")
SET(VERSION_MINOR "0")
SET(VERSION_PATCH "0")

SET(VERSION "${VERSION_MAJOR}.${VERSION_MINOR}.${VERSION_PATCH}")

SET(PACKAGE_NAME "keyple-card-generic-cpp-lib")
SET(PACKAGE_VERSION ${VERSION})
SET(PACKAGE_STRING "${PACKAGE_NAME} ${PACKAGE_VERSION}")

SET(CMAKE_MACOSX_RPATH 1)
SET(CMAKE_CXX_STANDARD 11)

SET(LIBRARY_NAME keyplecardgenericcpplib)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DKEYPLECARDGENERIC_EXPORT")

SET(CALYPSONET_CARD_DIR    "../../../github.com.calypsonet.calypsonet-terminal-card-cpp-api")
SET(CALYPSONET_READER_DIR  "../../../github.com.calypsonet.calypsonet-terminal-reader-cpp-api")
SET(CALYPSONET_CALYPSO_DIR "../../../github.com.calypsonet.calypsonet-terminal-calypso-cpp-api")
SET(KEYPLE_COMMON_DIR      "../../../github.com.calypsonet.keyple-common-cpp-api")
SET(KEYPLE_PLUGIN_DIR      "../../../github.com.calypsonet.keyple-plugin-cpp-api")
SET(KEYPLE_UTIL_DIR        "../../../github.com.calypsonet.keyple-util-cpp-lib")
SET(KEYPLE_SERVICE_DIR     "../../../github.com.calypsonet.keyple-service-cpp-lib")
SET(KEYPLE_RESOURCE_DIR    "../../../github.com.calypsonet.keyple-service-resource-cpp-lib")
SET(KEYPLE_UTIL_LIB        "keypleutilcpplib")

INCLUDE_DIRECTORIES(
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/cpp/exception

    ${CALYPSONET_CARD_DIR}/src/main
    ${CALYPSONET_CARD_DIR}/src/main/spi

    ${CALYPSONET_READER_DIR}/src/main
    ${CALYPSONET_READER_DIR}/src/main/selection
    ${CALYPSONET_READER_DIR}/src/main/selection/spi
    ${CALYPSONET_READER_DIR}/src/main/spi

    ${CALYPSONET_CALYPSO_DIR}/src/main
    ${CALYPSONET_CALYPSO_DIR}/src/main/card
    ${CALYPSONET_CALYPSO_DIR}/src/main/sam

    ${KEYPLE_COMMON_DIR}/src/main

    ${KEYPLE_PLUGIN_DIR}/src/main
    ${KEYPLE_PLUGIN_DIR}/src/main/spi
    ${KEYPLE_PLUGIN_DIR}/src/main/spi/reader
    ${KEYPLE_PLUGIN_DIR}/src/main/spi/reader/observable
    ${KEYPLE_PLUGIN_DIR}/src/main/spi/reader/observable/state/insertion
    ${KEYPLE_PLUGIN_DIR}/src/main/spi/reader/observable/state/processing
    ${KEYPLE_PLUGIN_DIR}/src/main/spi/reader/observable/state/removal

    ${KEYPLE_UTIL_DIR}/src/main
    ${KEYPLE_UTIL_DIR}/src/main/cpp
    ${KEYPLE_UTIL_DIR}/src/main/cpp/exception

    ${KEYPLE_SERVICE_DIR}/src/main/cpp

    ${KEYPLE_RESOURCE_DIR}/src/main/spi
)

ADD_LIBRARY(
    ${LIBRARY_NAME}

    ${LIBRARY_TYPE}

    ${CMAKE_CURRENT_SOURCE_DIR}/ApduRequestAdapter.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/CardRequestAdapter.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/CardSelectorAdapter.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/CardTransactionManagerAdapter.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/GenericCardAdapter.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/GenericCardResourceProfileExtensionAdapter.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/GenericCardSelectionRequestAdapter.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/GenericExtensionService.cpp
)

FIND_LIBRARY(UTIL ${KEYPLE_UTIL_LIB} HINTS ${KEYPLE_UTIL_DIR}/build/bin)

TARGET_LINK_LIBRARIES(${LIBRARY_NAME} ${UTIL})
