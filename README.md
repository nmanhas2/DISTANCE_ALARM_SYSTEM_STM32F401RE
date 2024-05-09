# DISTANCE_ALARM_SYSTEM_STM32F401RE
A mini security system I made using the STM32F401RE MCU, the HC-SR04 Ultrasonic Sensor, a piezo buzzer, and an I2C LCD display. All libraries were developed by myself, and can keep seen here: https://github.com/nmanhas2/LIBRARIES_STM32F401, you'll need to follow the instructions for adding the chip headers in that link.

Datasheet for HC-SR04: https://cdn.sparkfun.com/datasheets/Sensors/Proximity/HCSR04.pdf

Datasheet for buzzer: https://product.tdk.com/en/system/files?file=dam/doc/product/sw_piezo/sw_piezo/piezo-buzzer/catalog/piezoelectronic_buzzer_ps_en.pdf

Datasheet for I2C LCD display: https://www.orientdisplay.com/wp-content/uploads/2019/10/AMC0802BR-B-Y6WFDY-I2C.pdf

For details on the HC-SR04, I made a separate repo to explain it: https://github.com/nmanhas2/HC-SR04_STM32F401RE, due to how the timing works to generate the PWM for measurement taking.
Essentially, a state machine was created based on the HCSR-04 datasheet, which involves the trigger and echo pins for that module. This consists of waiting 60ms, setting the trigger pin high for 10us, then waiting for an echo from the sensor, while using interrupts to keep track of timer ticks in order to perform a distance measurement (in CM). 

Once the entire echo has been complete, the distance will be calculated based on the timer ticks as mentioned, which will then be displayed on the LCD screen whenever a new distance is captured, while also displaying the measurement via UART communication.

The alarm (piezo buzzer) activates when an object distance of < 10CM is detected, which turns a timer that activates a PWM on, thus causing the buzzer to click at a rate of about 13Hz.




