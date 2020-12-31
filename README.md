# Плата DAC Lusya ES9038

<img src="https://ae01.alicdn.com/kf/Ufa0355bf45814bdf9531ceffadfef5b1I.jpg" width="400"/>
https://ru.aliexpress.com/item/32950289780.html


## Комплектация
### Bundle 1
- Плата
- Энкодер + кабель 4pin

### Bundle 2
- Плата
- Энкодер + кабель 4pin
- Плата c дисплеем с IR приёмником + кабель 8pin

## Power
Питание двухполярное +/- 15v на винтовую колодку. Либо однополярное +12v через штырьковый разъём. В этом случае включается DC-DC преобразователь.

## Display
Используется дисплей 1.8" 162x132 на ST7735S

Можно использовать дисплей 160x128 на ST7735S. Проверял на [таком](https://www.aliexpress.com/item/32994774078.html). Для этого нужно пропатчить прошивку
```
0x08000346	47 1C	->	07 1C	(ADDS R7, R0, #1  ->  ADDS R7, R0, #0)
0x08000348	4E 1C	->	0E 1C	(ADDS R6, R1, #1  ->  ADDS R6, R1, #0)
0x0800034A	95 1C	->	15 1C	(ADDS R5, R2, #2  ->  ADDS R5, R2, #0)
0x0800034C	9C 1C	->	1C 1C	(ADDS R4, R3, #2  ->  ADDS R4, R3, #0)
```

## Connections
### Buttons
```
Vol-  PA3	// 0 - active
Menu  PA4	// 0 - active
Vol+  PA5	// 0 - active
```

### Encoder
```
A     PA6	// 0 - active
B     PA7	// 0 - active
BTN   PB0	// 0 - active
```

### LED
Используются 2 последовательно соединённых 74HC164
```
DAT   PA15
CLK   PA12
```

### I2C
```
19    PA9  I2C1_SCL
20    PA10 I2C1_SDA
21    PA11 подключен к RESETB ?
```

## Pinout
###Разъём 8 pin
```
8 Vcc
7 PB3  SCK
6 PB4  DC
5 PB5  MOSI
4 PB6  CS (? сбрасывается в 0 только при инициализации дисплея. Поэтому чтобы работало, надо CS дисплея повесит на 0)
3 PB7  RST (?)
2 PA2  вход с IR датчика для управления с пульта
1 GND
```
###PROG
```
3v3
SWCLK
SWDIO
GND
```

##IR
Старшее слово 0x77E1, старший байт не проверяется (Apple Remote)
используются коды
```
0x77E1xxD0	KEY_UP
0x77E1xx50	KEY_UP
0x77E1xxB0	KEY_DOWN
0x77E1xx30	KEY_DOWN	
0x77E1xx10	KEY_LEFT
0x77E1xx90	KEY_LEFT
0x77E1xxE0	KEY_RIGHT
0x77E1xx60	KEY_RIGHT
0x77E1xx40	KEY_MENU
0x77E1xxC0	KEY_MENU
0x77E1xx20	KEY_PLAYPAUSE
0x77E1xxA0	KEY_PLAYPAUSE
```

## note
Управление на STM32F030K6T6, прошивка не защищена.


