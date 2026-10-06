# MQTT Workshop

รายการซอฟต์แวร์ประกอบการอบรมการประยุกต์ใช้โปรโตคอล MQTT สำหรับการพัฒนาแอปพลิเคชันมอนิเตอร์ระบบ ซอฟต์แวร์ทั้งหมดติดตั้ง ทดสอบ และใช้งานกับระบบปฏิบัติการ Windows 10 หรือ Windows 11 เท่านั้น หากใช้ระบบปฏิบัติการอื่น อาจใช้งานได้เพียงบางซอฟต์แวร์

## MQTT Broker

ทดสอบใช้งาน MQTT Broker แบบสาธารณะที่นี่ <https://test.mosquitto.org>

## MQTTBox

ติดตั้ง MQTTBox ผ่าน Microsoft Store ด้วยลิงก์ดังนี้ <https://www.microsoft.com/store/productId/9NBLGGH55JZG?ocid=pdpshare>

## Docker

ติดตั้ง Docker Desktop for Windows ด้วยลิงก์ดังนี้ <https://docs.docker.com/desktop/setup/install/windows-install>

### Start Container

การสร้างและเริ่มต้นใช้งาน Container ใน Docker (Computer ต้องเชื่อมต่อกับ Internet) ด้วย Command Prompt หรือ Windows PowerShell ด้วยคำสั่งดังนี้

```bash
docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

### Stop Container

หยุดการทำงาน Container ใน Docker ด้วย Command Prompt หรือ Windows PowerShell โดยการระบุ ID หรือชื่อของ Container ด้วยคำสั่งดังนี้

```bash
docker stop <container-id | container-name>
```

### การเชื่อมต่อระหว่าง Container

แต่ละ Container เปิดพอร์ตผ่านเครื่อง Host (`-p`) จึงเชื่อมต่อกันได้ด้วย `<host-ip>:<port>` หรือ `host.docker.internal:<port>` (Docker Desktop) ไม่ใช้ `localhost` เพราะภายใน Container จะหมายถึงตัว Container เอง

## Node-RED

สร้างและเริ่มต้นใช้งาน Container ของ Node-RED ด้วยคำสั่งดังนี้

```bash
docker run -d --name my-node-red -e TZ=Asia/Bangkok -p 1880:1880 -v my-node-red-data:/data nodered/node-red:5.0.7
```

หมายเหตุ คู่มือการติดตั้งฉบับสมบูรณ์ที่นี่ <https://nodered.org/docs/getting-started/docker>

## EMQX

สร้างและเริ่มต้นใช้งาน Container ของ EMQX ด้วยคำสั่งดังนี้

```bash
docker run -d --name my-emqx -e TZ=Asia/Bangkok -p 18083:18083 -p 1883:1883 -v my-emqx-data:/opt/emqx/data emqx/emqx:6.3
```

หมายเหตุ คู่มือการติดตั้งฉบับสมบูรณ์ที่นี่ <https://docs.emqx.com/en/emqx/latest/get-started/deploy/install-docker.html>

## Grafana

สร้างและเริ่มต้นใช้งาน Container ของ Grafana ด้วยคำสั่งดังนี้

```bash
docker run -d --name my-grafana -e TZ=Asia/Bangkok -p 3000:3000 -v my-grafana-data:/var/lib/grafana grafana/grafana:13.2.3
```

หมายเหตุ คู่มือการติดตั้งฉบับสมบูรณ์ที่นี่ <https://grafana.com/docs/grafana/latest/setup-grafana/installation/docker/>

## TimescaleDB

สร้างและเริ่มต้นใช้งาน Container ของ TimescaleDB ด้วยคำสั่งดังนี้

```bash
docker run -d --name my-timescaledb -e TZ=Asia/Bangkok -e POSTGRES_PASSWORD=password -p 5432:5432 -v my-timescaledb-data:/var/lib/postgresql/data timescale/timescaledb:2.30.2-pg17
```

หมายเหตุ คู่มือการติดตั้งฉบับสมบูรณ์ที่นี่ <https://www.tigerdata.com/docs/get-started/choose-your-path/install-timescaledb>

## pgAdmin

สร้างและเริ่มต้นใช้งาน Container ของ pgAdmin ด้วยคำสั่งดังนี้

```bash
docker run -d --name my-pgadmin -e TZ=Asia/Bangkok -e PGADMIN_DEFAULT_EMAIL=admin@example.com -e PGADMIN_DEFAULT_PASSWORD=password -p 5050:80 -v my-pgadmin-data:/var/lib/pgadmin dpage/pgadmin4:9.18
```

เปิดใช้งานที่ <http://localhost:5050> และเชื่อมต่อกับ TimescaleDB ด้วย Host เป็น `host.docker.internal` และ Port เป็น `5432`

หมายเหตุ คู่มือการติดตั้งฉบับสมบูรณ์ที่นี่ <https://www.pgadmin.org/docs/pgadmin4/latest/container_deployment.html>
