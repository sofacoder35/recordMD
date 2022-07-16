## 前后端部署笔记centos

##### 1、docker阿里云镜像

```bash
docker rm $(docker ps -a -q) 删除所有容器
```

```bash
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

##### 2、java环境

```bash
yum -y install java-1.8.0-openjdk*
```

##### 3.启动redis

```bash
docker run -p 6379:6379 --name redis -v /home/rural/redis:/data -d redis:5.0 --appendonly yes 

-p 6379:6379 端口映射：前表示主机部分，：后表示容器部分。
--name redis 指定该容器名称，查看和进行操作都比较方便。
-v 挂载目录，规则与端口映射相同。
-d redis 表示后台启动redis。
--appendonly yes 开启redis 持久化
```

##### 4、启动mysql

```bash
docker run -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=111111 -v /home/rural/mysql/data:/var/lib/mysql -v /home/rural/mysql/log:/etc/log/mysql -d mysql:5.7
```

##### 5、nginx配置

```bash
docker run --name nginx -p 80:80 -v /home/rural/nginx/nginx.conf:/etc/nginx/nginx.conf -v /home/rural/dist:/usr/local/dist -d nginx

```

```bash
docker exec -i [nginx容器名/id] nginx -s reload
```

```bash
server {
	listen 80;
	server_name 
	location / {
	#dist
	root /usr/local/dist;
	try_files $uri $uri/ /index.html;
	index index.html index.htm;
}

location /prod-api/ {
	proxy_set_header Host $http_host;
	proxy_set_header X-Real-IP $remote_addr;
	proxy_set_header REMOTE-HOST $remote_addr;
	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	#docker 部署需要用实际ip
	proxy_pass http://127.0.0.1:8000/;
}

error_page 500 502 503 504 /50x.html;
location = /50x.html {
		root html;
	}
}
```



##### 6、后台启动

```bash
nohup java -jar java-sport-0.0.1-SNAPSHOT.jar > log.out 2>&1 &
```

##### 7、命令

查找占用端口

```bash
netstat -lnp|grep 8080 
```

##### python镜像

```bash
pip3 install -r requirements.txt -t ./ -i https://mirrors.aliyun.com/pypi/simple
```

##### 8、网易云

```bash
docker run --name net -d -p 54321:8080 zsfzsf/neteasemusic:1.0
```

