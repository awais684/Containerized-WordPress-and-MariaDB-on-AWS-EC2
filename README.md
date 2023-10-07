**Summary of Tasks:**

1. Create a virtual machine on AWS

2. Setup docker and docker-compose on VM

3. Write a docker-compose file

4. Execute docker-compose file

5. Access your web server with VM public IP

6. Set-up Database

7. Watch my complete video of this project for troubleshooting

## 1. Create a virtual machine on AWS

> Sign in to your AWS account and click on "Launch instance".
> Choose Amazon Linux AMI or keep it default

![Choose Amazon Linux AMI or keep it default](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/te6iiq0l0y7r011fcuah.PNG)

> In the instance type section, choose t2.micro and a key-pair

![In the instance type section, choose t2.micro and a key-pair](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/fz90ms8vb4b4zjpwg6m5.PNG)

> In the networking section, keep the default settings

![In the networking section, keep the default settings](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/l6eo3exogpv04tt5hxm2.PNG)

> In the storage and advance section, use default settings and click on the "Launch Instance" button on the right top corner

![In the storage and advance section, use default settings and click on the "Launch Instance" button on the right top corner](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/lbz9fmuhndcvud4qwn0g.PNG)

> Your virtual machine is ready

![Your virtual machine is ready](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kes7hq2ja07z7ezqhccg.PNG)

## 2. Setup docker and docker-compose on VM

```
yum install docker -y
service docker start
```
```
curl -SL https://github.com/docker/compose/releases/download/v2.20.3/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose;
```

## 3. Write a docker-compose file

```
services:
  wordpress:
    container_name: wordpress_web
    image: wordpress
    ports:
      - "80:80"
    volumes:
      - ./efs:/var/www/html
    networks:
      - web_cont_net
    environment:
       WORDPRESS_DB_HOST: mariadb
       WORDPRESS_DB_USER: root
       WORDPRESS_DB_PASSWORD: awais123
       WORDPRESS_DB_NAME: cloud_db

  mariadb:
    container_name: wordpress_db
    image: mariadb
    environment:
      MYSQL_ROOT_PASSWORD: awais123
      MYSQL_DATABASE: cloud_db
    volumes:
      - ./database:/var/lib/mysql
    networks:
      - web_cont_net
networks:
  web_cont_net:
```

## 4. Execute docker-compose file

```
docker-compose up -d
```

## 5. Access your web server with VM public IP
you will see such an interface

![you will see such an interface](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/cemmpamlmwcpaxlqmgm8.PNG)

## 6. Set-up Database

![Set-up Database](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kp1ja29r8q96nqdykjxt.PNG)
> And your application is ready

![And your application is ready](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jo16so6d1biz3tl4l7hp.PNG)

## 7. Watch my complete video of this project for troubleshooting
If you face any issues, watch my complete video of this project on my channel
[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/mWWTpvgwD_E/0.jpg)](https://www.youtube.com/watch?v=mWWTpvgwD_E)


