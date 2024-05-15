
# Private Cloud For User (NextCloud)


With Nextcloud, you can collaborate with others, share files securely, and access your data from anywhere using a web interface or mobile apps. 


## Docker_Compose.yaml

```javascript
services:
  nc:
    image: nextcloud:apache
    restart: always
    ports:
      - 88:80
    volumes:
      - nc_data:/var/www/html
    networks:
      - redisnet
      - dbnet
    environment:
      - REDIS_HOST=redis
      - MYSQL_HOST=db
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_PASSWORD=nextcloud
  redis:
    image: redis:alpine
    restart: always
    networks:
      - redisnet
    expose:
      - 6379
  db:
    image: mariadb:10.5
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW
    restart: always
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - dbnet
    environment:
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_ROOT_PASSWORD=nextcloud
      - MYSQL_PASSWORD=nextcloud
    expose:
      - 3306
volumes:
  db_data:
  nc_data:
networks:
  dbnet:
  redisnet:
```


## Run Locally

Clone the project

```bash
  git clone git@github.com:Tarun-Tiwari10052001/Docker_projects.git
```

Go to the project directory

```bash
  cd my_project_repo
```

Command to run Container 

```bash
  docker-compose up -d
```
## Screenshots

![App Screenshot](https://github.com/Tarun-Tiwari10052001/Aws_file/blob/master/Git_pro_img_1.png)



Run command to check container working in proper way

```bash
  docker-compose ps
```

To check your local machine ip add

```bash
  ip add show wlp1s0
```
Output (in my case)

```bash
  wlp1s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether e4:02:9b:66:2f:47 brd ff:ff:ff:ff:ff:ff
    inet 192.168.0.169/24 brd 192.168.0.255 scope global dynamic noprefixroute wlp1s0
       valid_lft 78578sec preferred_lft 78578sec
    inet6 fe80::35e1:78e7:8bbf:af3d/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```
Note the ip (in my case)

```bash
  192.168.0.169
```

## Screenshots

![App Screenshot](https://github.com/Tarun-Tiwari10052001/Aws_file/blob/master/Git_proj_img2.png)



# Browse 


1. Open you favourite Browser 
2. Put the local ip add with port you provided     (in my case i provide port 88 )

## Screenshots

![App Screenshot](https://github.com/Tarun-Tiwari10052001/Aws_file/blob/master/Git_pro_img3.png)

1. Install and login (already mensioned in .yaml file environment:  1.user=nextcloud & 2. Pass=nextcloud)
2. Go to File icon 
3. Finally you got the Service 