# Configuração de Rotas no Nginx

## 1️⃣ Criar a network

docker network create webnet

---

## 2️⃣ Criar o arquivo default.conf

server {
    listen 80;
    server_name _;

    root /usr/share/nginx/html;
    index index.html;

    location / {
        try_files $uri /index.html;
    }
}

---

## 3️⃣ Subir o container Nginx

docker run -itd \
  --name nginx-server \
  --network webnet \
  -p 81:80 \
  -v CAMINHO/DO/HTML:/usr/share/nginx/html \
  -v CAMINHO/DO/default.conf:/etc/nginx/conf.d/default.conf \
  nginx:1.29.3-alpine

---

## 4️⃣ Reiniciar o container (se necessário)

docker restart nginx-server

---

## 5️⃣ Teste

Acesse:

http://localhost:81

Se configurado corretamente, não ocorrerá erro 404.
