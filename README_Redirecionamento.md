# Configuração das Rotas do ReactJS no Nginx

## 1️⃣ Criar a network

docker network create react-net

---

## 2️⃣ Gerar o build da aplicação React

npm run build

---

## 3️⃣ Criar o arquivo default.conf

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

## 4️⃣ Subir o container Nginx

docker run -itd \
  --name nginx-react \
  --network react-net \
  -p 81:80 \
  -v CAMINHO/DO/BUILD:/usr/share/nginx/html \
  -v CAMINHO/DO/default.conf:/etc/nginx/conf.d/default.conf \
  nginx:1.29.3-alpine

---

## 5️⃣ Reiniciar o container (se necessário)

docker restart nginx-react

---

## 6️⃣ Teste

Acesse no navegador:

http://localhost:81


Se configurado corretamente, não ocorrerá erro 404.
