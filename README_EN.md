This is an automatic translation, may be incorrect in some places. See sources and examples!

# Gyvermax7219
A sharp library for matrices Max7219 in the Wild West
- Inherits graphics from Gyvergfx
- Connection of matrices zigzag
- hardware and software SPI
- Incredible optimization
- works with displays of any design

## compatibility
Compatible with all arduino platforms (used arduino functions)

## Content
- [installation] (# Install)
- [initialization] (#init)
- [use] (#usage)
- [Example] (# Example)
- [versions] (#varsions)
- [bugs and feedback] (#fedback)

<a id="install"> </a>
## Installation
- For work, you need [gyvergfx] (https://github.com/gyverlibs/gyvergfx)
- The library can be found by the name ** gyvermax7219 ** and installed through the library manager in:
    - Arduino ide
    - Arduino ide v2
    - Platformio
- [download library] (https://github.com/gyverlibs/gyvermax7219/archive/refs/heads/main.zip). Zip archive for manual installation:
    - unpack and put in * C: \ Program Files (X86) \ Arduino \ Libraries * (Windows X64)
    - unpack and put in * C: \ Program Files \ Arduino \ Libraries * (Windows X32)
    - unpack and put in *documents/arduino/libraries/ *
    - (Arduino id) Automatic installation from. Zip: * sketch/connect the library/add .Zip library ... * and specify downloaded archive
- Read more detailed instructions for installing libraries [here] (https://alexgyver.ru/arduino-first/#%D0%A3%D1%81%D1%82%D0%B0%BD%D0%BE%BE%BE%BED0%B2%D0%BA%D0%B0_%D0%B1%D0%B8%D0%B1%D0%BB%D0%B8%D0%BE%D1%82%D0%B5%D0%BA)
### Update
- I recommend always updating the library: errors and bugs are corrected in the new versions, as well as optimization and new features are added
- through the IDE library manager: find the library how to install and click "update"
- Manually: ** remove the folder with the old version **, and then put a new one in its place.“Replacement” cannot be done: sometimes in new versions, files that remain when replacing are deleted and can lead to errors!

<a id="init"> </a>
## initialization

`` `CPP
Max7219 <w, h, cs> mtrx;// Connection to the hardware SPI
// Example: uno / nano (clk - d13, di - d11, cs - any pin)

Max7219 <w, h, CS, Data, Clk> Mtrx;// Connecting to any pins (SOFT SPI)
// w and h - the number of matrices horizontally and vertical
// CS, Data, Clk - Pino numbers
`` `

## display
! [settype] (/doc/settype.png)
! [setconnection] (/doc/setConnel)

<a id="usage"> </a>

## Usage
`` `CPP
// Setting
VOID Begin ();// Launch
VOID Setbright (Byte Value);// Set brightness [0-15]
VOID Setbright (Uint8_t* Values);// Install different brightness
VOID SetPower (Bool Value);// Switch power
VOID setpower (Bool* Values);// Switch power in the selected
VOID Cleardisplay ();// Clean the display (not a buffer)

// Orientation
VOID setrotation (Uint8_T ROT);// Turn of matrices (8x8): 0, 1, 2, 3 to 90 degrees clockwise
VOID setflip (Bool X, Bool Y);// Mirror reflection of matrices (8x8) by x and y
VOID Settype (Bool Type);// Display design (type of lowercy)
VOID setconnection (Uint8_T Conn);// Display connection point

// graphic arts
Void Fillbyte (Uint8_t Data);// Pour a byte
VOID Fill ();// Pour the buffer (turn on everything)
Void Clear ();// Clean the buffer
VOID update ();// update the display

VOID DOT (Int X, Int Y, UINT8_T FILL = 1);// set the point
Bool get (int16_t x, int16_t y);// Get a point from the buffer

// + inherits the capabilities of gyvergfx https://github.com/gyverlibs/gyvergfx

// Custom
VOID BeginData ();// Start sending
VOID Enddata ();// finish the sending
// Sending data directly to the matrix (line, byte)
VOID SENDBYTE (Uint8_T Address, Uint8_t Value);
`` `

<a id="EXAMPLE"> </a>
## Example
The rest of the examples look at ** Examples **!
`` `CPP
#include <gyvermax7219.h>
Max7219 <1, 1, 5> MTRX;// one matrix (1x1), pin cs on d5

VOID setup () {
  mtrx.begin ();// Launch
  mtrx.setbright (5);// brightness 0..15
  //mtrx.rotate(1);// you can turn 0..3, 90 degrees clockwise

  mtrx.dot (0, 0);// Pixel on coordinates 0.0
  mtrx.update ();// show
  DELAY (1000);
  mtrx.clear ();

  // Line Cross Cross
  mtrx.line (0, 0, 7, 7);// (x0, y0, x1, y1)
  mtrx.line (7, 0, 0, 7);
  mtrx.update ();
  DELAY (1000);
  mtrx.clear ();

  // circle
  mtrx.circle (3, 3, 3, gfx_fill);// x, y, radius, filling
  mtrx.update ();
  DELAY (1000);
  mtrx.clear ();

  // circle
  mtrx.circle (3, 3, 3, gfx_stroke);
  mtrx.update ();
  DELAY (1000);
  mtrx.clear ();

  // See the rest of the geometry in the documentation
}

VOID loop () {
}
`` `

<a id="versions"> </a>
## versions
- v1.0 - release
- V1.1 - optimized SPI
- V1.2 - Redeled Fastio
- v1.2.1 - fixed bug in SPI (with 1.2)
- v1.2.2 - removed Fastio
- V1.3 - minor improvements and optimization, added a turn of matrices
- V1.4 - added support for matrix displays of any configuration (connection point, direction, alternation)
- v1.5 - added separate control of the brightness and nutrition of matrices

<a id="feedback"> </a>
## bugs and feedback
Create ** Issue ** when you find the bugs, and better immediately write to the mail [alex@alexgyver.ru] (mailto: alex@alexgyver.ru)
The library is open for refinement and your ** pull Request ** 'ow!

When reporting about bugs or incorrect work of the library, it is necessary to indicate:
- The version of the library
- What is MK used
- SDK version (for ESP)
- version of Arduino ide
- whether the built -in examples work correctly, in which the functions and designs are used, leading to a bug in your code
- what code has been loaded, what work was expected from it and how it works in reality
- Ideally, attach the minimum code in which the bug is observed.Not a canvas of a thousand lines, but a minimum code