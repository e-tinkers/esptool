## Why this fork
If you have a Mac running older version of macOS High Sierra, and if you upgrade fom ESP32 Arudino Core 1.0.6 to 2.0.0 or above, ESP32 will refuse to compile your code because esptool which is an open source tool that ESP32 is used to upload the code to the ESP32 board is build with github CI Actions which is based on macOS10.15. The issue is documented [here](https://github.com/espressif/arduino-esp32/issues/5639) and is flagged as "Wontfix". So the only way to solve this is to compile the esptool yourself and replace the one installed on your computer. This need to be done each time the Arduino Core is updated because it could overrided the version you replaced.

## How to compile your own esptool
You need to have:
- python 3 installed in your computer;
- `pyserial` installed in your computer, if not, run `pip3 install pyserial` to install it;
- `pyinstaller` installed in your computer, if not, run `pip install -Iv pyinstaller==4.3`;
- Clone this repo or [official esptool](https://github.com/espressif/esp-idf/tree/1cb31e50943bb757966ca91ed7f4852692a5b0ed/examples/common_components/led_strip) repo.
- Make a build directory (i.e. this directory) with `cd esptool && mkdir esptool_py && cd esptool_py`;
- Build the esptool binary with `pyinstaller --onefile ../esptool.py`;
- Copy our version of `esptool` and replace the original binary.

```
mv /Users/${USER}/Library/Arduino15/packages/esp32/tools/esptool_py/3.x.x/esptool /Users/${USER}/Library/Arduino15/packages/esp32/tools/esptool_py/3.1.0/esptool_broken
cp dist/esptool /Users/${USER}/Library/Arduino15/packages/esp32/tools/esptool_py/3.x.x/
```

