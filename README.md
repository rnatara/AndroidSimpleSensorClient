# Android Sensor Solace Client

## About
A simple Android Client that connects to Solace Router and publishes some sensor data. The focus of 
this Client is to demonstrate sensor data gathering and communication to Solace router using MQTT.

The client first collects the list of sensor hardware avilable on the phone (Eg: Light sensor, 
pressure sensor,proximity sensor, GPS) and publishes this data on a predefined topic to Solace 
router. After this, when values change on certain sensors, the changed values are published 
on predefined topic to Solace router. 

The client also receives for any responses from the Solace router. For this to work, a backend
server should be publishing on the response topics. This, however is not a requirement and
the sensor client would work without the server.


## Functional Overview
To following components are required to test this client:

1. An Android hardware or an emulator
1. A Solace router (Solace VMR or Appliance)
1. Optionally, a Solace messaging client that listens to published data for verification 
1. Optionally, a backend server that listens and responds to sensor data

![](.README_images/81e8d82a.png)


## Testing
The following steps can be used to verify the Client connectivity to Solace router. Note that
the (optional) backend server setup is not discussed here.

1. Run a subscriber to gather whats being published from the client

This can be done using any tool such as sdkperf. Here Iam using standard Mosquitto client to 
subscribe to all the messages 

```
$ mosquitto_sub -h <solace-router-IP>  -p <mqtt-port> -t '#'  -u default -P <password> –v
```

2. Run the Android Sensor Client.

The application can be deployed on any Android hardware. Here Iam running it on an Android
Emulator from Android Studio.

![](.README_images/96962c43.png)


3.	Enter the Solace VMR/Appliance message interface IP, port, MQTT username, 
password and Connect.  For this demo, Iam using a Solace VMR hosted on Amazon AWS

![](.README_images/589a5d73.png)


4.	The Android client makes a connection to Solace VMR/Appliance and sends its list of 
sensors on predefined topic. The subscriber receives the data and dumps on the screen.

![](.README_images/abf13348.png)

5.	Change some sensor values. If you are using it on a phone move the phone near or away 
from light source to trigger light sensor data. Or you can move your hand close to screen 
to trigger proximity sensor data. Below, on the Android simulator, I changed some sensor 
values using Virtual Sensor Control panel:

![](.README_images/9662e599.png)


6.	You will notice the subscriber receives these via Solace router and dumps the values 
on the screen.

![](.README_images/4c56e933.png)

### **Get Started**

```
git clone https://github.com/SolaceLabs/XXX
cd XXX
./gradlew assemble
cf push
```


## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct, and the process 
for submitting pull requests to us.

## Authors

See the list of [contributors](https://github.com/SolaceLabs/XXX/graphs/contributors) 


## License

This project is licensed under the Apache License, Version 2.0. - 
See the [LICENSE](LICENSE) file for details.

## References
