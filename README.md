// Code of ESP32 controller to sense the Humidity and Temprature 
//STEP-1 Include necessary libraries:
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>


//STEP-2 Define the I2C address and dimensions of the LCD:
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4


//STEP-3 Define the pin connected to the DHT sensor:
const int DHT_PIN = 15;


//STEP-4 Create objects for DHTesp and LiquidCrystal_I2C:
DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);


//STEP-5 Setup function to initialize the sensor and LCD:
void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();

}


//STEP-6 Loop function to read and display sensor data:
void loop() {

  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  
  lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  lcd.print("Wokwi Online IoT");

  delay(1000);
}
