```py
wifi = pywifi.PyWiFi()
iface = wifi.interfaces()[0]
iface.scan()
time.sleep(5)
wifis= iface.scan_results()
for i in wifis:
    print(i.ssid)
```

### wifi状态：

```py
iface.status()
```



