## Docker 部署指南

docker-compose.yml

```yaml
services:
  qywx-push:
    image: chaoszhu/qywx-push:latest
    container_name: qywx-push
    restart: always
    ports:
      - "12121:12121"
    volumes:
      - ./data:/app/database
    environment:
      - PORT=12121 # 应用端口
      - DB_PATH=/app/database/notifier.db # 数据库路径
      - ENCRYPTION_KEY=32位随机字符 # 32位随机字符
      - NODE_ENV=production # 运行环境
      - WECHAT_API_BASE=https://qyapi.weixin.qq.com  # 企业微信API地址
```

**重要提示**：请务必修改 `ENCRYPTION_KEY` 为一个随机的32字符字符串，以确保数据安全。

## 访问应用

部署成功后，可以通过以下地址访问应用：

```
http://your-server-ip:12121
```
