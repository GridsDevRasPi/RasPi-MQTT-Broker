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

**ทดสอบ subscript & publish ภายในตัว Raspberry Pi**

คำสั่ง subscript & publish

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

### การเชื่อมต่อกับอุปกรณ์ Windows กับ Raspberry Pi

**ติดตั้ง MQTT บน Windows**

สำหรับ Windows สามารถ Download โปรแกรมจากเว็บ [mosquitto.org](https://mosquitto.org/download/)

**Tip** : คุณสามารถดูวิธีการติดตั้ง MQTT Server ได้จาก **[[ที่นี่](https://www.youtube.com/watch?v=tzAVwksEEfY)]**

**Identify Raspberry Pi บน Network (บน Raspberry Pi)**

ไคลเอ็นต์ MQTT จำเป็นที่จะต้องทราบว่ามันอยู่ในเครือข่ายใด ไคลเอ็นต์ MQTT ต้องมีชื่อโฮสต์หรือที่อยู่ IP ทุกครั้งที่คุณ sup หรือ pub ข้อความ

**NOTE** ค้นหาชื่อโฮสต์บน Pi โดยพิมพ์

~~~
$ hostname
~~~

หากมี Raspberry Pi มากกว่า 1 เครื่องในเครือข่ายของฉัน อาจจะใช้ชื่อ mqtt-server หรือชื่ออื่นเพื่อทำให้มันไม่เหมือนใคร วิธีที่ง่ายที่สุดคือผ่าน `sudo raspi-config` แต่ต้องรีบูต

หรือคุณสามารถใช้ที่อยู่ IP ของ Raspberry Pi แทนชื่อโฮสต์ได้ตลอดเวลา โยใช้คำสั่งนี้

~~~
$ ifconfig | grep inet | grep cast
~~~

**การ Subscribe to the Topic จากระยะไกล**

~~~
$ mosquitto_sub -h raspberrypi -t "test/message"
~~~

หรือ

~~~
$ mosquitto_sub -h 192.168.1.17 -t "test/message" 
~~~

**NOTE** : 192.168.1.17 เป็น IP ที่ใช้ในครั้งนี้เท่านั้น ถ้าต้องการ fix ip ก็ทำได้ แต่ในกรณีผมไม่ได้ fix

**การ Publish ข้อความทดสอบจากระยะไกล**

~~~
$ mosquitto_pub -h raspberrypi -t "test/message" -m "Hello from remote"
~~~

**ทดสอบ Subscribe และ Publish จาก Windows to RaspberryPi**

ใน Raspberry Pi ผม run service ด้วยคำสั่ง

~~~
$ sudo systemctl status mosquitto
~~~

จากนั้น ผมกำหนดให้ raspberry Subscribe topic ที่มีชื่อว่า test/message และรอรับข้อความ Publish

~~~
$ mosquitto_sub -h 192.168.1.17 -t "test/message"
~~~

ใน Windows เปิด cmd โดย Run as Administrator 

~~~
$ cd\

$ cd "Program Files"/mosquitto

$ net start mosquitto
~~~

**Tip** : ในกรณีที่ run service ไว้แล้วไม่ต้อง run ใหม่นะครับ

จากนั้นผมจะทำการ Publish ข้อความ "Hello from remote" ไปที่ topic "test/message"

~~~
$ mosquitto_pub -h 192.168.1.17 -t "test/message" -m "Hello from remote"
~~~

**ผลลัพธ์จะปรากฎขึ้นที่ Raspberry Pi ดังนี้**
~~~
Hello from remote
~~~

**NOTE** : สามารถดูตัวอย่างการใช้งานที่ผมเคยทำไว้แล้วได้ **[[ที่นี่](https://www.youtube.com/watch?v=we_bRC2Z_-I&t=71s)]**

update 9 Jun 2021

