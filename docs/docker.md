# Creación de un contenedor de servicios NGINX con Docker

Lo primero que he hecho ha sido descargar `docker.io` en mi máquina virtual con Kali Linux y comprobar que se ha instalado correctamente ejecutando el comando `sudo docker --version`, para verificar la versión instalada.

![Primera captura](https://github.com/user-attachments/assets/c41fbed8-7c0e-4f19-be8e-884d3acb657d)

![Segunda captura](https://github.com/user-attachments/assets/273a0179-762f-4d58-88d0-db69c4d6622e)

---

Una vez comprobado que Docker se ha instalado correctamente, he clonado el repositorio de GitHub en mi máquina virtual mediante el comando `git clone` y he cambiado a la rama `gh-pages`.

![Tercera captura](https://github.com/user-attachments/assets/6b585417-3b51-4624-9d5a-29fec2774d12)

---

Después de clonar el repositorio, he creado el contenedor Docker en modo demonio y he comprobado que se ha creado correctamente mediante el comando `docker ps`, que muestra los contenedores en ejecución.

![Cuarta captura](https://github.com/user-attachments/assets/708a1dca-ff1a-468b-899f-c9fa45c08856)

---

Tras verificar que el contenedor estaba en ejecución, he visualizado la página web desde el navegador accediendo a `localhost` a través del puerto **8085**.

![Quinta captura](https://github.com/user-attachments/assets/097aba40-1d1b-47c4-9463-0682255658a7)

---

Por último, he obtenido el archivo con toda la información del contenedor utilizando el comando:

docker inspect nombreContenedor
