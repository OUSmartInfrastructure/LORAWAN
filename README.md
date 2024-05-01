# LORAWAN

This repository provides a comprehensive guide on setting up various hardware components, including the Raspberry Pi, Adafruit QT PY ESP32 PICO, Seeed Studio XIAO Expansion Board and Grove-Lora-E5. The guide offers detailed instructions on installing the Raspberry OS and configuring it with the RAK HAT. It covers the process of connecting to The Things Network and provides step-by-step guidance on setting up the Adafruit QT PY ESP32 PICO micro-controller with the Seeed Studio XIAO Expansion Board. Additionally, the guide includes instructions for installing the Adafruit-QTPY-esp32-Pico and implementing a Blink program. Configuring Grove-Lora-E5 to send and receive messages to and from THE THINGS NETWORK. Configuring SENSECAP SENSORS(S2105) to transmit sensor data from end devices to gateway through THE THINGS NETWORK and integrating the THINGS NETWORK to DATACAKE platform to display the data through DATACAKE.

# Guide
## [Raspberry Pi](https://github.com/OUSmartInfrastructure/LORAWAN/blob/main/Raspberry%20Pi)
This guide gives a detailed overview of how to get started with raspberry pi 

# Product Description
Product Name: Raspberry Pi 3 
Product Description: The Raspberry Pi 3 Model B is the third generation Raspberry Pi. 
This powerful credit-card sized single board computer can be used for many applications and supersedes the original Raspberry Pi Model B+ and Raspberry Pi 2 Model B. 
Whilst maintaining the popular board format the Raspberry Pi 3 Model B brings you a more powerful processer, 10x faster than the first generation Raspberry Pi. 
Additionally it adds wireless LAN & Bluetooth connectivity making it the ideal solution for powerful connected designs.
For more info follow this link https://us.rs-online.com/m/d/4252b1ecd92888dbb9d8a39b536e7bf2.pdf

# Installation
Begin with the raspberry OS installation. Install Raspberry Pi OS using Raspberry Pi Imager. 
Use this link to https://www.raspberrypi.com/software/ (or) https://www.raspberrypi.com/software/operating-systems/ download
Open the raspberry pi imager application select choose device and select the device you are using(select the model). 
Choose the OS, choose storage(sd card). You can also edit the settings like username and password
(You can also change them later through command line using sudo raspi-config command, but it's better to change here). 
Set the locale settings(adding time zone), now flash the os into sd card.
Now you can fix the parts. You need to insert SD card after seeting up the equipment.
For detailed information on how to fix the parts use this link https://youtu.be/DdnzSmJ5Fxg?si=YDYS_Bi70eTiWGiy. Note: This is reference for setting up the parts.
For getting started with raspberry pi follow this links https://youtu.be/aR9-gbZvBh0?si=jhLzmiA2kFvTqd6E and https://youtu.be/bea7g5isD0w?si=KTFwbOSb_EdKQ-TD
Check the description of the videos for the github links.
Follow the link below to get detailed overview https://youtu.be/bea7g5isD0w?si=n5sUUBpQowxnjzMq
Once you log in to the raspberry desktop you can use the comand sudo raspi-config to make changes to password or to set time zone and language.
As we are in US we need to select en_US.UTF-8 UTF-8
On next selct screen select en_US.UTF-8. Now reboot to make the changes reflect.
df -h command gives info about the sd card storage
To increase the storage use the command sudo raspi-config, selct advanced options -> Expand file system.
You can get EUI address by using these commands
ip link show eth0 - if you are using ethernet cable
ip link show wlan0 - if using router
You will get a gateway EUI use that EUI to register your gateway in The Things Network.


# Cloning Repository

We are cloning a github repository. To clone the repository enter the command
git clone https://github.com/robertlie/RAK831-LoraGateway-RPi ~/rak831-loragateway - using CLI
https://github.com/robertlie/RAK831-LoRaGateway-RPi - Github link

After cloning use the command ls -al you should see the cloned folder rak-831loragateway.
Now go to this repository using cd rak-831loragateway use ls -al. You should see an install script.
Enter this command to execute install script sudo ./install.sh
You will see Gateway EUI. Set the configurations like region, latitude, longitude and altitude.
After install script is executed the system reboots.

Login into raspberry pi go to the folder opt i.e cd /opt then go to this folder cd /ttn-gateway
Install script installs lora_gateway and packet_forwarder packages. go to packet_forwarder i.e cd /packet_forwarder 
check the ttn-gateway status by using this command systemctl status ttn-gateway -l
This should be active and run withou errors.

Installing Global Json and Local Json

Global configuration json file is main file it contains information related to frequency, gateway EUI.
Install script installs global and local json files, but we will use different files.

now go to cd lora_pkt_fwd folder this folder contains global_conf.json file
Rename this file mv global_conf.json global_conf.json_orig

My gateway is operating in US so download this file
wget https://githubusercontent.com/TheThingsNetwork/gateway-conf/master/US-global_conf.json
After downloading this file rename this file mv US-global_conf.json global_conf.json
Reboot the raspberry pi
Check ttn-gateway server status systemctl status ttn-gateway -l there should be no errors
In the global_conf.json check all parameters and make sure that they align with your region like frequency, the region you are operating, etc.

# Adding Gateways

https://console.cloud.thethings.network/
Follow the link and click a cluster(i.e, where your gateway is operating(location) in my case it is North America nam1)

1. Go to Gateways in the top menu, and click + Register Gateway to reach the gateway registration page.

2. Fill the Gateway EUI and click Confirm. Some gateways do not use a Gateway EUI (e.g. The Things Kickstarter Gateway), in which case you can 
just click on Continue without EUI.

3. Depending on whether the Gateway EUI is claimable you will either be shown the claiming form or the manual registration form.

4. On the manual registration form fill in the Frequency Plan and the Gateway ID if it was not pre filled, The other fields are optional. 
Click Register Gateway to finish. Use the frequency United States 902-928 MHz, FSB 2 Used by TTN.

5. Your gateway will be created and you will be redirected to the gateway overview page of your newly created gateway.

# Set Gateway Location

1. Once you have added your gateway to The Things Stack, you can also set its location to be displayed on a map widget by clicking Change 
location settings.

2. If you want your gateway’s location to be publicly displayed, check the Publish location box.

3. The gateway location can be manually set by entering the Latitude, Longitude and Altitude values.

4. You can also check the Update from status messages box if you want to update the location based on the metadata from the incoming uplink 
gateway status messages. The location settings you manually entered will be overwritten by the updates from the gateway status messages.

5. Note: If you change the physical location of your gateway, the location update in The Things Stack will take place only after you restart the 
gateway.

Follow this link for detailed information 
https://www.thethingsindustries.com/docs/gateways/concepts/adding-gateways/#:~:text=CLI-,Adding%20Gateways%20using%20the%20Console,click%20on%20Continue%20without%20EUI

For configuring the Pi follow this link https://www.raspberrypi.com/documentation/computers/configuration.html - This is the official document.
## [Ada Fruit QT PY ESP32](https://github.com/OUSmartInfrastructure/LORAWAN/blob/main/Ada%20Fruit%20QT%20PY%20ESP32)

Product Name: Adafruit QT PY ESP32
Product description: This QT Py board is a thumbnail-sized PCB that features the ESP32-Pico-V3-02, an all-in-one chip that has an ESP32 chip
with dual-core 240MHz Tensilica processor, WiFi and Bluetooth classic + BLE, adds a bunch of required passives and oscillator, 8 MB of Flash memory and 2 MB of PSRAM. 
We add a USB to serial converter chip, some more passives, an antenna, USB C, buttons, NeoPixel and QT connector to outfit this super-hero 
chip for any task you want to throw it at.

![Adafruit QT PY ESP32 Pico](https://github.com/OUSmartInfrastructure/LORAWAN/assets/33726869/86d1815a-df59-4b8b-bc8f-35e7a1d27a00)

![Pinout](https://github.com/OUSmartInfrastructure/LORAWAN/assets/33726869/96205a70-f629-47b1-a7e1-902d5202e0c5)

[QT PY ESP 32](https://github.com/nikhilramini/Adafruit-QTPY-esp32-Pico/blob/master/assets/81555066/11ed5d85-2b80-4516-8d8d-460d063f736d)

Getting statred with QT PY ESP32

Arduino IDE Setup
Install Arduino - The first thing you will need to do is to download the latest release of the Arduino IDE.
https://www.arduino.cc/en/software

Install CP2104 / CP2102N USB Driver
The USB-to-Serial converter that talks to the ESP32 chip itself will need a driver on your computer's operating system. 
https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers?tab=downloads
For windows download CP210x Windows Drivers or CP210x Windows Drivers with Serial Enumerator if you are not sure what to install then install both.
For Mac install CP210x VCP Mac OSX Driver

Install CH9102 / CH34X USB Driver
Newer ESP32 boards have a different USB-to-serial converter that talks to the chip itself, and will need a driver on your computer's operating system. 
https://www.wch-ic.com/downloads/CH341SER_ZIP.html - windows
https://www.wch-ic.com/downloads/CH34XSER_MAC_ZIP.html - Mac

Install ESP32 Board Support Package
After you have downloaded and installed the latest version of Arduino IDE, you will need to start the IDE and navigate to the Preferences menu.
A dialog will pop up

We will be adding a URL to the new Additional Boards Manager URLs option. The list of URLs is comma separated, and you will only have to add each URL once. New Adafruit boards and updates to existing boards will automatically be picked up by the Board Manager each time it is opened. The URLs point to index files that the Board Manager uses to build the list of available & installed boards.

We will only need to add one URL to the IDE in this example, but you can add multiple URLS by separating them with commas. Copy and paste the link below into the Additional Boards Manager URLs option in the Arduino IDE preferences.
https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_dev_index.json

If you have multiple boards you want to support, say ESP8266 and Adafruit, have both URLs in the text box separated by a comma (,)

Once done click OK to save the new preference settings.

The next step is to actually install the Board Support Package (BSP). Go to the Tools → Board → Board Manager submenu. A dialog should come up with various BSPs. Search for esp32.
Click the Install button and wait for it to finish. Once it is finished, you can close the dialog.

In the Tools → Board submenu you should see ESP32 Arduino and in that dropdown it should contain the ESP32 boards along with all the latest ESP32 boards.

Look for the board called Adafruit QT Py ESP32.

BLINK PROGRAM

![QT PY connection](https://github.com/OUSmartInfrastructure/LORAWAN/assets/33726869/e9593dac-90a7-40f6-bc49-452d146d6de7)

Start up Arduino IDE and Select Board/Port
Open the Arduino IDE on your computer. Now you have to tell the IDE what board you are using, and how you want to connect to it.
In the IDE find the Tools menu. You will use this to select the board.

Install NeoPixel Library

You will need to add support by installing the library. Go to the Library Manager. 
Sketch -> Include Library -> Library Manager
Search for and install the Adafruit NeoPixel library. Install version 1.10.0

New Blink Sketch
From the File menu, select 
Then in the new window, copy and paste this program:

#include <Adafruit_NeoPixel.h>

// How many internal neopixels do we have? some boards have more than one!
#define NUMPIXELS        1

Adafruit_NeoPixel pixels(NUMPIXELS, PIN_NEOPIXEL, NEO_GRB + NEO_KHZ800);

// the setup routine runs once when you press reset:
void setup() {
  Serial.begin(115200);

#if defined(NEOPIXEL_POWER)
  // If this board has a power control pin, we must set it to output and high
  // in order to enable the NeoPixels. We put this in an #if defined so it can
  // be reused for other boards without compilation errors
  pinMode(NEOPIXEL_POWER, OUTPUT);
  digitalWrite(NEOPIXEL_POWER, HIGH);
#endif

  pixels.begin(); // INITIALIZE NeoPixel strip object (REQUIRED)
  pixels.setBrightness(20); // not so bright
}

// the loop routine runs over and over again forever:
void loop() {
  // say hi
  Serial.println("Hello!");
  
  // set color to red
  pixels.fill(0xFF0000);
  pixels.show();
  delay(500); // wait half a second

  // turn off
  pixels.fill(0x000000);
  pixels.show();
  delay(500); // wait half a second
}

Verify (Compile) Sketch

OK now you can click the Verify button to convert the sketch into binary data to be uploaded to the board.
If something went wrong with compilation, you will get red warning/error text in the bottom window letting you know what the error was. It will also highlight the line with an error.
On success you will see white text output and the message Done compiling. 

Upload Sketch

Once the code is verified/compiling cleanly you can upload it to your board. Click the Upload button.
Often times you will get a warning like this, which is kind of vague:

No device found on COM66 (or whatever port is selected)
An error occurred while uploading the sketch

This could be a few things.
This could be a few things.

Check again that you have the correct board selected! Many electronics boards have very similar names or look, and often times folks grab a board different from what they thought.

Finally, a Blink!

For more detailed information please navigate to this website

https://learn.adafruit.com/adafruit-qt-py-esp32-pico/arduino-ide-setup

## [XIAO Expansion Board](https://github.com/OUSmartInfrastructure/LORAWAN/blob/main/XIAO%20Expansion%20Board%20Display)

![Expansion Board](https://github.com/OUSmartInfrastructure/LORAWAN/assets/33726869/c4e9ec9a-fd62-4409-9c9f-21bfa6171b86)

Product Name : Seeed Studio XIAO Expansion Board
Product Description : Seeed Studio XIAO Expansion Board is a powerful functional expansion board for the Seeed Studio XIAO series. 
This board is only half the size of the Raspberry Pi 4. The XIAO expansion board features quick prototyping, rich peripherals, and
supports circuit python. This board includes rich peripherals
such as OLED, RTC, SD card slot, grove connectors, lipo battery charging, buzzer, reset button, and SWD pins.
The Seeeduino XIAO expansion board provides high-cost performance, plug and play, and needs no soldering. 
Typical applications include SWD debugging, rapid prototyping, data display, and mini-size projects.
For more info follow the link https://wiki.seeedstudio.com/Seeeduino-XIAO-Expansion-Board/ 

# Programs(Hello world, Blink, User_input and Blink programs)
Adafruit QT Py ESP32 Pico using the Adafruit SSD1306 library

1. Blink program

#include <Adafruit_NeoPixel.h>

// How many internal neopixels do we have? some boards have more than one!
#define NUMPIXELS        1

Adafruit_NeoPixel pixels(NUMPIXELS, PIN_NEOPIXEL, NEO_GRB + NEO_KHZ800);

// the setup routine runs once when you press reset:
void setup() {
  Serial.begin(115200);

#if defined(NEOPIXEL_POWER)
  // If this board has a power control pin, we must set it to output and high
  // in order to enable the NeoPixels. We put this in an #if defined so it can
  // be reused for other boards without compilation errors
  pinMode(NEOPIXEL_POWER, OUTPUT);
  digitalWrite(NEOPIXEL_POWER, HIGH);
#endif

  pixels.begin(); // INITIALIZE NeoPixel strip object (REQUIRED)
  pixels.setBrightness(20); // not so bright
}

// the loop routine runs over and over again forever:
void loop() {
  // say hi
  Serial.println("Hello!");
  
  // set color to red
  pixels.fill(0xFF0000);
  pixels.show();
  delay(250); // wait half a second

  // turn off
  pixels.fill(0x000000);
  pixels.show();
  delay(500); // wait half a second
}

2. User_input and Blink program

#include <Adafruit_NeoPixel.h>

// How many internal neopixels do we have? some boards have more than one!
#define NUMPIXELS        1
#define PIN_NEOPIXEL 5   // Example pin for NeoPixels

Adafruit_NeoPixel pixels(NUMPIXELS, PIN_NEOPIXEL, NEO_GRB + NEO_KHZ800);

#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64

// Create an instance of the display
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, -1);

void setup() {
  Serial.begin(9600);

  // Initialize I2C communication for the OLED display
  Wire.begin();

  // Initialize OLED display with I2C address 0x3C
  if (!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) { // Change 0x3C to your display's address
    Serial.println(F("SSD1306 allocation failed"));
    for (;;);
  }

  // Initialize NeoPixels
  pixels.begin(); // INITIALIZE NeoPixel strip object (REQUIRED)
  pixels.setBrightness(20); // Set brightness
}

void loop() {
  // Read user input from the Serial monitor
  if (Serial.available() > 0) {
    String userInput = Serial.readStringUntil('\n'); // Read until newline character

    // Clear the display before printing new input
    display.clearDisplay();

    // Display user input on the OLED display
    display.setTextSize(1);
    display.setTextColor(SSD1306_WHITE);
    display.setCursor(0, 0);
    display.println(userInput);

    // Display on the OLED screen
    display.display();
  }
  
  // Blink NeoPixel
  pixels.fill(0xFF0000); // Set color to red
  pixels.show(); // Display the color
  delay(250); // Keep the color for 250 milliseconds

  pixels.fill(0x000000); // Turn off the NeoPixel
  pixels.show(); // Display the cleared NeoPixel
  delay(250); // Wait for half a second before repeating
}

3. Hello World Program

#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64

// Create an instance of the display
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, -1);

void setup() {
  // Initialize with the I2C addr 0x3D (for the 128x64)
  if(!display.begin(SSD1306_I2C_ADDRESS, Wire)) {
    Serial.println(F("SSD1306 allocation failed"));
    for(;;);
  }

  // Clear the display
  display.clearDisplay();
  display.display();
}

void loop() {
  // Display "Hello World!"
  display.setTextSize(1);
  display.setTextColor(SSD1306_WHITE);
  display.setCursor(0, 0);
  display.println(F("Hello World!"));

  // Display on the screen
  display.display();
  delay(2000);  // You can adjust the delay as needed
  display.clearDisplay();
}
## [Grove-Lora-E5](https://github.com/OUSmartInfrastructure/LORAWAN/blob/main/Grove-Lora-E5)
#Product Details
Product Name: Grove - Wio-E5.
Product description: The Grove - Wio-E5 features an extremely compact size, ultra-low power consumption, low cost and amazing performance.
The Grove - Wio-E5 can endow your development boards' strong features of ultra-long transmitting range, great performance and high efficiency 
via simple plug-and-play with the Grove connector on board. By connecting Grove, the Wio-E5 to your development boards, your devices are able to 
communicate with and control Wio-E5 conveniently by AT command through a UART connection.

#Getting Started

Connecting the Grove LoRa E5 module and the QT Py ESP32 using a breadboard involves wiring the necessary connections between the two components.
Here's a general guide on how to do this:

Components Needed:
Grove LoRa E5 module
QT Py ESP32
Breadboard
Jumper wires

Instructions:

Power Connection:

Connect the VCC pin of the Grove LoRa E5 module to the 3.3V pin on the QT Py ESP32.
Connect the GND (Ground) pin of the Grove LoRa E5 module to the GND pin on the QT Py ESP32.

Communication Connection (Serial/UART):

Connect the TXD pin of the Grove LoRa E5 module to a GPIO pin that supports UART TX on the QT Py ESP32.
Connect the RXD pin of the Grove LoRa E5 module to a GPIO pin that supports UART RX on the QT Py ESP32.

Communication Connection (Serial/UART using Bread-board):

Connect the TX pin of the Grove LoRa E5 module to the bread board and connect the QT Py ESP32 RX.
Connect the RX pin of the Grove LoRa E5 module to the bread board and connect the QT Py ESP32 TX.

Power Up:

Ensure the connections are secure and correct.
Connect the QT Py ESP32 to your computer using USB. 

Programming:

If you intend to program the QT Py ESP32 to communicate with the Grove LoRa E5 module, make sure you have the necessary software and libraries 
installed. For the ESP32, the Arduino IDE with the ESP32 board support is commonly used.

Coding:

Write or upload a program to the QT Py ESP32 that communicates with the Grove LoRa E5 module using the UART (Serial) interface. 
Use the appropriate library and commands for LoRa communication.

Testing:

Upload a simple test program to the QT Py ESP32 to check the communication with the Grove LoRa E5 module.
Monitor the serial output to verify that the devices are communicating successfully.

Follow the documentation for detailed information about Lora-E5 use this link to access the document 
https://files.seeedstudio.com/products/317990687/res/LoRa-E5%20AT%20Command%20Specification_V1.0%20.pdf

#Program for serial communication between QT PY ESP32 and Grove-Lora-E5

#include <Arduino.h>

#define MICRO_RX_PIN 0    // RX pin of microcontroller
#define MICRO_TX_PIN 1    // TX pin of microcontroller
#define LORA_RX_PIN 10    // RX pin of Grove-Lora-E5
#define LORA_TX_PIN 11    // TX pin of Grove-Lora-E5

void setup() {
  Serial.begin(9600);    // Start serial communication for microcontroller
  Serial1.begin(9600);   // Start serial communication for Grove-Lora-E5
  Serial.println("Microcontroller and Grove-Lora-E5 communication initialized.");
}

void loop() {
  // Check for data from microcontroller and send to Grove-Lora-E5
  if (Serial.available() > 0) {
    String userInput = Serial.readStringUntil('\n');  // Read user input from Serial Monitor
    Serial.println("Sending data to Grove-Lora-E5: " + userInput);
    Serial1.println(userInput);  // Send user input to Grove-Lora-E5
  }

  // Check for data from Grove-Lora-E5 and send to microcontroller
  if (Serial1.available() > 0) {
    String receivedData = Serial1.readStringUntil('\n');  // Read data from Grove-Lora-E5
    Serial.println("Received data from Grove-Lora-E5: " + receivedData);
    // Process received data as needed

    // Echo back the received data to the microcontroller
    Serial.println("Sending data to microcontroller: " + receivedData);
  }
}

Commands to test Serial Communication

AT
Use to test if connection of module is OK. This is a dummy command just like other common "AT modules" 

Format: 
AT
Return: 
+AT: OK

VER
Check firmware version. Versioning rule refers to Semantic Versioning 2.0.0. 
Format:
AT+ VER
Return: 
+VER: $MAJOR.$MINOR.$PATCH
+VER: 4.0.11

ID
Use to check the ID of the LoRaWAN module, or change the ID. ID is treated as big endian numbers. 
ReadIDFormat: AT+ ID
/ / Read all, DevAddr( ABP) , DevEui( OTAA) , AppEui( OTAA) AT+ ID= DevAddr 
/ / Read DevAddr AT+ ID= DevEui / / Read DevEui AT+ ID= AppEui 
/ / Read AppEui AT+ ID= DevAddr, " devaddr"
/ / Set new DevAddr AT+ ID= DevEui, " deveui"
/ / Set new DevEui AT+ ID= AppEui, " appeui" 
/ / Set new AppEui 
Return: 
+ID: DevAddr, xx: xx: xx:xx 
+ID: DevEui, xx:xx:xx:xx:xx:xx:xx:xx 
+ID: AppEui13, xx:xx:xx:xx:xx:xx:xx:xx

Change end device address (DEVADDR)(Usally not required)
AT+ ID= DevAddr, “ 4 bytes length hex identifier” 
eg: AT+ID=DevAddr, "01234567" 
eg: AT+ID=DEVADDR, "01 23 45 67" 
Return: 
+ID: DevAddr, 01:23:45:67

## Grove - Wio-E5 TTN Demo

Hardware Required:
Grove LoRa E5 module
QT Py ESP32
Breadboard
Jumper wires

#Program for Synthetic Data Exchange

#include <Arduino.h>
#include <U8x8lib.h>
# include <SoftwareSerial.h> 

U8X8_SSD1306_128X64_NONAME_HW_I2C u8x8(/*reset=*/U8X8_PIN_NONE);
static char recv_buf[512];
static bool is_exist = false;
static bool is_join = false;
const byte rxPin = 2;
const byte txPin = 3;

const byte ultrasonicPin = 4;

//----- what pin the components are connected to -----

SoftwareSerial SoftSerial (rxPin, txPin);       // Set up a new SoftwareSerial object

static int at_send_check_response(char *p_ack, int timeout_ms, char *p_cmd, ...) {
  int ch;
  int index = 0;
  int startMillis = 0;
  va_list args;
  memset(recv_buf, 0, sizeof(recv_buf));
  va_start(args, p_cmd);
  Serial1.printf(p_cmd, args);
  Serial.printf(p_cmd, args);
  va_end(args);
  delay(200);
  startMillis = millis();

  if (p_ack == NULL) {
    return 0;
  }

  do {
    while (Serial1.available() > 0) {
      ch = Serial1.read();
      recv_buf[index++] = ch;
      Serial.print((char)ch);
      delay(2);
    }

    if (strstr(recv_buf, p_ack) != NULL) {
      return 1;
    }

  } while (millis() - startMillis < timeout_ms);
  return 0;
}

static void send_synthetic_data() {
  static int synthetic_data = 0;
  char cmd[128];
  sprintf(cmd, "AT+CMSGHEX=\"%04X\"\r\n", synthetic_data);
  int ret = at_send_check_response("Done", 5000, cmd);
  if (ret) {
    Serial.print("Sent synthetic data: ");
    Serial.println(synthetic_data);
  } else {
    Serial.print("Send failed!\r\n\r\n");
  }
  synthetic_data++;  // Change the synthetic data for the next iteration
}

void setup(void) {
  u8x8.begin();
  u8x8.setFlipMode(1);
  u8x8.setFont(u8x8_font_chroma48medium8_r);

  Serial.begin(9600);

  pinMode(rxPin, INPUT);            // Define pin modes for TX and RX
  pinMode(txPin, OUTPUT);
  Serial1.begin(9600);
  Serial.print("E5 LORAWAN TEST\r\n");
  u8x8.setCursor(0, 0);
 
  // Additional setup code for LoRaWAN configuration and initialization can be added here
  if (at_send_check_response("+AT: OK", 100, "AT\r\n")) {
    is_exist = true;
    at_send_check_response("+ID: AppEui", 1000, "AT+ID\r\n");
    //at_send_check_response("+ID: DevEui", 1000, "AT+ID\r\n");
    //at_send_check_response("+ID: DevAddr", 1000, "AT+ID\r\n");
    at_send_check_response("+MODE: LWOTAA", 1000, "AT+MODE=LWOTAA\r\n");
    at_send_check_response("+DR: US915", 1000, "AT+DR=0\r\n");
    at_send_check_response("+CH: NUM", 1000, "AT+CH=NUM,8\r\n");
    at_send_check_response("+KEY: APPKEY", 1000, "AT+KEY=APPKEY,\"2B7E151628AED2A6ABF7158809CF4F3C\"\r\n");
    at_send_check_response("+CLASS: C", 1000, "AT+CLASS=A\r\n");
    at_send_check_response("+PORT: 8", 1000, "AT+PORT=8\r\n");
    delay(200);
    u8x8.setCursor(5, 0);
    u8x8.print("LoRaWAN");
    is_join = true;
  } else {
    is_exist = false;
    Serial.print("No E5 module found.\r\n");
    u8x8.setCursor(0, 1);
    u8x8.print("unfound E5 !");
  }
}

      // Additional code for joining the network can be added here
void loop(void) {
  if (is_exist) {
    if (is_join) {
      int ret = at_send_check_response("+JOIN: Network joined", 12000, "AT+JOIN\r\n");
      if (ret) {
        is_join = false;
      } else {
        at_send_check_response("+ID: AppEui", 1000, "AT+ID\r\n");
        Serial.print("JOIN failed!\r\n\r\n");
        delay(5000);
      }
    } else {
      send_synthetic_data();  // Call the function to send synthetic data
      delay(5000);
    }
  } else {
    delay(1000);
  }
}

TTN Console Configuration Setup

Step 1. Visit The Things Network website and sign up for a new account

Step 2. After logging in, click your profile and select Console

Step 3. Select a cluster to start adding devices and gateways

Step 4. Click Go to applications

Step 5. Click + Add application

Step 6. Fill Application ID and click Create application

Note: Here Application name and Description are not compulsory fields. If Application name is left blank, it will use the same name as 
Application ID by default.

Step 7: Navigate to Payload formatters > Uplink, select Formatter Type as Javascript and fill the Formatter parameter as follows

function Decoder(bytes, port) {
  
  var decoded = {};
  if (port === 8) {
    decoded.temp = bytes[0] <<8 | bytes[1];
    decoded.humi = bytes[2] <<8 | bytes[3];
  }

  return decoded;
}

Step 8: Upload the Arduino code(Program for serial communication between QT PY ESP32 and Grove-Lora-E5) to QT PY ESP32, 
and open serial monitor and enter the command AT+ID
Note down DevEui and AppEUi generated above.

Step 9: Go back to the Overview page of the created application and click + Add end device

Step 10. Click Manually, to enter the registration credentials manually

Step 11. Select the Frequency plan according to your region. Also make sure you use the same frequency as the gateway in which you will connect 
this device to. Select LoRaWAN Specification 1.0.2 as the LoRaWAN® version and RP001 Regional Parameters 1.0.2 REVISION B as the Regional 
Parameters version. These settings are according to the LoraWAN® stack of Wio-E5.

Step 12. Copy and paste the previously obtained information from step 8 into DevEUI and AppEUI fields. End device ID field will be automatically
filled when we fill DevEUI. For AppKey field, use: 2B7E151628AED2A6ABF7158809CF4F3C.

Finally click Register end device.

Step 14. Go back to the application page and navigate to End devices, select the created device and click Live data.
Here you will see the data displayed in real-time!

## [SenseCAP S2105 Sensors](https://github.com/OUSmartInfrastructure/LORAWAN/blob/main/SenseCAP%20Sensors)

<img width="604" alt="SenseCAP S2105 Sensor" src="https://github.com/OUSmartInfrastructure/LORAWAN/assets/33726869/011916bf-f523-4bb8-8e74-5d584ccab251">

#Product Details
Product Name: SenseCAP S2105 - LoRaWAN Soil Moisture, Temperature and EC Sensor
Product description: LoRaWAN Soil Moisture, Temperature, and EC Sensor, SenseCAP S2105. An IP66 wireless soil moisture, temperature, and EC 
sensor that runs on batteries. Its measurement ranges are 0 ~ 100% (m³/m³), -40 ~ 80℃, and 0 to 23 dS/m. It also has built-in Bluetooth and APP 
service for remote device management and OTA configuration.

#Getting Started
Download the SenseCAP Mate app from appstore or playstore
You can also create an account via the SenseCAP Portal: http://sensecap.seeed.cc
LED indicator on the Sensor Node and its status


Actions, Description and Green LED Status

Actions -> Description: First power up, press and hold for 3s -> Power on and activate the Bluetooth.

Green LED Status: LED flashes at 1s frequency, waiting for Bluetooth connection. If Bluetooth not connected within1 minute, the machine would shut down again.

Actions -> Description: Press once -> Reboot device and join LoRa network	

Green LED Status:

1. The LED will be on for 5 seconds for initialization 

2. Waiting for join LoRa network: breathing light flashing 

3. Join LoRa network success: LED flashes fast for 2s 

4. LoRa network join failure: LED suddenly stop.

Actions -> Description: Press and hold for 3s -> Activate Bluetooth again	

Green LED Status:

1. Waiting for Bluetooth connection: LED flashes at 1s frequency 

2. Enter configuration mode after Bluetooth connection is successful: LED flashes at 2s frequency If Bluetooth is not connected within1 minute, the device will reboot and join LoRa network.

Actions -> Description: Press and hold for 9s -> Power off	

Green LED Status:

In the 3rd seconds will start flashing at 1s frequency, until the light is steady on, release the button, the light will go out.

Download the App and connect to the APP

Hold down the button for three seconds, and the LED will flash once per second. If you don't use the app to connect the sensor within a minute, the device will restart or turn off.

Navigate to Users and select Device Bluetooth Configuration, choose "S210X Sensor," which includes products from the S210X series. To enable Bluetooth on the sensor click the "Setup" and 
"Advanced Configuration" buttons. Then, click "Scan" to begin the Bluetooth scanning process. (or) you can use the camera to scan the QR code on the sensor to bind the device.

Choose the Sensor using its S/N (found on the label on the front of the sensor). After logging in, the sensor's basic data will be presented.

After a successful Bluetooth connection, enter setup mode: LED flashes for two seconds.

# Downloading the SenseCAP APP and Configuring Parameters

Bind the device

Click add device and scan the QR code on the device to bind the device to your account.

Once you download the app open it and press the button on sensor and hold for 3 seconds, the LED will flash at 1s frequency.

Click on setup and Advanced Configuration to configure the sensor via bluetooth and click scan to find for available devices.

Select the sensor by S/N lable which you can find on the box

Choose the platform, I am using The Things Network. If you want to use SenseCAP for Things Network It must be used with SenseCAP Outdoor Gateway.

Choose the frequency plan for US choose US915.

Set the interval wake up the device and collect information for certain period of time. For example, the device collects and uploads data every 60 minutes by default.

The SenseCAP portal has a limit on uplink interval: minimum interval is 5 minutes. The interval using the other platforms ranges from 1 to 1440 minutes.

Choose the packet policy you have 3 options

2C+1N (default): 2C+1N (2 confirm packets and 1 none-confirm) is the best strategy, the mode can minimize the packet loss rate, however the device will consume the most data packet in TTN, 
or date credits in Helium network 

1C: 1C (1 confirm) the device will sleep after get 1 received confirm packet from server.

1N: 1N (1 none-confirm) the device only send packet and then start to sleep, no matter the server received the data or not.

Choose the activation type the OTAA is the default option. Over The Air Activation, it joins the network throughDevice EUI, App EUI, and App Key. You can also use 
ABP Activation By Personalization, it joins the network through DevAddr, NwkSkey, and AppSkey.

If you want to connect to The Things Network
Please refer to this manual:
https://files.seeedstudio.com/products/SenseCAP/S210X/How%20to%20Connect%20SenseCAP%20S210X%20to%20The%20Things%20Network.pdf

We need to follow same procees as we did for the Lora-E5
Navigate to THE THINGS NETWORK -> Applications -> Create Application -> Register End Device -> Enter brand name(SenseCAP) -> Model - S2105 -> Profile(region) - US_902_928
Choose Frequency plan, I am using US 902-928 MHz, FSB (used by TTN)
Enter the details Join EUI/ App EUI which you can find in the Sense CAP App and even on the box.

## [Connecting to DataCake to display sensor data](https://github.com/OUSmartInfrastructure/LORAWAN/blob/main/Data%20Cake)

![Data Cake Platform](https://github.com/OUSmartInfrastructure/LORAWAN/assets/33726869/a7a670a1-4bf5-491a-9c75-932b25bbe4ef)
![Sensor Dashboard](https://github.com/OUSmartInfrastructure/LORAWAN/assets/33726869/a11ae197-bb62-480e-a62e-8494057db712)

Website Name: DATACAKE
First you need to have your gateways and applications configured in THE THINGS NETWORK
Go to Datacake and create a new account, creating account is free.
Once you login you will see your workspace there will be no devices on your workspace
To add a device click the + Add Device button 
Here you need to select your device and model
My manifacturer is Seeed and the device I am using is SenseCAP S2105 Sensor
Click next, now select the network I am using THE THINGS NETWORK, If you are using any other network you can select the network you are using
Now, enter the DEV EUI (DEV EUI of your sensor or application) and give a name to your device
Click next, basically this DATACAKE supports upto 5 free devices, so select on free when it asks for payment options
Now we can see the dashboard but the misiing thing is the data that is sent from device, so now we need to bring that on DATACAKE
First, we need to create a token in DATACAKE which we can use in THE THINGS NETWORK 
To create a token go to members section on the sidebar, Click on API usres and create a API user by clicking on Add API User
Give a name for your token and click on Add permission for all Devices in Workspace and now check mark the can record measurements option
This means the token is allowed to record data on your device
Click save and your token is created
Now, copy the token and go to THE THINGS NETWORK on the side bar click on the integrations section
Click on Weebhooks option and click on + Add Webhook
Now select DATACAKE and give an ID and paste the token you copied and click on create datacake webhook
It is pending because no data has been forwarded
Go to DATACAKE website and send a data packet from your device now you will see the data on the dashboard
In DATACAKE we also have a Debug section to troubleshoot the integration it tells us what is going to on
In DATACAKE there is also an option to send downlinks from datacake to the device to configure things like transmission intervals
But, right now the configuration has not been done to send downlinks to device
To enable downlinks go to configuration section and scroll down until you find the LoRaWAN section
Here you can see the downlinks are not configured, to do that click on change
Now, enter the Dev ID which can be found in THE THINGS NETWORK, now we need to enter the server url which is the url from THE THINGS NETWORK
but copy only the first element for ex copy us1.cloud.thethings.network
Now we need to provide TTN Application Id which can be found in the Overview of the application in THE THINGS NETWORK
Now we need to create an API key, this step is to authenticate DATACAKE to your devices
Go to TTN, on side click on API keys and create one, give it a name and select Grant all current and future rights and click on create API key
Now you need to copy the API key which you can do only once, Once you click I have copied the key, you can't access the key again
So make sure you copy the key correctly
Go back to datacake and paste the key and click update and now we are set to send the downlinks.

