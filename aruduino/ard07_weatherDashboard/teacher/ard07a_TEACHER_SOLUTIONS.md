# Lesson 07 Task — Teacher Solutions

**Multi-City Weather Tour**

---

## Main Task Solution — Multi-City Weather Display

The key changes from the walkthrough code:

### WeatherDashboard.ino (modified)

```cpp
/*
  Weather Dashboard — Multi-City Version
  Cycles through multiple NWS stations
*/

#include <WiFiS3.h>
#include <ArduinoJson.h>
#include "ArduinoGraphics.h"
#include "Arduino_LED_Matrix.h"
#include "Secrets.h"

ArduinoLEDMatrix matrix;

const char* ssid = WIFI_SSID;
const char* pass = WIFI_PASS;

// City list — students pick at least 3
String cities[] = {"KCAK", "KJFK", "KLAX"};
int numCities = 3;
int currentCity = 0;

int br = 115200;
unsigned long fetchInterval = 60000;  // 1 minute between city switches

// Weather data for current city
String weatherText = "Starting... ";
float tempF = 0.0;
String condition = "";
int humidity = 0;

unsigned long lastFetch = 0;

void setup() {
    Serial.begin(br);
    matrix.begin();

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

    // Fetch the first city
    fetchWeather(cities[currentCity]);
}

void loop() {
    unsigned long now = millis();

    if (now - lastFetch >= fetchInterval) {
        // Move to next city
        currentCity = (currentCity + 1) % numCities;
        fetchWeather(cities[currentCity]);
    }
    else {
        showScrolling(weatherText);
    }

    delay(1000);
}
```

### WeatherAPI.ino (modified to accept station parameter)

```cpp
/* ---- Weather fetch from api.weather.gov ---- */

#include <WiFiSSLClient.h>

WiFiSSLClient sslClient;

void fetchWeather(String station) {
    Serial.print("Fetching weather for: ");
    Serial.println(station);

    if (!sslClient.connect("api.weather.gov", 443)) {
        Serial.println("Connection failed!");
        return;
    }

    String url = "/stations/" + station + "/observations/latest";

    sslClient.println("GET " + url + " HTTP/1.1");
    sslClient.println("Host: api.weather.gov");
    sslClient.println("User-Agent: MCCCWeatherDashboard (school@example.com)");
    sslClient.println("Accept: application/geo+json");
    sslClient.println("Connection: close");
    sslClient.println();

    unsigned long timeout = millis();
    while (!sslClient.available()) {
        if (millis() - timeout > 10000) {
            Serial.println("Timeout!");
            sslClient.stop();
            return;
        }
    }

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

    JsonDocument filter;
    filter["properties"]["temperature"]["value"] = true;
    filter["properties"]["textDescription"] = true;
    filter["properties"]["relativeHumidity"]["value"] = true;

    JsonDocument doc;
    DeserializationError error = deserializeJson(
        doc, sslClient,
        DeserializationOption::Filter(filter)
    );

    sslClient.stop();

    if (error) {
        Serial.print("JSON error: ");
        Serial.println(error.c_str());
        weatherText = station + " Error  ";
        lastFetch = millis();
        return;
    }

    float tempC = doc["properties"]["temperature"]["value"].as<float>();
    tempF = (tempC * 9.0 / 5.0) + 32.0;
    condition = doc["properties"]["textDescription"].as<String>();
    humidity = doc["properties"]["relativeHumidity"]["value"].as<int>();

    // Include station code in the display
    weatherText = station + " " + String(int(tempF)) + "F " + condition + "  ";

    Serial.println("--- " + station + " ---");
    Serial.print("Temp: ");
    Serial.print(tempF, 1);
    Serial.println(" F");
    Serial.print("Condition: ");
    Serial.println(condition);
    Serial.print("Humidity: ");
    Serial.print(humidity);
    Serial.println("%");

    lastFetch = millis();
}
```

### LEDMatrix.ino (unchanged from walkthrough)

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

### Key Differences from Walkthrough

1. `station` changed from a single `String` to an array `cities[]`
2. `fetchWeather()` now takes a `String station` parameter instead of using a global
3. `loop()` increments `currentCity` using modulo to wrap around
4. `weatherText` includes the station code prefix
5. Added error handling that shows the station code + "Error" on the LED if a fetch fails

---

## Challenge A Solution — Temperature Comparison

Add these globals to `WeatherDashboard.ino`:

```cpp
// Temperature tracking
float allTemps[10];        // Store temps (max 10 cities)
String allCodes[10];       // Store codes
int fetchedCount = 0;
```

At the end of a successful fetch in `WeatherAPI.ino`, add:

```cpp
allTemps[fetchedCount] = tempF;
allCodes[fetchedCount] = station;
fetchedCount++;

// After all cities fetched, show comparison
if (fetchedCount >= numCities) {
    float hottest = allTemps[0];
    float coldest = allTemps[0];
    String hotCode = allCodes[0];
    String coldCode = allCodes[0];

    for (int i = 1; i < numCities; i++) {
        if (allTemps[i] > hottest) {
            hottest = allTemps[i];
            hotCode = allCodes[i];
        }
        if (allTemps[i] < coldest) {
            coldest = allTemps[i];
            coldCode = allCodes[i];
        }
    }

    String summary = "Hot:" + hotCode + " " + String(int(hottest)) + "F  Cold:" + coldCode + " " + String(int(coldest)) + "F  ";
    showScrolling(summary);

    fetchedCount = 0;  // Reset for next round
}
```

---

## Challenge B Solution — Weather Alerts

Add a flash function to `LEDMatrix.ino`:

```cpp
void flashMatrix(int times) {
    for (int i = 0; i < times; i++) {
        // All LEDs on
        matrix.beginDraw();
        matrix.textFont(Font_5x7);
        matrix.beginText(0, 1, 0xFFFFFF);
        matrix.print("!!!");
        matrix.endText();
        matrix.endDraw();
        delay(200);

        // All LEDs off
        matrix.beginDraw();
        matrix.endDraw();
        delay(200);
    }
}
```

Then in `WeatherAPI.ino`, after calculating tempF:

```cpp
if (tempF < 32.0 || tempF > 100.0) {
    flashMatrix(3);
}
```

---

## Challenge C Solution — Formatted Table

Add to `WeatherDashboard.ino`:

```cpp
// Storage for all cities
String allResults[10];
int resultCount = 0;
```

At the end of a successful fetch in `WeatherAPI.ino`:

```cpp
// Store formatted result
allResults[resultCount] = station;
// Pad to 6 chars
while (allResults[resultCount].length() < 6) allResults[resultCount] += " ";
allResults[resultCount] += String(int(tempF)) + "F  " + condition;
resultCount++;

// Print table after all cities
if (resultCount >= numCities) {
    Serial.println();
    Serial.println("=== Weather Report ===");
    for (int i = 0; i < numCities; i++) {
        Serial.println(allResults[i]);
    }
    Serial.println("======================");
    Serial.println();
    resultCount = 0;
}
```

---

## Grading Notes

### Full credit requires:
- At least 3 cities in the array
- Code compiles and runs
- LED matrix displays station code + weather for each city
- Cities cycle and loop back to the beginning
- Serial Monitor shows fetch activity

### Common issues:
- **Students forget to change `fetchWeather()` signature** — the walkthrough version has no parameter, so they need to add `String station`
- **Off-by-one on modulo** — make sure `numCities` matches the actual array length
- **Timeout on some stations** — occasionally a station may not respond. The timeout handler should prevent a hang, but students might think their code is broken
- **Temperature showing as nan** — the NWS occasionally returns `null` for temperature if the station has a sensor issue. Advanced students can add a null check; for others, just try a different station
- **WiFi drops mid-fetch** — the Jetpack might lose signal briefly. The connection failure check at the top of `fetchWeather()` handles this gracefully

### Extra credit:
- Any of the three challenges completed and working
- Student added additional cities beyond the minimum 3
- Student found their own station codes
- Clean, well-commented code
