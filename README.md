/*
   ESP32 Inductive Metal Detector
   Reads data from an NPN Inductive Proximity Sensor
*/

#define METAL_SENSOR_PIN 27  // GPIO pin connected to the sensor output
#define BUZZER_PIN       2   // GPIO pin connected to a buzzer or built-in LED

void setup() {
  Serial.begin(115200);
  
  // NPN sensors pull the pin LOW when metal is detected
  pinMode(METAL_SENSOR_PIN, INPUT_PULLUP); 
  pinMode(BUZZER_PIN, OUTPUT);
  
  Serial.println("--- ESP32 Metal Detector Initialized ---");
}

void loop() {
  // Read sensor state
  int sensorState = digitalRead(METAL_SENSOR_PIN);

  // LJ12A3-4-Z/BX NPN NO drops to LOW when it senses metal
  if (sensorState == LOW) {
    Serial.println("METAL DETECTED!");
    digitalWrite(BUZZER_PIN, HIGH); // Turn on Buzzer/LED
  } else {
    Serial.println("No metal in range.");
    digitalWrite(BUZZER_PIN, LOW);  // Turn off Buzzer/LED
  }

  delay(200); // Small delay to avoid flooding the Serial Monitor
}
