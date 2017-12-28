# 跑在 docker 里的 google 镜像
======

# 简单两步获得 Google 镜像，使用方法：

```
docker pull rpmdpkg/docker-google-mirror
docker run -d -p 80:80 rpmdpkg/docker-google-mirror
```

默认打开基本的“谷歌搜索”和“谷歌学术”，如需打开或者自定义其他功能，请下载项目文件修改nginx.conf并且自行构建镜像

# 自行构建镜像：

```
git clone https://github.com/GEM7/docker-google-mirror
cd docker-google-mirror
#如要自定义`nginx.conf`文件，详情参考[源项目](https://github.com/cuber/ngx_http_google_filter_module/blob/master/README.zh-CN.md)
docker build -t google-mirror .
docker run -d -p 80:80 google-mirror
```

# 配置https

## 使用其他镜像或者Nginx，Caddy进行反向代理

## 自身实现
1. 编辑Dockerfile文件,注释第22行，并解注释第24、25行
2. 申请域名证书，具体参考[Nginx 配置 SSL 证书 + 搭建 HTTPS 网站教程](https://s.how/nginx-ssl/)
3. 添加自己的域名证书到该目录下

```shell
cd docker-google-mirror
cp ~/ssl.csr domain.csr
cp ~/ssl.key.unsecure domain.key.unsecure
docker build -t google-mirror .
docker run -d -p 80:80 -p 443:443 google-mirror
```

去除证书phrase的命令：

```shell
openssl rsa -in ssl.key -out ssl.key.unsecure
```
