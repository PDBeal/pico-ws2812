# WS2812 NeoPixel Library
RP2040 library for controlling strips/pixels using WS2812 (NeoPixel) LEDs using PIO and pico-sdk

I wanted a library for use with the WS2812 (NeoPixel) on the RP2040 that didn't rely on Arduino.h or any other AVR include file.  So I created this library using the pico-examples, the Adafruit NeoPixel library and some other RP2040 sources as reference.

## 1. Importing the library
* Clone this project into your pico project
* Add this to your CMakeLists.txt
  ```cmake
    add_subdirectory(pico-ws2818)
  
    target_link_libraries(${PROJECT_NAME}
        pico_ws2818
    )
  ```
  * Import library in your code
  ```c++
  #include "pico-ws2812/ws2812.h"
  ```
  * Define your IO and create the class instance in your code
  ```c++
  const uint NEOPIXELIO = 10; // Define your GPIO pin
  const int NUMNEOPIXELS = 279; // Define number of neopixels

  WS2812 neopixel = WS2812(NUMNEOPIXELS, NEOPIXELIO); // Create your instance of the library
  ```
  * Alternatively you can also specify the statemachine and pio manually
  ```c++
  const uint NEOPIXELIO = 10; // Define your GPIO pin
  const int NUMNEOPIXELS = 279; // Define number of neopixels
  PIO pio = pio0;
  int sm = 1;
  
  WS2812 neopixel = WS2812(NUMNEOPIXELS, NEOPIXELIO, pio0, sm); // Create your instance of the library
  ```
## 2. Basic usage
```c++
void init()
{
  // Initialize the Neopixel (this starts the PIO program)
  neopixel.begin();
}

void loop()
{
  // Fill all the pixels with same value
  neopixel.fillPixelColor(0,0,255);
  neopixel.show();

  // wait 500ms
  sleep_ms(500);

  // Clear the entire string
  neopixel.clear();
  neopixel.show();
}
```

## 3. Functions in library
Two different constructors are available for use
```c++
WS2812(uint16_t num, uint8_t pin, PIO pio, int sm); // Basic Constructor

WS2812(uint16_t num, uint8_t pin); // This constructor tries to autoselect pio and sm
```

Various functions for controlling LEDs
```c++
neopixel.begin(); // Initialize the class instance after calling constructor

neopixel.show(); // Display all the pixels in the buffer

neopixel.setPixelColor(uint16_t led, uint8_t red, uint8_t green, uint8_t blue); // Set a NeoPixel to a given color.

neopixel.setPixelColor(uint16_t led, uint32_t color); // set a pixel color fomr 'packed' 32-bit RGB value

neopixel.clear(); // Clear the entire string

neopixel.fillPixelColor(uint8_t red, uint8_t green, uint8_t blue); // Fill all the pixels with same value

neopixel.updateLength(uint16_t num); // Change strand length
    
neopixel.numPixels(); // Returns the number of pixels currently connected
    
neopixel.getPixelColor(uint16_t led); // Query color from previously-set pixel
```
