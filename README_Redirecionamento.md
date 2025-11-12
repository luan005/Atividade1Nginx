# Balanceador de Carga com Nginx (3 Nós)

## Instalação dos serviços
```bash
docker network create lb_net

docker run -itd --name loadbalancer --network lb_net -p 81:80 nginx:1.29.3-alpine
docker run -itd --name node1 --network lb_net nginx:1.29.3-alpine
docker run -itd --name node2 --network lb_net nginx:1.29.3-alpine
docker run -itd --name node3 --network lb_net nginx:1.29.3-alpine

# Acesse o bash do loadbalancer

docker exec -it loadbalancer sh
apk add --no-cache nano


# Acesse o arquivo default.conf

cd /etc/nginx/conf.d
nano default.conf


# Edite o arquivo da seguinte forma

upstream webfront {
    server node1:80;
    server node2:80;
    server node3:80;
}

server {
    listen 80;

    location / {
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_pass http://webfront;
    }
}


# Reinicie todos os containers

nginx -t
nginx -s reload
exit
docker restart loadbalancer node1 node2 node3

# Por fim, teste o balanceamento

curl -i http://localhost:81/
