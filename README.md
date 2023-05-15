## Microservicios
Microservicio en Flask + MySQL

### Paso 1.
Clonar el repositorio, abrir la carpeta ```frontend``` y verificar que esté el archivo ```docker-compose.deploy.yml``` file:
```
cd frontend
ls -la
```

### Paso 2.
Crear una nueva red en Docker llamada ```micro_network```:
```
docker network create micro_network
```

### Paso 3.
Desplegar los microservicios:
```
sudo docker-compose -f docker-compose.deploy.yml up -d
sudo docker ps
```

### Paso 4.
Preparar la base de datos para cada servicio:
```
for service in corder-service cproduct-service cuser-service;
do 
 docker exec -it $service flask db init
 docker exec -it $service flask db migrate
 docker exec -it $service flask db upgrade
done
```

### Paso 5.
Popular la base de datos:
```
curl -i -d "name=prod1&slug=prod1&image=product1.jpg&price=100" -X POST localhost:5002/api/product/create
curl -i -d "name=prod2&slug=prod2&image=product2.jpg&price=200" -X POST localhost:5002/api/product/create
```

### Paso 6.
Navegar a la siguiente URL para registrarse:
```
http://ip:5000/register
```

