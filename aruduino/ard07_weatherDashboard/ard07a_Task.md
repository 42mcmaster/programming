# Lesson 07 Task: Multi-City Weather Tour

**Programming — Medina County Career Center**

---

## The Challenge

Your weather dashboard currently shows the weather for one station (KCAK — Akron-Canton). Your job is to modify it so it **cycles through multiple cities**, showing each city's name and weather before moving to the next one.

The LED matrix should scroll something like:

```
KCAK 47F Cloudy    KJFK 52F Sunny    KLAX 68F Clear
```

...then loop back to the first city and repeat.

---

## What You Need to Know

### NWS Station Codes

Every airport weather station has a 4-letter ICAO code starting with K (for US stations). The NWS API uses these codes. Here are some to choose from:

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

You can find more station codes at: https://www.weather.gov

### Arrays in Arduino

To store a list of cities, you'll use an **array** — a variable that holds multiple values:

```cpp
String cities[] = {"KCAK", "KJFK", "KLAX"};
int numCities = 3;
int currentCity = 0;    // Index — which city we're on
```

To get the current city: `cities[currentCity]`

To move to the next city (looping back to 0 at the end):
```cpp
currentCity = (currentCity + 1) % numCities;
```

The `%` (modulo) operator wraps the count back to 0. If `numCities` is 3, the sequence goes: 0, 1, 2, 0, 1, 2, 0, ...

---

## Your Task

### Requirements

1. Pick **at least 3 US cities** from the table above (or find your own)
2. Store them in an array at the top of your code
3. Modify `fetchWeather()` so it accepts a station code as input (or reads from the array)
4. After displaying one city's weather, move to the next city
5. The LED matrix should show the **station code** followed by the **temperature and condition** for each city
6. After the last city, loop back to the first

### Display Format

For each city, the LED should scroll:
```
CODE TEMP CONDITION
```
For example: `KJFK 52F Sunny`

The Serial Monitor should also print which city is being fetched and the data received.

### Hints

- You'll need to change the `station` variable from a single `String` to an array of `String`s
- The `fetchWeather()` function currently uses the global `station` variable — you could either change that global before calling `fetchWeather()`, or modify the function to take a parameter
- Make sure you update `lastFetch` properly so each city gets its turn
- Think about timing — you probably want each city to display for a reasonable amount of time before switching

---

## Optional Challenges

If you finish early, try one of these:

### Challenge A — Add a Temperature Comparison
After cycling through all cities, display a summary line:
```
Hottest: KMIA 82F  Coldest: KDEN 31F
```
You'll need to track the min and max temperatures as you fetch each city.

### Challenge B — Weather Alerts
Check if any city is below freezing (32°F) or above 100°F. If so, flash the LED matrix on and off a few times before showing that city's weather, as a visual alert.

### Challenge C — Detailed Serial Log
Print a formatted table to the Serial Monitor after all cities have been fetched:
```
=== Weather Report ===
KCAK  Akron-Canton    47F  Cloudy       72%
KJFK  New York        52F  Sunny        45%
KLAX  Los Angeles     68F  Clear        38%
======================
```
You'll need to store results for all cities and print them together.

---

## Submission Checklist

- [ ] At least 3 cities in your array
- [ ] Dashboard cycles through all cities, displaying each on the LED matrix
- [ ] Station code is visible before each city's weather
- [ ] Serial Monitor shows each fetch and the data received
- [ ] Code compiles with no errors
- [ ] Dashboard loops back to the first city after showing the last one

**Show your multi-city dashboard to your instructor!**
