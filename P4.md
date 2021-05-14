# Práctica 4
## Experimento 1
- Código
~~~
int ledBlanco = 11;
int ledAzul = 12;
int motorIzquierda = 5;
int motorDerecha = 3;
int enable = 13;
int botonIzquierda = 9;
int botonDerecha = 7;

void setup()
{
  pinMode(botonIzquierda, INPUT);
  pinMode(botonDerecha, INPUT);
  pinMode(ledBlanco, OUTPUT);
  pinMode(ledAzul, OUTPUT);
  pinMode(motorIzquierda, OUTPUT);
  pinMode(motorDerecha, OUTPUT);
  pinMode(enable, OUTPUT);
}

void loop()
{
  digitalWrite(enable, HIGH);
  if (digitalRead(botonIzquierda) == LOW && digitalRead(botonDerecha) == LOW){
  	digitalWrite(ledBlanco, LOW);
    digitalWrite(ledAzul, LOW);
    digitalWrite(motorIzquierda, LOW);
    digitalWrite(motorDerecha, LOW);
    
  } else if (digitalRead(botonIzquierda) == HIGH && digitalRead(botonDerecha) == LOW){
  	digitalWrite(ledBlanco, HIGH);
    digitalWrite(ledAzul, LOW);
    digitalWrite(motorIzquierda, HIGH);
    digitalWrite(motorDerecha, LOW);
    
  } else if (digitalRead(botonIzquierda) == LOW && digitalRead(botonDerecha) == HIGH){
  	 digitalWrite(ledBlanco, LOW);
    digitalWrite(ledAzul, HIGH);
    digitalWrite(motorIzquierda, LOW);
    digitalWrite(motorDerecha, HIGH);
   
  } else {
  	digitalWrite(motorDerecha, HIGH);
    digitalWrite(ledAzul, HIGH);
    digitalWrite(motorIzquierda, HIGH);
    digitalWrite(botonDerecha, HIGH);
   
  } 
}
~~~
[Experimento 1](https://www.tinkercad.com/things/lE8ZwK1qLen-copy-of-control-de-un-motor-cc-/editel?sharecode=4_CYDfXp0UsK7l3wrkx7D65CSuuf_vMruqfCbfuQNxU)


## Experimento 2
- Código
~~~
int motorIzquierda=5;
int motorDerecha=3;
int enable=11;
int potenciometro=A0;
int valor;
int pwm1;
int pwm2;          
 
void setup()
{
  pinMode(motorIzquierda,OUTPUT);
  pinMode(motorDerecha,OUTPUT);
  pinMode(enable,OUTPUT);
}
 
void loop()
{ 
  valor=analogRead(potenciometro);
  pwm1=map(valor, 0, 1023, 0, 255);
  pwm2=map(valor, 0, 1023, 255, 0);
   if(valor < 512){
    digitalWrite(motorIzquierda, HIGH);
    digitalWrite(motorDerecha, LOW);
    analogWrite(enable,pwm2);
  }else{
    digitalWrite(motorIzquierda, LOW);
    digitalWrite(motorDerecha, HIGH);
    analogWrite(enable,pwm1);
  
   }
}
~~~
[Experimento 2](https://www.tinkercad.com/things/92bf8kOnpNl-copy-of-control-de-un-motor-cc-/editel?sharecode=Q9h-9aAeFacWhrPVzINg5Z_cMnVBOQxLFPgZps1qsKk)
