# SPDX-License-Identifier: GPL-3.0-only
# Copyright (c) 2023 CERN
#
# Please retain this header in all redistributions and modifications of the code.

cmake_minimum_required(VERSION 3.25)
project(common_cells NONE)

add_ip(tech_cells_generic
    VENDOR pulp_platform
    LIBRARY ip
    VERSION 0.2.13
    )

ip_include_directories(${IP} SYSTEMVERILOG
    ${PROJECT_SOURCE_DIR}/include
)

# TODO add SYSTEMVERILOG_BHV category
ip_sources(${IP} SYSTEMVERILOG
    # ${PROJECT_SOURCE_DIR}/src/deprecated/cluster_clk_cells.sv
    # ${PROJECT_SOURCE_DIR}/src/deprecated/cluster_pwr_cells.sv
    # ${PROJECT_SOURCE_DIR}/src/deprecated/generic_memory.sv
    # ${PROJECT_SOURCE_DIR}/src/deprecated/generic_rom.sv
    # ${PROJECT_SOURCE_DIR}/src/deprecated/pad_functional.sv
    # ${PROJECT_SOURCE_DIR}/src/deprecated/pulp_buffer.sv
    # ${PROJECT_SOURCE_DIR}/src/deprecated/pulp_clk_cells.sv
    # ${PROJECT_SOURCE_DIR}/src/deprecated/pulp_pwr_cells.sv
    ${PROJECT_SOURCE_DIR}/src/rtl/tc_clk.sv
    ${PROJECT_SOURCE_DIR}/src/rtl/tc_sram.sv
    ${PROJECT_SOURCE_DIR}/src/tc_pwr.sv
)

ip_sources(${IP} SYSTEMVERILOG_FPGA
    # {PROJECT_SOURCE_DIR}/src/deprecated/cluster_clk_cells_xilinx.sv
    # {PROJECT_SOURCE_DIR}/src/deprecated/cluster_pwr_cells.sv
    # {PROJECT_SOURCE_DIR}/src/deprecated/pulp_clk_cells_xilinx.sv
    # {PROJECT_SOURCE_DIR}/src/deprecated/pulp_pwr_cells.sv
    # {PROJECT_SOURCE_DIR}/src/deprecated/pulp_buffer.sv
    ${PROJECT_SOURCE_DIR}/src/fpga/tc_clk_xilinx.sv
    ${PROJECT_SOURCE_DIR}/src/fpga/tc_sram_xilinx.sv
    ${PROJECT_SOURCE_DIR}/src/tc_pwr.sv
)

if(NOT PROJECT_IS_TOP_LEVEL)
    set(RTL_LIB_NAME ${IP} PARENT_SCOPE)
endif()
