# Kconfig - nRF91 Thingy:91 X board configuration
#
# Copyright (c) 2024 Nordic Semiconductor
# SPDX-License-Identifier: LicenseRef-Nordic-5-Clause

if(CONFIG_BOARD_THINGY91X_NRF9151 OR CONFIG_BOARD_THINGY91X_NRF9151_NS)
  zephyr_library()
  zephyr_library_sources_ifdef(CONFIG_WIFI_NRF700X nrf70_support.c)
endif()

if(CONFIG_BOARD_THINGY91X_NRF9151_NS)
  # Use static partition layout to ensure the partition layout remains
  # unchanged after DFU. This needs to be made globally available
  # because it is used in other CMake files.
  set(PM_STATIC_YML_FILE ${CMAKE_CURRENT_LIST_DIR}/thingy91x_pm_static.yml CACHE INTERNAL "")
endif()

if(CONFIG_BOARD_THINGY91X_NRF5340_CPUAPP OR CONFIG_BOARD_THINGY91X_NRF5340_CPUAPP_NS)
  zephyr_library()
  zephyr_library_sources_ifdef(CONFIG_BOARD_ENABLE_CPUNET nrf5340_cpunet_reset.c)
  set(PM_STATIC_YML_FILE ${CMAKE_CURRENT_LIST_DIR}/thingy91x_nrf5340_pm_static.yml CACHE INTERNAL "")
endif()
