//-------------------BLYNK-----------------------//

#include <WiFi.h>
#include <WiFiClient.h>
#include <BlynkSimpleEsp32.h>
int pin = 2;

char auth[] = "DmubG85t1XWnAi66MHCG0R7MrvdSSWK5";
char ssid[] = "HUAWEI_CUN-L21_EEFC";
char pass[] = "Vatykan45";

//-------------------TEMPERATUUR SENSOR------------//

#include <Adafruit_BMP280.h>
Adafruit_BMP280 bmp; // I2C Interface

//-------------------LICHTMETER-----------------//

#include <Wire.h>
#include <BH1750.h>
BH1750 lichtMeter;

//-------------------OLED----------------------//

#include <SPI.h>
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_BMP280.h>

#define SCREEN_WIDTH 128 // OLED display width, in pixels
#define SCREEN_HEIGHT 64 // OLED display height, in pixels

// Declaration for an SSD1306 display connected to I2C (SDA, SCL pins)
#define OLED_RESET     -1 // Reset pin # (or -1 if sharing Arduino reset pin)
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

#define NUMFLAKES     10 // Number of snowflakes in the animation example

#define LOGO_HEIGHT   16
#define LOGO_WIDTH    16
static const unsigned char PROGMEM logo_bmp[] =
{ B00000000, B11000000,
  B00000001, B11000000,
  B00000001, B11000000,
  B00000011, B11100000,
  B11110011, B11100000,
  B11111110, B11111000,
  B01111110, B11111111,
  B00110011, B10011111,
  B00011111, B11111100,
  B00001101, B01110000,
  B00011011, B10100000,
  B00111111, B11100000,
  B00111111, B11110000,
  B01111100, B11110000,
  B01110000, B01110000,
  B00000000, B00110000 };


void setup(){

//------------------------LICHTMETER------------------------//
  
  Serial.begin(9600);
  lichtMeter.begin();
  Serial.begin(9600);
  Serial.println(F("BMP280 test"));
  
//--------------------------TEMPERATUUR SENSOR------------------//

  if (!bmp.begin()) {
    Serial.println(F("Could not find a valid BMP280 sensor, check wiring!"));
    while (1);
  }
bmp.setSampling(Adafruit_BMP280::MODE_NORMAL,     /* Operating Mode. */
                  Adafruit_BMP280::SAMPLING_X2,     /* Temp. oversampling */
                  Adafruit_BMP280::SAMPLING_X16,    /* Pressure oversampling */
                  Adafruit_BMP280::FILTER_X16,      /* Filtering. */
                  Adafruit_BMP280::STANDBY_MS_500); /* Standby time. */

//-----------------------BLYNK--------------------------------//
 
  Serial.begin(115200);
  delay(10);
  Serial.print("Connecting to ");
  Serial.println(ssid);
  WiFi.begin(ssid, pass);
  int wifi_ctr = 0;
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
 Serial.println("WiFi connected"); 
  Blynk.begin("DmubG85t1XWnAi66MHCG0R7MrvdSSWK5", ssid, pass);

}

 
void loop() {

//-----------------------LICHTMETER---------------------------------//
  
  uint16_t lux = lichtMeter.readLightLevel();
  Serial.print("Licht: ");
  Serial.print(lux);
  Serial.println(" lux");
  delay(500);

//-------------------------TEMPERATUUR SENSOR---------------------//
 
 Serial.print(F("Temperature = "));
    Serial.print(bmp.readTemperature());
    Serial.println(" *C");

    Serial.print(F("Pressure = "));
    Serial.print(bmp.readPressure()/100); //displaying the Pressure in hPa, you can change the unit
    Serial.println(" hPa");

    Serial.print(F("Approx altitude = "));
    Serial.print(bmp.readAltitude(1019.66)); //The "1019.66" is the pressure(hPa) at sea level in day in your region
    Serial.println(" m");                    //If you don't know it, modify it until you get your current altitude

    Serial.println();
    delay(2000);

//--------------------------BLYNK---------------------------//
    Blynk.run();
}
