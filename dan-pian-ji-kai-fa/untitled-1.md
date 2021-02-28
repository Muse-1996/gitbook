# Untitled

1. 下载固件 [地址](https://micropython.org/download/esp32/)
2. 安装esptool

```bash
pip install esptool
```

> 连接esp32，并获取端口 /dev/cu.SLAB\_USBtoUART

![](../.gitbook/assets/image%20%2817%29.png)

3. 擦除Flash

```text
esptool.py --port /dev/cu.SLAB_USBtoUART erase_flash
-----------------------------------------------------
esptool.py v3.0
Serial port /dev/cu.SLAB_USBtoUART
Connecting........___
Detecting chip type... ESP32
Chip is ESP32-D0WDQ6 (revision 1)
Features: WiFi, BT, Dual Core, 240MHz, VRef calibration in efuse, Coding Scheme None
Crystal is 40MHz
MAC: 24:6f:28:b2:d4:dc
Uploading stub...
Running stub...
Stub running...
Erasing flash (this may take a while)...
Chip erase completed successfully in 9.5s
Hard resetting via RTS pin...
```

4. 写入固件

```text
esptool.py --chip esp32 --port /dev/cu.SLAB_USBtoUART write_flash -z  0x1000 esp32-idf4-20210202-v1.14.bin
--------------------------------------------------
esptool.py v3.0
Serial port /dev/cu.SLAB_USBtoUART
Connecting........__
Detecting chip type... ESP32
Chip is ESP32-D0WDQ6 (revision 1)
Features: WiFi, BT, Dual Core, 240MHz, VRef calibration in efuse, Coding Scheme None
Crystal is 40MHz
MAC: 24:6f:28:b2:d4:dc
Uploading stub...
Running stub...
Stub running...
Changing baud rate to 460800
Changed.
Configuring flash size...
Auto-detected Flash size: 4MB
Compressed 1484624 bytes to 951640...
Wrote 1484624 bytes (951640 compressed) at 0x00000000 in 22.1 seconds (effective 537.2 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...
```

固件刷入后开启webrepl

```text
# 开启一个名为Monster-Python的热点
import network
ap = network.WLAN(network.AP_IF) 
ap.active(True)
ap.config(essid='Monster-Python')

# 初始化webrepl 这一步根据提示 E开启自启 n不重启
import webrepl_setup
# 开启webrepl的服务:
import webrepl
webrepl.start()
```

start\(\)之后会给一个ws连接地址，打开[该地址](http://micropython.org/webrepl/#192.168.4.1:8266/)进行连接

```python
# main.py
import network

def HotAP():
	ap = network.WLAN(network.AP_IF)
    ap.active(True)
    ap.config(essid='Monster-Python',authmode=network.AUTH_WPA_WPA2_PSK, password="pynbpynb") # set the ESSID of the access point


HotAP()
```

![](../.gitbook/assets/image%20%2816%29.png)

