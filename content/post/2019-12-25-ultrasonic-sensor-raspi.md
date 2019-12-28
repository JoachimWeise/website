---
title: Ultrasonic Range Sensor on the Raspberry Pi
subtitle: 
date: 2019-12-24
# lastmod: 2019-12-25
bigimg: [{src: "/img/2019-12-21-AI-weekly-51-2019.jpg", desc: "Sunset (2017)"}]
tags: ["raspberry", "robot", "python"]
---

In this project I am interfacing the HC-SR04 ultrasonic sensor module to a Raspberry Pi to measure distance. Later on the Raspberry as well as the sensor will be part of an obstacle avoiding robot.


<!--more-->


A basic ultrasonic sensor consists of one or more ultrasonic transmitters (basically speakers), a receiver, and a control circuit. The transmitters emit a high frequency ultrasonic sound, which bounces off any nearby solid object. Some of that ultrasonic signal is reflected and detected by the receiver on the sensor. That return signal is then processed by the control circuit to calculate the time difference between the signal being transmitted and received. This time can subsequently be used to calculate the distance between the sensor and the reflecting object.

The HC-SR04 ultrasonic module operates at 5 V with a current of some 15 mA and measures the distance effectively starting from 2 cm to 400 cm.  It has four pins: ground (GND), Echo Pulse Output (ECHO), Trigger Pulse Input (TRIG), and 5 V Supply (Vcc). We power the module using Vcc, ground it using GND, and use our Raspberry Pi to send an input signal to TRIG.

The HC-SR04 sensor requires a short 10 uS pulse to trigger the module, which will cause the sensor to start the ranging program (8 ultrasound bursts at 40 kHz) in order to obtain an echo response. Once the 8 burst pattern is sent, the Echo pin is set high (i.e 5 V), and when the signal reflects and comes back the Echo pin is set low (0 V). This time duration for which the Echo pin stays high is the time taken for the ultrasonic wave to travel and come back (round trip). The distance can then be calculated using the speed of sound 343 m/s.


<center>
{{< figure src="/img/2019-12-25-ultrasonic-sensor-raspi/timing-diagram2.jpg" width="700px" caption="Timing Diagram" caption-position="bottom" caption-effect="fade">}}
</center>


Like mentioned above the operating voltage of the module is 5V.  The input pin on the Raspberry Pi GPIO is only 3.3V tolerant. Sending a 5V signal into a 3.3V input port could damage the GPIO pins. We use a small voltage divider to solve this problem. A voltage divider consists of two resistors (R1 and R2) in series connected to an input voltage (Vin), which needs to be reduced to our output voltage (Vout). In our circuit, Vin will be ECHO, which needs to be decreased from 5V to our Vout of 3.3V.

<center>
{{< figure src="/img/2019-12-25-ultrasonic-sensor-raspi/voltage-divider.jpg" width="500px" caption="Voltage Divider" caption-position="bottom" caption-effect="fade">}}
</center>

Using the great software [fritzing](https://fritzing.org/home/) we can draw a schematic of how it will look like in reality, when all pins are connected using a breadboard and jumper wires:



<center>
{{< figure src="/img/2019-12-25-ultrasonic-sensor-raspi/schematic3.jpg" width="400px" caption="Schematic" caption-position="bottom" caption-effect="fade">}}
</center>

Some pictures how it looks in reality. The distance is displayed in a single line in the shell which is constantly updated:

{{< gallery caption-effect="fade" >}}
  {{< figure thumb="-thumb" link="/img/2019-12-25-ultrasonic-sensor-raspi/pic1.jpg" caption="Overview">}}
  {{< figure thumb="-thumb" link="/img/2019-12-25-ultrasonic-sensor-raspi/pic2.jpg" caption="Closeup">}}
  {{< figure link="/img/2019-12-25-ultrasonic-sensor-raspi/pic3.jpg" caption="Ouput in shell">}}
{{< /gallery >}}


And finally the corresponding Python code. The `time.time()` function will record the latest timestamp for a given condition. For example, if a pin goes from low to high, and we’re recording the low condition using the `time.time()` function, the recorded timestamp will be the latest time at which that pin was low.
  

{{< highlight bash "linenos=inline">}}
# GPIO example using an NC-SR04 ultrasonic rangefinder

# import the GPIO and time libraries
import RPi.GPIO as GPIO
import time

# Set the GPIO mode to BCM mode and disable warnings
GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)

# Define pins
trig = 23
echo = 24
GPIO.setup(trig,GPIO.OUT)
GPIO.setup(echo,GPIO.IN)
print("Measuring distance")

# Begin while loop
while True:

    # Set trigger pin to low for 1/10 second
    GPIO.output(trig,False)
    time.sleep(0.1)

    # Send a 10uS pulse
    GPIO.output(trig,True)
    time.sleep(0.00001)
    GPIO.output(trig,False)

    # Get the start and end times of the return pulse
    while GPIO.input(echo)==0:
        pulse_start = time.time()

    while GPIO.input(echo)==1:
        pulse_end = time.time()

    pulse_duration = pulse_end - pulse_start

    # Calculate the distance in centimeters
    distance = pulse_duration * 17150
    distance = round(distance, 2)

    # Display the results. end = '\r' forces the output to the same line
    print("Distance: " + str(distance) + "cm             ", end = '\r')
{{</ highlight >}}