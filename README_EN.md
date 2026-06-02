This is an automatic translation and may be incorrect in some places. See the source README and examples for authoritative information.

[![latest](https://img.shields.io/github/v/release/GyverLibs/GyverMAX7219.svg?color=brightgreen)](https://github.com/GyverLibs/GyverMAX7219/releases/latest/download/GyverMAX7219.zip)
[![PIO](https://badges.registry.platformio.org/packages/gyverlibs/library/GyverMAX7219.svg)](https://registry.platformio.org/libraries/gyverlibs/GyverMAX7219)
[![Foo](https://img.shields.io/badge/Website-AlexGyver.ru-blue.svg?style=flat-square)](https://alexgyver.ru/)
[![Foo](https://img.shields.io/badge/%E2%82%BD%24%E2%82%AC%20%D0%9F%D0%BE%D0%B4%D0%B4%D0%B5%D1%80%D0%B6%D0%B0%D1%82%D1%8C-%D0%B0%D0%B2%D1%82%D0%BE%D1%80%D0%B0-orange.svg?style=flat-square)](https://alexgyver.ru/support_alex/)
[![Foo](https://img.shields.io/badge/README-ENGLISH-blueviolet.svg?style=flat-square)](https://github-com.translate.goog/GyverLibs/GyverMAX7219?_x_tr_sl=ru&_x_tr_tl=en)  

[![Foo](https://img.shields.io/badge/ПОДПИСАТЬСЯ-НА%20ОБНОВЛЕНИЯ-brightgreen.svg?style=social&logo=telegram&color=blue)](https://t.me/GyverLibs)

# GyverMAX7219
The sharpest library for MAX7219 in the wild west
- Inherits graphics from GyverGFX
- Connecting matrices with zigzag
- Hardware and software SPI
- Incredible optimization
- Works with displays of any design

### Compatibility
Compatible with all Arduino platforms (Arduino features are used)

## Contents
- [Installation](#install)
- [Initialization](#init)
- [Use of use](#usage)
- [Example](#example)
- [Versions](#versions)
- [Bugs and feedback](#feedback)

<a id="install"></a>
## Installation
- You need to work.[GyverGFX](https://github.com/GyverLibs/GyverGFX)
- The library can be found under the name **GyverMAX7219** and installed through the library manager in:
    - Arduino IDE
    - Arduino IDE v2
    - PlatformIO
- [Download the library](https://github.com/GyverLibs/GyverMAX7219/archive/refs/heads/main.zip).zip archive for manual installation:
    - Unpack and put in *C:\Program Files (x86)\Arduino\libraries* (Windows x64)
    - Unpack and put in *C:\Program Files\Arduino\libraries* (Windows x32)
    - Unpack and put in *Documents/Arduino/libraries/ *
    - (Arduino IDE) Automatic installation from .zip: *Sketch/Connect library/Add .ZIP library...* and specify downloaded archive
- Read more detailed instructions for installing libraries[here](https://alexgyver.ru/arduino-first/#%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_%D0%B1%D0%B8%D0%B1%D0%BB%D0%B8%D0%BE%D1%82%D0%B5%D0%BA)
### Update
- I recommend always updating the library: new versions fix errors and bugs, as well as optimize and add new features.
- Through the library manager IDE: find the library as when installing and click "Update"
- Manually: **Delete the folder with the old version** and then put the new one in its place. “Replacement” can not be done: sometimes new versions delete files that will remain when replaced and can lead to errors!

<a id="init"></a>
## Initialization

```cpp
MAX7219 < W, H, CS > mtrx;            // SPI connection
// Example: UNO/Nano (CLK - D13, DI - D11, CS - any pin)

MAX7219 < W, H, CS, DATA, CLK > mtrx; // Connection to any pins (SPI software)
// W and H are the horizontal and vertical number of MATRICS
// CS, DATA, CLK - pin numbers
```

## Display.
![setType](/doc/setType.png)
![setConnection](/doc/setConnection.png)

<a id="usage"></a>

## Use of use
```cpp
// setup
void begin();                       // launch
void setBright(byte value);         // set the brightness [0-15]
void setBright(uint8_t* values);    // brighten
void setPower(bool value);          // switch off
void setPower(bool* values);        // switch off power from selected
void clearDisplay();                // clear the display (not buffer)

// orientation
void setRotation(uint8_t rot);      // Matrix rotation (8x8): 0, 1, 2, 3 by 90 degrees clockwise
void setFlip(bool x, bool y);       // mirror image of the matrix (8x8) by x and y
void setType(bool type);            // display design (type of stitching)
void setConnection(uint8_t conn);   // display-point

// graphics
void fillByte(uint8_t data);        // byte
void fill();                        // fill the buffer (include all)
void clear();                       // buffer
void update();                      // upgrade

void dot(int x, int y, uint8_t fill = 1); // point
bool get(int16_t x, int16_t y);           // buffer

// + inherits the capabilities of GyverGFXhttps://github.com/GyverLibs/GyverGFX

// custom
void beginData();     // launch
void endData();       // finish off
// sending data directly to the matrix (line, byte)
void sendByte(uint8_t address, uint8_t value);
```

<a id="example"></a>
## Example
For more examples see **examples**!
```cpp
#include <GyverMAX7219.h>
MAX7219 < 1, 1, 5 > mtrx;   // one matrix (1x1), pin CS on D5

void setup() {
  mtrx.begin();       // launch
  mtrx.setBright(5);  // brightness 0.15.
  //mtrx.rotate(1); // can be rotated 0.3, 90 degrees clockwise

  mtrx.dot(0, 0);     // pixel
  mtrx.update();      // show off
  delay(1000);
  mtrx.clear();

  // cross-line
  mtrx.line(0, 0, 7, 7);  // (x0, y0, x1, y1)
  mtrx.line(7, 0, 0, 7);
  mtrx.update();
  delay(1000);
  mtrx.clear();

  // circle
  mtrx.circle(3, 3, 3, GFX_FILL); // oh, radius, pour.
  mtrx.update();
  delay(1000);
  mtrx.clear();

  // circumference
  mtrx.circle(3, 3, 3, GFX_STROKE);
  mtrx.update();
  delay(1000);
  mtrx.clear();

  // See the rest of the geometry in the documentation
}

void loop() {
}
```

<a id="versions"></a>
## Versions
- v1.0 - release
- v1.1 - optimized for SPI
- v1.2 - redesigned FastIO
- v1.2.1 - corrected the SPI bug (c 1.2)
- v1.2.2 - FastIO removed
- v1.3 - minor improvements and optimization, added matrix rotation
- v1.4 - added support for matrix displays of any configuration (connection point, direction, alternation)
- v1.5 - added separate control of brightness and power matrices

<a id="feedback"></a>
## Bugs and feedback
If you find bugs, create **Issue**, or better write to the mail immediately.[alex@alexgyver.ru](mailto:alex@alexgyver.ru)  
The library is open for revision and your **Pull Requests*!

When reporting bugs or incorrect work of the library, it is necessary to specify:
- Library version
- What is used by the IC
- SDK version (for ESP)
- Arduino IDE version
- Are embedded examples that use features and designs that cause bugs in your code working correctly?
- What code was downloaded, what work was expected from it and how it works in reality
- Ideally, attach the minimum code in which the bug is observed. Not a canvas of a thousand lines, but a minimum code.
