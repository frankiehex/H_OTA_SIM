# H_OTA_SIM — HuiFlow 洗車機模擬板 OTA 倉庫

模擬板（`frankiehex/huiflow_washer_sim_esp32`）online OTA 的 manifest + firmware 來源。

## URLs

- Manifest: https://raw.githubusercontent.com/frankiehex/H_OTA_SIM/main/manifest.json
- Firmware: https://raw.githubusercontent.com/frankiehex/H_OTA_SIM/main/firmware.ota.bin

模擬板每次開機 8 秒後檢查 manifest，若 `version` 與韌體內建 `SIM_FIRMWARE_VER` 不同則下載並 OTA。

## 發布新版本

```bash
cd /Users/f/huiflow_washer_sim_esp32
# 1. 修改版本號：iot-washer-sim-base.yaml substitutions.SIM_FIRMWARE_VER
# 2. 編譯
esphome compile iot-washer-sim-base.yaml
# 3. 拷 binary + 更新 manifest
cp .esphome/build/iot-washer-sim/.pioenvs/iot-washer-sim/firmware.ota.bin ota/firmware.ota.bin
# 4. 更新 ota/manifest.json 的 version
# 5. 同步到 H_OTA_SIM repo
cp ota/firmware.ota.bin /Users/f/H_OTA_SIM/
cp ota/manifest.json /Users/f/H_OTA_SIM/
cd /Users/f/H_OTA_SIM
git add . && git commit -m "release: vX.Y.Z" && git push
```
