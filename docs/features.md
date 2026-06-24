# MicroTaskX Features

## Kernel & Scheduling

- Template-based scheduler: `MicroTaskXKernel<MAX_TASKS>`
- Priority levels: `MTX_LOW`, `MTX_MEDIUM`, `MTX_HIGH`
- One-shot tasks: `addOneShotTask`
- Dynamic control: `pauseTask`, `resumeTask`, `setInterval`

## Power & Performance

- Smart Sleep: AVR Idle Sleep, ESP32 Light Sleep
- Real-time CPU usage: `getCPUUsage`
- Idle-window calibration for deterministic profiling

## Macro Timers

- `MTX_EVERY_MS(ms)`
- `MTX_EVERY_HZ(hz)`
- `MTX_EVERY(interval)`

## MTXUtils Toolkit

- Anti-windup PID: `computePID`
- Hysteresis: `applyHysteresis`
- Moving average: `movingAverage`
- Circular queue: `MTXCircularQueue`
- Edge detection: `isRisingEdge`, `isFallingEdge`
- CRC8: `computeCRC8`
- Battery percentage: `calculateBatteryPercentage`
- Flicker-free LCD: `updateScreenSmart`
- Typewriter effect: `printTypewriter`
