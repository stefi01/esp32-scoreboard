# Kickoff

A touchscreen desk for the day's pro football games. It shows the board, a countdown to the next kickoff, one favorite team, and a temperature for a city you pick.

Two boards live in this folder. They are not the same screen. Do not flash one sketch onto the other board. The 7 inch sketch is the Waveshare ESP32-S3-Touch-LCD-7. It is not the Sunton 7 inch.

## 7 inch, Waveshare

Sketch: `kickoff-7inch/kickoff7/kickoff7.ino`

Prefs name is `kick7`. Screen clock `12500000`, bounce `800 * 20`.

Slide the switch to UART1. The cable stays in the socket marked UART. Do not hold BOOT.

The rows below are the ones written for this board in `kickoff-7inch/settings to change.txt`.

| Setting | Value |
| --- | --- |
| Board | ESP32S3 Dev Module |
| PSRAM | OPI PSRAM |
| Flash Size | 16MB |
| USB CDC On Boot | Disabled |
| Partition Scheme | 16M Flash (3MB APP/9.9MB FATFS) |
| Upload Speed | 921600 |
| USB Mode | Hardware CDC and JTAG |
| Upload Mode | UART0 / Hardware CDC |
| CPU Frequency | 240MHz (WiFi) |
| Flash Mode | QIO 80MHz |

Keep that partition. It has the second slot the update writes into.

## 4.3 inch, Freenove FNK0115B

Sketch: `kickoff-43/kickoff43/kickoff43.ino`

The XPT2046 touch files sit beside that sketch. Prefs name is `kick43`. Screen clock `9000000`, bounce `272 * 20`. Use the Type-C port that shows up as CH340.

| Setting | Value |
| --- | --- |
| Board | ESP32S3 Dev Module |
| PSRAM | OPI PSRAM |
| Flash Size | 16MB |
| USB CDC On Boot | Enabled |
| Partition Scheme | 16M Flash (3MB APP/9.9MB FATFS) |

Keep that partition. It has the second slot the update writes into.

## Libraries

GFX Library for Arduino, from the Library Manager. Wi-Fi, HTTP, Preferences, and Update come with the ESP32 board package.

## Updates

Both sketches use one GitHub repo, branch `main`, folder `ota`.

- `https://raw.githubusercontent.com/stefi01/esp32-scoreboard/main/ota/version.txt`
- `https://raw.githubusercontent.com/stefi01/esp32-scoreboard/main/ota/kick_7.bin` for the 7 inch
- `https://raw.githubusercontent.com/stefi01/esp32-scoreboard/main/ota/kick_43.bin` for the 4.3 inch

`version.txt` is one number for both boards. `KICK_VER` in each sketch is `1.0`, and `ota/version.txt` in this folder says `1.0`. **Check for updates** offers **Install** only when the number on GitHub is higher than the one already on the desk. A desk already on that number says newest firmware already installed.

After you compile `kickoff7.ino`, copy that bin to `ota/kick_7.bin`. After you compile `kickoff43.ino`, copy that bin to `ota/kick_43.bin`. When the build changes, raise `KICK_VER` in both sketches and raise `version.txt` to the same number, then upload both bin files. `ota/PUBLISH.txt` is the note for that upload. Do not upload `PUBLISH.txt`.

## What it shows

The buttons along the bottom are BOARD, NEXT, TEMP, TEAM, WIFI, and UPDATE.

- **BOARD** is the day's pro games, read from the public ESPN football scoreboard. You do not type in who is playing. Each game shows the two teams and the score. A game that is on now can show ON NOW on the title line. If Wi-Fi is down, the page says no link yet. If the list is empty, it says no games listed.
- **NEXT** is the countdown to the next kickoff, in days, hours, and minutes. If a game is already on, the page says ON NOW. The clock is hours and minutes. Tap the clock to move the time zone: Pacific, Mountain, Central, Eastern. It starts on Pacific until you change it, and the choice is saved on the desk. The time comes from pool.ntp.org and time.nist.gov after Wi-Fi connects.
- **TEMP** is one city. The list has 156 cities, starting from Fresno. PREV and NEXT move through the list. The card shows the temperature, a short weather word, and the wind. F and C switch the temperature. The reading comes from Open-Meteo.
- **TEAM** is the 32 club abbreviations. Tap one to mark it. Tap it again to clear it. On the board, that club's game is outlined in gold.
- **WIFI** is where you join the network.
- **UPDATE** shows the version and checks GitHub.

It needs 2.4 GHz Wi-Fi and USB power. There is no account.

## Listing

`kickoff-7inch/etsy/` holds example screens for the 7 inch listing, plus `ETSY-LISTING.txt` and `Kickoff-manual.pdf`. The games, scores, and temperature in those pictures are samples. That listing is the 7 inch desk. The 4.3 sketch is not in that listing.
