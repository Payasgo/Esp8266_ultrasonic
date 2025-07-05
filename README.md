📏 ESP8266 Ultrasonic Distance Measurement System

This project uses an ESP8266 NodeMCU and an HC-SR04 ultrasonic sensor to measure distances in real-time. It's a beginner-friendly embedded system project often used in obstacle detection, smart parking, water level monitoring, or basic IoT automation.

🧠 Project Overview

The HC-SR04 sensor sends ultrasonic pulses and receives their echoes to calculate the distance between the sensor and an object in front of it. The ESP8266 processes this data and can optionally display it, log it, or send it over Wi-Fi.
🧩 Components Used
Component	Quantity	Description
ESP8266 NodeMCU	1	Wi-Fi-enabled microcontroller board
HC-SR04	1	Ultrasonic distance sensor
Jumper Wires	4	For connections
Breadboard (opt)	1	For prototyping
USB Cable	1	For power & code upload
🔌 Circuit Diagram
HC-SR04 Pin	ESP8266 Pin	Description
VCC	3V3	Power supply
GND	GND	Ground
TRIG	D5 (GPIO14)	Trigger pin (send pulse)
ECHO	D6 (GPIO12)	Echo pin (receive pulse)

    ⚠️ Note: HC-SR04 works on 5V logic. But it generally works with ESP8266’s 3.3V if distance is less. For safety, use a voltage divider or logic level shifter on ECHO.

🧪 How It Works

    ESP8266 sends a HIGH signal to the TRIG pin for 10 microseconds.

    This triggers the sensor to emit an ultrasonic pulse.

    The pulse reflects off an object and returns to the ECHO pin.

    The ESP8266 measures the duration of the pulse and calculates distance using:

    distance (cm) = duration / 58.0

🧾 Sample Arduino Code

#define TRIG_PIN D5
#define ECHO_PIN D6

void setup() {
  Serial.begin(115200);
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
}

void loop() {
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  long duration = pulseIn(ECHO_PIN, HIGH);
  float distance = duration / 58.0;

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  delay(500);
}

📺 Output Example

When connected to the Arduino Serial Monitor (baud: 115200):

Distance: 23.45 cm
Distance: 22.80 cm
Distance: 24.10 cm

📦 Applications

    🚗 Smart Parking Systems

    🛑 Obstacle Detection in Robotics

    🚰 Water Level Monitoring

    🚪 Automatic Door Openers

    📏 DIY Digital Rulers or Ranging Tools

🔄 Future Enhancements

    ✅ Add OLED display for visual output

    ✅ Send data to cloud (e.g., ThingSpeak / Firebase)

    ✅ Trigger alarms if objects are too close

    ✅ Integrate with Wi-Fi dashboard or mobile app

🧠 Troubleshooting
Issue	Possible Fix
Always 0 cm	Check TRIG/ECHO pins; wiring; delays
Readings too high/unstable	Use stable 5V power; avoid noisy surfaces
ESP8266 rebooting	Add a voltage divider on ECHO pin
