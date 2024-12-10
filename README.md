# Practica-ESP32-con-DHT22-y-LCD

## Introducción
En este repositorio utilizaremos la ```ESP32``` en un entorno de adquisición de datos, también le conectaremos un sensor ```DTH22``` para que nos muestre cada 2s la temperatura y la humedad en una patalla LCD; todo esto se hará en el simulador  [WOKWI](https://wokwi.com/).


## Material Necesario
- [WOKWI](https://wokwi.com/)
- Trajeta ESP32
- Sensor DTH32
- pantalla LCD I2C


## Instrucciones

### Requisitos Previos

Necesitas abrir la la pagina [WOKWI](https://wokwi.com/).


### Preparación del entorno

1. Ya en la plataforma debes seleccionar la tarjeta que usaremos en este caso seria la  ```ESP32```.
![](https://github.com/AntoniodeJesus19/Practica-ESP32-con-DHT22/blob/main/Captura%20de%20pantalla%202024-12-09%20223637.png?raw=true)

2. Luego bajamos un poco el cursor y en ```Starter Templates``` seleccionamos ESP32.
![](https://github.com/AntoniodeJesus19/Practica-ESP32-con-DHT22/blob/main/Captura%20de%20pantalla%202024-12-09%20224130.png?raw=true)

3. En la terminal de programacion borramos todo y colocamos la siguiente programación:
```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();

}

void loop() {

 lcd.clear();
 lcd.setCursor(2,0);
 lcd.print("Diplomado V");
 lcd.setCursor(2,1);
 lcd.print("Mecatronica");
 delay(2000);

 lcd.clear();
 lcd.setCursor(0,0);
 lcd.print("Antonio de Jesus");
 lcd.setCursor(2,1);
 lcd.print("Ing. Mecanico");
 delay(2000);

 lcd.clear();
  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  
  lcd.setCursor(2, 0);
  lcd.print("Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");

  delay(2000);
}

```

4. Instalar la libreria **DHT sensor library for ESPx** y **LiquidCrystal I2C**.
![]()

5. Seleccionamos nuestro sensor en la parte de **Simulacion** en el boton **+** y buscamos **DHT22**, luego buscamos **LCDI2C** y los conectamos de la siguiente manera.
![]()


### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial.


## Resultados

Cuando haya funcionado, verás los valores y los textos en la pantalla LCD como se muestran en las siguentes imagenes cada 2s.
![]()
![]()
![]()


# Créditos

Desarrollado por Antonio de Jesús Mentado Huerta

- [GitHub](https://github.com/AntoniodeJesus19)
