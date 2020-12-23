---
title: "Dip-Coater Instrument Code for Arduino"
date: 2019-04-18T15:34:30-04:00
categories:
  - blog
tags:
  - arduino
  - instrument
---
Arduino Code:

```ruby
/*
 DIP-COATER INSTRUMENT CODE
 
This sketch is for running a dip-coater instrument controlled by an
arduino and drived by a servo-motor. The progress is reported on 16X2 
LCD display.
originally added 16 Dec 2020
by Paramesh Chandra

This code is in the public domain.
https://github.com/paramphy/DIp-Coater.git
*/

// include the library code:
#include <LiquidCrystal.h>
#include <Servo.h>

// initialize the library with the numbers of the interface pins
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
int pos = 0, dip = 0, set = 50, dly = 500;
// pos, dip are the iniciators. set = number of dips wanted, dly = delay between changing position 

Servo servo_9;

void setup() {
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 5);
  servo_9.attach(9);
  // Print a message to the LCD.
  lcd.print("Number of Dips");
}

void loop() {
  // going down
  if(dip <= set)
  {
     for (pos = 0; pos <= 180; pos += 1) {
    // tell servo to go to position in variable 'pos'
    servo_9.write(pos);
    // wait 'dly' ms for servo to reach the position
    delay(dly); // Wait for dly
  }
  // going up
  for (pos = 180; pos >= 0; pos -= 1) {
    // tell servo to go to position in variable 'pos'
    servo_9.write(pos);
    // wait 'dly' ms for servo to reach the position
    delay(dly);// Wait for dly
  }
  // delay after one full cycle
  delay(10000);
  // increase the dip count
  dip = dip + 1;
  
  // set the cursor to column 0, line 1
  // (note: line 1 is the second row, since counting begins with 0):
  lcd.setCursor(0, 1);
  // print the number of seconds since reset:
  lcd.print(dip);
  lcd.print(" t(s)=");
  lcd.print(millis()/1000);
  
  }
}
```
Circuit Diagram:

![Circuit Diagram](\../assets/CIrcuit.png)

Check out the [Github Code][github-code] for more info. File all bugs/feature requests at [GitHub repo][github-code].

[github-code]: https://github.com/paramphy/DIp-Coater.git