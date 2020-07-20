# AD9833-STM32
A Simple Library for AD9833 based on STM32

This is a library for AD9833 DDS Chip from Analog Devices.

For my project, I used STM32F030F4P6 and HAL libraries based on STM32CubeMX. I tried to write the library simple so as you can port it on other microcontrollers. It uses Software-Based SPI, so you do not need to configure SPI registers on your microcontroller. I tested it in IAR for ARM and Eclipse with GCC-ARM, and it worked fine. Moreover, I used FREQ0 and PHASE0 Register of AD9833. You can easily change it to FREQ1 and PHASE1 if you need it.




[AD9833 DATASHEET](https://www.analog.com/media/en/technical-documentation/data-sheets/AD9833.pdf)

[AD9833 Application Note](https://www.analog.com/media/en/technical-documentation/application-notes/AN-1070.pdf)

## How to use
You have to allocate 3 GPIOs of your controller. In my case, I used PA5, PA6 and PA7, and I configured them as output in STM32CubeMX. After that, you have to define output pins in AD9833.h.

![2020-05-19_143422](https://user-images.githubusercontent.com/54714609/82322492-d9489b80-99eb-11ea-981f-019835446b26.jpg)
![2020-05-19_143603](https://user-images.githubusercontent.com/54714609/82322499-dbaaf580-99eb-11ea-832a-74b28b01ef15.jpg)


There are three functions to change the behavior of AD9833 that you can use :

```C
void AD9833_Init(uint16_t Wave,float FRQ,float Phase);   // Initializing AD9833
void AD9833_SetWave(uint16_t Wave);                      // Sets Output Wave Type
void AD9833_SetWaveData(float Frequency,float Phase);    // Sets Wave Frequency & Phase
```
## Note
Regarding the fact that this library uses a delay to execute software SPI, it can act differently with different microcontrollers. It depends on the master clock on your uC. If this library did not work for you, you have to change delay times in Write SPI function. You can do this with trial and error by adding some assembly nopes. Of course, you can use hardware SPI and add your functions to the library to avoid timing problems.



## Test Results

Some Frequency Sweep test :)
![Sweep](https://user-images.githubusercontent.com/54714609/82322982-9dfa9c80-99ec-11ea-9e1c-8bb710916de2.gif)
![SIN](https://user-images.githubusercontent.com/54714609/82323202-f03bbd80-99ec-11ea-81cc-d0b09c403c66.jpg)
![SQR](https://user-images.githubusercontent.com/54714609/82323208-f3cf4480-99ec-11ea-8527-2cb99277f20d.jpg)
![TRI](https://user-images.githubusercontent.com/54714609/82323210-f467db00-99ec-11ea-9091-a1c439c01001.jpg)
