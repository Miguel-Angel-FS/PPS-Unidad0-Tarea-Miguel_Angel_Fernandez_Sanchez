# Documentación del Workflow

## Creación del archivo de configuración `mkdocs.yml`

El primer paso para configurar el workflow es crear el archivo **`mkdocs.yml`** en la raíz del repositorio.  
Este archivo será utilizado por MkDocs para generar la documentación del proyecto.

📸 Captura del proceso:

<img width="1920" height="1051" alt="Primera" src="https://github.com/user-attachments/assets/6236c0d0-aff1-482b-90e8-d1d1defa22ef" />

---

## Creación del Workflow en GitHub Actions

Una vez creado el archivo `mkdocs.yml`, procedemos a crear el archivo del workflow:

📁 Ruta:  
`.github/workflows/CreacionDocumentacion.yml`

Este archivo contiene la automatización para generar la documentación en GitHub Pages mediante MkDocs.

📸 Captura del proceso:

<img width="1920" height="1048" alt="Segunda" src="https://github.com/user-attachments/assets/cbd7cb5a-82d3-4c30-99e2-14fb9860aca9" />

---

## Ejecución del Workflow

Después de subir los archivos al repositorio, vamos a la pestaña **Actions** y verificamos que el workflow se ha ejecutado correctamente.

Si todo está bien, aparecerá un **check verde** indicando que la acción se ha realizado con éxito.  
Podemos abrir los logs para comprobar que no ha ocurrido ningún error.

📸 Ejemplo de ejecución correcta:

<img width="1920" height="1051" alt="Tercera" src="https://github.com/user-attachments/assets/ad98f70a-ea15-4761-8fc7-ff79f642a71d" />
<img width="1920" height="1049" alt="Cuarta" src="https://github.com/user-attachments/assets/f28786f9-7595-4bf1-84d5-713938a5d8ef" />

---

## Configuración de GitHub Pages

Si el workflow ha generado correctamente los archivos, configuramos **GitHub Pages**:

Ruta:  
**Settings → Pages**

Seleccionamos la rama `gh-pages` como fuente de despliegue y guardamos los cambios.

📸 Ejemplo de configuración:

<img width="1920" height="1052" alt="Quinta" src="https://github.com/user-attachments/assets/598b4516-8e68-4305-8928-1758730289a5" />

---

## Comprobación del despliegue

Regresamos a la página principal del repositorio y verificamos en la sección **Deployments** que la acción más reciente tenga estado correcto.

Si la publicación ha sido exitosa, se mostrará la URL de GitHub Pages donde podremos visualizar nuestra página web estática generada con MkDocs.

📸 Ejemplos:

<img width="1920" height="1049" alt="Sexta" src="https://github.com/user-attachments/assets/d1437148-5700-451f-a3c2-ceb4397f445d" />
<img width="1920" height="1051" alt="Septimo" src="https://github.com/user-attachments/assets/61ed0cd9-3bba-4d97-91b7-f12057d958c6" />
<img width="1920" height="1050" alt="Octava y ultima" src="https://github.com/user-attachments/assets/af17ec2f-b67c-4d90-ae64-c511b6a23579" />

---

## Conclusión

Hemos configurado correctamente un workflow automatizado para generar y desplegar documentación empleando **MkDocs** y **GitHub Pages**.  
Gracias a esta automatización, cada cambio realizado en la documentación se publicará automáticamente en nuestra web estática sin intervención manual.
