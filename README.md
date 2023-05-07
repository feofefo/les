## 技术栈

1、golang 1.20+

2、vue 3.2+

3、xtermjs 4.0+



## 快速开始

### 1、修改ssh主机信息server/server.go

主机名或ip地址

ssh服务端口号22

ssh远程用户root

ssh远程用户密码root



### 2、启动server

cd  server

go run main.go



### 3、启动web

cd web

pnpm install

pnpm run dev
