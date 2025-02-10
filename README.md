## 推荐阅读
- 代码仓库: https://github.com/lwmacct/250210-cr-php
- 语雀文档: https://www.yuque.com/lwmacct/docker-run/php

## 运行示例
```bash
#!/usr/bin/env bash

__main() {

  {
    # 镜像准备
    _image1="registry.cn-hangzhou.aliyuncs.com/lwmacct/php:8.4.3-apache-bookworm-t250204"
    _image2="$(docker images -q $_image1)"
    if [[ "$_image2" == "" ]]; then
      docker pull $_image1
      _image2="$(docker images -q $_image1)"
    fi
  }

  _apps_name="www"
  _apps_data="/data/$_apps_name"
  cat <<EOF | docker compose -p "$_apps_name" -f - up -d --remove-orphans
services:
  main:
    container_name: $_apps_name
    image: "$_image2"
    restart: always
    network_mode: bridge
    ports:
      - "8081:80"
    volumes:
      - $_apps_data:/var/www/html
    environment:
      - TZ=Asia/Shanghai
EOF
}

__help() {
  cat <<EOF

EOF
}

__main

```