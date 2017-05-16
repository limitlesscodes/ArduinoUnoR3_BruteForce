# ArduinoUnoR3_BruteForce
A tool that uses an UnoR3 as an HID keyboard to bruteforce all pins from 0000-9999


This was a small project I worked on to access pictures on an old phone that I no longer remembered the pin for. My arduino didn't have the correct firmware so I had to use one of my AW dev boards to flash the chip using avrdude. Then I wrote a program for the arduino that counts from 0000-9999 simulating each combination as keystrokes.
