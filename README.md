# falta cosas aun()
1er . cambiar tus datos en .env.dev
2do verificar tambien tanto el micro-usuarios & micro-cursos el .env de ambos modificar sus datos correspondientes
3er. levantar el compose   ->  docker compose --env-file .env.dev up -d --build


-- 
Verificar el estado de los contenedores
docker compose ps


Todos los servicios deberían aparecer con estado Up.

Detener y limpiar los contenedores
docker compose down -v
