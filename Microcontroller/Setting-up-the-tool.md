# Bare-Metal Embedded C Programming

Let's be brave and dive into this `bit`ful world of embedded C programming.
First we have to setup our toolset.


## Technical Requirement 
1. The development board we will be using is `NUCLEO-F411`
    ```bash
    NUCLEO-F411RE Development Board
            │
            └── STM32F411RE Microcontroller
                    │
                    └── ARM Cortex-M4 CPU Core
    ```
    To check the STM32 MCUs portfolio - [link](https://www.st.com/en/microcontrollers-microprocessors/stm32-32-bit-arm-cortex-mcus.html)

2. STM32CubeIDE [download link](https://www.st.com/en/development-tools/stm32cubeide.html)

3. GNU Arm Embedded Toolchain [link](https://gitlab.arm.com/tooling/gnu-toolchains-for-arm)

    ![alt text](image.png)
    ```bash
    arm-gnu-toolchain-15.3.rel1-darwin-arm64-arm-none-eabi.pkg
    │                 │         │            │             │
    │                 │         │            │             └─ Package format
    │                 │         │            └─ Target architecture
    │                 │         └─ Host: Apple Silicon macOS
    │                 └─ Toolchain version
    └─ Arm GNU Toolchain
    ```

    Let's dissect the target architecture:
    ```bash
    arm  -  none  -  eabi
    │       │       │
    │       │       └── Embedded Application Binary Interface
    │       └────────── No operating system
    └────────────────── 32-bit ARM target
    ```
    I would prefer `.pkg` over `.tar.xz` as a beginner. `.pkg` will install as regular macOS software package. With `.tar.xz`, we have granular control.

    Now our choice filters down to `eabi` or `elf`. Arm officially labels aarch64-none-elf as the AArch64 bare-metal target and arm-none-eabi as the AArch32 bare-metal target.

    Since NUCLEO-F411RE has ARM-Cortex M4 which is 32-bit core, our option boils down to 
    ```bash
    arm-gnu-toolchain-15.3.rel1-darwin-arm64-arm-none-eabi.pkg
    ```
    Here is the download [link](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/15.3.rel1/arm-gnu-toolchain-15.3.rel1-darwin-arm64-arm-none-eabi.pkg)

    I will update the list for my Fedora later.

4. OpenOCD 
    * Installation [instruction](https://xpack-dev-tools.github.io/openocd-xpack/docs/install/)
    * Package [Repo](https://github.com/xpack-dev-tools/openocd-xpack/releases)

    We will revisit this topic later when we start our project.



