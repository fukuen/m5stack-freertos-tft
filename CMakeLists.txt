cmake_minimum_required(VERSION 3.13)

project(freertos-ex)

add_definitions(-DCONFIG_SPIFFS_BASE_ADDR=180000)
add_definitions(-DCONFIG_SPIFFS_SIZE=1048576)
add_definitions(-DCONFIG_SPIFFS_LOG_BLOCK_SIZE=8192)
add_definitions(-DCONFIG_SPIFFS_LOG_PAGE_SIZE=256)
add_definitions(-DCONFIG_EXAMPLE_DISPLAY_TYPE=3)
add_definitions(-DCONFIG_EXAMPLE_USE_WIFI=true)

add_executable(freertos-ex src/tft_demo.c
  ESP32_TFT_library/components/tft/comic24.c
  ESP32_TFT_library/components/tft/def_small.c
  ESP32_TFT_library/components/tft/DefaultFont.c
  ESP32_TFT_library/components/tft/DejaVuSans18.c
  ESP32_TFT_library/components/tft/DejaVuSans24.c
  ESP32_TFT_library/components/tft/minya24.c
  ESP32_TFT_library/components/tft/SmallFont.c
  ESP32_TFT_library/components/tft/tft.c
  ESP32_TFT_library/components/tft/tftspi.c
  ESP32_TFT_library/components/tft/tooney32.c
  ESP32_TFT_library/components/tft/Ubuntu16.c
  ESP32_TFT_library/components/spiffs/esp_spiffs.c
  ESP32_TFT_library/components/spiffs/list.c
  ESP32_TFT_library/components/spiffs/mutex.c
  ESP32_TFT_library/components/spiffs/spiffs_cache.c
  ESP32_TFT_library/components/spiffs/spiffs_check.c
  ESP32_TFT_library/components/spiffs/spiffs_gc.c
  ESP32_TFT_library/components/spiffs/spiffs_hydrogen.c
  ESP32_TFT_library/components/spiffs/spiffs_nucleus.c
  ESP32_TFT_library/components/spiffs/spiffs_vfs.c
  ESP32_TFT_library/components/spidriver/spi_master_lobo.c
  amazon-freertos/demos/demo_runner/aws_demo_network_addr.c
  amazon-freertos/demos/network_manager/aws_iot_network_manager.c
 )
target_include_directories(freertos-ex
  PUBLIC
  ESP32_TFT_library/components/tft
  ESP32_TFT_library/components/spiffs
  ESP32_TFT_library/components/spidriver
  amazon-freertos/libraries/c_sdk/standard/https/include
  amazon-freertos/demos/include
  amazon-freertos/demos/network_manager
  amazon-freertos/libraries/freertos_plus/standard/utils/include
)

# Tell IDF build to link against this target.
set(IDF_PROJECT_EXECUTABLE freertos-ex)

# Add amazon freertos as a subdirectory. AFR_BOARD tells which board to target.
set(AFR_BOARD espressif.esp32_wrover_kit CACHE INTERNAL "")
add_subdirectory("amazon-freertos")

# Link against the mqtt library so that we can use it. Dependencies
# linked.
target_link_libraries(freertos-ex PRIVATE AFR::mqtt AFR::wifi AFR::https)
