##  搭建 Concourse Pipeline

### 安装 docker

```shell
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli docker-compose containerd.io docker-compose-plugin
sudo service docker start
sudo docker run hello-world # 进入到 docker 中
exit # 退出 docker
```


### 安装 Concourse CI

```shell
git clone https://github.com/concourse/concourse-docker.git
cd concourse-docker
./keys/generate
docker-compose up -d
```

接着用浏览器打开 `http://localhost:8080` 看部署是否成功，看到下述画面表示成功安装 Concourse CI。

<img width="1916" alt="截屏2022-09-30 16 56 23" src="https://user-images.githubusercontent.com/13810907/193233277-4ee02ae3-3d8e-45a5-bc80-4c949de790b3.png">



### 安装 Fly CLI

https://github.com/concourse/concourse/releases

下载对应的包，使得 `fly` 命令可用。解压后，

```shell
mv fly /usr/local/bin
```

### Hello World Demo

```shell
fly targets
```

```shell
fly -t ci set-pipeline -p test_pipeline -c pipeline.yml
```
<img width="1920" alt="截屏2022-09-30 17 18 50" src="https://user-images.githubusercontent.com/13810907/193237906-ac8e5795-0b3e-4896-bc13-9a673f4db079.png">



### 参考

1. https://github.com/concourse/concourse

