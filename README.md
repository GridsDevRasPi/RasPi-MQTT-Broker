# RasPi-MQTT-Broker
RaspberryPi4 B install MQTT 

อ้างอิงจาก https://mqtt.org/

**ติดตั้ง**
~~~
$ sudo apt update
$ sudo apt full-upgrade
$ sudo apt install mosquitto mosquitto-clients
~~~

**กำหนดค่าเริ่มต้น**
~~~
$ sudo systemctl enable mosquitto
~~~

**เปิดใช้งาน**
~~~
$ sudo systemctl status mosquitto
~~~

**subscript**
~~~
$ mosquitto_sub -h localhost -t "mqtt/pimylifeup"
~~~

**publish**
~~~
$ mosquitto_pub -h localhost -t "mqtt/pimylifeup" -m "Hello world"
~~~

**ผลลัพธ์**
~~~
Hello world
~~~

update 28 May 2021

Identify Raspberry Pi บน Network
