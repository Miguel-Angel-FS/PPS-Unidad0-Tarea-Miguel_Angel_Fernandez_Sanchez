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
