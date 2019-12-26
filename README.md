# m5stack-freertos-tft

TFT demo for Amazon FreeRTOS on M5Stack

Requir ESP-IDF development environment.



### Run

Check out this repo.

```
git clone https://github.com/fukuen/m5stack-freertos-tft --recursive
```

Set or copy Wi-Fi infos.


Build (Windows example)

```
cmake -DCMAKE_TOOLCHAIN_FILE=amazon-freertos/tools/cmake/toolchains/xtensa-esp32.cmake -GNinja -S . -B build
cd build
ninja
```

Flash and monitor

```
idf.py flash monitor
```

### Todo

 - sntp (not implemented yet)
