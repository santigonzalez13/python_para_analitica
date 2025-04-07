**Guía detallada paso a paso para enseñar Git y GitHub desde cero, con ejemplos de uso en proyectos de analítica y Machine Learning**

---

## 1. Introducción

1. **¿Qué es el control de versiones y por qué es importante?**  
   - Permite llevar registro de todos los cambios en un proyecto y revertirlos en caso de errores.  
   - Fundamental para trabajar en equipo y mantener un histórico de versiones.  
   - Especialmente útil en proyectos de **analítica de datos** o **Machine Learning**, donde se generan múltiples scripts, notebooks y conjuntos de datos que evolucionan con el tiempo.

2. **Ejemplos prácticos en analítica y Machine Learning**  
   - **Seguimiento de notebooks**: En proyectos de ciencia de datos, se suelen tener Jupyter Notebooks con experimentos, visualizaciones y modelos. Con Git, puedes guardar cada versión de tus notebooks, de modo que si un experimento empeora los resultados, puedas volver a una versión anterior.  
   - **Control de scripts de preprocesamiento**: Los archivos donde limpias y transformas datos cambian con frecuencia. Git te permite probar distintas estrategias de preprocesamiento y guardar cada una de ellas.  
   - **Gestión de ramas para modelos**: Puedes tener una rama por cada modelo (por ejemplo, `modelo_regresion_lineal`, `modelo_random_forest`) y compararlas fácilmente antes de unificarlas si es necesario.  
   - **Trabajo colaborativo**: Distintos científicos de datos pueden trabajar en paralelo en distintas tareas (EDA, ingeniería de características, pruebas de algoritmos) y luego integrar todo en un repositorio central.

3. **¿Qué es Git?**  
   - Es el sistema de control de versiones distribuido más utilizado.  
   - Permite tener una copia completa del repositorio en cada máquina local.

4. **¿Qué es GitHub?**  
   - Es una plataforma en la nube para alojar repositorios Git.  
   - Facilita la colaboración, revisión de código, seguimiento de issues y despliegue de proyectos.

---

## 2. Configuración inicial de Git

1. **Instalación de Git**  
   - En Windows: descargar el instalador desde [https://git-scm.com/](https://git-scm.com/) e instalar.  
   - En Mac o Linux: normalmente se puede instalar con el gestor de paquetes (por ejemplo, `apt` en Ubuntu o `brew` en macOS).  
   - Verificar la instalación con:
     ```bash
     git --version
     ```

2. **Configuración de nombre e email**  
   - Configurar el nombre y el correo que se registrarán en cada commit:
     ```bash
     git config --global user.name "Tu Nombre"
     git config --global user.email "tu_correo@example.com"
     ```
   - Verificar la configuración con:
     ```bash
     git config --list
     ```

---

## 3. Primer repositorio local

1. **Crear una carpeta de proyecto**  
   - En tu computadora, crea una carpeta que contenga, por ejemplo, un archivo de Python o un Jupyter Notebook relacionado con tu trabajo de analítica o ML.  
   - Asume que la carpeta se llama `MiPrimerProyecto`.

2. **Inicializar el repositorio**  
   - Abre la terminal en la carpeta `MiPrimerProyecto`.  
   - Ejecuta:
     ```bash
     git init
     ```
   - Esto creará una carpeta oculta llamada `.git`, que señala que Git está listo para rastrear los cambios.

3. **Añadir un archivo y hacer el primer commit**  
   - Crea un archivo llamado `README.md` con una breve descripción del proyecto (por ejemplo, “Pruebas con dataset de predicción de precios”).  
   - En la terminal:
     ```bash
     git status
     ```
     Verás que `README.md` está sin seguimiento.  
   - Añade este archivo al *stage* (área de preparación):
     ```bash
     git add README.md
     ```
   - Realiza tu primer commit:
     ```bash
     git commit -m "Primer commit: añade README"
     ```
   - Verifica el estado:
     ```bash
     git status
     ```
     Ahora debería indicar que no hay cambios pendientes.

4. **Examinar el historial**  
   - Consulta el historial de commits:
     ```bash
     git log
     ```
   - Para salir de la vista de `git log`, presiona `q`.

---

## 4. Conexión con GitHub y subida del repositorio

1. **Crear un nuevo repositorio en GitHub**  
   - Entra en [GitHub](https://github.com/) con tu cuenta.  
   - Haz clic en “New” (nuevo repositorio).  
   - Asigna un nombre como `MiPrimerProyecto` (el mismo o uno similar al de la carpeta local).  
   - Selecciona si será público o privado.  
   - No marques la opción “Initialize this repository with a README” para evitar conflictos con el README local.

2. **Enlazar el repositorio local con el remoto**  
   - Copia la URL que te proporciona GitHub, usualmente con el formato:
     ```
     https://github.com/tu_usuario/MiPrimerProyecto.git
     ```
   - En la terminal, dentro de la carpeta local, escribe:
     ```bash
     git remote add origin https://github.com/tu_usuario/MiPrimerProyecto.git
     ```
   - Verifica la configuración del remoto:
     ```bash
     git remote -v
     ```

3. **Subir los cambios al repositorio remoto**  
   - Envía los commits locales a GitHub:
     ```bash
     git push -u origin main
     ```
     (En algunas versiones de Git, la rama principal se llama `master`. Ajusta según corresponda).  
   - Introduce tus credenciales o utiliza SSH si lo tienes configurado.

4. **Verificar en GitHub**  
   - Abre el enlace de tu repositorio en GitHub y comprueba que tu archivo `README.md` aparece allí.

---

## 5. Flujo de trabajo básico

1. **Creación de ramas (branches)**  
   - Para añadir una nueva función en un proyecto de ML o un nuevo script de análisis, crea una rama específica:
     ```bash
     git checkout -b feature-analisis-nuevo
     ```
   - Con esto, todos los cambios quedarán aislados de la rama principal mientras realizas experimentos.

2. **Editar y hacer commits**  
   - Modifica o añade archivos (por ejemplo, `analysis_nuevo.py` o un notebook `analisis_nuevo.ipynb`).  
   - Añade los cambios al *stage*:
     ```bash
     git add .
     ```
   - Crea un nuevo commit:
     ```bash
     git commit -m "Implementa nuevo análisis de correlación"
     ```

3. **Fusionar (merge) a la rama principal**  
   - Cambia de vuelta a la rama principal:
     ```bash
     git checkout main
     ```
   - Fusiona los cambios de la rama `feature-analisis-nuevo`:
     ```bash
     git merge feature-analisis-nuevo
     ```
   - De esta forma, la rama principal incluirá las modificaciones aprobadas.

4. **Subir los cambios a GitHub**  
   - Primero, sube la nueva rama (si quieres mantenerla en remoto):
     ```bash
     git push -u origin feature-analisis-nuevo
     ```
   - Luego, sube la rama principal actualizada:
     ```bash
     git push origin main
     ```
   - Si la rama de feature ya no se necesita, se puede eliminar en remoto:
     ```bash
     git push origin --delete feature-analisis-nuevo
     ```

---

## 6. Cierre y siguientes pasos

1. **Buenas prácticas**  
   - Realizar **commits con mensajes claros y concisos**.  
   - Comprobar siempre `git status` antes y después de trabajar.  
   - Mantener ramas separadas para nuevas funciones o experimentos de ML para no comprometer el trabajo estable.  
   - Hacer `pull` o `fetch` frecuentemente, sobre todo en equipo, para mantener los cambios sincronizados.

2. **Otras funcionalidades a explorar**  
   - **`git clone`**: para copiar repositorios existentes (útil al unirse a un proyecto ya iniciado).  
   - **`git stash`**: para guardar temporalmente cambios sin realizar un commit definitivo (muy útil si descubres que necesitas cambiar rápidamente de tarea).  
   - **Pull requests y revisiones de código**: ideal para un flujo de trabajo colaborativo en equipo.  
   - **Gestión de Issues**: para reportar y organizar tareas, bugs o nuevas propuestas.  
   - **GitHub Actions**: para automatizar pruebas, validaciones o despliegues.  

3. **Aplicaciones en analítica y ML**  
   - Uso de Git para versionar experimentos en notebooks, datos procesados y resultados intermedios.  
   - Documentar métricas y resultados de modelos en commits, lo que permite rastrear la evolución del rendimiento a lo largo del tiempo.  
   - Trabajar en equipo en repositorios privados o públicos, compartiendo código y datasets, aprovechando las funcionalidades de seguimiento de proyectos.

Con esta guía, los estudiantes podrán iniciarse en Git y GitHub de manera práctica, entendiendo cómo aplicar el control de versiones a sus trabajos de analítica y Machine Learning.