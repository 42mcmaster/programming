---
marp: true
theme: default
paginate: true
---

# Lesson 07: WiFi Weather Dashboard

**Programming — Medina County Career Center**

---

## What We're Building

A live weather dashboard that:
- Connects to WiFi
- Fetches real weather data from the **National Weather Service**
- Displays temperature and conditions on the **LED matrix**

No extra hardware — just the Arduino Uno R4 WiFi board and a USB cable.

---

## The Big Picture

```
Arduino  ──WiFi──►  Internet  ──►  api.weather.gov
                                        │
                                   JSON response
                                        │
Arduino  ◄──────────────────────────────┘
   │
   ├── Serial Monitor (text)
   └── LED Matrix (scrolling display)
```

The Arduino acts as a **client** — it asks a server for data and displays the result.

---

## What Is an API?

**API** = Application Programming Interface

It's a way for programs to talk to each other. Instead of visiting weather.gov in a browser, our Arduino sends a request directly to their data server and gets back **structured data** (JSON) instead of a web page.

The NWS API is:
- **Free** — no cost, no account needed
- **No API key** — just a User-Agent header
- **US weather only** — covers all 50 states

---

## How HTTP Requests Work

When your Arduino fetches weather, it sends something like this:

```
GET /stations/KCAK/observations/latest HTTP/1.1
Host: api.weather.gov
User-Agent: MCCCWeatherDashboard
```

The server responds with:
- **HTTP headers** (status code, content type, etc.)
- **A blank line** (separates headers from data)
- **JSON data** (the actual weather information)

---

## What Is JSON?

**JSON** = JavaScript Object Notation

It's a way to structure data as text. The NWS response looks something like this (simplified):

```json
{
  "properties": {
    "temperature": {
      "value": 8.3,
      "unitCode": "wmo:degC"
    },
    "textDescription": "Mostly Cloudy",
    "relativeHumidity": {
      "value": 72.5
    }
  }
}
```

Data is organized in **key-value pairs** inside curly braces. Values can be numbers, strings, or nested objects.

---

## JSON Filtering — Why It Matters

The actual NWS response is **thousands of characters** — way more than the Arduino's memory can handle.

**ArduinoJson's filter feature** lets us say: "Only keep these specific fields, skip everything else."

```cpp
JsonDocument filter;
filter["properties"]["temperature"]["value"] = true;
filter["properties"]["textDescription"] = true;
```

This shrinks the parsed data from thousands of bytes to just the few numbers we need.

---

## HTTPS and SSL

The NWS API requires **HTTPS** (secure HTTP). That means:
- The connection is **encrypted**
- We use port **443** instead of port 80
- We need `WiFiSSLClient` instead of regular `WiFiClient`

The Arduino Uno R4 WiFi handles SSL encryption in hardware — we just swap the client type and it works.

---

## NWS Weather Stations

The NWS has weather stations at airports across the country. Each has a 4-letter **ICAO code**:

| Code | Location |
|---|---|
| KCAK | Akron-Canton, OH |
| KCLE | Cleveland, OH |
| KJFK | New York (JFK) |
| KLAX | Los Angeles, CA |
| KORD | Chicago O'Hare |

The API endpoint is: `api.weather.gov/stations/CODE/observations/latest`

---

## The LED Matrix

The Arduino Uno R4 WiFi has a built-in **12×8 LED matrix** on the top of the board.

- It can display text using the ArduinoGraphics library
- Only a few characters fit at once, so we **scroll** the text
- `textScrollSpeed(75)` controls how fast it moves (milliseconds per pixel)
- `SCROLL_LEFT` makes text flow from right to left

---

## Temperature Conversion

The NWS returns temperature in **Celsius**. To convert to Fahrenheit:

```
°F = (°C × 9 / 5) + 32
```

In Arduino code:
```cpp
float tempC = doc["properties"]["temperature"]["value"].as<float>();
float tempF = (tempC * 9.0 / 5.0) + 32.0;
```

**Why 9.0 and 5.0 instead of 9 and 5?** Same reason as the potentiometer lesson — integer division in C would truncate the result. Using floats gives us the decimal precision we need.

---

## The Secrets File

WiFi passwords don't belong in your main code. We put them in a separate file:

```cpp
// Secrets.h
#define WIFI_SSID "YourNetwork"
#define WIFI_PASS "YourPassword"
```

This is a real-world practice — keeping credentials separate so you don't accidentally share them. Professional developers use the same concept with `.env` files.

---

## Recap

- **API**: a way for programs to request data from servers
- **JSON**: structured text format for data (key-value pairs)
- **HTTPS**: encrypted web connection (port 443, WiFiSSLClient)
- **NWS API**: free US weather data, no key needed
- **JSON Filter**: parse only the fields you need to save memory
- **LED Matrix**: built-in 12×8 display on the R4 WiFi board
- **Secrets.h**: keep passwords out of your main code
