#include <Servo.h>
#include <Wire.h>
Servo leftservo;
Servo rightservo;
int a =0;
int b =0;
int c =0;
int d =0;
const int trigPin = 12;
const int echoPin = 13;
long duration;
int distanceCm;
void setup()
{
  Serial.begin(9600);
  leftservo.attach(10);
  rightservo.attach(9);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(3,OUTPUT);
  pinMode(5,OUTPUT);
  pinMode(9,OUTPUT);
  pinMode(10,OUTPUT);
  digitalWrite(3,LOW);
  digitalWrite(5,LOW);
  Wire.begin(9);
  Wire.onReceive(receiveEvent);
  Wire.onRequest(requestEvent);
}
void receiveEvent(int bytes)
{
  a = Wire.read();
  b = Wire.read();
  c = Wire.read();
  d = Wire.read();
}

void requestEvent ()
{
  Wire.write(distanceCm);
}

void loop()
{
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  distanceCm= duration*0.034/2;
  
  if(a ==1 && distanceCm >50)
  {
    digitalWrite(5,HIGH);
  }
  else
  {
    digitalWrite(5,LOW);
  }
  
  if(b ==1)
  {
    digitalWrite(3,HIGH);
  }
  else
  {
    digitalWrite(3,LOW);
  }
  
  if(c ==1)
  {
      leftservo.write(65);
      rightservo.write(65);
  }
  
  if(d ==1)
  {
      leftservo.write(115);
      rightservo.write(115);
  }

  if(c ==0 && d ==0)
  {
      leftservo.write(90);
      rightservo.write(90);
  }
}
