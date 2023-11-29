#  dev-ops 

docker container cp Nginx:/etc/nginx/nginx.conf /users/xiaoxin/chatgpt/dev-ops/nginx/conf
docker container cp Nginx:/etc/nginx/conf.d/default.conf /users/xiaoxin/chatgpt/dev-ops/nginx/conf/conf.d/
docker container cp Nginx:/usr/share/nginx/html/index.html /users/xiaoxin/chatgpt/dev-ops/nginx/html


#有ssl 配置443
docker run \
--name Nginx \
-p 443:443 -p 80:80 \
-v /users/xiaoxin/chatgpt/dev-ops/nginx/logs:/var/log/nginx \
-v /users/xiaoxin/chatgpt/dev-ops/nginx/html:/user/share/nginx/html \
-v /users/xiaoxin/chatgpt/dev-ops/nginx/conf/nginx.conf:/etc/nginx/nginx.conf \
-v /users/xiaoxin/chatgpt/dev-ops/nginx/conf/conf.d:/etc/nginx/conf.d \
-v /data/nginx/ssl:/etc/nginx/ssl/ \
--privileged=true -d --restart=always nginx

#没有不配置443
docker run \
--name Nginx \
-p 80:80 \
-v /users/xiaoxin/chatgpt/dev-ops/nginx/logs:/var/log/nginx \
-v /users/xiaoxin/chatgpt/dev-ops/nginx/html:/user/share/nginx/html \
-v /users/xiaoxin/chatgpt/dev-ops/nginx/conf/nginx.conf:/etc/nginx/nginx.conf \
-v /users/xiaoxin/chatgpt/dev-ops/nginx/conf/conf.d:/etc/nginx/conf.d \
-v /users/xiaoxin/chatgpt/dev-ops/nginx/ssl:/etc/nginx/ssl/ \
--privileged=true -d --restart=always nginx