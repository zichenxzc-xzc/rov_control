#include <Servo.h>
Servo ESC_Front;  // create servo object to control the ESC (Electronic Speed Controller)
Servo ESC_Back;
Servo ESC_UpLeft;
Servo ESC_UpRight;

int joystickForward;                 // value from the analog pin
int joystickTurn;
int joystickUpDown;

void setup() {
  ESC_Back.attach(4, 1000, 2000);  // (pin, min pulse width, max pulse width in microseconds)
  ESC_Front.attach(12, 1000, 2000);
  ESC_UpLeft.attach(10, 1000, 2000);
  ESC_UpRight.attach(7, 1000, 2000);
  Serial.begin(9600);
}
void loop() {
  //1
  joystickForward = analogRead(A10);   // reads the value of the potentiometer (Joystick)(value between 0 and 1023)    
  joystickForward = map(joystickForward, 1023, 0, 0, 180);   // scale it to use it with the servo library (value between 0 and 180)    
  ESC_Front.write(joystickForward);  // Send the signal to the ESC
  //2
  joystickTurn = analogRead(A3);   // reads the value of the potentiometer (Joystick)(value between 0 and 1023)    
  joystickTurn = map(joystickTurn, 1023, 0, 0, 180);   // scale it to use it with the servo library (value between 0 and 180)    
  ESC_Back.write(joystickTurn);  // Send the signal to the ESC
  //3
  joystickUpDown = analogRead(A1);   // reads the value of the potentiometer (Joystick)(value between 0 and 1023)    
  joystickUpDown = map(joystickUpDown, 1023, 0, 0, 180);   // scale it to use it with the servo library (value between 0 and 180)    
  ESC_UpLeft.write(joystickUpDown);  // Send the signal to the ESC
  ESC_UpRight.write(joystickUpDown);
  
}
