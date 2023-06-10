# Practica ESP32 con Sensor de Distancia HC-SR04 con LCD
Este repositorio muestra como podemos programar una ESP32 con el sensor de distancia HC-SR04  con un LCD.


### Descripción

La ```Esp32``` la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor (```HC-SR04```) para medir distancia y una (```LCD 16X2 (l2C)```); y en este poder ver digitalmente la distancia obtenida por medio del sensor. Cabe aclarar que esta practica se usara en el simulador llamado [WOKWI](https://https://wokwi.com/).


## Material Necesario

Para realizar esta practica necesitas lo siguiente

- [WOKWI](https://https://wokwi.com/)
- Tarjeta ESP 32
- Sensor HC-SR04
- LCD 16X2 (l2C)


## Instrucciones


### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://https://wokwi.com/).


### Instrucciones de preparación de entorno 

1. Abrir la terminal de programación y colocar la siguente programación:

```
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 34;   //Pin digital 3 para el Echo del sensor

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);



void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  lcd.init();
  lcd.backlight();
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0



}

void loop()
{

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros


  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(3000);          //Hacemos una pausa de 100ms

  lcd.setCursor(0, 0);
  lcd.print("  Distancia: " + String(d) +"cm  ");
  lcd.setCursor(0, 1);
  lcd.print("Ing. OMAR ");
  delay(2000);
}

```
2. Instalar la libreria de  **LiquidCrystal I2C** como se muestra en la siguente imagen.

![](https://github.com/Omarcollado23/PRACSENSORDISTANCIA/blob/main/libreria.jpg?raw=true)

3. Hacer la conexion de **HC-SR04** con la **ESP32** y el **LCD** como se muestra en la siguente imagen.

![](https://github.com/Omarcollado23/PRACSENSORDISTANCIA/blob/main/conexiones.jpg?raw=true)

### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial.
3. Colocar la distancia dando *doble click* al sensor **HC-SR04** 

  

## Resultados

Cuando haya funcionado, verás los valores dentro del monitor serial como se muestra en la siguente imagen.

![](https://github.com/Omarcollado23/PRACSENSORDISTANCIA/blob/main/datos.jpg?raw=true)


## Evidencias

[Video de Youtube](https://https://wokwi.com/)


# Créditos

Desarrollado por Ing. Omar Alejandro Collado Carriola

- [GitHub](https://github.com/DiegoJm10)