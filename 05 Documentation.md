# Documentation

---

## Language

All documentation is prefferably in English.

## Readme

Each project must contain a `README.md` file that explains the file structure and the most important files. 

Put yourself in the position where you have to take over your own project. 
What information do you need to get familiar with the project as quickly as possible?

## Code Comments

Comments are documentation enough - as long as they are updated when code changes. 
Better 3 lines of comment than 1 line.

Every function must be accompanied by a Doxygen-compatible comment.
At least the following keywords must be present:

- `@brief`

The keyword `@see` or `@note` is desirable when referencing other software projects, datasheets, or other sources.

**Example:**
/**
  * @brief  reads from internal registers
  * @param  *ads pointer to ads handle
  * @param  reg  first register to be read
  * @param  *pData pointer for return data
  * @param  n number of registers to read
  * @return register value read from chip
  * @see    Datasheet Fig. 34 RREG Command Example
  * @todo   fix issue #5
  */
uint8_t ADS125X_Register_Read(ADS125X_t *ads, uint8_t reg, uint8_t* pData, uint8_t n)

## File Header

Each newly created file (source / header) must contain a comment header. 
At least the following Doxygen keywords must be present:
- `@file`
- `@brief`
- `@author`
- `@date`

Desirable are `@note` and `@see` with references to external sources. 
In addition, a copyright statement (according to) open source licenses is necessary or desirable.

**Example:**

```c
/** 
  ******************************************************************************
  * @file    main.c
  * @brief   Firmware for Silent Generator Micro SO8 "Comparator"
  *           - controlls one RGBW LED as battery meter
  *           - reads ADC value from battery voltage
  *           - reads ADC value for Power LED brightness
  *           - PWM control of white Power LED
  * @author  simon.burkhardt@eta-systems.ch
  * @version 0.3.0
  * @date    2021-04-09
  * 
  * @note    stm8s001j3Mx
  * @note    IAR Embedded Workbench for STM8 v3.11.1
  *          PC-locked license
  *          IAR for STMicroelectronics STM8, 8K KickStart Edition 3.11
  * 
  * @note    see CubeMX PDF
  *
  * @note    Code Size: 5'457 bytes (approximately)
  * 
  ******************************************************************************
  * Copyright (c) 2021 eta Systems GmbH
  ******************************************************************************
  */
```

## Spliting Code Sections

The subdivision and structuring into sections are not mandatory but already given for STM32 projects. 
Such a subdivision is also desirable for other projects or libraries.

```c
/* Includes ------------------------------------------------------------------*/

/* Typedef -------------------------------------------------------------------*/

/* Define --------------------------------------------------------------------*/

/* Macro ---------------------------------------------------------------------*/

/* Variables -----------------------------------------------------------------*/

/* Function Prototypes -------------------------------------------------------*/

/* User Main -----------------------------------------------------------------*/

  /* Infinite Loop -----------------------------------------------------------*/
```



## Backup and File History

Compiled binaries are important for production and tracking of already produced devices. 
If a customer sends in a defective device you may want to reproduce issues using an older firmware.
The older firmware could be build from a previous release tag in the git repository. 
However, maybe your IDE / toolchain have changed. It is always desirable to keep a log of the actual binaries.

Once software is actively in use in a manufactured or sold product, the binary file must be stored in the file repository.

Use a specific location for this (cloud storage / network drive etc.)

`Binaries > [Project Name] > [MCU Type] > [Version] > firmware_v0.0.0_yyyy-MM-dd.hex`

or

`Binaries > [Project Name] > [Hardware Revision] > [Version] > firmware_v0.0.0_yyyy-MM-dd.hex`

e.g.

`./Binaries/2.501.113.01/STM32F373cc/v7/firmware_v7.0.0_2021-05-21.hex`



