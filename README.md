#include <DHT.h>
#include <DHT_U.h>

#include <LiquidCrystal.h>

const int DHTPIN 5;

LiquidCrystal lcd(13, 12, 11, 10, 9, 8);

const int ledPin = 6; 
//const int input = 7; 
void setup()
{
  
  Serial.begin(9600);
  //pinMode(input, INPUT);
  pinMode(ledPin, OUTPUT);
  pinMode(DHTPIN, INPUT);
  lcd.begin(20, 4);
  // Print a message to the LCD.
  lcd.setCursor(0,0);
  lcd.print("----INFORMATION----");
  lcd.setCursor(0,1);
  lcd.print("SOIL MOISTURE LEVEL.");
  lcd.setCursor(2,2);
  lcd.print("Analog Value: ");
  lcd.setCursor(2,3);
  lcd.print("Voltage: ");
}
void loop()
{
  int dht=DHT.read(DHTPIN);
  Serial.print("Temperature: ");
  Serial.print(DHT.temperature);
  Serial.print("Humidity: ");
  Serial.print(DHT.temperature);
  float s=analogRead(A0);
  int d=map(s,0,1023,0,255);
  if (d>100)
  {
    //delay(1000);
    digitalWrite(ledPin,HIGH);
    Serial.print(d);
  }
  else
  {
    //delay(1000);
    digitalWrite(ledPin,LOW);
  }

  int SensorValue = analogRead(A0);   
  float SensorVolts = analogRead(A0)*0.0048828125;   
  
  lcd.setCursor(16, 2);  
  lcd.print(SensorValue);
  lcd.setCursor(9, 3);  
  lcd.print(SensorVolts);     
  lcd.print("V");
  delay(1000);
}
