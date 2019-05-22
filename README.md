# PWM Freak

This is very small library for configuring the PWM frequency for AVR based Arduinos. I didnt write it, It is taken from the playground.arduino.cc site and provided in this library for your convenience.

# Why Change the Default Frequency?

If you are controlling a motor, voice coil or any sort of inductive device you 
are likely hearing a humming sound while using the default PWM frequency. This
is simply because the switching of the inductive device is within our hearing 
range. By increasing the frequency to 20Khz (or higher like 31.2Khz) we'll put it
well above our hearing range...but dont expect the dogs to like it!

# Setting PWM base frequency

Simply add the library using the Arduino library manager and include the PWMFreak.h
include file.

```
#include <PWMFreak.h>
```

Then in your setup function call the function to set the frequency for the given
pin. The function will figure out what timer is backing that pin and set the PWM
frequency. Other PWM pins that rely on the same timer will also be affected!

```
void setup()
{
    // change PWM for pin 6 to use divisor value 1
    setPwmFrequency(6, 1);

}
```

The resulting frequency is equal to the base frequency divided by
the given divisor:
   - Base frequencies:
      o The base frequency for pins 3, 9, 10, and 11 is 31250 Hz.
      o The base frequency for pins 5 and 6 is 62500 Hz.
   - Divisors:
      o The divisors available on pins 5, 6, 9 and 10 are: 1, 8, 64,
        256, and 1024.
      o The divisors available on pins 3 and 11 are: 1, 8, 32, 64,
        128, 256, and 1024.
 
PWM frequencies are tied together in pairs of pins. If one in a
pair is changed, the other is also changed to match:
* Pins 5 and 6 are paired on timer0
* Pins 9 and 10 are paired on timer1
* Pins 3 and 11 are paired on timer2
 
Note that this function will have side effects on anything else
that uses timers:
*   Changes on pins 3, 5, 6, or 11 may cause the delay() and
    millis() functions to stop working. Other timing-related
    functions may also be affected.
*   Changes on pins 9 or 10 will cause the Servo library to function
    incorrectly.
 
Thanks to macegr of the Arduino forums for his documentation of the
PWM frequency divisors. His post can be viewed at:
   https://forum.arduino.cc/index.php?topic=16612#msg121031


