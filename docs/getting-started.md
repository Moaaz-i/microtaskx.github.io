# Getting Started with MicroTaskX

MicroTaskX is an ultra-lightweight micro-RTOS and multitasking framework for Arduino and embedded boards.

## Installation

- Search for **MicroTaskX** in the Arduino Library Manager
- Or clone the GitHub repository:

```cpp
#include <MicroTaskX.h>
```

Basic Setup

```cpp
#include <MicroTaskX.h>

void blinkTask() {
  MTXUtils::toggleFast<LED_BUILTIN>();
}

MTX_START()
  mtx.addTask(blinkTask, 500, MTX_HIGH);
  mtx.enableSmartSleep(true);
MTX_RUN()
MTX_END
```
