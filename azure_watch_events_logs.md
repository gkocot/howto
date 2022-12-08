## How to watch events in different components
### VRx
```code
./ZreoMq_listener localhost 41001 /usr/local/s2/s2vms/config/EventDefinitions.json
```

### Mediaservice
```code
tail -f /var/snap/mediaservice/current/logs/mediaservice20210414.log | grep payload
```

### azurebridge
```code
sudo tcpdump -i lo udp port 7041 -nvvvX
```

### IoT Hub
In azure portal, go to 's72040-dev-ioth | Message routing'.
Add 'events' built-in endpoint and save/restart IoT service.
```code
az iot hub monitor-events --output table --hub-name s72040-dev-ioth
az iot hub monitor-events --output table --hub-name f5736-int-dev-ioth --device-id 128788
```
In case of CLI error try
```
az extension update --name azure-iot
```

### Service (DeviceEentProcessorFunction)
In azure portal, go to 'deviceeventprocessorfunction-s72040-dev-fapp | Configuration'.
Set 'LOG_TO_STDOUT' to 'true'.
```code
az webapp log tail --name deviceeventprocessorfunction-s72040-dev-fapp --resource-group S72040-dev-rg
```
