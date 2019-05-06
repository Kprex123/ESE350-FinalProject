Slap-a-Nap Pack

ESE 350-001

Cassandra Menshouse

Katrina Pham

May 10, 2019


Week 1 (March 15 - March 22):

The initial proposal for our final project was first enacted on March 22. The problem we sought to solve was that of people who suffer from narcolepsy or similar obstacles and fall unconscious at unpedictable times. We wanted to improve this situation by creating a system to detect when the user falls asleep, to collect that data, and to buzz to wake them up.


Baseline Goals:

● Use a wearable sensor to determine when the user is falling asleep (either breathing rate, heart rate, or head movement when the user is "nodding off")

● Measure when and for how long they are asleep

● Send that data to the Cloud (the Cloud can store data and transfer it to different platforms, like a watch)

● Use a buzzer that receives the data and activates when the user falls asleep (the buzzer will only vibrate, so no sound should be produced to reduce disruptions in quiet settings and it should also not cause pain)


Reach Goal:

● Start an app on the Samsung Galaxy Watch or some equivalent wearable device to process this data and display it graphically


Need to Learn More in Depth:

● Samsung Galaxy/Android API

● Wi-Fi/Cloud

● How to classify that a person has fallen asleep

● Photon (main microcontroller)


For testing, Katrina herself shall be the subject since she has severe anemia. This causes her blood cells to bind to oxygen at a lesser rate, therefore her body exhausts its energy quickly. This means she falls unconscious at unpredictable hours, making her a prime test subject.


Week 2 (March 23 - March 30):

The second proposal for our final project was enacted on March 29. We refined the system by focusing more on the sensor feedback loop rather than the data collection.


Overall System Architecture:

Our system has a closed loop because it operates under the following process:

The person starts falling asleep -> The sensors detect the person falling asleep -> The buzzer is activated by the sensors -> The person wakes up -> The sensor goes back to its original state of waiting to activate the buzzer -> The person starts falling asleep again -> … (Repeats cyclically)


Baseline Goals (Updated):

● Use a sensor (ECoG) to determine when the user is falling asleep

● Make the mechanism wearable

● Measure when and for how long they are asleep

● Use a buzzer that receives the data and activates when the user falls asleep (the buzzer will only vibrate, so no sound should be produced to reduce disruptions in quiet settings and it should also not cause pain)


Stretch Goals (Updated):

● Determine levels of exhaustion (starting to fall asleep versus being fully asleep) via breathing rate sensor and an accelerometer (head movement when the user is "nodding off")

● Use a client/server to send and receive information about the user’s unintentional-sleeping patterns

● Control amount of vibration based on how heavily asleep the user is


Need to Learn More in Depth (Updated):

● PCB

● Hosting websites (server/client)

● How to classify eye movement

● Photon (main microcontroller)


Week 3 (March 31 - April 7):

We began obtaining parts for the first demo. Since Photons were not already available in the lab, we switched to the ESP32-WROOM-32 because it also has on-board Wi-Fi. The accompanying software program we used was called Zerynth, which used hybrid C++. After many unsuccessful attempts to get the ESP32-WROOM-32 registered and running, we realized that we could just use an Mbed and an ESP8266 Wi-Fi module instead to achieve a similar (if not an entirely better) result. 

The balance bot lab for this course was our starting point for the Wi-Fi code we would need to implement. We were unfortunately unable to completely finish that lab (specifically part 3), so we had to spend some time trying to figure out how to communicate between the two Mbeds. We tried implementing a header file and its corresponding .cpp file, but came across an error (L6320W) that stated it could not find the argument "os_cb_sections". Some time was spent debugging this, but we received advice from an instructor that radio may be a better option.

A 3-D accelerometer was used first, since the lab already had some in stock. It was powered by the Mbed's 3.3 volt output. The accelerometer's "baseline" readings were recorded so that rapid changes in velocity could be compared to that baseline. Then print statements were sent to the terminal only when large changes were recorded.

We unfortunately did not realize the ECG sensors and the eye movement sensors would need extra cables to properly clip on, so we stripped some wires and wrapped them around the sensor electrodes to increase signal clarity as much as possible. This still resulted in noisy outputs, so we were unable to present reliable data for the first demo.


Week 4 (April 8 - April 15):

A breakout board and proper cables were ordered for the second demo. They were also powered by the Mbed's 3.3 volt output. The ECG sensors seemed better at reading heart rate than breathing rate, so we did not implement breathing rate in the final product. To enhance the heart rate sensor, we implemented an instrumentation amplifier (AD620AN) to increase the ouput's gain by 1000 using a 50 Ohm resistor, since the voltage varied around 1 mV initially. The amplifier needed a much larger voltage supply however, so it was powered externally by positive and negative 9 volts from a power supply in the lab.

We also switched to the MRF24J40 radio chips instead of the ESP8266 Wi-Fi modules this week, since it only requires that both chips be relatively near each other and that they are sharing the same channel. One chip was connected to the Mbed in current use (and powered by its 3.3 volt output) so that we could test that one alone and then later implement the second Mbed and its MRF24J40.


Week 5 (April 16 - April 23):

To reduce the noise from the heart rate sensor, we built a lowpass filter that took in the amplified signal from the instrumentation amplifier. It worked quite well and smoothed out the signal. The resistor value was 2 kOhms and 3 capacitors in parallel were used: one at 1 uF and two at 4.5 uF to make a total of 10 uF. We then built a PCB in Altium to hold both the amplifier and the filter. Some headers were also added to that PCB for the external power, as well as input and output wires.

We looked at some example code for the MRF24J40, but it was difficult to find much due to the lack of documentation. Eventually an instructor was able to find helpful documentation for us, and we began once again with a header file and its corresponding .cpp file. The Mbeds only needed to communicate in one direction, with one Mbed transmitting (the one on the head) and the other receiving (the one on the wrist). This increased our code's clarity since we could reliably depend on which direction the data is being sent.


Week 6 (April 24 - May 1):

We realized that the breakout board that we had been using to read heart rate signals was in fact a muscle sensor, so the readings were inaccurate for several weeks. Thankfully, we were able to use a heart rate sensor breakout board from another group. With this now working, we began trying to make our project more compact and to have our Mbeds to communicate with each other via the MRF24J40 chips. We stripped wires and used smaller breadboards to achieve compactness. After much trial and error with the MRF24J40 chips, we successfully created a C++ project that, using the online Mbed compiler, could send a signal from one Mbed to the other. This signal would be of a pre-determined length if the receiving Mbed's motor was to turn on. With this code, we were able to turn on and off the motor in the second Mbed from the first Mbed's transmitted signal.

The morning before the reach demo, the motor was replaced with a 1 kOhm resistor and an LED, for visual demo purposes, but one of the MRF24J40 chips stopped working. Despite replacing both of the MRF24J40 chips, both of the Mbeds, and using new breadboards, we still couldn't get the Mbeds to communicate with each other via the MRF24J40 chips (like they had earlier) before the reach demo. Nonetheless, we were able to show that we had correct code such that the LED in the larger breadboard for the forehead would turn on when the user had their eyes closed for 20 seconds.

Week 7 (May 2 - May 8):

We repaired and finished our project. We discovered that one pin was connected to the wrong port of the MRF24J40, and one of the two MRF24J40 chips was not working. We had switched that MRF24J40 out with a different one, in a previous attempt to get our project to work, but that MRF24J40 was also not working. Eventually, we successfully obtained two properly working MRF24J40 chips. With the radio and Mbeds now working and communicating with each other via our written code for sending and receiving messages, we began modifying the code such that the data from all 3 sensors —heart rate, eye movement, and accelerometer — was being analyzed. If the heart rate was lower than average or the accelerometer was abruptly shook, the motor on the larger breadboard would vibrate for 10 seconds. If no blinking was detected for 20 seconds or more, the motor on the smaller breadboard would vibrate for 10 seconds.

We connected 6 volts to both of the MBeds (each one had four 1.5 volt batteries), so a connection to a computer was no longer needed. We decided that the larger breadboard was too large and simply inconvenient to have on a headband, so we changed our design to still include the smaller breadboard on a wearable wristband, but the larger breadboard is stuck on the inside of a hoodie pocket, making it less conspicuous than it would've been on the headband (we had to remove the accelerometer as a result). To attach the breadboards to their respective wearable articles, we used electrical tape. Thus, if a person is resting or nodding off, the motor will vibrate in their hoodie pocket (a small alert, similar to if someone's phone went off in their pocket). However, if the person is asleep, the motor will vibrate in their wristband (more likely to wake the user up, since there is direct contact between them and the motor). 
