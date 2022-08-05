# Code Templates

---

## IDE Templates

(todo)

## Frequently used Code

### main.h

**Include stdio for printf**

```c
#include <stdio.h>  // printf ( linker flag: "-u _printf_float" uses 7kB memory)
```

```c
/**
 *  @see https://github.com/STMicroelectronics/STM32CubeF4/blob/master/Projects/STM32F401RE-Nucleo/Examples/UART/UART_Printf/Src/main.c
 */
#ifdef __GNUC__
/* With GCC, small printf (option LD Linker->Libraries->Small printf
 set to 'Yes') calls __io_putchar() */
#define PUTCHAR_PROTOTYPE int __io_putchar(int ch)
#else
#define PUTCHAR_PROTOTYPE int fputc(int ch, FILE *f)
#endif /* __GNUC__ */

/* USER CODE BEGIN Private defines */
#define _LEN_VERSION_STR (48) // v12.345.678 (Jan 01 1970 22:29:37)\n
#define _VERSION_MAJOR (1)
#define _VERSION_MINOR (4)
#define _VERSION_PATCH (12)
#define _LEN_PCB_STR (16)
#define _PCB_REVISION "2.xxx.xxx.xxx" 
/* USER CODE END Private defines */
```

### main.c

**Printing the Code Version String to UART Console**

```c
/* USER CODE BEGIN 2 */
char _version_string[64];
snprintf(_version_string, _LEN_VERSION_STR, "v%d.%d.%d (%s %s)", _VERSION_MAJOR, _VERSION_MINOR, _VERSION_PATCH, __DATE__, __TIME__);
printf("PCB rev. %s\n", _PCB_REVISION);
printf("%s\n", _version_string);
```

```c
/* USER CODE BEGIN 4 */
/**
 * @brief  Retargets the C library printf function to the USART.
 * @param  None
 * @retval None
 */
PUTCHAR_PROTOTYPE {
    /* Place your implementation of fputc here */
    /* e.g. write a character to the EVAL_COM1 and Loop until the end of transmission */
    HAL_UART_Transmit(&huart2, (uint8_t *) &ch, 1, 0xFFFF);

    return ch;
}
```

### I2C Scanner

```c
void I2C_ScanAddresses(I2C_HandleTypeDef *hi2c);

void I2C_ScanAddresses(I2C_HandleTypeDef *hi2c){
    uint8_t error, address;
    uint16_t nDevices;
    nDevices = 0;
    printf("Scanning for available I2C devices...");
    for(address = 0; address <= 255; address++ )
    {
        HAL_Delay(10);
        error = HAL_I2C_Master_Transmit(hi2c, address, 0x00, 1, 1);
        //error = HAL_I2C_Master_Receive(hi2c, address, 0x00, 1, 1);
        if (error == HAL_OK)
        {
            printf("I2C device found at address 0x%02X!\n", address);
            nDevices++;
        }
    }
    if (nDevices == 0)
        printf("No I2C devices found\n");
    else
        printf("done\n");
}
```

