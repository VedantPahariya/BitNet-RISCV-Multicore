# BitNet-RISCV-Multicore: 1-Bit LLM Orchestration on Multi-Core RISC-V Vector Accelerators

![RISC-V](https://img.shields.io/badge/Architecture-RISC--V-orange)
![LLM](https://img.shields.io/badge/Domain-1--Bit_LLM-blue)
![Vector Extension](https://img.shields.io/badge/Extension-RVV_1.0-green)

This consolidated repository contains the source code, hardware architecture extensions, and documentation for the "Hardware for AI" project: **Bitnet (1-bit LLM) orchestration on multi-core RISC-V accelerator-vector cores**.

## 📌 Project Overview

This project aims to enhance PULP's **Ara multicore RISC-V architecture** with custom accelerator extensions to efficiently implement and orchestrate **1-bit Large Language Models (BitNet)** natively on RISC-V based hardware. 

By leveraging the RISC-V Vector (RVV 1.0) architecture and exploring both single- and multi-core vector processing patterns (inspired by *Ara2: Exploring Single- and Multi-Core Vector Processing With an Efficient RVV 1.0 Compliant Open-Source Processor*), we created a highly optimized hardware-software co-design to facilitate ultra-low precision neural network inference.

### Key Highlights
* **1-Bit LLM Implementation**: Deployment and testing of BitNet algorithms tailored for constrained environments without sacrificing significant model fidelity.
* **Vectorized Architecture**: Enhancements to the CVA6 core and Ara vector processor to support rapid 1-bit MAC (Multiply-Accumulate) / Bit-serial operations.
* **Systolic Array Integration**: Exploring matrix multiplication acceleration via Gemmini.
* **Scalable Orchestration**: Workload distribution across a multi-core paradigm.

---

## 📂 Repository Structure (Submodules)

This project spans multiple subsystems. To manage the complexity, this repository links to the following submodules, each containing specific enhancements for the 1-bit LLM orchestration:

### 1. [Ara-Multicore](https://github.com/VedantPahariya/Ara-Multicore)
Top-level multi-core SoC design, interconnects, and orchestration logic for scaling the Ara vector units alongside multiple CVA6 cores. 

### 2. [Ara (Development Branch)](https://github.com/VedantPahariya/ara/tree/development)
Our custom fork of the Ara vector processor. 
* **Modifications**: Includes specific RVV 1.0 custom instructions and optimizations to optimally pipeline the 1-bit weight calculations needed by BitNet.

### 3. [CVA6 (Vector-Integration Branch)](https://github.com/VedantPahariya/cva6/tree/vector-integration)
Our branch of the Application class configurable RISC-V CPU (CVA6).
* **Modifications**: Custom decoding and tight coupling for the Ara vector extension to dispatch 1-bit specific vector instructions seamlessly.

### 4. [Gemmini](https://github.com/VedantPahariya/Gemmini)
Systolic array integration. We leverage the spatial architecture of Gemmini to co-process dense matrix operations that complement the vector-level optimizations.

---

## 🚀 Getting Started

To clone this repository and pull all the associated submodules containing the complete system:

`ash
git clone --recurse-submodules https://github.com/VedantPahariya/BitNet-RISCV-Multicore.git
cd BitNet-RISCV-Multicore
`

*Note: If you have already cloned the repository without submodules, run:*
`ash
git submodule update --init --recursive
`

## 🛠️ Build and Simulation

*Due to the multi-component nature of this project, you will need tools like **Verilator**, **VCS**, and the **RISC-V GNU Toolchain**.*

1. **Toolchain Setup**: Ensure you build the RISC-V toolchain with the `rv64gcv` architecture flag.
2. **Cores & Vector Units**: Navigate to the `ara` and `cva6` submodules to run RTL simulations.
3. **Software Stack**: BitNet kernels mapped to the RVV 1.0 intrinsics can be compiled and simulated using Spike or directly on the RTL.

## 📄 Documentation and Reports

* **Project Report**: Details our methodology, bit-serial hardware enhancements, evaluation against baseline RISC-V cores, and final throughput/latency metrics.
* **Presentation**: Slides detailing the architectural modifications and the BitNet deployment phase.

---
*Developed as part of the "Hardware for AI" Course.*
