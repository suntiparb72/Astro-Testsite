---
title: 'Dockerfile'
description: 'Docker file มันทำยังไงกันนะ'
pubDate: 'Nov 15 2023'
heroImage: '/dockerfile.png'
---

dockerfile with Pasertcbs

Customize image for docker 

Dockerfile ตัวแรกเป็นตัวพิมพ์ใหญ่ และถ้าใช้ vscode ให้หา extension docker by Microsoft

เบื้องต้นถ้าจะรันตัว dockerfile ให้ลองรัน image นั้นๆก่อนจะทำการ custom images

สามารถรันได้โดย

```bash
docker run --rm --name banana cloudflare/cloudflared:latest 
tunnel --no-autoupdate --hello-world
```

จริงๆเราสามารถใช้ extension docker ใน vscode เพื่อสามารถ attach shell

แต่ไม่ใช่ทุกตัว จะสามารถ attach shell ได้

จำวิธีการ ขั้นตอน และคำสั่ง เพื่อให้สามารถนำมาทำการ custom image ได้

```docker
# Instruction arguments
FROM postgres:11
RUN mkdir /root/data
COPY src /root/data

```

วิธีการ build → same source as Dockerfile

```bash
docker build -t sql_lab .
```

```bash
docker run --rm --name banana -e POSTGRES_PASSWORD=banana -d -p 5432:5432 sql_lab
```

กำหนด workdir ได้ ในรูปแบบนี้

```docker
# Instruction arguments
FROM postgres:11
RUN mkdir /root/data
WORKDIR /root/data
COPY src .

```

หากต้องการ apt-get update

```bash
cat /etc/os-release
# ไว้เช็ค distribution of Linux
```

หลังจากนั้น หากต้องการจะติดตั้ง vim ก็ให้เพิ่มไปดังนี้

```bash
RUN apt-get update -y && apt-get install -y vim
```

เป็นการสั่งให้ apt-get update กด yes อัตโนมัติ และทำการ ติดตั้ง package vim