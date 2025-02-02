# SPDX-License-Identifier: LicenseRef-Elastic-License-2.0

# Copyright 2021 Elasticsearch B.V. and/or licensed to Elasticsearch B.V. under one
# or more contributor license agreements. Licensed under the Elastic License 2.0;
# you may not use this file except in compliance with the Elastic License 2.0.

# Library
add_library(KprobeLoader STATIC KprobeLoader.c)

target_include_directories(KprobeLoader PRIVATE
    "${LIBELF_SRC}/common" 
    "${LIBBPF_TARGET_INCLUDE_DIR}"
    "${LIBBPF_UAPI_INCLUDE_DIR}"
    "${LIBBPF_INCLUDE_DIR}"
    "${PROJECT_SOURCE_DIR}/non-GPL/Common")

target_link_libraries(KprobeLoader Common ${LIBBPF_LIB} ${LIBELF_LIB} -lz)
add_dependencies(KprobeLoader Common libbpf libelf)

configure_file(KprobeLoader.h ${TARGET_INCLUDE_DIR} COPYONLY)

# Demo using the library
add_executable(KprobeConnectHookDemo KprobeConnectHookDemo.c)
target_include_directories(KprobeConnectHookDemo PRIVATE
    "${LIBBPF_TARGET_INCLUDE_DIR}"
    "${LIBBPF_UAPI_INCLUDE_DIR}"
    "${LIBBPF_INCLUDE_DIR}"
    "${PROJECT_SOURCE_DIR}/non-GPL/Common")

target_link_libraries(KprobeConnectHookDemo KprobeLoader)
