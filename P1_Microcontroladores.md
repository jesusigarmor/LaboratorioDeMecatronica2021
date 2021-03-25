# Práctica 1
## Experimento 1

- Código:

int estadoP=0;
int estadoA=0;
int estado=0;
int ledrojo=13;
int boton= 8;
int ledverde=5;

void setup()
{
  pinMode(ledrojo, OUTPUT);
  pinMode(ledverde, OUTPUT);
  pinMode(boton, INPUT);
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop()
{
  estadoP=digitalRead(boton);
  
  /*
  if((estadoP == HIGH) && (estadoA == LOW)){
  	estado=1-estado;
    delay(10);
  }
  
  estadoA = estadoP;
  */
  
  /*
  digitalWrite(LED_BUILTIN, HIGH);
  delay(1000);
  digitalWrite(LED_BUILTIN, LOW);
  delay(1000);
  */
  
  
  if(estadoP == HIGH){
    //digitalWrite(ledverde,HIGH);
    
    digitalWrite(ledrojo,HIGH);
    delay(250);
    digitalWrite(ledrojo,LOW);
    delay(250);
  }else{
    //digitalWrite(ledverde,LOW);
    
    digitalWrite(ledrojo,HIGH);
    delay(1000);
    digitalWrite(ledrojo,LOW);
    delay(1000);
   
  }
  
}

- Simulación:

[Simulación 1]( https://www.tinkercad.com/things/ahbj8L2C083 )

## Experimento 2

- Código:

int ledRojo1 = 13;
int ledAmarillo1 = 12;
int ledVerde1 = 11;

int ledRojo2 = 10;
int ledAmarillo2 = 9;
int ledVerde2 = 8;

void setup()
{
  pinMode(ledRojo1, OUTPUT); //rojo1
  pinMode(ledAmarillo1, OUTPUT); //amarillo1
  pinMode(ledVerde1, OUTPUT); //verde1
  pinMode(ledRojo2, OUTPUT); //rojo1
  pinMode(ledAmarillo2, OUTPUT); //amarillo1
  pinMode(ledVerde2, OUTPUT); //verde1
}

void loop()
{
  digitalWrite(ledRojo1, HIGH);
  digitalWrite(ledAmarillo1, LOW);
  digitalWrite(ledVerde1, LOW);
  digitalWrite(ledRojo2, LOW);
  digitalWrite(ledAmarillo2, LOW);
  digitalWrite(ledVerde2, HIGH);
  delay(5000);
  
  digitalWrite(ledRojo1, HIGH);
  digitalWrite(ledAmarillo1, LOW);
  digitalWrite(ledVerde1, LOW);
  digitalWrite(ledRojo2, LOW);
  digitalWrite(ledAmarillo2, HIGH);
  digitalWrite(ledVerde2, LOW);
  delay(1000);
  
  digitalWrite(ledRojo1, LOW);
  digitalWrite(ledAmarillo1, LOW);
  digitalWrite(ledVerde1, HIGH);
  digitalWrite(ledRojo2, HIGH);
  digitalWrite(ledAmarillo2, LOW);
  digitalWrite(ledVerde2, LOW);
  delay(5000);
  
  digitalWrite(ledRojo1, LOW);
  digitalWrite(ledAmarillo1, HIGH);
  digitalWrite(ledVerde1, LOW);
  digitalWrite(ledRojo2, HIGH);
  digitalWrite(ledAmarillo2, LOW);
  digitalWrite(ledVerde2, LOW);
  delay(1000);
}

- Simulación:

[Simulación 2]( https://www.tinkercad.com/things/cq55BjfzMbK )
