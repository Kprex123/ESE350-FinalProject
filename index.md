Slap-a-Nap Headband

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

● Use a buzzer that receives the data and activates when the user falls asleep (the buzzer will only vibrate, so no sound should be produced to reduce disruptions in quiet settings and it should not be painful)


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

The person starts falling asleep -> The sensors detects the person falling asleep -> The buzzer is activated by the sensors -> The person wakes up -> The sensor goes back to its original state of waiting to activate the buzzer -> The person starts falling asleep again -> … (Repeats cyclically)


Baseline Goals (Updated):

● Use a wearable sensor (ECoG) to determine when the user is falling asleep

● Make the mechanism wearable

● Measure when and for how long they are asleep

● Use a buzzer that receives the data and activates when the user falls asleep (the buzzer will only vibrate, so no sound should be produced to reduce disruptions in quiet settings and it should not be painful)


Stretch Goals (Updated):

● Determine levels of exhaustion (starting to fall asleep versus being fully asleep) via breathing rate sensor and an accelerometer (head movement when the user is "nodding off")

● Use a client/server to send and receive information about the user’s unintentional-sleeping patterns.

● Control amount of vibration based on how heavily asleep the user is


Need to Learn More in Depth (Updated):

● PCB

● Hosting websites (server/client)

● How to classify eye movement

● Photon (main microcontroller)


Week 3 (March 31 - April 7):

We began obtaining parts for the first demo. Since Photons were not already available in the lab, we switched to the ESP32-WROOM-32 since it also has on-board Wi-Fi. The accompanying software program we used was called Zerynth. After many unsuccessful attempts to get the ESP32-WROOM-32 running, we realized that we could just use an Mbed and an ESP8266 instead to achieve a similar (if not entirely better) result.
