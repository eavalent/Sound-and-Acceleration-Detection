# Sound-and-Acceleration-Detection

Do you have an ADXL 335 accelerometer and an Arduino compatable sound sensor? Well you're in luck!

We used the ADXL 335 from Adafruit and a sound sensor from Amazon to develop this code. Both are available here: http://www.amazon.com/Arduino-compatible-Mini-Sound-Sensor/dp/B00AF2GB1U http://www.adafruit.com/products/163

It creates 2 arrays, one for sound and one for vibrations from the accelerometer. These arrays are updated 4 times every second, as stated by the interrupt handler.
We used timer 1 to control a number of functions every time the handler is called.

When it's called, the handler runs all of those functions and aims to see if there are 1's or 0's for the sP and vP patterns. To get a 1 for the sP or vP, the array elements must contain the sequence: LOW HIGH LOW, or 010 somewhere in the 12 array elements. Now, these three elements can be anywhere in the array but they ahve to be in order. To make things clearer, the array could start with a 1 and that would still be okay if you saw the 010 later.
In addition, there can be multiple transmitted signals in-between the 010 pattern. Some examples are below: Possible sequence 1: 000000111111 Possible sequence 2: 010101010101 Possible sequence 3: 101010101010 Possible sequence 4: 111001000011

Example 1 here is not a valid pattern because it reaches LOW HIGH not LOW HIGH LOW.
To be counted as a true pattern fit, it must fit all of the requirements. Example 2 is valid because it reaches the LOW HIGH LOW signal.
Example 3 is valid because even though he first bit is a 1, the pattern is still met elsewhere in the binary sequence.
Example 4 is valid because it has LOW HIGH LOW bits, and the bits in-between them do not alter the pattern.

If you have any questions about this code, please send us an email and we'll get back to you!
