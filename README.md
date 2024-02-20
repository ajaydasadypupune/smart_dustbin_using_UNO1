# smart_dustbin_using_UNO1
#include <Servo.h>

const int trigPin = 9;  // Ultrasonic sensor trigger pin
const int echoPin = 10; // Ultrasonic sensor echo pin
const int servoPin = 5; // Servo motor control pin

Servo myServo;

void setup() {
  Serial.begin(9600);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  myServo.attach(servoPin);
  closeLid(); // Close the lid initially
}

void loop() {
  long duration, distance;
  
  // Trigger ultrasonic sensor
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  // Measure the echo duration
  duration = pulseIn(echoPin, HIGH);
  
  // Convert the duration to distance in centimeters
  distance = (duration / 2) / 29.1;

  // Check if an object is detected within a certain range (adjust as needed)
  if (distance < 20) {
    openLid();
  } else {
    closeLid();
  }

  delay(1000); // Add a delay for stability
}

void openLid() {
  myServo.write(90); // Open position
}

void closeLid() {
  myServo.write(0); // Close position
}
