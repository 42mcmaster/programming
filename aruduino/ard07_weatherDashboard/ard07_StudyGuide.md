# Lesson 07 Study Guide: WiFi Weather Dashboard

**Programming — Medina County Career Center**

---

## 1. WiFi on the Arduino Uno R4 WiFi

The Uno R4 WiFi has a built-in WiFi module (ESP32-S3). The `WiFiS3` library handles the connection.

### Connecting

```cpp
#include <WiFiS3.h>

WiFi.begin(ssid, pass);           // Start connecting
WiFi.status()                     // Returns connection state
WiFi.localIP()                    // Returns the assigned IP address
```

`WiFi.status()` returns `WL_CONNECTED` when the board has joined the network. The typical pattern is to call `WiFi.begin()` once, then loop until the status changes.

### Common WiFi Issues

**Won't connect at all:** Double-check SSID and password (case-sensitive). Make sure the network is 2.4GHz — the Uno R4 WiFi doesn't support 5GHz networks.

**Connects then drops:** Could be signal strength, or the network might have a captive portal (a login page). The Arduino can't interact with captive portals — you need a network that connects directly.

---

## 2. HTTP Requests

HTTP (Hypertext Transfer Protocol) is how web browsers and programs talk to servers. An HTTP request has three parts: the **method** (GET, POST, etc.), the **URL path**, and **headers**.

### GET Request Format

```
GET /stations/KCAK/observations/latest HTTP/1.1
Host: api.weather.gov
User-Agent: MCCCWeatherDashboard (school@example.com)
Accept: application/geo+json
Connection: close
```

**GET** means "give me data." The path after GET tells the server what data you want. Headers provide additional info — the NWS requires a `User-Agent` header that identifies your program.

### HTTPS

HTTPS adds encryption (SSL/TLS) to HTTP. The NWS API requires it. On the Arduino:
- Use `WiFiSSLClient` instead of `WiFiClient`
- Connect to port **443** instead of port 80
- The ESP32-S3 chip handles encryption automatically

---

## 3. The NWS API

The National Weather Service provides a free, open API at `api.weather.gov`. No account, no API key, no cost.

### Key Endpoints

**Get the nearest stations for a location:**
```
https://api.weather.gov/points/41.13,-81.86
```
Returns a list of nearby observation stations, sorted by distance.

**Get the latest observation from a station:**
```
https://api.weather.gov/stations/KCAK/observations/latest
```
Returns current temperature, conditions, humidity, wind, and more.

### Station Codes

NWS stations use **ICAO codes** — 4-letter identifiers used internationally for airports. US codes start with K.

| Code | Airport | City |
|---|---|---|
| KCAK | Akron-Canton | Akron, OH |
| KCLE | Hopkins Intl | Cleveland, OH |
| KCMH | John Glenn | Columbus, OH |
| KJFK | JFK Intl | New York, NY |
| KLAX | LAX | Los Angeles, CA |
| KORD | O'Hare Intl | Chicago, IL |

### User-Agent Requirement

The NWS asks that every request include a `User-Agent` header with a name and contact info. This isn't authentication — it's so they can contact you if your program is causing problems.

```cpp
sslClient.println("User-Agent: MCCCWeatherDashboard (school@example.com)");
```

---

## 4. JSON (JavaScript Object Notation)

JSON is a text format for structured data. It's the standard way APIs send data over the internet.

### Structure

```json
{
    "name": "Akron",
    "temperature": 47.5,
    "sunny": false,
    "tags": ["Ohio", "weather"]
}
```

**Objects** use `{ }` and contain key-value pairs. **Arrays** use `[ ]` and contain lists of values. Values can be strings (in quotes), numbers, booleans (`true`/`false`), `null`, or nested objects/arrays.

### Nested Objects

The NWS response nests data several levels deep:

```json
{
    "properties": {
        "temperature": {
            "value": 8.3,
            "unitCode": "wmo:degC"
        }
    }
}
```

To get the temperature: `doc["properties"]["temperature"]["value"]`

Each `[ ]` digs one level deeper into the structure.

---

## 5. ArduinoJson Library

ArduinoJson is a library for parsing (reading) and building JSON on Arduino.

### Basic Parsing

```cpp
JsonDocument doc;
deserializeJson(doc, jsonString);
float temp = doc["properties"]["temperature"]["value"].as<float>();
```

`deserializeJson()` reads JSON text and fills a `JsonDocument`. Then you access values using the key names, chained with `[ ]` for nested objects.

### The `.as<type>()` Method

ArduinoJson doesn't know what type you want, so you tell it:
- `.as<float>()` — decimal number
- `.as<int>()` — whole number
- `.as<String>()` — text

### JSON Filtering

The NWS response is huge — too big for the Arduino's RAM. ArduinoJson can filter during parsing:

```cpp
JsonDocument filter;
filter["properties"]["temperature"]["value"] = true;
filter["properties"]["textDescription"] = true;

JsonDocument doc;
deserializeJson(doc, input, DeserializationOption::Filter(filter));
```

Setting a field to `true` in the filter means "keep this." Everything else gets skipped, saving memory.

---

## 6. The LED Matrix

The Uno R4 WiFi has a 12×8 LED matrix built into the top of the board. The `Arduino_LED_Matrix` and `ArduinoGraphics` libraries control it.

### Scrolling Text

```cpp
matrix.beginDraw();
matrix.textFont(Font_5x7);
matrix.textScrollSpeed(75);           // ms per pixel shift
matrix.beginText(0, 1, 0xFFFFFF);     // x, y, color
matrix.print("Hello!");
matrix.endText(SCROLL_LEFT);
matrix.endDraw();
```

The matrix is only 12 pixels wide, so most messages need to scroll. `textScrollSpeed` controls the speed — lower numbers = faster scrolling. `SCROLL_LEFT` makes text flow right to left, like a news ticker.

---

## 7. Timing Without Blocking

The dashboard uses `millis()` for timing instead of a long `delay()`:

```cpp
unsigned long lastFetch = 0;
unsigned long fetchInterval = 300000;   // 5 minutes

void loop() {
    if (millis() - lastFetch >= fetchInterval) {
        fetchWeather();
    }
}
```

`millis()` returns the number of milliseconds since the board powered on. By comparing the current time to the last fetch time, the code checks if enough time has passed without freezing the whole program.

This is better than `delay(300000)` because the board can keep scrolling text on the LED matrix while waiting for the next fetch.

---

## 8. Separating Credentials — Secrets.h

Passwords and keys should never be in your main code file:

```cpp
// Secrets.h
#pragma once
#define WIFI_SSID "NetworkName"
#define WIFI_PASS "Password123"
```

```cpp
// Main .ino file
#include "Secrets.h"
const char* ssid = WIFI_SSID;
```

`#define` creates a text replacement — the compiler swaps `WIFI_SSID` for `"NetworkName"` before compiling. `#pragma once` prevents the file from being included twice.

In professional software, credentials go in `.env` files, environment variables, or secret managers — never committed to version control. `Secrets.h` is the Arduino equivalent.

---

## Vocabulary

**API (Application Programming Interface)** — A set of rules for how programs request and exchange data with a server.

**HTTP/HTTPS** — The protocol web browsers and APIs use to communicate. HTTPS adds encryption.

**SSL/TLS** — The encryption layer that makes HTTPS secure. The Arduino handles this in hardware.

**JSON** — A text-based data format using key-value pairs in curly braces. The standard for web APIs.

**ICAO Code** — A 4-letter airport identifier used internationally. US codes start with K (e.g., KCAK).

**Endpoint** — A specific URL on an API server that provides particular data (e.g., `/stations/KCAK/observations/latest`).

**User-Agent** — An HTTP header that tells the server what program is making the request.

**LED Matrix** — A grid of LEDs that can display patterns and scrolling text. The Uno R4 WiFi has a 12×8 matrix built in.

**millis()** — Arduino function that returns milliseconds since power-on. Used for non-blocking timing.

**JsonDocument** — The ArduinoJson container that holds parsed JSON data in memory.

---

## Standards Alignment

- **5.1.1** — Variables and data types (String arrays, float, int, unsigned long)
- **5.1.3** — Conditional logic (WiFi status check, timeout handling)
- **5.1.4** — Loops (while for WiFi connection, cycling through cities)
- **5.2.3** — Arithmetic operations (temperature conversion)
- **5.3.2** — Networking concepts (HTTP, HTTPS, client-server)
- **5.4.1** — Data formats (JSON parsing and filtering)
