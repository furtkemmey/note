# Docker

## 啟動容器
    docker run -p 電腦的port:容器的port --name 自以定義 -d 映像檔名
    docker run -p 8080:3000 --name myapp -d demo/myapp
    
## 刪除所有容器
    docker rm $(docker ps -aq)

## 刪除所有映像檔
    docker rmi $(docker images -q)

## 刪除執行中的 container
    //Get container ID
    $ docker ps
    
    //使用CONTAINER ID刪除container
    $ docker container kill [CONTAINER-ID]
    
## 查看images
    docker images

## 查看當前運作的容器狀況
    docker ps -a

## 停止容器
    docker stop myapp

## 啟動容器
    docker start myapp
    
## 執行容器的bash
    docker exec -it nginx /bin/bash

## image存成檔案
    docker save -o mytomcat.tar mytomcat
    
## load到其他電腦
    docker load -i mytomcat.tar
    
    
# Dockerfile
## 建立映像檔
    docker build -t [名稱:tag] .
## 設定檔
    FROM balenalib/raspberrypi3-node:10.10
    ENTRYPOINT []
    
    # 這邊是指容器的工作目錄，就像 cd workspace 意思一樣，因為我們把檔案複製於該目錄，所以一同切換目錄。
    WORKDIR /home/
    
    # 複製當前目錄到容器中的/home/
    COPY . /home/
    
    RUN npm install
    
    # 聲明當容器運行時所提供的服務端口，並不會真正的對外開放,做提示的作用而已
    EXPOSE 3000
    # CMD npm start
    CMD ["npm","start"]
    
# docker-Compose 
## pip 安裝,但是版本太舊
    // 下載安裝pip
    wget https://bootstrap.pypa.io/get-pip.py
    sudo python get-pip.py
    sudo pip install docker-compose
    
## 設定要包含的docker(yml格式)
    docker-compose.yml
## 啟動服務
    docker-compose up -d
## 結束服務
    docker-compose stop
## 移除所有 container
    docker-compose down --volumes
## 範例
    version: '3'
    
    services:
      movie:
        image: node/movie:arm
        ports:
          - "8080:3000"
      youtube:
        image: node/youtube:arm
        ports:
          - "8081:3000"
      alert:
        image: node/alert:arm
        ports:
          - "8082:3000"