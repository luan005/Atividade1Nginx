# Teste de Carga com Apache Bench (ab)

## 1️⃣ Criar a network (caso use Docker)

docker network create react-net

---

## 2️⃣ Rodar o teste usando Docker

docker run --rm --network react-net jordi/ab -n 500 -c 50 http://nginx-react/

---

## 3️⃣ Rodar o teste sem Docker

Instalar o Apache Bench:

apt-get update  
apt-get install apache2-utils

Executar o teste:

ab -n 500 -c 50 http://localhost:81/

---

## 📊 Parâmetros

-n 500 → total de requisições  
-c 50 → conexões simultâneas  

---

## 📈 Resultado Esperado

Complete requests: 500  
Failed requests: 0  
Requests per second: (valor variável)  
Time per request: (valor variável)

Se Failed requests for 0, o servidor respondeu corretamente sob carga.
