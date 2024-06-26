# comandos de Git

## Índice

1. Configuración de Git
2. Trabajando con ramas
3. Comandos de GIT
4. Colaboración
5. Restauración y eliminación
6. Tags

### 1. Configuración de Git

- Mostrar la configuración del Git: `git config --global --list`
- Mostrar el nombre del usuario: `git config --global user.name`
- Cambiar el nombre del usuario: `git config --global user.name "nombre"`
- Cambiar el email del usuario: `git config --local emailuser. email@email.com`
- Ver configuración en el editor de codigo: `git config --local -e`

### 2. Trabajando con ramas

- Crear una nueva rama y posicionarse en esa rama: `git checkout -b nombre_rama`
- Eliminar la rama que está en remoto: `git push origin --delete nombre_rama`
- Mostrar las ramas y sus fusiones de forma gráfica: `git log --oneline --graph --all`
- Saber en cuál rama estamos trabajando: `git branch`
- Para cambiarnos de rama: `git checkout nombre_rama`
- Hacer push en la nueva rama: `git push -u origin nombre_rama`
- Fusionar main con la rama(Rama_Temporal): `git merge nombre_rama`
- Mostrar las ramas privadas: `git branch -a`
- Borrar la rama temporal: `git branch -D nombre_rama`
- Borrar rama: `git branch -d nombre_rama`

### 3. Comandos de GIT

- Pasar los archivos al Área de ensayo (staking area): `git add .`
- Pasar los archivos al Repositorio Local: `git commit -m "mensaje"`
- Pasar el archivo desde el directorio de trabajo directamente al Repositorio Local (hacer add y commit a la vez): `git commit -am "mensaje"`
- Ver directorio del trabajo: `pwd`
- Ver el estado: `git status`
- Listado de todas las copias en el repositorio: `git log --oneline`
- Editar el último commit: `git commit --amend`
- Forzar push al repositorio remoto (¡Cuidado! Puede sobrescribir el trabajo de otros): `git push origin main --force`

### 4. Colaboración

- Se debe forkear el proyecto y hacer un pull request
- Cuando se tienen más de 1 cuenta, se debe hacer una configuracion local: `git config --local user.name "nombre_usuario"`

### 5. Restauración y eliminación

- Restaurar el archivo index.html: `git reset --hard 5404050`
- Elimina lo último siempre que sea antes del commit (luego del add .), BORRA TODO: `git reset --hard`
- Eliminar el historial y tener el repositorio como al principio: `git reset --mixed`
- PASOS PARA QUITAR EL SEGUIMIENTO A UN ARCHIVO QUE ESTA SUBIDO EN GITHUB:
  1. `git rm --cached src/environments/environment.ts`
  2. `git commit -m "Eliminar environment.ts del seguimiento de Git"`
  3. `git push`
- Eliminar una rama sin fusionar los cambios:
  1. `git switch main`
  2. `git branch -D feature#215y`
- Eliminar la rama si esta en remoto:
  1. `git push origin --delete feature#215y`
  2. `git checkout .` # Esto descartará todos los cambios en los archivos modificados
  3. `git clean -fd` # Esto eliminará todos los archivos no rastreados en tu directorio de trabajo, como archivos generados
  4. `git switch develop` # Esto te cambiará a la rama "develop"

### 6. Tags

- Con las tags podemos especificar la version: `git tag 15-09-20v1 -m "Versión 1 del proyecto”`
- Subir el tag: `git push --tags`
