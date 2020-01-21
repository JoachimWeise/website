---
title: Ultrasonic Range Sensor on the Raspberry Pi
subtitle: 
date: 2019-12-28
# lastmod: 2019-12-25
bigimg: [{src: "/img/2019-12-25-ultrasonic-sensor-raspi/background.jpg", desc: "8 ultrasound bursts at 40kHz"}]
tags: ["raspberry", "electronics", "robot", "python", "code"]
---

In this project I am interfacing the HC-SR04 ultrasonic sensor module to a Raspberry Pi to measure distance. Later on the Raspberry as well as the sensor will be part of an obstacle avoiding robot. I use my oscilloscope to check whether the sensor is working as announced.


<!--more-->

***


A basic ultrasonic sensor consists of one or more ultrasonic transmitters (basically speakers), a receiver, and a control circuit. The transmitters emit a high frequency ultrasonic sound, which bounces off any nearby solid object. Some of that ultrasonic signal is reflected and detected by the receiver on the sensor. That return signal is then processed by the control circuit to calculate the time difference between the signal being transmitted and received. This time can subsequently be used to calculate the distance between the sensor and the reflecting object.

The HC-SR04 ultrasonic module operates at 5V with a current of some 15mA and measures the distance effectively starting from 2cm to 400cm.  It has four pins: ground (`GND`), Echo Pulse Output (`ECHO`), Trigger Pulse Input (`TRIG`), and 5V Supply (`Vcc`). We power the module using `Vcc`, ground it using `GND`, and use our Raspberry Pi to send an input signal to `TRIG`.

The HC-SR04 sensor requires a short 10-100us pulse to trigger the module, which will cause the sensor to start the ranging program (8 ultrasound bursts at 40kHz) in order to obtain an echo response. Once the 8 burst pattern is sent, the `ECHO` pin is set high (i.e 5V), and when the signal reflects and comes back the `ECHO` pin is set low (0V). This time duration for which the `ECHO` pin stays high is the time taken for the ultrasonic wave to travel and come back (round trip). The distance can then be calculated using the speed of sound 343m/s.


<center>
{{< figure src="/img/2019-12-25-ultrasonic-sensor-raspi/timing-diagram2.jpg" width="600px" caption="Fig. 1: Timing Diagram" caption-position="bottom" caption-effect="fade">}}
</center>


As mentioned above the operating voltage of the module is 5V.  The input pin on the Raspberry Pi GPIO is only 3.3V tolerant. Sending a 5V signal into a 3.3V input port could damage the GPIO pins. We use a  voltage divider to solve this problem. A voltage divider consists of two resistors (R1 = 1kOhm and R2 = 2kOhm) in series connected to an input voltage (`V_in`), which needs to be reduced to our output voltage (`V_out`). In our circuit, `V_in` will be `ECHO`, which needs to be decreased from 5V to our `V_out` of 3.3V.

<center>
{{< figure src="/img/2019-12-25-ultrasonic-sensor-raspi/voltage-divider.jpg" width="500px" caption="Fig. 2: Voltage Divider" caption-position="bottom" caption-effect="fade">}}
</center>
 
I am a big fan of the software [fritzing](https://fritzing.org/home/) which allows to draw neat schematics in next to no time. That's how it will look like when all pins are connected using a breadboard and jumper wires:



<center>
{{< figure src="/img/2019-12-25-ultrasonic-sensor-raspi/schematic3.jpg" width="300px" caption="Fig. 3: Schematic" caption-position="bottom" caption-effect="fade">}}
</center>

Figures 4 and 5 show my cabling, as it looks in reality (slightly messy). Figure 6 shows a screenshot of how the distance is displayed in a single line in the shell that is constantly being updated:

{{< gallery caption-effect="fade" >}}
  {{< figure thumb="-thumb" link="/img/2019-12-25-ultrasonic-sensor-raspi/pic1.jpg" caption="Fig. 4: Overview">}}
  {{< figure thumb="-thumb" link="/img/2019-12-25-ultrasonic-sensor-raspi/pic2.jpg" caption="Fig. 5: Closeup">}}
  {{< figure link="/img/2019-12-25-ultrasonic-sensor-raspi/pic3.jpg" caption="Fig. 6: Ouput in shell">}}
{{< /gallery >}}


The Python code to trigger and read out the sensor can be kept quite simple. The `RPi.GPIO`  library allows to easily configure and read-write the input/output pins on the Pi’s GPIO interface within a Python script. It is installed by default on recent versions of Raspbian Linux. The `time.time()` function will record the latest timestamp for a given condition. For example, if a pin goes from low to high, and we’re recording the low condition using the `time.time()` function, the recorded timestamp will be the latest time at which that pin was low.
  

{{< highlight bash "linenos=inline">}}
# GPIO example using an HC-SR04 ultrasonic rangefinder

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


Next I use my Tektronix 2465 oscilloscope to check whether the sensor really works as desribed above. Let's first see if the distance conversion, using the speed of sound in air, works as promised. I connect the scope to `GND` (black) and `ECHO` (red/orange), as shown in Figures 7 and 8. After a short fight with the trigger, the scope shows that `ECHO` is high for some 23ms. Multiplying this with the speed of sound of 343m/s and dividing by 2 (round trip) yields a distance of some 3.9m which is in line with what was displayed. Nice!


{{< gallery caption-effect="fade" >}}
  {{< figure thumb="-thumb" link="/img/2019-12-25-ultrasonic-sensor-raspi/osci01.jpg" caption="Fig. 7: Connecting the scope">}}
  {{< figure thumb="-thumb" link="/img/2019-12-25-ultrasonic-sensor-raspi/osci02.jpg" caption="Fig. 8: Connecting the scope">}}
  {{< figure link="/img/2019-12-25-ultrasonic-sensor-raspi/osci03.jpg" caption="Fig. 9: ECHO set high for 23ms">}}
{{< /gallery >}}


As a last step I try to take a look at the "8 burst pattern" that the sensor is supposed to send out after being triggered by the Raspberry. The letters 'T' and 'R' on the front of the sensor board seem to indicate that the transmitter sits left and the receiver right. I use a probe head to connect to one of the contacts of the transmitter on the backside of the circuit board, as shown in Figures 10 and 11. The scope shows in fact 8 peaks in a time span of some 210us. The peaks thus come at a frequency of 38kHz. The description didn't lie!


{{< gallery caption-effect="fade" >}}
  {{< figure thumb="-thumb" link="/img/2019-12-25-ultrasonic-sensor-raspi/osci04.jpg" caption="Fig. 10: Probe head on sensor board">}}
  {{< figure thumb="-thumb" link="/img/2019-12-25-ultrasonic-sensor-raspi/osci05.jpg" caption="Fig. 11: Probe head on sensor board">}}
  {{< figure link="/img/2019-12-25-ultrasonic-sensor-raspi/osci06.jpg" caption="Fig. 12: Eight burst at 38kHz">}}
{{< /gallery >}}

A fun GIF as a farewell from this experiment:

<center>
{{< figure src="/img/2019-12-25-ultrasonic-sensor-raspi/osci4.gif" width="500px" caption="Schematic" caption-position="bottom" caption-effect="fade">}}
</center>