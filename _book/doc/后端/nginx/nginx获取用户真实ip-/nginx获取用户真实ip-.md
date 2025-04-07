# nginx获取用户真实ip&#x20;

```nginx 
server {
    listen 8000;
    server_name localhost;

    location / {
        # 配置根目录
        root /usr/share/nginx/html;
          # 配置首页
        index index.html;

        # nginx 主机ip
        proxy_set_header Host $proxy_host;
        # 获取客户真实ip 解决方案1
        proxy_set_header X-Real-IP $remote_addr;
        # 获取客户真实ip 解决方案2
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

        # $host：nginx主机ip
        # $http_host：nginx主机ip和端口
        # $proxy_host: proxy_pass配置的主机名和端口
        # $remote_addr:用户真实ip
    }
}
```
