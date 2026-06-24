# Examples

## 1. Multitasking with Smart Sleep

```cpp
#include <MicroTaskX.h>

void sensorTask() { /* ... */ }
void logTask()    { /* ... */ }

MTX_START()
  mtx.addTask(sensorTask, 200, MTX_HIGH);
  mtx.addTask(logTask,    1000, MTX_LOW);
  mtx.enableSmartSleep(true);
MTX_RUN()
MTX_END
```

## 2. Flicker-Free LCD UI

```cpp
#include <MicroTaskX.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);
char currentFrame[2][17];
char memoryFrame[2][17];
MTXPID speedPID = { 2.5, 0.5, 0.1, 0, 0, 0, 255 };

void loop() {
  float motorPWM = MTXUtils::computePID(100.0, readEncoder(), speedPID, 0.01);
  sprintf(currentFrame[0], "PWM Out: %03d    ", (int)motorPWM);
  MTXUtils::getProgressBarString(16, (motorPWM/255)*100, currentFrame[1]);
  MTXUtils::updateScreenSmart<16, 2>(lcd, currentFrame, memoryFrame);
}
```
