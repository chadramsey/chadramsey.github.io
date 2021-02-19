---
layout: posts
title: From Silicon to the Web
date: 2021-02-17
---

Once a quarter my place of work grants our teams a 'day of autonomy' to work on any projects we see fit to grow our knowledge and development skill set. For this day of autonomy I decided to take an idea that was outside the box (or, outside the barn) and see how far I could run with a hardware-based project using the Raspberry Pi, an accelerometer and the power of the web.

### What's an Accelerometer?
First thing's first, what's an accelerometer and what does it do? In short an accelerometer is a chipset capible of detecting orientation on an x, y, and z axis by measuring the acceleration forces applied to it. Your smart phone uses an accelerometer to determine its orientation to trigger screen rotation. The chipset itself will only run you a few dollars and looks something like this:

![](https://chadramsey.github.io/assets/images/2021/mpu6050.jpg){: .center-image }

*"The MPU6050 chipset was used for this project."*

The setup for this project involved the use of a breadboard and jump wires to connect the chipset to the GPIO pins of the Raspberry Pi.

![](https://chadramsey.github.io/assets/images/2021/mpu6050-interface.png){: .center-image }

### Cool, But Why?
An accelerometer has many applications. For this particular application we're going to discuss bicycles. The initial pitch was simply, "Wouldn't it be interesting if bikes included an accelerometer?" Bicycles are dynamic machines, frequently pivoting in coordinate space. What kind of information could we derive from a rider if we had this data? A few thoughts included the potenial for unique insights into coaching and progress building through analysis of rider and bike dynamics, product development and testing through use of 3D modeling software, or the potential for integrated safety features such as crash detection (the measure of an accelerated force in a given direction).

### Hardware Interfacing
Now that I've covered the 'why', let's cover the technical implementation. With the hardwire configuration wired up some code needs to be written to read the analog data produced from the accelerometer. The Raspberry Pi has libraries to help interface with the GPIO pins, but rather than spending time reinventing the wheel I discovered [a Python module](https://github.com/m-rtijn/mpu6050) that effectively gets right to the point of abstracting the low level communication between the MPU6050 chipset and the Raspberry Pi. All that was left to do was to import this module within my own Python script and make use of the data.

```
from mpu6050 import mpu6050
sensor = mpu6050(0x68)
accelerometer_data = sensor.get_accel_data() # Get the current X, Y and Z coordinates from the accelerometer
```

The Python script imports the necessary module, instantiates the sensor based on its I2C address, and pulls the coordinate data from the accelerometer. Tilts in the X-axis represent leaning the bike left or right, while tilts in the Y-axis represent an incline or decline (or a wheelie/stoppie when measured in short durations). Once the script is running, the breadboard holding the accelerometer can be picked up and rotated to produce feedback.

![](https://chadramsey.github.io/assets/images/2021/python-accel.gif){: .center-image }

*"The running Python application with X/Y-axis feedback for turns, wheelies, and stoppies"*

### Passing the Data via Websockets
For this proof of concept I wanted to distribute the data as close to real time as possible to an external system. The thought was to explore the possibility of distributing the data across the web to an external service that could parse the coordinate details and analyze the data for patterns that might offer helpful insight. Websockets offer a convent way to ingest the data in real time across the network, and have the added benefit of allowing others to view this data in real time as well. For this I used Spring Boot to develop a websocket server that would accept an asyncronous connection from the Python script managing the accelerometer and pass the data as it's being generated. The Spring Boot application also includes static HTML and JavaScript resources to allow clients to connect to the embeded websocket server and view the data stream in real time.

![](https://chadramsey.github.io/assets/images/2021/demo.gif){: .center-image }

*"Connection to the websocket server via JavaScript shows the real time data stream from Python"*

### Further Implementation
Now that the data is being accepted by the websocket server the sky is the limit. Instead of simply appending the input the server can further parse the coordinate data being passed in and be analyzed to form patterns for the use cases above (and more!). This kind of shared coordinate data might also be used in game development to transform game objects in real time (let's get some wheelies up in Zwift).

### Final Thoughts
This project was interesting to work through on a number of levels. Dusting off the Raspberry Pi to work on another hardware-based project reminded me why I've made a career of development - it's exciting to brainstorm concepts and see how far they can be taken. While it's easy to get caught up in the day-to-day tasks of development, taking the time to conceptualize the ideas rolling around in mind keeps the craft interesting.

I've uploaded the source code base for both the [websocket server](https://github.com/chadramsey/websocket-server) and [Python script](https://gist.github.com/chadramsey/e58f14c6e07cc41660b39de30af2f8a0) for anyone interested in taking this day one proof of concept to the next level.