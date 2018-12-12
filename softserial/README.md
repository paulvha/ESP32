Based on the softserial from https://github.com/jdollar/espsoftwareserial
Which in turn is based on the SoftSerial from the ESP8266 and Arduino

The softserial from Jdollar could not be compile. Once that fixed it hang and paniced constant and was working very instable 
on Sparkfun ESP32 Thing. Unfortunately one can not provide issues on the github and the code is now 2 years old.

A number of changes have been applied to make it work.
. only enableRX after the speed is set to prevent "hang"
. The disable of interrupts has been implemented that it really works on an ESP32 during RX and TX
. The timing for bit-banging RX has been adjusted to be more accurate
. The reset for GPIO detected interrups now works
. Added yield() for low baudrate in the wait during TX

MAKE SURE TO ADJUST the following in cores ESP.cpp. it must be set for IRAM_ATTR as it is called during
interrupt: 
line 103 uint32_t IRAM_ATTR EspClass::getCycleCount()   // is called from interrupt !

It now works OK-is, most of the time. But do not expect it to work above 56K (stretch already !!) 

It is still better to use any of the three serial interfaces, which are supported by a real uart. 
The nice aspect is that the pins of each UART/Serial can be assigned to nearly all pins on the ESP32. 
The pins 9 and 10, default for Serial1, on SparkFun ESP32 Thing are used for flash memory. 
However as the pins can be assigned for Serial, one can still use Serial1 port bu then on other pins ( e.g. 25 and 26).

December 2018
Paul vah Haastrecht

