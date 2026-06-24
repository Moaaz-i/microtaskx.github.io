# Architecture

MicroTaskX is split into two main modules:

## MTXKernel

- Responsible for task scheduling, priorities, timing, and CPU profiling.
- Implemented as a template class: `MicroTaskXKernel<MAX_TASKS>`.
- No dynamic memory allocation; all tasks are statically bounded.

## MTXUtils

- Standalone utility toolkit for:
  - Control systems (PID, hysteresis)
  - Signal processing (EMA, moving average, edge detection)
  - Data integrity (CRC8)
  - UI rendering (LCD differential updates, typewriter)
  - Hardware helpers (fast toggling, battery monitoring)

This separation keeps the scheduler lean and allows MTXUtils to evolve independently.
