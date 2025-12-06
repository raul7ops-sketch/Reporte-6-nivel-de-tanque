# Reporte-6-nivel-de-tanque
## Introduccion
### En esta practica se realizo un medidor de nivel de un tanque de agua en el cual se utilizo un sensor ultrasonico junto con unos leds para marcar la altura del nivel del agua ademas de agregar una LCD para poder visualizar incluso el porcentaje que se encuentra dicho tanque.
## Materiales y equipo a utilizar
- ESP 32
- Sensor ultrasonico
- LCD
- Leds variados
## Procedimiento
1. Abriremos nuestro Wokwi para poder acomodar los dispositivos anterior mencionados de la siguiente manera:
![](https://github.com/raul7ops-sketch/Reporte-6-nivel-de-tanque/blob/main/reporte%206.png?raw=true)
2. Siguiente a esto tendremos que copiar y agregar el siguiente codigo a nuestro wokwi.
``` #include <LiquidCrystal_I2C.h>
const int trigPin = 4;
const int echoPin = 15;
const int led1 = 17;
const int led2 = 5;
const int led3 = 19;
const int led4 = 18;
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   16
// defines variables
long duration;
int distance;
int safetyDistance;
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
pinMode(echoPin, INPUT); // Sets the echoPin as an Input
pinMode(led1, OUTPUT);
pinMode(led2, OUTPUT);
pinMode(led3, OUTPUT);
pinMode(led4, OUTPUT);
Serial.begin(9600); // Starts the serial communication
  lcd.init();
  lcd.backlight();
}


void loop() {
// Clears the trigPin
digitalWrite(trigPin, LOW);
delayMicroseconds(2);

// Sets the trigPin on HIGH state for 10 micro seconds
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);

// Reads the echoPin, returns the sound wave travel time in microseconds
duration = pulseIn(echoPin, HIGH);

// Calculating the distance
distance= duration*0.034/2;

safetyDistance = distance;
if (safetyDistance>=1 && safetyDistance<=99)
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
  lcd.clear();
  lcd.print("Porcentaje: 100%");
  delay(2000);
}
else if(safetyDistance>=100 && safetyDistance<=199) 
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
   lcd.clear();
  lcd.print("Porcentaje: 75%");
  delay(2000);
}
else if(safetyDistance>=200 && safetyDistance<=299) 
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
   lcd.clear();
  lcd.print("Porcentaje: 50%");
  delay(2000);
}
else if(safetyDistance>=300 && safetyDistance<=399) 
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, HIGH);
   lcd.clear();
  lcd.print("Porcentaje: 25%");
  delay(2000);
}
else if(safetyDistance>=400 && safetyDistance<=499) 
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
   lcd.clear();
  lcd.print("Porcentaje: 0%");
  delay(2000);
}
else
{
 digitalWrite(led1,  LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
   lcd.clear();
  lcd.print("Eror");
  delay(2000);
}

// Prints the distance on the Serial Monitor
Serial.print("Distancia: ");
Serial.println(distance);
lcd.clear();
lcd.setCursor(2, 0);
lcd.print("Distancia: " + String(distance));
delay (2000);

  delay(2000);
  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("Bienvenidos");
  lcd.setCursor(2, 1);
  lcd.print("al curso");
  delay(2000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Raul Aguilar L.");
  lcd.setCursor(0, 1);
  lcd.print("Ing. Mecanico");
  delay(2000);
   lcd.clear();
  lcd.setCursor(1, 0);
  lcd.print("Fecha:  ");
  lcd.setCursor(5, 1);
  lcd.print("28/11/25");
  delay(2000);
}
```
3. Instalamos las siguiente libreria ```LiquidCrystal I2C```.
## Resultados y evidencia
- Pusimos que cada led iluminado indica el porcentaje del tanque que marca nuestro sensor ultrasonico.
![](https://github.com/raul7ops-sketch/Reporte-6-nivel-de-tanque/blob/main/reporte%206.1.png?raw=true)
### Aqui se puede ver claramente como indica que el tanque esta a su 50% de su capacidad y se encienden los dos leds deinferiores para señalar con un indicador luminico
## Creditos
Esta practica fue elaborada por Raul Aguilar https://github.com/raul7ops-sketch
