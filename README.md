# Strikelink - WiFi SIXFOUR Modem

A virtual WiFi modem based on the ESP8266, designed to get your Commodore 64 (or other retro computers) online via Telnet. This firmware emulates a Hayes modem, bridging your retro hardware's serial connection to the modern internet.

## Features
- **Hayes AT Command Set**: Emulates standard modem commands (ATDT, ATH, etc.).
- **Telnet Support**: Connect to BBSs and Telnet servers.
- **PETSCII Translation**: Native translation for C64 compatibility.
- **Web Config & Status**: Simple status page served over HTTP.
- **Phonebook**: Storage for 10 speed dial numbers in EEPROM.
- **Flash Protection**: Optimized to reduce ESP8266 flash memory wear.
- **Safe & Secure**: 
  - Credentials are stored in EEPROM, not hardcoded.
  - Memory optimizations (`F()` macro) for better stability.

## Hardware Requirements
- **ESP8266**: Designed for devices like the Sparkfun ESP8266 WiFi Shield, but compatible with generic ESP8266 modules (NodeMCU, D1 Mini) with appropriate level shifting (3.3V <-> 5V) for your retro computer.

## Installation
1. Install [Arduino IDE](https://www.arduino.cc/en/software).
2. Install **ESP8266 Board Support** in Arduino IDE (Boards Manager).
3. Open the `strikelink` file in this repository.
4. Select your generic ESP8266 board.
5. Click **Upload**.

## Configuration
**Important**: WiFi credentials are NOT hardcoded. You must configure them via serial terminal.

1. Connect your computer to the ESP8266 via USB/Serial (Default Baud: **300**).
   *Note: If 300 is too slow for your terminal, you can hold the generic button (GPIO0) for 5 seconds to reset baud, or modify the source.*
2. Enter the following commands to set up WiFi:
   ```
   AT$SSID=YourWiFiName
   AT$PASS=YourWiFiPassword
   AT&W
   ```
   *(The `AT&W` command saves these settings to non-volatile EEPROM)*
3. Use `ATC1` to connect immediately, or reset the board.

## Common Commands
| Command | Description |
|Args|---|
| `AT?` | Show Help |
| `ATDT<host>:<port>` | Dial a specific address (e.g., `ATDTbbs.fozztexx.com:23`) |
| `ATDS<0-9>` | Speed dial stored number |
| `AT&Z<0-9>=<host>:<port>` | Store speed dial number |
| `ATI` | Show Network/WiFi Status |
| `ATC0` / `ATC1` | WiFi Disconnect / Connect |
| `AT&W` | Save settings to EEPROM |
| `AT&F` | Factory Reset |

## Credits
Strikelink modifications by C. Mack (2023).
Optimizations and Fixes by Antigravity (2025).

Based on:
- **WiFi SIXFOUR** by Paul Rickards (2016)
- **ESP8266 based virtual modem** by Jussi Salin (2016)