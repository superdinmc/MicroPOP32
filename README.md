# MicroPOP32

Fast, efficient and minimal POP32 library for Line Follower robot.

## Installation

This library is mainly developed on PlatformIO, There might be issues with using it on Arduino IDE.
Same as POP32, Board must be selected to STM32F103CBT6 if you're using PlatformIO, or POP32 on Arduino IDE.

## Usage

### Options

``` cpp
// Enable motor expansion
// m(int id, int power) is included
// Full 4 motors can be used(Default 2)
#define EXTRA_MOTORS
// Disable motor module entirely, saves about 10Kb of flash
#define NO_MOTOR
// Disable detection of OLED_I2C_SSD1309 and proceed without OLED
#define NO_OLED
// Disable the use of extra buttons macro
// Slightly speed up compile time(<1ms), doesn't affect flash size
#define NO_EXTRA_BUTTONS
// Include MUST BE AFTER options define
#include <MicroPOP32.cpp>
```

### Functions

* `m(int id: 1 - 4, int pow: -100 - 100): void`
    * Set individual motor's speed.
    * Requires `EXTRA_MOTORS`.
* `motor(int powl: -100 - 100, int powr: -100 - 100): void`
    * Set motor 1 & 2's speed, recommended for robots.
    * Will be disabled if `NO_MOTOR` is set.
* `OLED_I2C_SSD1309 oled`
    * Pre-initialized OLED Class.
    * Will be disabled if `NO_OLED` is set or OLED\_I2C\_SSD1309 is not found.
* `beep(int time = 100): void`
    * Turn on the buzzer for `time` ms.
    * Defaults to 100ms.
* `OK(): void`
    * Wait until OK button is pressed.
    * Can be falsy when used too early on startup.
* `EXTRA_ALIASES` expansion
    * Creates a short alias for few commonly used functions
    * Doesn't affect flash size
    * `a` = `analogRead`
    * `d` = `digitalRead`
    * `p` = `pinMode`
    * `o` = `digitalWrite`
    * `b` = `beep`
* `EXTRA_BUTTONS` expansion
    * Adds extra button functions
    * Can be disabled with `NO_EXTRA_BUTTONS`
    * Doesn't affect flash size
    * `ok(): bool`: Returns true if OK is being pressed
    * `sw_A(): bool`: Returns true if A is being pressed
    * `sw_B(): bool`: Returns true if B is being pressed
    * `wait_A(): void`: Returns once B have been pressed
    * `wait_B(): void`: Returns once B have been pressed