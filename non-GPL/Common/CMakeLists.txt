# SPDX-License-Identifier: LicenseRef-Elastic-License-2.0

# Copyright 2021 Elasticsearch B.V. and/or licensed to Elasticsearch B.V. under one
# or more contributor license agreements. Licensed under the Elastic License 2.0;
# you may not use this file except in compliance with the Elastic License 2.0.

add_library(Common STATIC Common.c)
target_include_directories(Common PRIVATE "${LIBBPF_TARGET_INCLUDE_DIR}" "${LIBBPF_UAPI_INCLUDE_DIR}" "${LIBBPF_INCLUDE_DIR}")
add_dependencies(Common libbpf)

set_target_properties(Common PROPERTIES PUBLIC_HEADER Common.h)

configure_file(Common.h ${TARGET_INCLUDE_DIR} COPYONLY)
