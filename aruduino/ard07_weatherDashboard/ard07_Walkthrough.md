# Arduino Walkthrough: WiFi Weather Dashboard

**Programming — Medina County Career Center**

---

## Overview

You're going to connect your Arduino Uno R4 WiFi to the internet, fetch real weather data from the **National Weather Service API** (api.weather.gov), and display the current temperature and conditions on the board's built-in **LED matrix**.

No extra sensors, no accounts, no API keys — the NWS API is free and open to everyone.

**What you'll learn:**
- Connecting to WiFi from the Arduino
- Making HTTPS requests to a web API
- Parsing JSON data
- Displaying scrolling text on the LED matrix

---

## What You Need

- Arduino Uno R4 WiFi + USB cable
- WiFi network name and password (your instructor will provide this)
- Arduino IDE 2.x installed

### Libraries to Install

In the Arduino IDE, go to **Sketch → Include Library → Manage Libraries** and install:

1. **ArduinoJson** by Benoit Blanchon (version 7.x)
2. **ArduinoGraphics** by Arduino (version 1.x)

The `WiFiS3` and `Arduino_LED_Matrix` libraries come built-in with the Uno R4 WiFi board package — you don't need to install those.

---

## Part 1 — Create the Project Files

This project uses multiple `.ino` files in one folder. The Arduino IDE automatically combines all `.ino` files in the same folder into one program. This keeps the code organized.

### Step 1: Create the project folder

1. In the Arduino IDE, go to **File → New Sketch**
2. Immediately go to **File → Save As** and name it `WeatherDashboard`
3. This creates a folder called `WeatherDashboard` with `WeatherDashboard.ino` inside

### Step 2: Create the secrets file

1. Click the **"…"** button (or the tab dropdown) near the top of the IDE
2. Choose **New Tab**
3. Name it `Secrets.h`
4. Paste this code:

```cpp
#pragma once
// WiFi credentials — get these from your instructor
#define WIFI_SSID "YourNetworkName"
#define WIFI_PASS "YourNetworkPassword"
```

**Replace** the values with the WiFi name and password your instructor gives you. Keep the quotes.

### Step 3: Create the weather fetch file

1. New Tab again → name it `WeatherAPI.ino`
2. Leave it empty for now — we'll fill it in Part 3.

### Step 4: Create the LED display file

1. New Tab again → name it `LEDMatrix.ino`
2. Leave it empty for now — we'll fill it in Part 4.

You should now have **4 tabs** in the IDE:
- `WeatherDashboard.ino` (main file)
- `Secrets.h`
- `WeatherAPI.ino`
- `LEDMatrix.ino`

---

## Part 2 — Connect to WiFi

Let's get the Arduino on the network first. Paste this into `WeatherDashboard.ino`:

```cpp
/*
  Weather Dashboard — Medina County Career Center
  Fetches weather from the National Weather Service API
  and displays it on the built-in LED matrix.

  No API key needed — NWS is free and open.
*/

#include <WiFiS3.h>
#include <ArduinoJson.h>
#include "ArduinoGraphics.h"
#include "Arduino_LED_Matrix.h"
#include "Secrets.h"

ArduinoLEDMatrix matrix;

// WiFi credentials (from Secrets.h)
const char* ssid = WIFI_SSID;
const char* pass = WIFI_PASS;

// NWS API settings — Akron-Canton Airport weather station
// To find your station: https://api.weather.gov/points/LAT,LON
// then look at the observationStations list
String station = "KCAK";          // ICAO station code
int br = 115200;                   // Baud rate
unsigned long fetchInterval = 300000;  // 5 minutes between fetches (in ms)

// Weather data
String weatherText = "Starting... ";
float tempF = 0.0;
String condition = "";
int humidity = 0;

unsigned long lastFetch = 0;

void setup() {
    Serial.begin(br);
    matrix.begin();

    // Connect to WiFi
    Serial.print("Connecting to WiFi");
    WiFi.begin(ssid, pass);

    while (WiFi.status() != WL_CONNECTED) {
        Serial.print(".");
        delay(500);
    }
    Serial.println();
    Serial.println("Connected!");
    Serial.print("IP: ");
    Serial.println(WiFi.localIP());

    showScrolling("WiFi OK ");

    // Fetch weather right away
    fetchWeather();
}

void loop() {
    unsigned long now = millis();

    if (now - lastFetch >= fetchInterval) {
        fetchWeather();
    }
    else {
        // Keep scrolling the last weather info
        showScrolling(weatherText);
    }

    delay(1000);
}
```

### Test WiFi First

Before we add the weather code, let's make sure WiFi works.

1. Add a temporary placeholder to `WeatherAPI.ino`:

```cpp
void fetchWeather() {
    Serial.println("(Weather fetch not implemented yet)");
    weatherText = "WiFi works! ";
    lastFetch = millis();
}
```

2. Add the LED function to `LEDMatrix.ino`:

```cpp
void showScrolling(const String& text) {
    matrix.beginDraw();
    matrix.textFont(Font_5x7);
    matrix.textScrollSpeed(75);
    matrix.beginText(0, 1, 0xFFFFFF);
    matrix.print(" ");
    matrix.print(text);
    matrix.print(" ");
    matrix.endText(SCROLL_LEFT);
    matrix.endDraw();
}
```

3. **Upload** and open the **Serial Monitor** (set to 115200 baud)

**What you should see:**
- Serial Monitor prints dots while connecting, then "Connected!" with an IP address
- The LED matrix scrolls "WiFi OK" then "WiFi works!"

**Troubleshooting:**
- If it keeps printing dots forever → double-check SSID and password in `Secrets.h`
- Make sure you're using the correct WiFi network
- The board must be within range of the WiFi

---

## Part 3 — Fetch Weather from the NWS API

Now for the real stuff. Replace the contents of `WeatherAPI.ino` with:

```cpp
/* ---- Weather fetch from api.weather.gov ---- */

#include <WiFiSSLClient.h>

WiFiSSLClient sslClient;

void fetchWeather() {
    Serial.println("Fetching weather...");

    // Connect to the NWS API (HTTPS on port 443)
    if (!sslClient.connect("api.weather.gov", 443)) {
        Serial.println("Connection failed!");
        return;
    }

    // Build the request URL
    String url = "/stations/" + station + "/observations/latest";

    // Send the HTTP GET request
    // NWS requires a User-Agent header with contact info
    sslClient.println("GET " + url + " HTTP/1.1");
    sslClient.println("Host: api.weather.gov");
    sslClient.println("User-Agent: MCCCWeatherDashboard (school@example.com)");
    sslClient.println("Accept: application/geo+json");
    sslClient.println("Connection: close");
    sslClient.println();

    // Wait for the response
    unsigned long timeout = millis();
    while (!sslClient.available()) {
        if (millis() - timeout > 10000) {
            Serial.println("Timeout waiting for response!");
            sslClient.stop();
            return;
        }
    }

    // Skip HTTP headers — look for the blank line
    bool headersEnded = false;
    while (sslClient.available()) {
        String line = sslClient.readStringUntil('\n');
        if (line == "\r") {
            headersEnded = true;
            break;
        }
    }

    if (!headersEnded) {
        Serial.println("Never found end of headers");
        sslClient.stop();
        return;
    }

    // Set up a JSON filter — only parse the fields we need
    // This saves a TON of memory (the full response is huge)
    JsonDocument filter;
    filter["properties"]["temperature"]["value"] = true;
    filter["properties"]["textDescription"] = true;
    filter["properties"]["relativeHumidity"]["value"] = true;

    // Parse the JSON with the filter
    JsonDocument doc;
    DeserializationError error = deserializeJson(
        doc, sslClient,
        DeserializationOption::Filter(filter)
    );

    sslClient.stop();

    if (error) {
        Serial.print("JSON parse error: ");
        Serial.println(error.c_str());
        return;
    }

    // Extract the data
    // NWS returns temperature in Celsius — convert to Fahrenheit
    float tempC = doc["properties"]["temperature"]["value"].as<float>();
    tempF = (tempC * 9.0 / 5.0) + 32.0;
    condition = doc["properties"]["textDescription"].as<String>();
    humidity = doc["properties"]["relativeHumidity"]["value"].as<int>();

    // Build the display string
    weatherText = String(int(tempF)) + "F " + condition + "  ";

    // Print to Serial Monitor too
    Serial.println("--- Weather Update ---");
    Serial.print("Temp: ");
    Serial.print(tempF, 1);
    Serial.println(" F");
    Serial.print("Condition: ");
    Serial.println(condition);
    Serial.print("Humidity: ");
    Serial.print(humidity);
    Serial.println("%");
    Serial.println("---------------------");

    lastFetch = millis();
}
```

### Upload and Test

1. Upload the code
2. Open the Serial Monitor (115200 baud)
3. Wait for WiFi to connect, then watch for the weather data

**What you should see in Serial Monitor:**
```
Connecting to WiFi....
Connected!
IP: 192.168.x.x
Fetching weather...
--- Weather Update ---
Temp: 45.2 F
Condition: Mostly Cloudy
Humidity: 72%
---------------------
```

**And on the LED matrix:** scrolling text like `45F Mostly Cloudy`

The weather refreshes every 5 minutes automatically.

---

## Part 4 — Understanding the Code

Let's break down what's happening:

### WiFi Connection
```cpp
WiFi.begin(ssid, pass);
while (WiFi.status() != WL_CONNECTED) { ... }
```
The board tries to join the WiFi network. The `while` loop waits until it connects.

### HTTPS Request
```cpp
sslClient.connect("api.weather.gov", 443);
sslClient.println("GET " + url + " HTTP/1.1");
```
We use `WiFiSSLClient` for a secure (HTTPS) connection on port 443. The NWS requires HTTPS. We send a standard HTTP GET request with headers.

### The NWS API Endpoint
```
https://api.weather.gov/stations/KCAK/observations/latest
```
This asks for the latest weather observation from the **Akron-Canton Airport** weather station. Every airport has a 4-letter ICAO code — KCAK is Akron-Canton.

### JSON Filtering
```cpp
JsonDocument filter;
filter["properties"]["temperature"]["value"] = true;
```
The NWS sends back a HUGE JSON response (thousands of characters). The Arduino doesn't have enough memory to parse all of it. The filter tells ArduinoJson to **only keep the fields we care about** and skip everything else.

### Temperature Conversion
```cpp
float tempC = doc["properties"]["temperature"]["value"].as<float>();
tempF = (tempC * 9.0 / 5.0) + 32.0;
```
The NWS returns temperature in Celsius. We convert to Fahrenheit because this is Ohio.

### LED Matrix Scrolling
```cpp
matrix.textScrollSpeed(75);    // milliseconds per pixel shift
matrix.endText(SCROLL_LEFT);   // scroll direction
```
The 12×8 LED matrix is tiny — it can only show a few characters at once. Scrolling lets us display a longer message.

---

## Part 5 — Quick Experiments

Try these small changes to explore:

**Change the scroll speed:**
In `LEDMatrix.ino`, try `matrix.textScrollSpeed(50)` for faster scrolling or `100` for slower.

**Show more info:**
Change the `weatherText` line in `WeatherAPI.ino` to include humidity:
```cpp
weatherText = String(int(tempF)) + "F " + String(humidity) + "% " + condition + "  ";
```

**Fetch more often (for testing):**
In `WeatherDashboard.ino`, temporarily change:
```cpp
unsigned long fetchInterval = 30000;  // 30 seconds (for testing only!)
```
**Change it back to 300000 when you're done testing** — don't hammer the NWS servers.

---

## Troubleshooting — If WiFi Isn't Working

If the WiFi network is down or having issues, you can still see the weather data through the **Serial Monitor only**. The code already prints everything to Serial — the LED matrix is just the visual bonus.

If WiFi connects but the API call fails:
- **"Connection failed!"** → The board reached WiFi but can't get to api.weather.gov. Could be a firewall or DNS issue on the network.
- **"Timeout waiting for response!"** → The request went out but no answer came back. Try again — sometimes the first attempt after power-on is slow.
- **"JSON parse error"** → The server responded but the data wasn't what we expected. Check the Serial Monitor for clues.
- **"Temperature shows nan"** → The weather station returned null for temperature (sensor issue at that station). Try a different station code.

**Quick test:** If you just want to verify your code compiles and the LED matrix works without WiFi, you can temporarily comment out the WiFi and fetch code in `setup()` and hardcode test data:

```cpp
// Quick test — paste this in setup() after matrix.begin()
// to test the LED without needing WiFi
weatherText = "TEST 72F Sunny  ";
showScrolling(weatherText);
```

---

## Completion Checklist

- [ ] Libraries installed (ArduinoJson, ArduinoGraphics)
- [ ] WiFi connects successfully — Serial Monitor shows IP address
- [ ] Weather data appears in Serial Monitor (temp, condition, humidity)
- [ ] LED matrix scrolls the temperature and condition
- [ ] Can explain: what is an API? What does the Arduino send and receive?
- [ ] Can explain: why do we use a JSON filter?

**Show your working dashboard to your instructor. Nice work — your Arduino is on the internet!**
