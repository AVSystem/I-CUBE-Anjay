# I-CUBE-Anjay

**Preview package, official version will be released through official ST pack repository**

Package contains Anjay LwM2M client library along with necessary components: X-CUBE-CELLULAR, mbedTLS,
LwIP for developement under STM32CubeMX environment.

## CubeMX Setup
To install the package, press `INSTALL/REMOVE` under install or remove embedded software packages, `From Local...` and select `.pack` file downloaded from this repository.

After installing the package, select desired components, there is Anjay LwM2M library available, support for three different modems, demo application and BSP for B-L462E-CELL1 and P-L496-CELL02
boards with implemented LwM2M sensor objects.

### B-L462E-CELL1

Start from board selector with B-L462E-CELL1 board, **do not** initialize all peripherals with their default mode.

Through `Select Components` menu choose desired components from the pack, in this example select:

- LwM2M Stack: Anjay, LwIP, mbedtls
- Device Application: FullExample
- Board Support: LwM2M Objects: B-L462E-CELL1, B-L462E-CELL1 BSP
- Board Support: X_STMOD_PLUS_MODEMS: Modem: TYPE1SC
- STM32_Cellular - Core, Platform config: B-L462E-CELL1

Apply following settings:

- Connectivity tab:
  - I2C1 - Enable
  - USART1 - Enable asynchronous, enable global interrupts
  - USART2 - Enable asynchronous, enable global interrupts
  - USART3 - Enable asynchronous, enable global interrupts
- Middleware tab:
  - FreeRTOS
    - Interface - CMSIS_V1
    - TOTAL_HEAP_SIZE - 32768 Bytes
    - USE_COUNTING_SEMAPHORES - Enabled
- Project Manager:
  - Code Generator - Enable Generate peripheral initialization as a pair of '.c/.h' files per peripheral.
- Software Packs:
  - I-CUBE-Anjay - select all enabled components and modify `Client Settings` with connection parameters. `Parameter settings` can be modified to alter Anjay LwM2M Library configuration.

Generate the project and open it in STM32CubeIDE.

Right click on the project `Build Configurations -> Set Active -> Release`

Select generated project and modify `Properties -> C/C++ Build -> Settings -> MCU Settings`

Change `Runtime library` to `Standard C`

Flash the project using `Run As -> STM32 Cortex-M C/C++ Application`


### P-L496G-CELL02

Start from board selector with STM32L496G-DISCO board, **do not** initialize all peripherals with their default mode.

Through `Select Components` menu choose desired components from the pack, in this example select:

- LwM2M Anjay
- LwM2M Stack: Anjay, LwIP, mbedtls
- Device Application: FullExample
- Board Support: LwM2M Objects: P-L496G-CELL02, P-L496G-CELL02 BSP
- Board Support X_STMOD_PLUS_MODEMS: Modem: BG96 / MONARCH
- STM32_Cellular: Core, Platform config: P-L496G-CELL02

Apply following settings:
- System Core tab:
  - SYS
    - Timebase Source - TIM1
- Connectivity tab:
  - I2C1 - Enable
  - USART1 - Enable asynchronous, enable global interrupts
  - USART2 - Enable asynchronous, enable global interrupts
- Security tab:
  - RNG - Enable
- Middleware tab:
  - FreeRTOS
    - Interface - CMSIS_V1
    - TOTAL_HEAP_SIZE - 32768 Bytes
    - USE_COUNTING_SEMAPHORES - Enabled
    - USE_TIMERS - Enabled
    - vTaskDelayUntil - Enabled
    - uxTaskGetStackHighWatermark - Enabled
- Project Manager:
  - Code Generator - Enable Generate peripheral initialization as a pair of '.c/.h' files per peripheral.
- Software Packs:
  - I-CUBE-Anjay - select all enabled components and modify `Client Settings` with connection parameters. `Parameter settings` can be modified to alter Anjay LwM2M Library configuration.


Generate the project and open it in STM32CubeIDE.

Select generated project and modify `Properties -> C/C++ Build -> Settings -> MCU Settings`

Change `Runtime library` to `Standard C`

Flash the project using `Run As -> STM32 Cortex-M C/C++ Application`


## Compilers/toolchains

This document shows step-by-step examples generated for STM32CubeIDE. This is the suggested environment.

When generating code, CubeMX might warn you that `USE_NEWLIB_REENTRANT` option must be set. However, not all the IDEs have `newlib` in their toolchain libraries and checking this option can make your project uncompilable. For IAR and Keil simply press `Yes` to skip it.

When generating a project targeted for IAR Embedded Workbench, you need to enable VLA in `Project -> Options... -> C/C++ Compiler -> Language 1 -> C dialect -> Standard C`.
IAR Embedded Workbench for ARM version 9.20.2 or higher is required to compile the project.

When generating a project targeted for ARM Keil, there will be a conflict between the toolchain's built-in and LwIP's `errno` definitions. To solve this issue you should add a Compiler Misc Control `-J ../Middlewares/Third_Party/LwIP/src/include/compat/stdc -J "$J"` (ensure there is a valid path).
