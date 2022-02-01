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

- LwM2M Anjay
- Device TYPE1SC
- Device Application - anjay
- Board Support B-L462E-CELL1

Apply following settings:

- Connectivity tab:
  - I2C1 - Enable
  - USART1 - Enable, enable global interrupts
  - USART2 - Enable, enable global interrupts
  - USART3 - Enable, enable global interrupts
- Middleware tab:
  - FreeRTOS
    - Interface - CMSIS_V1
    - TOTAL_HEAP_SIZE - 18432 Bytes (Required by X-CUBE-CELLULAR)
    - USE_COUNTING_SEMAPHORES - Enabled
- Project Manager:
  - Code Generator - Enable Generate peripheral initialization as a pair of '.c/.h' files per peripheral.
- Software Packs:
  - I-CUBE-Anjay - select all enabled components and modify `Client Settings` with connection parameters. `Parameter settings` can be modified to alter Anjay LwM2M Library configuration.

Generate the project and open in STM32CubeIDE.

Right click on the project `Build Configurations -> Set Active -> Release`

Select generated project and modify `Properties -> C/C++ Build -> Settings -> MCU Settings`

Flash the project using `Run As -> STM32 Cortex-M C\C++ Application`


### P-L496G-CELL02

Start from board selector with STM32L496G-DISCO board, **do not** initialize all peripherals with their default mode.

Through `Select Components` menu choose desired components from the pack, in this example select:

- LwM2M Anjay
- Device TYPE1SC
- Device Application - anjay
- Board Support B-L462E-CELL1

Apply following settings:

- Connectivity tab:
  - I2C1 - Enable
  - USART1 - Enable, enable global interrupts
  - USART2 - Enable, enable global interrupts
- Security tab:
  - RNG - Enable
- Middleware tab:
  - FreeRTOS
    - Interface - CMSIS_V1
    - TOTAL_HEAP_SIZE - 18432 Bytes (Required by X-CUBE-CELLULAR)
    - USE_COUNTING_SEMAPHORES - Enabled
- Project Manager:
  - Code Generator - Enable Generate peripheral initialization as a pair of '.c/.h' files per peripheral.
- Software Packs:
  - I-CUBE-Anjay - select all enabled components and modify `Client Settings` with connection parameters. `Parameter settings` can be modified to alter Anjay LwM2M Library configuration.


Generate the project and open in STM32CubeIDE.

Select generated project and modify `Properties -> C/C++ Build -> Settings -> MCU Settings`

Flash the project using `Run As -> STM32 Cortex-M C\C++ Application`
