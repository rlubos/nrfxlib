#
# Copyright (c) 2019 Nordic Semiconductor
#
# SPDX-License-Identifier: LicenseRef-BSD-5-Clause-Nordic
#

include(${NRFXLIB_DIR}/common.cmake)

nrfxlib_calculate_lib_path(lib_path)

if (CONFIG_NRFXLIB_LWM2M_CARRIER)

set(NRF_LWM2M_CARRIER_LIB_PATH ${CMAKE_CURRENT_SOURCE_DIR}/${lib_path})

if(NOT EXISTS ${NRF_LWM2M_CARRIER_LIB_PATH})
  message(WARNING "This combination of SoC and floating point ABI is not supported by the nrf_lwm2m_carrier lib."
                  "(${NRF_LWM2M_CARRIER_LIB_PATH} doesn't exist.)")
endif()

set(                    NRF_LWM2M_CARRIER_TARGET ${IMAGE}libnrf_lwm2m_carrier)
zephyr_library_import(${NRF_LWM2M_CARRIER_TARGET} ${NRF_LWM2M_CARRIER_LIB_PATH}/libnrf_lwm2m_carrier.a)
target_link_libraries(${NRF_LWM2M_CARRIER_TARGET} INTERFACE ${IMAGE}bsd_nrf9160_xxaa -lc)

zephyr_include_directories(include)

endif()
