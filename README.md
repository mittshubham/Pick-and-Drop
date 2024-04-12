# Pick-and-Drop
#include <Servo.h>

// Alloting the pins for the servo motors
#define servo1 6
#define servo2 7
#define servo3 8
#define servo4 9

int pos = 0;
// Define servo

Servo mservo1, mservo2, mservo3, mservo4;

char IncomingValue = '0';

void setup() {
  Serial.begin(9600);

  mservo1.attach(servo1);
  mservo2.attach(servo2);
  mservo3.attach(servo3); 
  mservo4.attach(servo4);
  
  //Setting the reset positions
  mservo1.write(100); // Up - down range: 50 - 150
  mservo2.write(0); // Right - left range: 0 - 180
  mservo1.write(80); // Forward - Backward range: 40 - 120
  mservo1.write(0); // Clamp range: 0 - 35
}

//Defining the initial values
int srv1 = 100;
int srv2 = 0;
int srv3 = 80;
int srv4 = 0;

void loop() {

  //Checking the availability of bluetooth
  if (Serial.available() > 0){
    IncomingValue = Serial.read();
  }
  
  //Defining the initial condition
  if (IncomingValue == '0'){
    srv1 = 100;
    srv2 = 0;
    srv3 = 80;
    srv4 = 0;
  }

  //Defining for the UP movement
  if (IncomingValue == 'A'){
    if (srv1 < 150){
      srv1 ++; //iterating
      mservo1.write(srv1);
      delay(10);
    }
  }

  //Defining for the DOWN movement
  if (IncomingValue == 'B'){
    if (srv1 > 0){
      srv1 --; //iterating
      mservo1.write(srv1);
      delay(10);
    }
  }
  
  //Defining for the RIGHT movement
  if (IncomingValue == 'C'){
    if (srv2 < 180){
      srv2 ++; //iterating
      mservo2.write(srv2);
      delay(10);
    }
  }

  //Defining for the LEFT movement
  if (IncomingValue == 'D'){
    if (srv2 > 0){
      srv2 --; //iterating
      mservo2.write(srv2);
      delay(10);
    }
  }

  //Defining for the FORWARD movement
  if (IncomingValue == 'E'){
    if (srv3 > 40){
      srv3 --; //iterating
      mservo3.write(srv3);
      delay(10);
    }
  }

   //Defining for the BACKWARD movement
  if (IncomingValue == 'F'){
    if (srv3 <120){
      srv3 ++; //iterating
      mservo3.write(srv3);
      delay(10);
    }
  }

   //Defining for the CLAMP CLOSING movement
  if (IncomingValue == 'G'){
    if (srv4 > 0){
      srv4 --; //iterating
      mservo4.write(srv4);
      delay(10);
    }
  }

   //Defining for the CLAMP OPENING movement
  if (IncomingValue == 'H'){
    if (srv4 < 35){
      srv4 ++; //iterating
      mservo4.write(srv4);
      delay(10);
    }
  }


}
