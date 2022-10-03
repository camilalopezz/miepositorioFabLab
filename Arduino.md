## Placa Adafruit_HUZZAH32_ESP32_Feather

# Pin out
![AdafruitHuzzah32PinDiagram](https://user-images.githubusercontent.com/49143566/193604273-de6c3e52-1e2f-4b55-bb50-664529964142.png)


Seguir e siguiente tutorial para los proyectos
https://fablabbcn.github.io/digifab/modulo_4/arduino/

/***********************************************************************/
# Lectura y escritura analogica

Las entradas analogicas son todas las que dicen ADC, las salidas de pwm solo A0 y A1

/*************************************************************************/
# Buzzer 
no funciona la libreria tone de arduino hay que instalar libreria  "Makeability Lab Arduino Library" manualmente

para esto se debe descargar el fichero .zip desde git https://github.com/makeabilitylab/arduino

luego dentro de este fichero, buscar la carpeta Makeability Lab Arduino Library, y copiarla dentro de la carpeta de intalacion de arduino

/*******************************************************************************/
# Touch

con las librerias instaladas 

/**
 * This example demonstrates the capacitive touch sensing functionality on the ESP32. The ESP32
 * has 10 capacitive touch pins. We're using T6 (GPIO 14).
 * 
 * When the capacitance value on T6 falls below a set threshold (TOUCH_THRESHOLD), we turn on an LED
 * 
 * Official Espressif ESP32 touch sensing docs:
 * https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/peripherals/touch_pad.html
 * https://github.com/espressif/esp-iot-solution/blob/master/documents/touch_pad_solution/touch_sensor_design_en.md
 * 
 * By Jon E. Froehlich
 * @jonfroehlich
 * http://makeabilitylab.io
 * 
 * Circuit diagram and walkthrough here:
 * https://makeabilitylab.github.io/physcomp/esp32/capacitive-touch-sensing
 * 
 */

const int CAPACITIVE_TOUCH_INPUT_PIN = T6; // GPIO pin 14
const int LED_OUTPUT_PIN = 21;
const int TOUCH_THRESHOLD = 20; // turn on light if touchRead value < this threshold
const boolean PRETTY_PRINT = false;

void setup() {
  Serial.begin(9600);
  pinMode(LED_OUTPUT_PIN, OUTPUT);
}

void loop() {
  unsigned long startReadTimestamp = micros();

  // By default, touchRead should take ~500 microseconds according to the ESP32 source code
  // https://github.com/espressif/arduino-esp32/blob/a59eafbc9dfa3ce818c110f996eebf68d755be24/cores/esp32/esp32-hal-touch.h
  // You can configure these settings using touchSetCycles
  int touchVal = touchRead(CAPACITIVE_TOUCH_INPUT_PIN);
  unsigned long elapsedTime = micros() - startReadTimestamp;
  boolean ledOn = false;
  
  // Turn on LED if touchRead value drops below threshold
  if(touchVal < TOUCH_THRESHOLD){
    ledOn = true;
  }
  
  digitalWrite(LED_OUTPUT_PIN, ledOn);
  if(PRETTY_PRINT){
    Serial.println((String)touchVal + ", " + elapsedTime + " microseconds, LED " + ledOn);
  }else{
    Serial.println((String)touchVal + ", " + ledOn);
  }
  delay(50);
}
/*********************************************************************************************************/

# IO 

Se carga el firmware desde la pagina
se crea un dashboar, se crean unos blocks que pueden ser senores u otras cosas

