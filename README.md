# [ssr-test](http://nuxt.haixiao.online)

## Build Setup

```bash
# install dependencies
$ yarn install

# serve with hot reload at localhost:3000
$ yarn dev

# build for production and launch server
$ yarn build
$ yarn start

# generate static project
$ yarn generate
```

For detailed explanation on how things work, check out [Nuxt.js docs](https://nuxtjs.org).


## server
```
upstream nuxt {
  server 127.0.0.1:3000; #nuxt项目 监听端口
}
server {
  listen 80;
  server_name xxxx.com;
  location / {
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_set_header Host $host;
    proxy_set_header X-Nginx-Proxy true;
    proxy_cache_bypass $http_upgrade;
    proxy_pass http://nuxt; #反向代理
  }
}

```
## pm2 进程守护

```
  pm2 start npm --name "nuxt" -- run start
```