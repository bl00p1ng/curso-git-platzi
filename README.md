# Curso Profesional de Git y GitHub
Apuntes y repositorio de prueba del [Curso Profesional de Git y GitHub de Platzi](https://platzi.com/clases/git-github/)

- Proyecto guitarras Invie-sibles (2018)
- Actualización 2020

## - Comandos útiles

```bash
git show # Muestra todos los cambios histoicos hechos. Incluye información útil como que cambios se hicieron, cuando se hicieron y quien los hizo.

git log file.txt # Ver el historial de un archivo
```

## - ¿Qué es el staging y los repositorios? Ciclo básico de trabajo en Git

Al ejecutar *git init* se crea un área en la memoria RAM  llamada **staging** donde se almacenarán los cambios al principio, es una especie de *estado temporal*. 

En estado temporal se pueden hacer todos los cambios que se necesiten, de cierta forma esta es un área de preparación, en la que git estará al tanto de que archivos estamos modificando. Una vez se hace un commit se crea un hash (identificador) a las modificaciones para que cada uno de los miembros del proyecto pueda saber que se cambio.

Para mandar archivos al staging area se usa el comando:

```bash
git add file.py # El archivo pasa al staging area (tracked file) donde estará "esperando" hasta ser enviado al repositorio.

git rm --cached file.py # Quitar un archivo del staging area. --cached → Borrar el archivo de la memoria RAM 

git commit # Manda los archivos del staging area al repositorio.

```

Cuando los archivos aún no se han agregado al staging area con *git add*, son lo que se conoce como **untracked files**.

En ocasiones al trabajar en equipos puede ser necesario traer  un cambio que esta en el repositorio pero no esta en el sistema de archivo local en el que se esta trabajando. Para traer esos cambios se usa el comando:

```bash
git checkout
```

- ### Ramas (branch):

  Son una especie de líneas de tiempo en las que se puede dividir un proyecto para por ejemplo trabajar en funciones experimentales, características nuevas, o trabajar en paralelo.

  El crear una rama se crea una copia de determinada versión de la rama master para trabajar sobre ella. Una vez se termina de trabajar con esa rama nueva se hace un **merge ** para fusionar los cambios hechos en la rama nueva con la rama principal. Las ramas típicas en un proyecto de software son:

  - **master** (main en GitHub)
  - **development**
  - **hotfix**

- ### Mostrar configuración por defecto de Git

  ```bash
  git config --list
  git config --list --show-origin # Muestra donde están guardadas las configuraciones.
  ```

- ## Analizar cambios en los archivos con Git

  - Mostar los cambios hechos sobre un archivo:

    ```bash
    git show file.js
    ## @@ -1,5 +1,6 @@ → Indica la diferencia en bytes estre los cambios.
    ```

  - Ver diferencias entre commits

    ```bash
    git diff hashCommitViejo hastCommitNuevo # Se recomienda poner primero el commit más antiguo y luego el más reciente.
    ```

- ## Volver en el tiempo en el repositorio utilizando reset y checkout

  - **git reset**

    ```bash
    git reset --hard hashCommitVersionAnterior # --hard → Todo vuelve al estado anterior
    
    git reset --soft hashCommitVersionAnterior # --soft → Se regresa a la versión anterior pero se conservan los cambios que esten en el staging area
    ```

    Para ver las diferencias entre los untracked files el la unidad de almacenamiento del PC y el staging area en la memoria RAM se usa el comando:

    ```bash
    git diff # Asi sin más, sin hash ni nada
    ```

    Ver los cambios específicos que se hicieron en cada commit:

    ```bash
    git log --stat
    ```

  - **git checkout**

    Permite entre otras cosas traer archivos de regreso entre commits

    ```bash
    git checkout hashCommit file.js
    git checkout master file.js  # Regresa al archivo original de master
    ```

    Para mantener los cambios y conservar el,archivo viejo sólo hay que hacer un commit

    Si se van a renombrar archivos o a cambiarlos de ubicación en el repositorio lo recomendable es esar:

    ```bash
    git mv
    ```

    De lo contrario se puede perder el tracking y generar conflictos.

- ## git reset vs git rm

  - ### git rm

    Permite eliminar archivos de git sin eliminar su historial en el sistema de versiones. Por lo que para recuperar el archivo solo hay que *"viajar en el tiempo"*  y recuperar el archivo del último commit antes de borrarlo.

    ```bash
    git rm --cached # Elimina los archivos del área de Staging y del próximo commit pero los mantiene en el disco duro.
    
    git rm --force # Elimina los archivos de Git y del disco duro. Git siempre guarda todo, por lo que se acceder al registro de la existencia de los archivos, asi que se puede recuperar si es necesario (pero se deben usar comandos más avanzados).
    ```

  - **git reset**

    Permite *"volver en el tiempo"* pero de una forma diferente a git checkout que permite regresar, mirar, pasear y volver. **Git reset** se regresa al pasado sin la posibilidad de volver. Se borra y sobrescribe la historia. Por lo tanto es un comando muy peligroso que no se puede usar a la ligera.

    ```bash
    git reset --hard # Regresa y borra lo que este el el staging area
    
    git reset --soft # Mantiene los cambios que esten en ele staging area para que se pueda aplicar dichos cambios en un commit anterior
    
    git reset HEAD # Sirve para sacar archivos del staging area para que esos cambios no se envíen al último commit. Se puede deshacer agregando de nuevo los archivos con git add
    ```

    