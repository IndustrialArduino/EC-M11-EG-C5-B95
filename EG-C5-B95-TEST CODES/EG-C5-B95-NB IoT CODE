#include <Wire.h>

#define RXD2 4
#define TXD2 2
#define PIN 5
#define RES 19
#define DEVICE_ADDRESS 0x49

void setup() {
  Serial.begin(9600);
  Serial2.begin(9600, SERIAL_8N1, RXD2, TXD2);
  pinMode(PIN, OUTPUT);
  pinMode(RES, OUTPUT);

  digitalWrite(RES, HIGH);
  digitalWrite(PIN, HIGH);

  Wire.begin(16, 17);  // SDA on GPIO16, SCL on GPIO17
  Serial.begin(115200);
}

void loop() {
  // Serial Communication
  if (Serial2.available()) {
    int inByte = Serial2.read();
    Serial.write(inByte);
  }

  if (Serial.available()) {
    int inByte = Serial.read();
    Serial2.write(inByte);
  }

  // I2C Communication
  Wire.beginTransmission(DEVICE_ADDRESS);
  Wire.write(0x01);  // Replace with your data
  Wire.write(0x02);
  Wire.write(0x03);
  Wire.endTransmission();
  delay(100);

  Wire.requestFrom(DEVICE_ADDRESS, 3);  // 3 bytes of data
  if (Wire.available() >= 3) {
    byte data1 = Wire.read();
    byte data2 = Wire.read();
    byte data3 = Wire.read();
    Serial.print("Read Data: ");
    Serial.print(data1, HEX);
    Serial.print(" ");
    Serial.print(data2, HEX);
    Serial.print(" ");
    Serial.println(data3, HEX);
  }

  delay(1000);
}
