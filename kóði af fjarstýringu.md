#include <Wire.h>
#include <LiquidCrystal.h>
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
bool forward , backward , right , left =0;
int a =0;
int b =0;
int c =0;
int d =0;
int distanceCm;
void setup()
{
  Serial.begin(9600);
  lcd.begin(16,2);
  lcd.setCursor(0,0);
  lcd.print("Loading...");
  delay(2000);
  lcd.clear();
  pinMode(6,INPUT);
  pinMode(7,INPUT);
  pinMode(8,INPUT);
  pinMode(9,INPUT);
  digitalWrite(6,HIGH);
  digitalWrite(7,HIGH);
  digitalWrite(8,HIGH);
  digitalWrite(9,HIGH);
  Wire.begin();
}

void loop()
{
  Wire.requestFrom(9,1);
  distanceCm = Wire.read();
    lcd.setCursor(0,0);
    lcd.print(distanceCm);
    lcd.print(" cm");
    delay(500);                                     
    lcd.clear();
  
  forward = digitalRead(6);
  right = digitalRead(7);
  left = digitalRead(8);
  backward = digitalRead(9);
  
  if (forward ==1)
  {
    a = 1;
  }

  else
  {
    a = 0;
  }
    
  if (backward ==1)
  {
    b = 1;
  }
  else
  {
    b = 0;
  }
  
   if (left ==1)
  {
    c = 1;
  }
  else
  {
    c = 0;
  }
  
   if (right ==1)
  {
    d = 1;
  }
  else
  {
    d = 0;
  }
  
  Wire.beginTransmission(9);
  Wire.write(a);
  Wire.write(b);
  Wire.write(c);
  Wire.write(d);
  Wire.endTransmission();
}
