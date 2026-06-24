# MicroTaskX — API Reference

This document provides a complete reference for all public APIs in MicroTaskX, including the Kernel, Macro Timers, MTXUtils, and data structures.

---

# 1) MTXKernel — Scheduling Core

## Creating the Kernel

```cpp
MicroTaskXKernel<MAX_TASKS> mtx;
```

### `addTask(function, interval, priority)`

Registers a recurring task.

```cpp
mtx.addTask(myTask, 500, MTX_HIGH);

```

**Parameters:**

- `function` — pointer to a void function
- `interval` — milliseconds
- `priority` — `MTX_LOW` / `MTX_MEDIUM` / `MTX_HIGH`

---

### `addOneShotTask(function, delay, priority)`

Schedules a task that runs once and then disables itself.

```cpp
mtx.addOneShotTask(alertTask, 5000, MTX_HIGH);

```

---

### `pauseTask(function)`

Temporarily disables a task.

```cpp
mtx.pauseTask(readSensorTask);

```

---

### `resumeTask(function)`

Re-enables a paused task.

```cpp
mtx.resumeTask(readSensorTask);

```

---

### `setInterval(function, newInterval)`

Changes the execution interval at runtime.

```cpp
mtx.setInterval(readSensorTask, 100);

```

---

### `getCPUUsage()`

Returns the real-time CPU load percentage.

```cpp
int load = mtx.getCPUUsage();

```

---

### `enableSmartSleep(bool)`

Enables low-power sleep modes:

- **AVR** → Idle Sleep
- **ESP32** → Light Sleep

```cpp
mtx.enableSmartSleep(true);

```

---

# 2) Macro Timers — Non-Blocking Inline Timers

### `MTX_EVERY_MS(ms)`

Executes a block every X milliseconds.

```cpp
MTX_EVERY_MS(1000) {
  Serial.println("1 second passed");
}

```

---

### `MTX_EVERY_HZ(hz)`

Executes a block at a given frequency.

```cpp
MTX_EVERY_HZ(2) {
  // Runs twice per second
}

```

---

### `MTX_EVERY(interval)`

General-purpose interval timer.

```cpp
MTX_EVERY(15000) {
  Serial.println("15 seconds passed");
}

```

---

# 3) MTXUtils — Advanced Utility Toolkit

## 3.1 Control Systems

### `computePID(setpoint, measurement, MTXPID, dt)`

PID controller with anti-windup.

```cpp
float output = MTXUtils::computePID(100.0, currentSpeed, speedPID, 0.01);

```

---

### `applyHysteresis(value, threshold, gap)`

Prevents rapid switching near threshold boundaries.

```cpp
bool state = MTXUtils::applyHysteresis(temp, 40, 2);

```

---

## 3.2 Signal Processing

### `smoothReadFast(pin, historyRef)`

EMA filter without cross-talk.

```cpp
int filtered = MTXUtils::smoothReadFast(A0, sensorHistory);

```

---

### `movingAverage(buffer, size, newValue)`

Sliding-window average filter.

```cpp
int avg = MTXUtils::movingAverage(buffer, 10, newSample);

```

---

### `isRisingEdge(current, previous)` / `isFallingEdge(current, previous)`

```cpp
if (MTXUtils::isRisingEdge(btn, lastBtn)) { ... }

```

---

## 3.3 Data Integrity

### `computeCRC8(buffer, length)`

Computes CRC8 checksum.

```cpp
uint8_t crc = MTXUtils::computeCRC8(data, len);

```

---

### `calculateBatteryPercentage(voltage, minV, maxV)`

Maps voltage to battery percentage.

```cpp
int percent = MTXUtils::calculateBatteryPercentage(v, 3.0, 4.2);

```

---

## 3.4 Display Engine

### `updateScreenSmart<COLS, ROWS>(lcd, currentFrame, memoryFrame)`

Differential LCD update with zero flicker.

```cpp
MTXUtils::updateScreenSmart<16, 2>(lcd, currentFrame, memoryFrame);

```

---

### `printTypewriter(lcd, text, speed)`

Non-blocking typewriter animation.

```cpp
MTXUtils::printTypewriter(lcd, "Hello!", 50);

```

---

### `getCenterOffset(textLength, displayWidth)`

Returns the offset needed to center text.

---

### `getProgressBarString(width, percent, outBuffer)`

Generates a text-based progress bar.

```cpp
MTXUtils::getProgressBarString(16, 75, buffer);

```

---

## 3.5 Hardware Utilities

### `toggleFast<PIN>()`

Ultra-fast direct port toggle.

```cpp
MTXUtils::toggleFast<13>();

```

---

### `isButtonPressed(pin)`

Debounced button input.

```cpp
if (MTXUtils::isButtonPressed(2)) { ... }

```

---

# 4) Data Structures

### `MTXPID`

```cpp
struct MTXPID {
  float Kp, Ki, Kd;
  float integral;
  float previousError;
  float outputMin;
  float outputMax;
};

```

---

# 5) Macros

- `MTX_START`
- `MTX_RUN`
- `MTX_END`

These macros wrap the program structure cleanly.

---

# 6) Compatibility

Supported architectures (All Arduino-supported architectures):

- AVR
- SAMD
- ESP32
- ESP8266
