## Notes and Issues Encountered

- Make sure to install ESP32 Driver
- Clone the ESP-Rainmaker repository
- Work directory should avoid having spaces or special characters in path name (`idf.py` may complain otherwise)
- Use ESP-IDF terminal to run idf.py

## Hardware Setup

1. Connect a LED to one of the GPIOs of ESP32 (GPIO 4 in this case)
2. Connect ESP32 to the computer
3. Take note of the port of the ESP32 in the computer (`COM3` in my case)

## Software Setup

cd to `example/switch` folder, and make the change to the `./main/app_driver` file, to define the GPIO pin of our LED (pin 4 in our case)

```c
#define OUTPUT_GPIO    4
```

```bash
idf.py set-target esp32 # Set target for build
```

```bash
idf.py build # Build app on rainmaker cloud
```

Flash application on ESP32 and jump into the serial monitor, on port `COM3` and baud rate of `115200`

```bash
idf.py -p COM3 -b 115200 flash monitor
```
Make sure to install ESP Rainmaker app on the phone and scan the QR Code, to register the device with WIFI, the Rainmaker cloud and our application.

We can now use the phone to control the LED on/off.

## Advantages and Disadvantages

Advantages:

1. Fast on-borading, no need to provision own cloud resources
2. No need to write app to control ESP32 from scratch, just write logic for the app, deploy on Rainmaker cloud and mobile app will automatically reflect our changes
3. Free

Disadvantages:

1. No control over our own cloud resources
2. Mobile app may have limited functionalities, unable to create for more specific cases
3. Must use ESP-Rainmaker API which may be limited, cannot really change underlying architecture