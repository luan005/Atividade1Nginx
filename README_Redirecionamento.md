# Balanceador de Carga com Nginx (3 Nós)

## Instalação dos serviços
```bash
docker network create lb_net

docker run -itd --name loadbalancer --network lb_net -p 81:80 nginx:1.29.3-alpine
docker run -itd --name node1 --network lb_net nginx:1.29.3-alpine
docker run -itd --name node2 --network lb_net nginx:1.29.3-alpine
docker run -itd --name node3 --network lb_net nginx:1.29.3-alpine

