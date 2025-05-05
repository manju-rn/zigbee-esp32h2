***Pre-requistes:***
1. Running Z2M  - recommend to have a seperate setup and not your existing production setup as this would require some tinkering. Atleast take a backup if no spare co-ordinator is available
2. Linux & Docker - You can do with windows I guess but not tested.
3. ESP32H2 connected as a serial to System / passthrough to VM, if applicable

***Setup and Install:***
- Step 1:  git clone https://github.com/manju-rn/zigbee-esp32h2.git
- Step 2:  Go into zigbee-esp32h2 and check compose.yaml.  Edit the device to match the device path (Change only the left part - Don't change the right hand side :/dev/ttyACM0)
- Step 3: docker compose up -d idf; docker logs -f idf   The image pull will take a long time, the image size is about 6 GB as this is a ESP IDF SDK
- Step 4:  If the container above is running fine, exec into the container docker exec -it idf sh
- Step 5: Execute . $IDF_PATH/export.sh
- Step 6:  cd project/esp_zigbee_HA_sample/HA_on_off_light
- Step 7:  idf.py set-target esp32h2 build   This will compile the project and generate a bin file in the build directoty
- Step 8:   idf.py flash  This will connect to the serial port and flash the bin to esp32h2
---
The above sample zigbee code will enable the onboard light of esp32h2.
On your Zigbee2MQtt UI - Enable the PermitJoin.  You should see this device show up.  It will show configuration error, but you should still be able to go into "Expose" and toggle the light which is on PIN 10
