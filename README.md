# ElegantOTA for Meshtastic

Run elegantOTA next to meshtastic for OTA updates

## Prerequisites
platformio is installed
esptool is installed
meshtastic client installed

## Getting Started

1. compile elegantOTA demo using `platformio run -e <board>`
Meshtastic boards and variants are added. In platformio.ini heltec-v4 is available and esp32s3. Checkout the meshtastic-fw repo for other boards. 

Example: platformio run -e "heltec_v4"

2. Check the partition table for your board.

esp32s3 = 0x340000
heltec_v4 = 0x650000

In the meshtastic repo the CSV file for the partitions can be found:
https://github.com/meshtastic/firmware/blob/develop/variants/esp32s3/heltec_v4/platformio.ini

```
board_build.partitions = default_16MB.csv
```
https://github.com/espressif/arduino-esp32/blob/master/tools/partitions/default_16MB.csv

3. Run esptool `esptool write-flash  0x650000 .pio/build/heltec_v4/firmware.bin`

### Installing Meshtastic

1. Clone the meshtastic firmware repo
https://github.com/meshtastic/firmware.git

2. Copy meshtastic_patch/src to the meshtastic repo. `cp meshtastic_patch/src firmware/ -r`

3. Edit firmware/userPrefs.jsonc to configure the meshtastic settings. 

4. Upload to the meshtastic firmware to the board.  `platformio run -t upload -e <board>`


### Reboot meshtastic in OTA mode

* How to run the program
`meshtastic --host <ip> --reboot-ota`

ElegantOTA will be available at `http://<ip>/update`

