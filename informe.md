# Wordpress con postgresql-pgadmin  en docker-compose
## 1. Tiempo de duración:
El tiempo de ejecución: Aproximadamente 30 minutos.
## 2. Fundamentos:
Docker Compose permite definir y correr múltiples contenedores Docker con un solo archivo YAML. En esta práctica se despliegan tres servicios: una base de datos PostgreSQL, su administrador web pgAdmin, y WordPress como CMS. Aunque WordPress no es compatible nativamente con PostgreSQL, se incluye para fines didácticos.
## 3. Conocimientos previos.
- Comandos básicos de Linux y terminal (cd, mkdir, nano).
- Uso básico de Docker y Docker Compose.
- Conocimiento general sobre CMS y bases de datos relacionales.
- Fundamentos de redes y volúmenes en contenedores.
## 4. Objetivos a alcanzar.
- Desplegar tres contenedores usando Docker Compose.
- Configurar una red personalizada para la comunicación entre servicios.
- Verificar el funcionamiento de pgAdmin conectado a PostgreSQL.
- Comprender la configuración básica de servicios mediante YAML.
## 5. Equipo necesario:
- Sistema operativo: Ubuntu 20.04 o superior.
- Docker y Docker Compose instalados.
- Conexión a internet para descargar imágenes desde Docker Hub.
- Navegador web (Firefox, Chrome, etc.).
## 6. Material de apoyo.
- Documentación oficial de Docker Compose.
- Imagen oficial de PostgreSQL en Docker Hub.
- Imagen oficial de pgAdmin.
- Imagen oficial de WordPress.
## 7. Procedimiento.
# Paso 1: Crear carpeta del proyecto:
````
mkdir wordpress-pg-docker
````
````
cd wordpress-pg-docker
````
# Evidencia:
<imag!![imagen 1](https://github.com/user-attachments/assets/61ac901c-223e-4e42-b7a3-10a99314d510)

# Paso 2: Crear archivo docker-compose.yml
````
nano docker-compose.yml
````
# Evidencia:
<imag!![imagen 2](https://github.com/user-attachments/assets/e6c98e1f-f04a-41ea-828c-a8801634e4a7)

# Paso 3: Escribir el siguiente contenido:
````
version: '3.8'

services:
  postgres:
    image: postgres:15
    container_name: postgres
    restart: always
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: admin123
      POSTGRES_DB: wordpress_db
    volumes:
      - pgdata:/var/lib/postgresql/data
    networks:
      - wp_network

  pgadmin:
    image: dpage/pgadmin4
    container_name: pgadmin
    restart: always
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@admin.com
      PGADMIN_DEFAULT_PASSWORD: admin123
    ports:
      - "8080:80"
    depends_on:
      - postgres
    networks:
      - wp_network

  wordpress:
    image: wordpress:latest
    container_name: wordpress
    restart: always
    environment:
      WORDPRESS_DB_HOST: dummyhost
      WORDPRESS_DB_USER: dummy
      WORDPRESS_DB_PASSWORD: dummy
      WORDPRESS_DB_NAME: dummy
    ports:
      - "8000:80"
    networks:
      - wp_network

volumes:
  pgdata:

networks:
  wp_network:
````
# Evidencia:
<imag!![imagen 4](https://github.com/user-attachments/assets/1108a53e-fb12-4402-a3bd-1c7d34d340e2)

# Paso 4: Levantar los contenedores
````
docker-compose up -d
````
# Evidencia:
<imag!![imagen 6](https://github.com/user-attachments/assets/57c425bf-dc55-4bfb-8f84-6638de450331)

# Paso 5: Verificar que están corriendo
````
docker ps
````
# Evidencia:
<imag!![imagen 7](https://github.com/user-attachments/assets/95bc930d-3147-4a85-ac74-a204e59cc146)

## 8. Resultados esperados:
- Contenedor de PostgreSQL ejecutándose correctamente.
- Acceso a pgAdmin para administrar la base de datos PostgreSQL.
- Contenedor de WordPress funcionando aunque no conectado a PostgreSQL.
- Comunicación estable entre contenedores en la red personalizada.
# Evidencia:
<imag!![resultado](https://github.com/user-attachments/assets/a7361aec-ee0d-497f-9618-f31562ad8485)

<imag!![resultado 2](https://github.com/user-attachments/assets/fbfdf471-0013-412d-ab11-c4842b7e870a)

## 9. Bibliografía:
- Docker Docs: https://docs.docker.com
- PostgreSQL Docs: https://www.postgresql.org/docs/
- pgAdmin Docs: https://www.pgadmin.org/docs/
- WordPress Codex: https://codex.wordpress.org/
- Compose File Reference: https://docs.docker.com/compose/compose-file/




