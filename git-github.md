# Manual Git & GitHub

- [**Introducción**](#introducción 'Ir a Introducción')
- [**Configuración rápida de un nuevo repositorio**](#configuración-rápida-de-un-nuevo-repositorio 'Ir a Configuración rápida de un nuevo repositorio')
- [**Publicar una página web en GitHub**](#publicar-una-página-web-en-github 'Ir a Publicar una página web en GitHub')
- [**Descargar el contenido de una rama remota a una rama local**](#descargar-el-contenido-de-una-rama-remota-a-una-rama-local 'Ir a Descargar el contenido de una rama remota a una rama local')
- [**Subir el contenido de una rama local a una rama remota**](#subir-el-contenido-de-una-rama-local-a-una-rama-remota 'Ir a Subir el contenido de una rama local a una rama remota')
- [**Contribución a una Rama de Funcionalidad y Fusión usando "Merge Recursive"**](#contribución-a-una-rama-de-funcionalidad-y-fusión-usando-merge-recursive 'Ir a Contribución a una Rama de Funcionalidad y Fusión usando "Merge Recursive"')
- [**Listado de comandos básicos**](#listado-de-comandos-básicos 'Ir a Listado de comandos básicos')

<hr>

## 1. Introducción

**GitHub** es una plataforma de alojamiento de código fuente y colaboración basada en Git. Permite a los desarrolladores trabajar juntos en proyectos desde cualquier lugar. Fundada en 2008, GitHub se ha convertido en un punto de referencia para la comunidad de desarrollo de software, facilitando la colaboración, el seguimiento de problemas, la gestión de proyectos y mucho más.

**Git** es un software de control de versiones creado por **_Linus Torvalds_** en 2005 como un sistema de control de versiones distribuido de código abierto para el desarrollo del kernel de Linux. Permite crear ramas, dividir el proyecto en diferentes flujos de trabajo y fusionar las ramas en un único archivo, proceso conocido como **_Merge_**.

### Tipos de Merge

1. **Merge Fast-Forward (Avance rápido):** Ocurre cuando la rama que se desea fusionar tiene una secuencia de commits que se pueden aplicar fácilmente a la rama de destino sin necesidad de crear un nuevo commit de fusión.
2. **Merge Recursive (Recursivo):** Se utiliza cuando la historia de la rama que se desea fusionar y la historia de la rama de destino han divergido. Git crea un nuevo commit de fusión que combina los cambios de ambas ramas.
3. **Merge Octopus (Pulpo):** Se utiliza cuando se desean fusionar más de dos ramas a la vez. Git intenta fusionar las ramas de manera simultánea, creando un nuevo commit de fusión que combina los cambios de todas las ramas involucradas.

### Áreas de Trabajo en Git

Cuando Git inicia el seguimiento con el comando `git init`, crea un **_repositorio local_** donde se almacenan los archivos del proyecto. Además, establece dos áreas **_(Directorio de trabajo y Área de ensayo)_** para gestionar los cambios en los archivos, por lo que ahora se pueden identificar tres áreas distintas:


1. **Directorio de trabajo:** Es el lugar donde se encuentran los proyectos y donde el usuario trabaja directamente con los archivos del proyecto.
2. **Área de ensayo (staging area):** Temporalmente almacena los archivos y permite al usuario revisar los cambios antes de confirmarlos en el repositorio local. Los archivos llegan a esta área con el comando `git add`.
3. **Repositorio local:** Aquí se almacenan las copias que Git hace de los archivos cuando se confirma un cambio utilizando el comando `git commit`. Este repositorio local es la versión oficial del proyecto en ese momento.

Los ficheros en el **_Área de ensayo_** pueden tener los siguientes estados:

- **Untracked files (U):** No tienen seguimiento.
- **Tracked files (T):** Tienen seguimiento.
- **Not Staged (M):** Archivo modificado.
- **Staged (S):** Archivo listo para ser confirmado.



[⬆️ Subir](#manual-git--github 'Subir')

<hr>


## 2. Configuración rápida de un repositorio

### Crear un nuevo repositorio

1. Inicializar un nuevo repositorio:
    ```bash
    git init
    ```
2. Agregar todos los archivos del directorio:
    ```bash
    git add .
    ```
3. Crear el primer commit:
    ```bash
    git commit -m "first commit"
    ```

4. Renombrar la rama actual a "main":
    ```bash
    git branch -M main
    ```

5. Conectar el <repositorio-local> a un repositorio <remoto-remoto>:
    ```bash
    git remote add origin [repositorio-remoto]
    ```

6. Empujar los cambios del <repositorio-local> a la rama "main" del <repositorio-remoto>:
    ```bash
    git push -u origin main
    ```

### Enviar un repositorio por primera vez

1. Conectar el <repositorio-local> a un repositorio <remoto-remoto>:
    ```bash
    git remote add origin [repositorio-remoto]
    ```

2. Renombrar la rama actual a "main":
    ```bash
    git branch -M main
    ```

3. Empujar los cambios del <repositorio-local> a la rama "main" del <repositorio-remoto>:
    ```bash
    git push -u origin main
    ```

  **Nota**
- La opción `-M` es una forma abreviada de `--move --force`. Esto significa que Git intentará cambiar el nombre de la rama, y si ya existe una rama con el nombre `main`, la sobrescribirá. Es una forma de asegurarse de que la rama se renombre a `main`, independientemente de si ya existe o no una rama con ese nombre.

- La opción `-u` es una abreviatura de `--set-upstream` y establece la rama remota como upstream de la rama local. "Upstream" se refiere a la rama remota principal de la cual la rama local obtiene sus cambios. Esto permite omitir `origin` en futuros comandos `git push` y `git pull`, ya que Git recordará la configuración. Solo es necesario usar `-u` la primera vez.

[⬆️ Subir](#manual-git--github 'Subir')

<hr>

## Publicar una página web en GitHub

1. Inicializar un nuevo repositorio Git:
    ```bash
      git init
    ```

2. Agregar todos los archivos al área de preparación (staging area):
    ```bash
    git add .
    ```

3. Hacer un commit con un mensaje:
    ```bash
    git commit -m "Add compiled files for gh-pages"
    ```

4. Crear una nueva rama `gh-pages`:
    ```bash
    git branch gh-pages
    ```

5. Agregar un repositorio remoto:
    ```bash
    git remote add origin [repositorio-remoto]
    ```

6. Subir la rama `gh-pages` al repositorio remoto:
    ```bash
    git push -u origin gh-pages
    ```


[⬆️ Subir](#manual-git--github 'Subir')

<hr>

## Descargar el contenido de una rama remota a una rama local

### Con `git pull`

1. Cambiar a la rama local (o crearla si no existe):
    - Forma más moderna:
      ```bash
      git switch -c <rama-local>
      ```

    - Forma Antigua:
      ```bash
      git checkout -b <rama-local>
      ```

2. Actualizar la rama local con los cambios de la rama remota y fusionarlos automáticamente:
    ```bash
    git pull origin <rama-remota>
    ```

### Con `git fetch` seguido de `git merge`

1. Cambiar a la rama local (o crearla si no existe):
    - Forma más moderna:
      ```bash
      git switch -c <rama-local>
      ```

    - Forma Antigua:
      ```bash
      git checkout -b <rama-local>
      ```

2. Actualizar la información de las ramas remotas:
    ```bash
    git fetch origin
    ```

3. Fusionar el contenido de la rama remota en la rama local:
    ```bash
    git merge origin/<rama-remota>
    ```

**Nota**: Cuando se hace `git merge` se crea automáticamente un `commit de fusión`. Este commit registra la combinación de los cambios de ambas ramas y sirve como punto de unión en el historial de Git.

[⬆️ Subir](#manual-git--github 'Subir')

<hr>

## Subir el contenido de una rama local a una rama remota

1. Cambiar a la rama local (o asegurarse de estar en ella):
    ```bash
    git switch <rama-local>
    ```

2. Subir los commits locales a la rama remota:
    ```bash
    git push origin <rama-remota>
    ```

[⬆️ Subir](#manual-git--github 'Subir')

<hr>

## Contribución a una Rama de Funcionalidad y Fusión usando "Merge Recursive"

1. Cambiar a la `developer` y asegurarse de tener los últimos cambios:
    ```bash
    git switch developer
    git pull origin developer
    ```

2. Cambiar a la `<rama-remota>` (o crearla si no existe):
    ```bash
    git switch -c <rama-remota>
    git pull origin <rama-remota>
    ```

3. Cambiar a la `<rama-hija-remota>` (o crearla si no existe):
    ```bash
    git switch -c <rama-hija-remota>
    ```

4. Realizar los cambios en la rama `<rama-hija-remota>`:
    ```bash
    git add .
    git commit -m "Mensaje descriptivo de los cambios"
    ```

5. Cambiar de vuelta a la rama `<rama-remota>`:
    ```bash
    git switch <rama-remota>
    ```

6. Fusionar la rama `<rama-hija-remota>` en la rama `<rama-remota>` usando un **merge recursivo**:
    ```bash
    git merge <rama-hija-remota>
    ```

7. Resolver los conflictos manualmente en el editor de código.

8. Hacer un commit para finalizar la fusión:
    ```bash
    git commit -m "Merge branch '<rama-hija-remota>' into <rama-remota>"
    ```

9. Subir los cambios a la rama remota `<rama-remota>`:
    ```bash
    git push origin <rama-remota>
    ```

[⬆️ Subir](#manual-git--github 'Subir')



<hr>

## Listado de comandos básicos
| Comando | Descripción |
|---------|-------------|
| `git init` | Inicializa un nuevo repositorio Git en el directorio actual. |
| `git add` | Agrega archivos al área de preparación de Git. |
| `git commit` | Crea un nuevo commit con los archivos en el área de preparación. |
| `git status` | Muestra el estado del repositorio Git. |
| `git push` | Sube los cambios al repositorio remoto. |
| `git pull` | Descarga los cambios del repositorio remoto. |
| `git clone` | Clona un repositorio remoto. |
| `git branch` | Muestra, crea o elimina ramas. |
| `git checkout` | Cambia a una rama o commit específico. |
| `git merge` | Combina los cambios de una rama a otra. |
| `git switch` | Cambia a una rama específica (a partir de Git 2.23). |
| `git log` | Muestra el historial de commits. |
| `git diff` | Muestra las diferencias entre commits, commit y área de preparación, etc. |
| `git stash` | Guarda los cambios en un área de trabajo sucia temporal. |
| `git reset` | Revierte ciertos commits o cambios en el área de preparación. |
| `git remote` | Administra conexiones a repositorios remotos. |
| `git config` | Configura opciones específicas de Git, como el nombre de usuario y el correo electrónico. |
| `git help` | Muestra la ayuda para un comando específico de Git. |

[⬆️ Subir](#manual-git--github 'Subir')

## Otros comandos...
| Comando | Descripción |
|---------|-------------|
| `cd` | Cambia el directorio actual. |
| `ls` | Lista todos los archivos en el directorio actual. |
| `pwd` | Muestra el camino del directorio actual. |
| `mkdir` | Crea un nuevo directorio. |
| `touch` | Crea un nuevo archivo. |
| `rm` | Elimina un archivo. |
| `cp` | Copia un archivo. |
| `mv` | Mueve o renombra un archivo. |
| `cat` | Muestra el contenido de un archivo. |
| `echo` | Imprime texto en la terminal. |
| `npm install` | Instala las dependencias de un proyecto Node.js. |
| `npm start` | Inicia la aplicación Node.js. |
| `npm test` | Ejecuta las pruebas de la aplicación Node.js. |
| `npm run build` | Crea una versión de producción de la aplicación Node.js. |

[⬆️ Subir](#manual-git--github 'Subir')