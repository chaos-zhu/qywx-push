## 使用指南


1. 准备好3个参数[AgentId、Secret、企业ID]，没企业号的先[注册](https://work.weixin.qq.com/)一个

   a. [创建一个应用](https://work.weixin.qq.com/wework_admin/frame#apps)，在应用详情即可获取AgentId、Secret
   
   b. 企业ID在[企业信息](https://work.weixin.qq.com/wework_admin/frame#/profile)里

2. 将服务器IP加入白名单【企业可信IP】
<img width="522" height="221" alt="image" src="https://github.com/user-attachments/assets/57a4e570-ad5b-4208-bd27-c630d34ddb8f" />

3. 应用管理 --> 接收消息 --> 启用API接收。Token和EncodingAESKey点随机获取
<img width="889" height="511" alt="image" src="https://github.com/user-attachments/assets/c812a0a5-45b6-4adc-9431-79ade714a404" />

4. 部署项目，配置并启动docker-compose.yml

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
      - ENCRYPTION_KEY=32位随机字符 # 务必修改 `ENCRYPTION_KEY` 为一个随机的32字符字符串，以确保数据安全
      - NODE_ENV=production # 运行环境
      - WECHAT_API_BASE=https://qyapi.weixin.qq.com  # 企业微信API地址
```
访问应用: http://your-server-ip:12121

5. 填写前面获取的参数
<img width="1171" height="571" alt="image" src="https://github.com/user-attachments/assets/01b661d5-0d40-4f33-b558-2adfc32411ff" />

生成回调后复制url，填写到这里，点击保存
<img width="1068" height="456" alt="image" src="https://github.com/user-attachments/assets/fdf6c1fe-39b1-4257-b6c6-ff0aea8623bb" />
<img width="1330" height="541" alt="image" src="https://github.com/user-attachments/assets/e2a448af-9b2e-4307-84cb-a41c052c403a" />

6. 完善配置
<img width="1110" height="838" alt="image" src="https://github.com/user-attachments/assets/ac9c02f5-6040-4422-97cf-80e04ea3d8e6" />

7. 保存好配置Code，就可以调用API服务了

8. 待完善图片发送
