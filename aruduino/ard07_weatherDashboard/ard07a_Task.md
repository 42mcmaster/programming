# Lesson 07 Task: Multi-City Weather Tour

**Programming — Medina County Career Center**

---

## The Challenge

Your weather dashboard currently shows the weather for one station (KCAK — Akron-Canton). Your job is to modify it so it **cycles through multiple cities**, showing each city's code and weather before moving to the next one.

The LED matrix should scroll something like:

```
KCAK 47F Cloudy    KJFK 52F Sunny    KLAX 68F Clear
```

...then loop back to the first city and repeat.

---

## The Ground Rule

**You only need to edit ONE file: `WeatherAPI.ino`.**

Leave `WeatherDashboard.ino`, `LEDMatrix.ino`, and `Secrets.h` alone. Everything you need to add lives inside `WeatherAPI.ino`.

This works because `fetchWeather()` already uses a global `station` variable — all you have to do is change which station it points to before each fetch.

---

## Step 1 — Add a City List

At the top of `WeatherAPI.ino` (above `fetchWeather()`), add an array of stations and a counter:

```cpp
String cities[] = {"KCAK", "KJFK", "KLAX"};
int numCities = 3;
int currentCity = 0;   // which city we're on
```

Pick **at least 3** cities. You can use the table below or find your own.

### NWS Station Codes

| Code | Location |
|---|---|
| KCAK | Akron-Canton, OH |
| KCLE | Cleveland, OH |
| KCMH | Columbus, OH |
| KJFK | New York (JFK), NY |
| KLAX | Los Angeles, CA |
| KORD | Chicago (O'Hare), IL |
| KMIA | Miami, FL |
| KDEN | Denver, CO |
| KSEA | Seattle, WA |
| KDFW | Dallas/Fort Worth, TX |

More codes at [weather.gov](https://www.weather.gov).

---

## Step 2 — Point the Fetch at the Current City

At the very **top** of `fetchWeather()`, add one line that reassigns the existing `station` global:

```cpp
void fetchWeather() {
    station = cities[currentCity];   // <-- add this line

    Serial.println("Fetching weather...");
    // ...rest of the function stays exactly the same...
}
```

Now every time `fetchWeather()` is called, it will fetch whichever city `currentCity` is pointing to.

---

## Step 3 — Advance the Counter (Your Job to Fix This)

After a successful fetch, we need to move to the next city. Here's a **broken starter** — paste it at the **bottom** of `fetchWeather()`, right before `lastFetch = millis();`:

```cpp
// Move to the next city for next fetch
currentCity = currentCity + 1;
// 🤔 Problem: what happens when currentCity reaches numCities?
//    cities[3] doesn't exist. This will crash.
//    Fix it so the counter wraps back to 0.
```

**Your job:** fix this so `currentCity` cycles `0 → 1 → 2 → 0 → 1 → 2 → ...` forever instead of running off the end of the array.

### Hints

Two valid approaches — either one gets full credit:

- **Option A:** Use an `if` statement to reset the counter back to 0 when it's too big.
- **Option B:** Use the modulo (`%`) operator — the one-line trick from the slides. The traffic light example is the same shape as this problem.

If you're not sure what modulo is, there's a full reference in this folder called `modulo_explainer.md`.

---

## Step 4 — Include the Station Code in the Display

In `fetchWeather()`, find this line:

```cpp
weatherText = String(int(tempF)) + "F " + condition + "  ";
```

Change it so the station code shows up first:

```cpp
weatherText = station + " " + String(int(tempF)) + "F " + condition + "  ";
```

Now the LED will show `KJFK 52F Sunny` instead of just `52F Sunny`.

---

## Step 5 — Test It

Upload and watch the Serial Monitor. You should see:

```
Fetching weather...
--- Weather Update ---
Temp: 47.2 F
Condition: Cloudy
Humidity: 72%
---------------------
Fetching weather...
--- Weather Update ---
Temp: 52.4 F
Condition: Sunny
...
```

And the LED matrix should scroll the city code + weather, advancing to the next city each time a new fetch fires.

### Quick Tip — Faster Rotation for Testing

By default, `fetchInterval` is 5 minutes. That's a long wait to see the rotation work. For testing, temporarily change it in `WeatherDashboard.ino`:

```cpp
unsigned long fetchInterval = 30000;   // 30 seconds — TESTING ONLY
```

**Change it back to 300000 when you're done testing** — please don't hammer the NWS servers.

---

## Optional Challenges

If you finish early, try one of these:

### Challenge A — Temperature Comparison

Track every city's temperature as you fetch. After all cities have been visited, scroll a summary line:

```
Hottest: KMIA 82F  Coldest: KDEN 31F
```

### Challenge B — Weather Alerts

If any city comes back below freezing (32°F) or above 100°F, flash the LED matrix a few times before showing that city's weather as a visual alert.

### Challenge C — Detailed Serial Report

After all cities have been fetched, print a formatted table to the Serial Monitor:

```
=== Weather Report ===
KCAK   47F  Cloudy       72%
KJFK   52F  Sunny        45%
KLAX   68F  Clear        38%
======================
```

---

## Submission Checklist

- [ ] At least 3 cities in your array
- [ ] Only `WeatherAPI.ino` was modified
- [ ] Dashboard cycles through all cities and loops back to the first
- [ ] Station code appears before the weather on the LED matrix
- [ ] Serial Monitor shows each fetch and the data received
- [ ] Code compiles with no errors
- [ ] Can explain **why** your fix works (modulo OR if-statement — be able to describe it)

**Show your multi-city dashboard to your instructor!**
