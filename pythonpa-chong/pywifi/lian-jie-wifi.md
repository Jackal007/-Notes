### 连接wifi：

```py
 wifi = pywifi.PyWiFi()

    iface = wifi.interfaces()[0]

    iface.disconnect()
    time.sleep(1)

    profile = pywifi.Profile()
    profile.ssid = 'wifi name'
    profile.auth = const.AUTH_ALG_OPEN
    profile.akm.append(const.AKM_TYPE_WPA2PSK)
    profile.cipher = const.CIPHER_TYPE_CCMP
    profile.key = 'password'

    iface.remove_all_network_profiles()
    tmp_profile = iface.add_network_profile(profile)

    iface.connect(tmp_profile)
    time.sleep(40)
    assert iface.status() == const.IFACE_CONNECTED
```

### 断开连接：

```py
    iface.disconnect()
    time.sleep(1)
    assert iface.status() in\
        [const.IFACE_DISCONNECTED, const.IFACE_INACTIVE]
```



