# Actividad Unidad 0 - DevSecOps Básico y Automatización de la Documentación

Lee atentamente la actividad hasta el final para asegurarte de lo que tienes que entregar, por que es posible que no tengas que hacer nada y también existe la posibilidad de que tengas que documentar la actividad, bien para la entrega de la propia actividad o para la entrega de la tarea obligatoria.

En esta actividad veremo cómo podemos provocar la ejecución de determinadas herramientas en determinados momentos. En este caso realizaremos la ejecución de `mkdocs` al hacer un `push` al repositorio. En el caso de `GitHub` esta ejecución desatendida la hacemos mediante las `Webhooks` y veremos el resultado de la ejecución en las `Actions` de `GitHub`.



**Índice**

[Objetivos](#objetivos)

[Resultados de aprendizaje y Criterios de Evaluación](#resultados-de-aprendizaje-y-criterios-de-evaluación)

[Desarrollo](#desarrollo)

[Entrega](#entrega)

---

# Objetivos

Implementar una *pipeline* de Integración Continua (CI) en GitHub Actions para automatizar la generación y validación de la documentación de un proyecto Python cada vez que se actualiza el código o la documentación fuente.


1.  **Integrar Herramientas:** Configurar y utilizar **GitHub Actions** como motor de una *pipeline* de Integración Continua (CI/CD).
2.  **Automatizar la Calidad:** Crear un flujo de trabajo que se dispare automáticamente con eventos clave (ej. `git push`).
3.  **Gestión de Dependencias:** Utilizar comandos de Python (`pip`) dentro de la *pipeline* para instalar las dependencias necesarias de la aplicación y la documentación (ej., `MkDocs`).
4.  **Despliegue Continuo (CD Básico):** Demostrar un proceso de **Despliegue Continuo** al actualizar y publicar la documentación en las GitHub Pages del proyecto.
5.  **Fomentar DevSecOps:** Aplicar la filosofía de que el mantenimiento y la validación de la documentación (una forma de "calidad y consistencia") deben ser un paso **obligatorio y automatizado** en el ciclo de vida del desarrollo.


---


# Resultados de aprendizaje y Criterios de Evaluación  

Esta actividad se relaciona con el resultado de aprendizaje y criterios de evaluación RA 5 f y g.

---

# Desarrollo

Lo primero que haremos será instalar `GitHub CLI`.  
**[GiHug CLI](https://docs.github.com/es/github-cli/github-cli/about-github-cli)** (o `gh`) es una herramienta de código abierto que te permite usar GitHub directamente desde la línea de comandos de tu terminal. Permite gestionar repositorios, solicitudes de extracción (pull requests), problemas, flujos de trabajo, lanzamientos y mucho más, sin necesidad de salir de tu entorno de línea de comandos, lo que ahorra tiempo y facilita la automatización de tareas con scripts. 
Vamos a partir de la estructura del repositorio que hemos creado en la Actividad sobre el uso de Git.

Recordamos que en ella hicimos un respositorio de una calculadora en Python.

A partír de ahí vamos a crear un `workflow` de `Github Actions`.  

**[GitHub Actions](https://docs.github.com/es/actions/get-started/understand-github-actions)** es una plataforma de automatización integrada en GitHub que permite crear flujos de trabajo (workflows) para automatizar tareas de desarrollo de software, como la compilación, las pruebas y el despliegue continuo (CI/CD). Se define mediante archivos YAML dentro del propio repositorio y puede ejecutarse en máquinas virtuales de Linux, Windows o macOS, o en ejecutores auto-hospedado.
En esta ocasión vamos a utilizar MkDocs para ver cómo funciona el `workflow`.  

**[MkDocs](https://geoinnova.org/blog-territorio/mkdocs-como-crear-y-publicar-documentacion-eficientemente/)** es un generador de sitios estáticos escrito en Python que permite crear rápidamente sitios de documentación para proyectos usando archivos en 
Markdown y un único archivo de configuración en YAML. Transforma el contenido de Markdown en páginas HTML, CSS y JavaScript, lo que facilita la generación y publicación de documentación técnica de proyectos de código abierto de manera eficiente.   

Esta documentación creada sobre el proyecto se creará en la rama `gh-pages` de nuestro repositorio y vamos a aprovechar para publicar esta docuemtación con `Git Pages`.  

**[Git Pages](https://docs.github.com/es/pages/getting-started-with-github-pages/what-is-github-pages)** GitHub Pages es un servicio de alojamiento web que permite a los usuarios de GitHub publicar sitios web estáticos (HTML, CSS, JavaScript) directamente desde un repositorio de Git, sin costo alguno. Es ideal para portafolios, blogs o páginas de proyectos, y no requiere experiencia previa en programación o servidores. 

Uniendo todo esto tenemos que cada vez que realizemos un `git push` en nuestro repositorio el workflow se va a disparar, haciendo que en nuestro equipo se construya la documentación HTML del proyecto en su rama `gh-pages` y a la vez es subida, junto a los cambios realizados en la rama main, al repositorio de github.  


Esta documentación la podremos visualizar a traves de `GitHub Pages`



## Paso 0:  Asignando Variables y preparando GitHub CLI##
## 
1. Para que sea más rápido el proceso de copiar y pegar los comandos vamos a crear variables en el sistema y así se sustituirán automáticamente por vuestros nombres, cuenta de git y email. Sustituye los tuyos abajo:
```bash
Tu_nombre=Aquí_Pones_Tu_Nombre
Tu_usuario_github=Aquí_Pones_Tu_usuario_github

    ```
1.  **Instalamos gh**  
```bash 
sudo apt update
sudo apt install gh
```

2. Nos autenticamos en gh:
```bash
gh auth login
```

Si nos diera algún problema, podemos crear un token en GitHub.com para utilizarlo para autenticarse en gh.

## Paso 1: Preparación del Proyecto y Documentación


1.  **Copiar el Repositorio:**  
  Copia los archivos del repositorio que hiciste en la actividad de Git y los colocas en una carpeta con el siguiente nombre:`CalculadoraPython-Tu_nombre`

1. Inicializamos el repositorio.
  Por si acaso configuramos la variable `init.defaulBranch` a `main` e inicializamos el repositorio:
```bash
git config --global init.defaultBranch main
git init
```

1.  **Estructura Base:** En el caso de que no tengas el resositorio creado, crea la siguiente estructura de archivos y directorios:
    ```
    1. La estructura del proyecto debe de ser la siguiente:

```

PPS-CalculadoraPython-Tu_nombre/  
├── calculator/  
│   ├── __init__.py  
│   └── gui.py  
├── docs/  
│   └── index.md  
├── mkdocs.yml  
├── requirements.txt  
└── .github/  
    └── workflows/  
        └── deploy_docs.yml  
``` 
1. **Guardamos los datos**
  Después de creada la estructura: 
```bash
git add .
git commit -am "inicializando repositorio"
# Especificamos que la rama principal va a ser `main`
#  Con gh vamos a crear un repositorio desde linea de comandos en nuestra cuenta GitHub.com
git branch -M main
# Creamos el repositorio git  
desde gh
gh repo create $Tu_usuario_github/CalculadoraPython-$Tu_nombre --public --source=. --remote=origin --push
```
1.  **Configuración de MkDocs:** Crea el archivo `mkdocs.yml` con una configuración mínima.
    
```yaml
# mkdocs.yml

# -------------------------------------------------------------
# CONFIGURACIÓN GENERAL DEL SITIO
# -------------------------------------------------------------
site_name: Documentación de Calculadora Python # Define el título que aparecerá en la barra de navegación y en la etiqueta <title> del navegador.

# -------------------------------------------------------------
# ESTRUCTURA DE NAVEGACIÓN (MENÚ)
# -------------------------------------------------------------
# Define la lista de enlaces y el orden de aparición en el menú de navegación principal.
nav:
  # El nombre de la sección en el menú: nombre_archivo.md
  - Home: index.md             # Primer elemento del menú, enlaza con el archivo 'index.md'.
  - Uso: guia_uso.md           # Segundo elemento del menú, enlaza con el archivo 'guia_uso.md'.
  # Se pueden añadir subsecciones anidando listas:
  # - Referencia: 
  #   - Funciones: referencia/funciones.md
  #   - Clases: referencia/clases.md

# -------------------------------------------------------------
# DIRECTORIOS
# -------------------------------------------------------------
# Ruta de la carpeta que contiene todos los archivos .md (Markdown) de la documentación.
# MkDocs buscará aquí los archivos listados en 'nav'.
doc_dir: docs 
# -------------------------------------------------------------
# TEMA (Opcional, pero común)
# -------------------------------------------------------------
# theme: 
#   name: 'material' # Si usas el popular tema Material for MkDocs.
#   # highlightjs: true
#   # code_fences: true
```
La configuracion le dice a MkDocs que espere la siguiente estructura de archivos dentro de tu repositorio:

/   
├── mkdocs.yml              <-- Archivo de configuración que acabas de mostrar  
├── docs/                   <-- Directorio principal de la documentación  
│   ├── index.md            <-- Contenido de la sección "Home"  
│   └── guia_uso.md         <-- Contenido de la sección "Uso"  
└── (resto de archivos del proyecto, ej: calculadora.py, etc.)  

### Paso 2: Configuración de la Pipeline (GitHub Actions)

1.  **Creación del Workflow:** Dentro del directorio `.github/`, crea el directorio `workflows/` y dentro de él, el archivo `deploy_docs.yml`.
2.  **Definición del Flujo de Trabajo (YAML):** Pega la siguiente configuración en `deploy_docs.yml`. Este *workflow* se dispara con cada *push* a la rama `main` (o `master`) y utiliza una acción oficial para gestionar el despliegue de MkDocs a GitHub Pages.

`.github/workflows/deploy_docs.yml`
```yaml
# -----------------------------------------------------------
# CONFIGURACIÓN DEL WORKFLOW
# -----------------------------------------------------------
name: Deploy MkDocs # Define el nombre de este flujo de trabajo (aparece en la pestaña 'Actions' de GitHub).

on:
  # Define el evento que dispara este flujo de trabajo.
  push:
    # Este workflow se ejecutará automáticamente cada vez que se haga un 'push' (subida)
    # de código al repositorio.
    branches:
      - main # Específicamente, solo se ejecuta si el push se realiza sobre la rama 'main'.

# -----------------------------------------------------------
# PERMISOS
# -----------------------------------------------------------
# Otorga permisos específicos al GITHUB_TOKEN que se usará en este workflow.
permissions:
  contents: write # Permite que el token pueda leer y escribir contenido (necesario para la rama gh-pages).
  pages: write    # Permite gestionar y escribir en la configuración de GitHub Pages.
  id-token: write # Permite solicitar tokens de OpenID Connect (necesario para algunas integraciones de seguridad).

# -----------------------------------------------------------
# DEFINICIÓN DEL TRABAJO (JOB)
# -----------------------------------------------------------
jobs:
  deploy: # Define un único trabajo llamado 'deploy'.
    runs-on: ubuntu-latest # Especifica que este trabajo se ejecutará en un servidor virtual con la última versión de Ubuntu.

    steps: # La secuencia de comandos o acciones a ejecutar en el servidor de Ubuntu.
    
    # -------------------------------------------------------
    # PASO 1: OBTENER EL CÓDIGO FUENTE
    # -------------------------------------------------------
    - name: Checkout Repo # Nombre descriptivo del paso.
      # Utiliza una acción oficial de GitHub para clonar el repositorio
      # completo en el entorno de trabajo del Runner.
      uses: actions/checkout@v3

    # -------------------------------------------------------
    # PASO 2: CONFIGURAR PYTHON
    # -------------------------------------------------------
    - name: Set up Python # Nombre descriptivo del paso.
      # Utiliza una acción oficial para configurar el entorno de Python.
      uses: actions/setup-python@v4
      with:
        python-version: '3.x' # Especifica que se debe usar la última versión de Python 3.

    # -------------------------------------------------------
    # PASO 3: INSTALAR DEPENDENCIAS
    # -------------------------------------------------------
    - name: Install dependencies # Nombre descriptivo del paso.
      # Comando que se ejecuta en la terminal de Ubuntu.
      # Instala el generador de documentación MkDocs (necesario para el siguiente paso).
      run: pip install mkdocs

    # -------------------------------------------------------
    # PASO 4: CONSTRUIR Y DESPLEGAR LA DOCUMENTACIÓN
    # -------------------------------------------------------
    - name: Deploy docs # Nombre descriptivo del paso.
      # Comando que se ejecuta en la terminal.
      # 1. 'mkdocs gh-deploy': Construye la documentación (generando los archivos HTML/CSS/JS).
      # 2. '--force': Sube esos archivos generados y fuerza su publicación en la rama 'gh-pages'.
      run: mkdocs gh-deploy --force
      # Configuración de variables de entorno específicas para este paso.
      env:
        # Pasa el Token de GitHub. MkDocs lo necesita para autenticarse y subir
        # los archivos a la rama 'gh-pages' del repositorio.
        GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Paso 3: Ejecución y Verificación

1.  **Commit Inicial:** 

Haz *commit* y *push* de los nuevos archivos .
```bash
git add .
git commit -m " Configuración inicial de MkDocs y pipeline CI/CD de documentación"
git push origin main
```
  > Sé paciente por que en el primer `push` en el que se ejecuta por primera vez `mkdocs` puede tardar varios minutos.

2.  **Monitoreo en GitHub:**

    * Ve a la pestaña **Actions** de tu repositorio. Deberías ver el *workflow* "Documentación CI/CD" ejecutándose.

    ![](./Imagenes/devsecops1.png)


    * Revisa el log para confirmar que los pasos **Construir Documentación** y **Desplegar a GitHub Pages** se completaron con éxito. Accedemos a él desde :  
    ![](./Imagenes/devsecops2.png)

    Podemos desplegar y ver todos los logs generados por nuestro equipo en la generación de la documentación:

    ![](./Imagenes/devsecops3.png)


3 .  **Activación de GitHub Pages:** 

  Una vez que la *pipeline* se complete por primera vez, ve a **Settings** -> **Pages** en tu repositorio de GitHub y configura la fuente de despliegue a la rama **`gh-pages`** que la *pipeline* acaba de crear. Pulsamos el botón de `save` para que se guarden los cambios.

  ![](./Imagenes/devsecops4.png)

  Salimos para que se guarden los datos y tras unos minutos, en la sección de `Pages` tenemos:

  ![](./Imagenes/devsecops5.png)

4.  **Verificación Final:** 
  La documentación debería estar accesible en la URL de GitHub Pages ( ej. `https://Tu_usuario_github.github.io/<repositorio>/`).
Podemos encontrarlo en **Deployments /Github pages** hacemos clic sobre ella y se mostrará el enlace para acceder a nuestra página web estática.

  ![alt text](./Imagenes/devsecops6.png)

  ![alt text](./Imagenes/devsecops7.png)


5.  **Modificando la documentación**

Para modificar la documentación tan sólo tenemos que hacerlo en los documentos contenidos en la carpeta `docs`.
Recordemos que tenemos un `index.md` cuyo contenido es el que se nos ha generado.
Añade un nuevo archivo Markdown dentro de la carpeta `docs`, por ejemplo una sección de contacto con el administrador.
Haz commit y push y observa cómo se modifica la documentación.

![alt text](./Imagenes/devsecops8.png)

### Reto DevSecOps: Fallo intencionado

Para reforzar la importancia del *Continuous Testing* (Pruebas Continuas):

1.  Modifica intencionalmente el archivo `mkdocs.yml` o borra la carpeta `docs/`.
2.  Haz *commit* y *push* de estos cambios.
3.  Observa cómo la *pipeline* en GitHub Actions **falla** en el paso **Construir Documentación**, impidiendo un despliegue defectuoso.

Esto demuestra que la calidad y la coherencia de la documentación son ahora una parte **integrada y obligatoria** de tu ciclo CI/CD, reflejando un principio clave de DevSecOps.
---

# Entrega

> Revisa la Tarea Obligatoria por si en ella tienes que incluir alguna documentación de esta actividad.
>
> Si eres estudiante de la modalidad On-Line, no tienes que hacer nada.
>
>Si eres de la modalidad presencial, a través de la plataforma pega el enlace del repositorio de git que has creado.

---
[![Licencia: CC BY-NC-SA 4.0](https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
