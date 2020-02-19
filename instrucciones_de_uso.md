# Instrucciones de uso

El objetivo de este portafolio es que el estudiante aprenda a utilizar `Git` y posea material demostrable de las habilidades aprendidas en el curso. Las instrucciones se dividen en la configuración del repositorio personal, configuración del repositorio del curso y en un flujo típico a lo largo del semestre.

En particular, se debe configurar `Binder` con tal de poder ejecutar el código del estudiante desde cualquier computador sin la necesidad de descargar, por eso es necesario que al subir los laboratorios estos se suban en conjunto a los datos.

## Configuración inicial para el curso

1. Crear cuenta de GitHub [aquí](https://github.com/join).
    - Es recomendable aprovechar el correo UTFSM y reclamar el [_Student Pack_](https://education.github.com/students) de GitHub. Uno de sus beneficios es acceder a una membresía Pro y así tener repositorios privados.
2. Instalar [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
    - En Windows lo ideal sería instalar _Git for Windows_.
3. Configurar tu forma de acceder a GitHub. [Recomendaciones.](https://help.github.com/en/articles/which-remote-url-should-i-use)
    - Si usas HTTPS no olvides usar [_credential helper_ ](https://help.github.com/en/articles/caching-your-github-password-in-git) para recordar tu usuario.
    - Para utilizar SSH seguir [estas instrucciones](https://help.github.com/en/articles/connecting-to-github-with-ssh).
4. Ir al repositorio [mat281_portfolio_template](https://github.com/aLoNsolml/mat281_portfolio_template) y presionar el botón *__Use this template__*.
5. Nombar el nuevo repositorio como __mat281_portfolio__ y dejarlo en modo público.
7. Se recomienda crear un directorio en el computador personal para repositorios de Git. Por ejemplo en `~/Documents/git/`.
6. Clonar el repositorio recién creado. Dependiendo de tu configuración de Git, reemplazar `{username}` por el nombre de usuario personal de GitHub uno de los siguientes comandos en la terminal (usuarios de Windows probablemente tengan que utilizar _Git Shell_.)
    - HTTPS: `git clone https://github.com/{username}/mat281_portfolio.git`
    - SSH: `git clone git@github.com:{username}/mat281_portfolio.git`
7. En el archivo `README.md` editar los campos personales:
    - Línea 15: `[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/{GITHUT_USER}/{REPO_NAME}/master?urlpath=lab)` donde deber cambiar `{GITHUB_USER}` por tu usuario de GitHub y `{REPO_NAME}` por el nombre del repositorio, que siguiendo las instrucciones debe llamarse __mat281_porfolio__.
    - Línea 17: Nombre personal y si se desea algún link a perfil profesional, por ejemplo Linkedin o GitHub.

## Configurar repositorio del curso

1. Clonar el repositorio del curso,por ejemplo, para el segundo semestre del año 2019 el repositorio del curso se encuentra disponible en el siguiente [link](https://github.com/aLoNsolml/mat281_2019S2).
2. En el transcurso del semestre, para actualizar se debe ejecutar `git pull` en la terminal dentro del directorio del repositorio. Por ejemplo, si el repositorio está en la ruta `~/Documents/git/mat281_2019S2`:
    - `cd ~/Documents/git/mat281_2019S2`
    - `git pull`
    - __¡IMPORTANTE!__ Para no tener problemas al _pullear_ no deben existir conflictos con el repositorio original, la mejor forma de evitar esto es no editar ningún archivo y realizar todos los laboratorios/tareas/etc. en el repositorio personal del curso.

## Flujo típico de uso

1. Al comenzar el semestre creaste y clonaste tu repositorio personal del curso y clonaste el repositorio oficial del curso. Deberías tener estructura de directorios similar a esta:
    ```
    - git
    |
    |- mat281_2019S2
    |  |
    |  |- ...
    |
    |- mat281_portfolio
        |
        |- ...
    ```
2. Al comenzar la clase actualizas el contenido en el respositorio oficial del curso, es decir, ejecutas `git pull` en `mat281_2019S2`.
3. A modo de ejemplo, supongamos es la cuarta clase del módulo 2. En el repositorio oficial del curso se encontrará el directorio `mat281_2019S2/m02_data_analysis/m02_c04_data_aggregation` que contiene la carpeta `data` y los jupyter notebooks relativos a la clase expositiva y el laboratorio.
En tu repositorio debes crear el directorio del módulo y de la clase, copiar y pegar la carpeta `data` y el fichero `m02_c04_lab.ipynb` en este. Te quedará algo así:

    ```
    - mat281_portfolio
    |
    |- m02_data_analyis
    |  |
    |  |- m02_c04_data_aggregation
    |  |  |
    |  |  |- data
    |  |  |  |
    |  |  |  |- ...
    |  |  |
    |  |  |- m02_c04_data_aggregation.ipynb
    |  |
    |  |- ...
    |
    |- ...
    ```
4. Abrir desde `jupyter lab` el jupyter notebook correspondiente a la clase que se encuentre en el __repositorio personal__. Realizar el laboratorio y guardar los cambios.
5. Agregar, _commitear_ y _pushear_ los cambios, lo típico sería:
    ```
    cd ~/Documents/git/mat281_portfolio
    git add m02_data_analysis/m02_c04_data_aggregation/
    git commit -m "Laboratorio 4 módulo 2."
    git push origin master
    ```
    Con esto se verán reflejados los cambios en tu cuenta de GitHub.

## Verifica que todo funcione correctamente!

Después de cada _commit_, prueba que Binder está bien configurado, ya que Binder necesita realizar una nueva imagen/contenedor de tu repositorio. Además, durante el curso se han instalado librerías o actualizado otras, por lo que debes editar el archivo `environment.yml` de tu respostorio.

Ejemplo:

- _Pusheaste_ la tarea del módulo de análisis datos (`m02_homework`)
- Vas a tu repositorio y ejecutas Binder haciendo click en el icono de Binder configurado anteriormente.
- Se va a tardar un par de minutos en crear la nueva imagen y lanzar la instancia de Jupyter Lab (__NO__ Jupyter Notebook!).
- Al estar lista la instancia de Jupyter Lab, abre el notebook `m02_homework.ipynb` que debe estar en la carpeta `m02_data_analysis/m02_homework`.
- Haz click en `Kernel -> Restart Kernel and Run All Cells`.
- Si al ejecutar `from PIL import Image` te arroja el error `ModuleNotFoundError: No module named 'PIL'` es porque no agregaste `pillow` a tu archivo `environment.yml`
    * Recuerda que las librerías instaladas en tu computador personal no se traspasan mágicamente a la instancia de Binder en tu repositorio, debes especificar las librerías en el famoso archivo `environment.yml`.
- En el caso que se te presente el caso anterior debes agregar la dependencia `pillow` y `environment.yml` te quedaría __algo__ como esto:

```yml
name: mat281
channels:
  - conda-forge
  - defaults
dependencies:
  - altair=3
  - jupyterlab=1.0.9
  - matplotlib=3.1.1
  - nodejs=12.8
  - numpy=1.17.0
  - pandas=0.25.1
  - pandas-profiling=2.3.0
  - pip
  - pillow=6.2.1
  - python=3.7
  - scikit-learn=0.21.3
  - scipy=1.3.1
  - seaborn=0.9.0
  - pip:
    - datachile
```

- Luego vuelves a hacer un _push_ con este cambio.
- Levantas la instancia de Binder en tu repostorio y vuelves a probar a ejectuar todas las celdas de `m02_homework.ipynb`.
- Repite el proceso hasta que todos tus entregables no tengan problema.

Finalmente, recuerda que la estructura de las carpetas es importante, así como los archivos que están en tu repositorio. Mostrar orden y pulcridad demuestra profesionalismo y seriedad. Recuerden que este repositorio será su carta de presentación el día de mañana.