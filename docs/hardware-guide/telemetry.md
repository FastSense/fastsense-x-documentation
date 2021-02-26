# Telemetry

Telemetry allows you to log temperature information about all the devices presented in the system (CPU and Edge AI devices).

Telemetry services are preinstalled and running as a service routine. You can check it's status via these commands:

```
sudo systemctl status cpu-telemetry.service
sudo systemctl status tpu-telemetry.service
```

All results are saved in real time to the folder `~/.telemetry/`.

Name of file has format (timestamp is a date and time when file was created):
```
device name + timestamp + .csv ( device_YYYY-MM-DD_HH-mm-SS.csv )
```

For example:
```
cpu_2020-05-08_10-55-33.csv 
vpu_2020-05-08_10-55-33.csv 
tpu_2020-05-08_10-55-33.csv
```

Files format is CSV. First line contains names of all columns.

CPU log file example:

```
time,cpu1_temp,cpu1_freq,cpu1_load 
2020-05-08T10:55:34.513,85,2000,100 
2020-05-08T10:55:34.517,84,2000,100
```