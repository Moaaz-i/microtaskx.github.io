# MicroTaskX — Changelog

This document provides a complete historical record of all major updates to the MicroTaskX framework, from the early UMOZ versions to the latest releases.

---

## v3.1.1 — Metadata Update (2026)

**Type:** Documentation-only release
**Code Changes:** None

### Updates

- Updated `library.properties` and `library.json` descriptions to fully reflect all features introduced in v3.1.0.
- Expanded keyword list for better discoverability on Arduino Registry and PlatformIO:
  - kalman-filter, software-pwm, rotary-encoder, watchdog
  - isr-queuing, coroutines, mutexes, signals
  - crc8, battery-monitor
- Fixed README formatting issues.

---

## v3.1.0 — Advanced Control Utilities & Flicker-Free Display Engine

**Type:** Major feature release

### MTXUtils Enhancements

- **Anti-Windup PID Controller**
- **Hysteresis Logic** for relay protection
- **Moving Average Filter**
- **Circular Queue (Ring Buffer)**
- **Edge Detection (Rising/Falling)**
- **CRC8 Checksum**
- **Battery Percentage Calculator**
- **Time Formatters (HH:MM:SS)**

### Display Engine

- **updateScreenSmart** — differential LCD updates with zero flicker
- **printTypewriter** — non-blocking typewriter animation
- **getCenterOffset** — automatic text centering
- **getProgressBarString** — text-based progress bar generator

---

## v3.0.0 — Modular Architecture & Kernel Rewrite

**Type:** Architectural overhaul

### Core Changes

- Full separation between:
  - **MTXKernel** (scheduler)
  - **MTXUtils** (utility toolkit)
- Kernel rewritten as a **template class**:
  ```cpp
  MicroTaskXKernel<MAX_TASKS>
  ```
