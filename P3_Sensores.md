# Práctica 3
## Experimento 3
- Código
~~~
#include <LiquidCrystal.h>
LiquidCrystal lcd(12,11,5,4,3,2);

void setup() {
  lcd.begin(16,2);
  Serial.begin(9600);

}

void loop() {
  int x = analogRead(A0);
  int y = analogRead(A1);
  int z = analogRead(A2);

  float Gx=((x-272.0)*2.0/140.0) -1.0;
  float Gy=((y-265.0) * 2.0/140.0)-0.986;
  float Gz=((z-205.0)*2.0/140.0)-1.0;

  float anguloZ =atan2(Gx,Gy)*57.2957795;
  float anguloX= Gx*90.0+88;
  float anguloY=Gy*90.0+82;

  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("Roll ");
  lcd.print(" Pitch ");
  lcd.print(" Yaw");
  lcd.setCursor(0,1);
  lcd.print(anguloX);
  lcd.setCursor(5,1);
  lcd.print("/");
  lcd.print(anguloY);
  lcd.setCursor(11,1);
  lcd.print("/");
  lcd.print(anguloZ);

  delay(1000);

}

~~~

[Experimento 3](https://www.tinkercad.com/things/2az2oSGw0XC-copy-of-accelerometer/editel?sharecode=voPM4Sj2MclTkc2tjbzr8hdZD6_0_Fm930dTTUzX6HE)
