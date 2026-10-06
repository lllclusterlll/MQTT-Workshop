# MQTT Workshop

รายการซอฟต์แวร์ประกอบการอบรมการประยุกต์ใช้โปรโตคอล MQTT สำหรับการพัฒนาแอปพลิเคชันมอนิเตอร์ระบบ ซอฟต์แวร์ทั้งหมดติดตั้ง ทดสอบ และใช้งานกับระบบปฏิบัติการ Windows 10 หรือ Windows 11 เท่านั้น หากใช้ระบบปฏิบัติการอื่น อาจใช้งานได้เพียงบางซอฟต์แวร์

## MQTT Broker

ทดสอบใช้งาน MQTT Broker แบบสาธารณะที่นี่ <https://test.mosquitto.org>

## MQTTBox

ติดตั้ง MQTTBox ผ่าน Microsoft Store ด้วยลิงก์ดังนี้ <https://www.microsoft.com/store/productId/9NBLGGH55JZG?ocid=pdpshare>

## Docker

ติดตั้ง Docker Desktop for Windows ด้วยลิงก์ดังนี้ <https://docs.docker.com/desktop/setup/install/windows-install>

### Working Directory

เปิด Command Prompt หรือ Windows PowerShell ที่โฟลเดอร์ราก (root) ของโปรเจกต์นี้ แล้วรันคำสั่ง Docker ทั้งหมดจากตำแหน่งนี้ ข้อมูลของแต่ละ Container จะถูกเก็บไว้ในโฟลเดอร์ `./workspace/` ซึ่งถูกกำหนดให้ Git ไม่ติดตาม (ignore)

### Start Container

การสร้างและเริ่มต้นใช้งาน Container ใน Docker (Computer ต้องเชื่อมต่อกับ Internet) ด้วย Command Prompt หรือ Windows PowerShell ด้วยคำสั่งดังนี้

```bash
docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

### Stop Container

คำสั่งสร้าง Container ในเอกสารนี้ทำงานอยู่ใน Terminal (ไม่ใช้ `-d`) กด `Ctrl + C` เพื่อหยุดการทำงาน และ Container จะถูกลบอัตโนมัติ (`--rm`) โดยข้อมูลยังคงอยู่ในโฟลเดอร์ `./workspace/` หากต้องการรันหลาย Container พร้อมกัน ให้เปิด Terminal แยกต่อ 1 Container

หรือหยุดการทำงาน Container ใน Docker ด้วย Command Prompt หรือ Windows PowerShell โดยการระบุ ID หรือชื่อของ Container ด้วยคำสั่งดังนี้

```bash
docker stop <container-id | container-name>
```

### User/Password

ค่า User/Password ของแต่ละ Application ระบุไว้ในหัวข้อของ Application นั้น ใช้สำหรับการอบรมเท่านั้น ห้ามนำไปใช้กับระบบจริง

### การเชื่อมต่อระหว่าง Container

แต่ละ Container เปิดพอร์ตผ่านเครื่อง Host (`-p`) จึงเชื่อมต่อกันได้ด้วย `<host-ip>:<port>` หรือ `host.docker.internal:<port>` (Docker Desktop) ไม่ใช้ `localhost` เพราะภายใน Container จะหมายถึงตัว Container เอง

## Node-RED

สร้างและเริ่มต้นใช้งาน Container ของ Node-RED ด้วยคำสั่งดังนี้

```bash
docker run --rm --name my-node-red -e TZ=Asia/Bangkok -p 1880:1880 -v ./workspace/node-red:/data nodered/node-red:5.0
```

เปิดใช้งานที่ <http://localhost:1880> ค่าเริ่มต้นไม่มี User/Password (ไม่ต้องล็อกอิน)

หมายเหตุ คู่มือการติดตั้งฉบับสมบูรณ์ที่นี่ <https://nodered.org/docs/getting-started/docker>

## EMQX

สร้างและเริ่มต้นใช้งาน Container ของ EMQX ด้วยคำสั่งดังนี้

```bash
docker run --rm --name my-emqx -e TZ=Asia/Bangkok -p 18083:18083 -p 1883:1883 -v ./workspace/emqx:/opt/emqx/data emqx/emqx:6.3
```

เปิดใช้งาน Dashboard ที่ <http://localhost:18083> ค่าเริ่มต้น User: `admin` Password: `public` (ระบบจะให้เปลี่ยน Password เมื่อล็อกอินครั้งแรก) และ MQTT Broker ใช้พอร์ต `1883`

หมายเหตุ คู่มือการติดตั้งฉบับสมบูรณ์ที่นี่ <https://docs.emqx.com/en/emqx/latest/get-started/deploy/install-docker.html>

## Grafana

สร้างและเริ่มต้นใช้งาน Container ของ Grafana ด้วยคำสั่งดังนี้

```bash
docker run --rm --name my-grafana -e TZ=Asia/Bangkok -p 3000:3000 -v ./workspace/grafana:/var/lib/grafana grafana/grafana:13.2
```

เปิดใช้งานที่ <http://localhost:3000> ค่าเริ่มต้น User: `admin` Password: `admin` (ระบบจะให้เปลี่ยน Password เมื่อล็อกอินครั้งแรก)

หมายเหตุ คู่มือการติดตั้งฉบับสมบูรณ์ที่นี่ <https://grafana.com/docs/grafana/latest/setup-grafana/installation/docker/>

## TimescaleDB

สร้างและเริ่มต้นใช้งาน Container ของ TimescaleDB ด้วยคำสั่งดังนี้

```bash
docker run --rm --name my-timescaledb -e TZ=Asia/Bangkok -e POSTGRES_PASSWORD=password -p 5432:5432 -v ./workspace/timescaledb:/var/lib/postgresql/data timescale/timescaledb:2.30.2-pg17
```

เชื่อมต่อที่ `localhost:5432` ด้วย User: `postgres` Password: `password` (กำหนดจาก `POSTGRES_PASSWORD` ในคำสั่ง) และ Database: `postgres`

หมายเหตุ คู่มือการติดตั้งฉบับสมบูรณ์ที่นี่ <https://www.tigerdata.com/docs/get-started/choose-your-path/install-timescaledb>

## pgAdmin

สร้างและเริ่มต้นใช้งาน Container ของ pgAdmin ด้วยคำสั่งดังนี้

```bash
docker run --rm --name my-pgadmin -e TZ=Asia/Bangkok -e PGADMIN_DEFAULT_EMAIL=admin@example.com -e PGADMIN_DEFAULT_PASSWORD=password -p 5050:80 -v ./workspace/pgadmin:/var/lib/pgadmin dpage/pgadmin4:9.18
```

เปิดใช้งานที่ <http://localhost:5050> ล็อกอินด้วย Email: `admin@example.com` Password: `password` (กำหนดจาก `PGADMIN_DEFAULT_EMAIL` และ `PGADMIN_DEFAULT_PASSWORD` ในคำสั่ง) และเชื่อมต่อกับ TimescaleDB ด้วย Host เป็น `host.docker.internal` และ Port เป็น `5432`

หมายเหตุ คู่มือการติดตั้งฉบับสมบูรณ์ที่นี่ <https://www.pgadmin.org/docs/pgadmin4/latest/container_deployment.html>
