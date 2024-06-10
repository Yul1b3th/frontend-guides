# Manual Git & GitHub

1. [**Introducción**](#1-introducción 'Ir a Introducción')
2. [**Configurar Git en la computadora**](#2-configurar-git-en-la-computadora 'Ir a Configurar Git en la computadora')
3. [**Configurar Git en un directorio de trabajo**](#3-configurar-git-en-un-directorio-de-trabajo 'Ir a Configurar Git en un directorio de trabajo')
4. [**Descargar el contenido de una rama remota a una rama local**](#4-descargar-el-contenido-de-una-rama-remota-a-una-rama-local 'Ir a Descargar el contenido de una rama remota a una rama local')
5. [**Subir el contenido de una rama local a una rama remota**](#5-subir-el-contenido-de-una-rama-local-a-una-rama-remota 'Ir a Subir el contenido de una rama local a una rama remota')
6. [**Contribución a una Rama de Funcionalidad y Fusión usando "Merge Recursive"**](#6-contribución-a-una-rama-de-funcionalidad-y-fusión-usando-merge-recursive 'Ir a Contribución a una Rama de Funcionalidad y Fusión usando "Merge Recursive"')
7. [**Publicación de una Página Web en GitHub**](#7-publicación-de-una-página-web-en-github 'Ir a Publicación de una Página Web en GitHub')
8. [**Despliegue de una Aplicación Angular**](#8-despliegue-de-una-aplicación-angular 'Ir a Despliegue de una Aplicación Angular')

<hr>

## 1. Introducción

**GitHub** es una plataforma de alojamiento de código fuente y colaboración basada en Git. Permite a los desarrolladores trabajar juntos en proyectos desde cualquier lugar. Fundada
en 2008, GitHub se ha convertido en un punto de referencia para la comunidad de desarrollo de software, facilitando la colaboración, el seguimiento de problemas, la gestión de
proyectos y mucho más.

**Git** es un software de control de versiones distribuido y de código abierto creado por **_Linus Torvalds_** en 2005 para el desarrollo del kernel de Linux. Este sistema facilita
la gestión de cambios en el código, permitiendo a los desarrolladores crear ramas, dividir proyectos en diferentes flujos de trabajo y fusionar esas ramas mediante un proceso
conocido como **_Merge_**. Git se ha convertido en una herramienta fundamental en el desarrollo de software y es la base sobre la cual se construyen las actividades de **GitHub**,
permitiendo a los usuarios colaborar y gestionar proyectos de software en sus computadoras portátiles o de escritorio de manera eficiente.

### Tipos de Merge

1. **Merge Fast-Forward (Avance rápido):** Ocurre cuando la rama que se desea fusionar tiene una secuencia de commits que se pueden aplicar fácilmente a la rama de destino sin
   necesidad de crear un nuevo commit de fusión.
2. **Merge Recursive (Recursivo):** Se utiliza cuando la historia de la rama que se desea fusionar y la historia de la rama de destino han divergido. Git crea un nuevo commit de
   fusión que combina los cambios de ambas ramas.
3. **Merge Octopus (Pulpo):** Se utiliza cuando se desean fusionar más de dos ramas a la vez. Git intenta fusionar las ramas de manera simultánea, creando un nuevo commit de fusión
   que combina los cambios de todas las ramas involucradas.

### Áreas de Trabajo en Git

Cuando Git inicia el seguimiento con el comando `git init`, crea un **_repositorio local_** donde se almacenan los archivos del proyecto. Además, establece dos áreas **_(Directorio
de trabajo y Área de ensayo)_** para gestionar los cambios en los archivos, por lo que ahora se pueden identificar tres áreas distintas:

1. **Directorio de trabajo:** Es el lugar donde se encuentran los proyectos y donde el usuario trabaja directamente con los archivos del proyecto.
2. **Área de ensayo (staging area):** Temporalmente almacena los archivos y permite al usuario revisar los cambios antes de confirmarlos en el repositorio local. Los archivos
   llegan a esta área con el comando `git add`.
3. **Repositorio local:** Aquí se almacenan las copias que Git hace de los archivos cuando se confirma un cambio utilizando el comando `git commit`. Este repositorio local es la
   versión oficial del proyecto en ese momento.

Los archivos en el **_Área de ensayo_** pueden tener los siguientes estados:

- **Untracked files (U):** No tienen seguimiento.
- **Tracked files (T):** Tienen seguimiento.
- **Not Staged (M):** Archivos modificados.
- **Staged (S):** Archivos listos para ser confirmados.

[⬆️ Subir](#manual-git--github 'Subir')

<hr>

## 2. Configurar Git en la computadora

- Comprobar si está instalado Git

  ```bash
  git --version
  ```

- Mostrar la configuración de Git

  ```bash
  git config --global --list
  ```

  \*Esto muestra la configuración global, local y de sistema.

- Asignar el nombre del usuario

  ```bash
    git config --global user.name "Nombre"
  ```

- Asignar el email del usuario

  ```bash
  git config --global user.email email@email.com
  ```

  \*El mismo email que está registrado en GitHub.

- Modificar el nombre del usuario

  ```bash
  git config --global --replace-all user.name “Nuevo nombre”
  ```

- Eliminar el usuario existente

  ```bash
  git config --global --unset-all user.name
  ```

- Añadir un nuevo usuario

  ```bash
  git config --global --add user.name “Nuevo nombre”
  ```

- Configurar interfaz de usuario

  ```bash
  git config --global user.ui true
  ```

- Establecer la rama predeterminada al inicializar un repositorio

  ```bash
  git config --global init.defaultBranch main
  ```

- Verificar la configuración actual

  ```bash
  git config --list
  ```

- Asignar Visual Studio Code como editor de configuración de Git

  ```bash
  git config --global core.editor "code --wait"
  git config --global -e
  ```

- Estandarizar los saltos de línea en Windows

  ```bash
  git config --global core.autocrlf true
  ```

- Estandarizar los saltos de línea en Linux/Mac

  ```bash
  git config --global core.autocrlf input
  ```

- Ver todas las opciones de configuración en la terminal

  ```bash
  git config -h
  ```

- Ver todas las opciones de configuración en el navegador
  ```bash
  git help config
  ```

[⬆️ Subir](#manual-git--github 'Subir')

<hr>

## 3. Configurar Git en un directorio de trabajo

### 3.1 Crear un nuevo repositorio

1. Inicializar un nuevo repositorio:

   ```bash
   git init
   ```

1. Agregar todos los archivos al área de ensayo (staging area):

   ```bash
   git add .
   ```

1. Crear el primer commit:

   ```bash
   git commit -m "first commit"
   ```

1. Renombrar la rama actual a "main":

   ```bash
   git branch -M main
   ```

1. Conectar el `<repositorio-local>` a un repositorio `<repositorio-remoto>` llamado **_origin_**:

   ```bash
   git remote add origin [repositorio-remoto]
   ```

1. Subir los cambios del `<repositorio-local>` a la rama "main" del `<repositorio-remoto>`:
   ```bash
   git push -u origin main
   ```

### 3.2 Subir un repositorio existente

1. Conectar el `<repositorio-local>` a un repositorio `<repositorio-remoto>` llamado **_origin_**:

   ```bash
   git remote add origin [repositorio-remoto]
   ```

1. Renombrar la rama actual a "main":

   ```bash
   git branch -M main
   ```

1. Subir los cambios del `<repositorio-local>` a la rama "main" del `<repositorio-remoto>`:

   ```bash
   git push -u origin main
   ```

   **Nota**

- La bandera `-M` es una forma abreviada de `--move --force`. Esto significa que Git intentará cambiar el nombre de la rama; si ya existe una rama con el nombre `main`, la
  sobrescribirá. Es una forma de asegurarse de que la rama se renombre a `main`, independientemente de si ya existe o no una rama con ese nombre.

- La bandera `-u` es una abreviatura de `--set-upstream` y establece la rama remota como upstream de la rama local. "Upstream" se refiere a la rama remota principal de la cual la
  rama local obtiene sus cambios. Esto permite omitir `origin` en futuros comandos `git push` y `git pull`, ya que Git recordará la configuración. Solo es necesario usar `-u` la
  primera vez.

[⬆️ Subir](#manual-git--github 'Subir')

<hr>

## 4. Descargar el contenido de una rama remota a una rama local

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

**Nota**: Cuando se hace `git merge` se crea automáticamente un `commit de fusión`. Este commit registra la combinación de los cambios de ambas ramas y sirve como punto de unión en
el historial de Git.

[⬆️ Subir](#manual-git--github 'Subir')

<hr>

## 5. Subir el contenido de una rama local a una rama remota

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

## 6. Contribución a una Rama de Funcionalidad y Fusión usando "Merge Recursive"

1. Cambiar a la `develop` y asegurarse de tener los últimos cambios:

   ```bash
   git switch develop
   git pull origin develop
   ```

2. Cambiar a la `<rama-tarea>` (o crearla si no existe):

   ```bash
   git switch -c <rama-tarea>
   git pull origin <rama-tarea>
   ```

3. Cambiar a la `<rama-tarea-hija>` (o crearla si no existe):

   ```bash
   git switch -c <rama-tarea-hija>
   ```

4. Realizar los cambios en la `<rama-tarea-hija>`:

   ```bash
   git add .
   git commit -m "Changes"
   ```

5. Cambiar de vuelta a la `<rama-tarea>`:

   ```bash
   git switch <rama-tarea>
   ```

6. Fusionar la `<rama-tarea-hija>` en la `<rama-tarea>` usando un **_merge recursivo_**:

   ```bash
   git merge <rama-tarea-hija>
   ```

7. Resolver los conflictos manualmente en el editor de código (si los hay), luego guardar los cambios:

   ```bash
   git add .
   git commit -m "Merge branch"
   ```

8. Subir los cambios a la `<rama-tarea>`:
   ```bash
   git push origin <rama-tarea>
   ```

[⬆️ Subir](#manual-git--github 'Subir')

<hr>

## 7. Publicación de una Página Web en GitHub

1. Inicializar un nuevo repositorio Git:

   ```bash
     git init
   ```

2. Agregar todos los archivos al área de ensayo (staging area):

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

5. Conectar el `<repositorio-local>` a un repositorio `<repositorio-remoto>` llamado **_origin_**:

   ```bash
   git remote add origin [repositorio-remoto]
   ```

6. Subir la rama `gh-pages` al repositorio remoto:
   ```bash
   git push -u origin gh-pages
   ```

[⬆️ Subir](#manual-git--github 'Subir')

<hr>

## 8. Despliegue de una Aplicación Angular

### 8.1 Creación del Build

1. Añadir la siguiente línea en el archivo `angular.json`, bajo la configuración de producción en `architect.build.configurations.production`:

   ```json
   "baseHref": "/nombre-repositorio/"
   ```

2. Ejecutar el siguiente comando para crear el build:
   ```bash
   ng build --configuration production
   ```

### 8.2 Realizar el Deployment

1. Inicializar un nuevo repositorio:

   ```bash
   git init
   ```

2. Agregar todos los archivos al área de ensayo (staging area):

   ```bash
   git add .
   ```

3. Crear el primer commit:

   ```bash
   git commit -m "Add compiled files for deployment"
   ```

4. Cambiar a la rama local (o crearla si no existe):

   ```bash
   git switch -c <gh-pages>
   ```

5. Conectar el `<repositorio-local>` a un repositorio `<repositorio-remoto>` llamado **_origin_**:

   ```bash
   git remote add origin [repositorio-remoto]
   ```

6. Subir la rama gh-pages al `<repositorio-remoto>`:

   ```bash
   git push -u origin gh-pages
   ```

7. Para sobreescribir el contenido de la rama `gh-pages` en futuras actualizaciones:
   ```bash
   git push -f origin gh-pages
   ```

[⬆️ Subir](#manual-git--github 'Subir')

<hr>

## 9. Listado de comandos básicos

| Comando        | Descripción                                                                               |
| -------------- | ----------------------------------------------------------------------------------------- |
| `git init`     | Inicializa un nuevo repositorio Git en el directorio actual.                              |
| `git add`      | Agrega archivos al área de preparación de Git.                                            |
| `git commit`   | Crea un nuevo commit con los archivos en el área de preparación.                          |
| `git status`   | Muestra el estado del repositorio Git.                                                    |
| `git push`     | Sube los cambios al repositorio remoto.                                                   |
| `git pull`     | Descarga los cambios del repositorio remoto.                                              |
| `git clone`    | Clona un repositorio remoto.                                                              |
| `git branch`   | Muestra, crea o elimina ramas.                                                            |
| `git checkout` | Cambia a una rama o commit específico.                                                    |
| `git merge`    | Combina los cambios de una rama a otra.                                                   |
| `git switch`   | Cambia a una rama específica (a partir de Git 2.23).                                      |
| `git log`      | Muestra el historial de commits.                                                          |
| `git diff`     | Muestra las diferencias entre commits, commit y área de preparación, etc.                 |
| `git stash`    | Guarda los cambios en un área de trabajo sucia temporal.                                  |
| `git reset`    | Revierte ciertos commits o cambios en el área de preparación.                             |
| `git remote`   | Administra conexiones a repositorios remotos.                                             |
| `git config`   | Configura opciones específicas de Git, como el nombre de usuario y el correo electrónico. |
| `git help`     | Muestra la ayuda para un comando específico de Git.                                       |
| `git revert`   | Crea un nuevo commit que deshace los cambios realizados en un commit anterior.            |
| `git fetch`    | Descarga los cambios del repositorio remoto sin fusionarlos con tu rama actual.           |

[⬆️ Subir](#manual-git--github 'Subir')

## Otros comandos...

| Comando         | Descripción                                              |
| --------------- | -------------------------------------------------------- |
| `cd`            | Cambia el directorio actual.                             |
| `ls`            | Lista todos los archivos en el directorio actual.        |
| `pwd`           | Muestra el camino del directorio actual.                 |
| `mkdir`         | Crea un nuevo directorio.                                |
| `touch`         | Crea un nuevo archivo.                                   |
| `rm`            | Elimina un archivo.                                      |
| `cp`            | Copia un archivo.                                        |
| `mv`            | Mueve o renombra un archivo.                             |
| `cat`           | Muestra el contenido de un archivo.                      |
| `echo`          | Imprime texto en la terminal.                            |
| `npm install`   | Instala las dependencias de un proyecto Node.js.         |
| `npm start`     | Inicia la aplicación Node.js.                            |
| `npm test`      | Ejecuta las pruebas de la aplicación Node.js.            |
| `npm run build` | Crea una versión de producción de la aplicación Node.js. |

[⬆️ Subir](#manual-git--github 'Subir')
