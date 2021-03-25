# Práctica 2 - Arduino
## Experimento 1
- Codigo
~~~
int analogPin=A0;
int val=0;
float volt=0;
int ledAmarillo=13;
int ledRojo=5;
int brillo=0;
void setup (){
  pinMode(ledAmarillo,OUTPUT);
  pinMode(ledRojo,OUTPUT);
  Serial.begin(9600);
}
void loop (){
  val=analogRead(analogPin);
  volt = val * (5.0 / 1023.0);
  Serial.print("Conversión analógico-digital:");
  Serial.println(val);
  Serial.print("Voltaje:");
  Serial.println(volt); //2.1.3
  //2.1.4
  if(volt>3.00){
    digitalWrite(ledAmarillo,HIGH);
  }else{
  	digitalWrite(ledAmarillo,LOW);
  }
  //2.1.5
  analogWrite(ledRojo,val/4); 
}
~~~
- Simulación 

[Experimento 1]( https://www.tinkercad.com/things/h9Bk7t086mj )

## Experimento 2
- Codigo

~~~
#include <LiquidCrystal.h>
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
int i=15;
void setup(){
  lcd.begin(16,2);
}
void loop(){
  /*
  //2.2.1
  lcd.setCursor(1,0);
  lcd.print("Principios de");
  lcd.setCursor(2,1);
  lcd.print("Mecatronica");
  delay(750);
  lcd.clear();
  delay(250);
  */
  //2.2.2
  if(i>=1){
    lcd.setCursor(i,0);
    lcd.print("Isaias Jesus");
    lcd.setCursor(i,1);
    lcd.print("Garcia Moreno");
    delay(550);
    lcd.clear();
    delay(50);
  }else{
    lcd.setCursor(1,0);
    lcd.print("Isaias Jesus");
    lcd.setCursor(1,1);
    lcd.print("Garcia Moreno");
  }
  i--;
}
~~~
- Simulación 

[Experimento 2](https://www.tinkercad.com/things/jN2yGjUiO2b)

## Experimento 3
- Codigo

~~~
#include <Servo.h>
#include <LiquidCrystal.h>
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
int pos = 0;
Servo servo;
int analogPin=A0;
int val=0;
float volt=0;
void setup()
{
  servo.attach(9, 500, 2500);
  lcd.begin(16,2);
}
void loop()
{
  val=analogRead(analogPin);
  volt = val * (5.0 / 1023.0);
  pos = map(val,0,1023,0,180);
  servo.write(pos);
  delay(20);
  lcd.setCursor(1,0);
  lcd.print("Voltaje:"+String(volt));
  lcd.setCursor(1,1);
  lcd.print("Angulo:"+String(pos));
  /*
  for (pos = 0; pos <= 180; pos += 1) {
    myservo.write(pos);
    delay(15); 
  }
  for (pos = 180; pos >= 0; pos -= 1) {
    myservo.write(pos);
    delay(15); 
  }
  */
}
~~~
- Simulación 

[Experimento 3](https://www.tinkercad.com/things/aVhPzS2edHc)
