#include <Servo.h>

// Servos for open/close and spin
Servo claw_OC; //open or close
Servo claw_S;  //spin

int x_key = A6;  //x means open or close
int y_key = A7;  //y means spin
int x_pos;
int y_pos;
int claw_OC_pin = 9;  //open close
int claw_S_pin = 8;  //spin
int initial_position0 = 90; //default: open
int initial_position1 = 0; //default: horizontal

// Motors for forward/backward and turning
Servo ESC_Front;  // Front Thruster (used for forward/backward and turning)
Servo ESC_Back;   // Back Thruster (used for forward/backward and turning)

// Motors for vertical movement (up/down)
Servo ESC_UpLeft;  // Up/Down Left Thruster
Servo ESC_UpRight; // Up/Down Right Thruster

int joystickForward;   // Joystick input for forward/backward motion
int joystickTurn;      // Joystick input for turning (yaw)
int joystickUpDown;    // Joystick input for vertical movement (up/down)


void setup() {
//CLAW
  // Serial.begin(9600); maybe don't need this line as it's repeating
  claw_OC.attach(claw_OC_pin);
  claw_S.attach(claw_S_pin);
  claw_OC.write(initial_position0);
  claw_S.write(initial_position1);
  pinMode(x_key, INPUT);
  pinMode(y_key, INPUT);

//MOVEMENT
  //NOT DONE TESTING
  ESC_Back.attach(4, 1000, 2000);   // Pin  for right vertical thruster


  //DONE TESTING - WORKING WELL
 // ESC_Front.attach(12, 1000, 2000);  // Pin 12 for left vertical thruster //joystick L
    //The following two thrusters work together, controlled by one joystick
  //ESC_UpLeft.attach(10, 1000, 2000); // Pin for front thruster //joystick UP
  //ESC_UpRight.attach(7, 1000, 2000);// Pin for back thruster //joystick UP

//Start serial communication for debugging
  Serial.begin(9600);
}

void loop() {
//CLAW
  x_pos = analogRead(x_key);
  y_pos = analogRead(y_key);

  if (x_pos < 300) {
    if (initial_position0 < 10) {
    } else {
      initial_position0 = initial_position0 - 20;
      claw_OC.write(initial_position0);
      //delay(100);
    }
  }
  if (x_pos > 700) { //changed if to else if
    if (initial_position0 > 180) {
    } else {
      initial_position0 = initial_position0 + 20;
      claw_OC.write(initial_position0);
      //delay (100) ;
    }
  }

  if (y_pos < 300) {
    if (initial_position1 < 10) {
    } else {
      initial_position1 = initial_position1 - 20;
      claw_S.write(initial_position1);
      //delay(100);
    }
  }
  if (y_pos > 700) { //changed if to else if
    if (initial_position1 > 180) {
    } else {
      initial_position1 = initial_position1 + 20;
      claw_S.write(initial_position1);
      //delay (100) ;
    }
  }

//MOVEMENT
  // Read joystick inputs
  joystickForward = analogRead(A10);   // Forward/backward
  joystickTurn = analogRead(A3);      // Turning (yaw)
  joystickUpDown = analogRead(A1);    // Up/down (vertical)
Serial.println(joystickForward);
  // Map joystick values (0-1023) to PWM (servo acceptable) range (1100-1900)
  int forwardPWM = map(joystickForward, 0, 1023, 1100, 1900); // Forward/backward
  int turnPWM = map(joystickTurn, 0, 1023, 1100, 1900);       // Turning
  int upDownPWM = map(joystickUpDown, 0, 1023, 1100, 1900);   // Up/down

  // Control forward/backward (both motors work together)
  ESC_Front.write(forwardPWM);  // Front motor
  ESC_Back.write(forwardPWM);   // Back motor

  // Turning control (yaw)
  ESC_Front.write(turnPWM);     // Front motor for turning
  ESC_Back.write(2000 - turnPWM); // Back motor for turning


  // Vertical movement (up/down)
  ESC_UpLeft.write(upDownPWM);  // Left thruster for up/down
  ESC_UpRight.write(upDownPWM); // Right thruster for up/down //writeMicroseconds

  delay(20);  // Small delay for stability
}
