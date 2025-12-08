#define BLYNK_TEMPLATE_ID ""
#define BLYNK_TEMPLATE_NAME ""
#define BLYNK_AUTH_TOKEN ""

#include <WiFi.h>
#include <BlynkSimpleEsp32.h>

#define TRIG_PIN 5
#define ECHO_PIN 18
#define FSR_PIN 34   // Analog pin for FSR
#define BUZZER_PIN 23

char ssid[] = "";          // Your WiFi name
char pass[] = "";      // Your WiFi password

long duration;
int distance;
int fsrValue;

void setup() {
  Serial.begin(115200);

  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  pinMode(BUZZER_PIN, OUTPUT);

  Blynk.begin(BLYNK_AUTH_TOKEN , ssid , pass);
}

void loop() {
  Blynk.run();

  // Ultrasonic Reading
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);
  duration = pulseIn(ECHO_PIN, HIGH);
  distance = duration * 0.034 / 2;

  // FSR Reading
  fsrValue = analogRead(FSR_PIN);

  Serial.print("Distance (cm): ");
  Serial.print(distance);
  Serial.print(" | FSR Value: ");
  Serial.println(fsrValue);

  // Decision Logic
  if (distance > 50 && fsrValue < 1000) {
    digitalWrite(BUZZER_PIN, HIGH);
    Blynk.logEvent("bed_exit", "Person likely exited the bed!");
  } else {
    digitalWrite(BUZZER_PIN, LOW);
  }

  delay(10000);  // 10 second delay to check again
}
