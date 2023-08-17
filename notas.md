# Notas y ayudas

- [LINUX](#linux)
  - [Config Linux](#config-linux)
  - [Varios Consola Linux](#varios-consola-linux)
- [LARAVEL](#laravel)
  - [Varios ORM](#varios-orm)
  - [Varios Artisan](#varios-artisan)
- [MYSQL](#mysql)
    - [Mysql Query a CSV](#mysql-query-a-csv)
    - [Guia de estilo DB](#guia-de-estilo-db)
- [VIM](#vim-cheat-sheet)
- [GIT](#git)

---


## LINUX


### Config Linux
Configuración inicial de un servidor linux con el stack LEMP (Linux, NGINX, MySql, Php):
- Configuración Inicial: https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-22-04
- LEMP: https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-22-04
- NGINX: https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-22-04
- PHP8.1: https://www.digitalocean.com/community/tutorials/how-to-install-php-8-1-and-set-up-a-local-development-environment-on-ubuntu-22-04
- Composer: https://www.digitalocean.com/community/tutorials/how-to-install-and-use-composer-on-ubuntu-22-04
- Let's encrypt: https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-22-04
- Remote mysql: https://www.digitalocean.com/community/tutorials/how-to-allow-remote-access-to-mysql
- Ssh-key: https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server

[volver al inicio](#notas-y-ayudas)


### Varios consola linux
- Guardar la salida de un comando a un archivo:
  - Opcion 1: 
  ```
  command > file.txt
  ```
  - Opción 2: 
  ```
  command | tee -a file.txt
  ```

[volver al inicio](#notas-y-ayudas)



## Laravel


### Varios ORM
- Mostrar el query generado con los parámetros
```php
DB::enableQueryLog();
// código del query, ej: Users::where('email', 'like','gmail')->get()
dd(DB::getQueryLog());
```


### Varios Artisan

- Generar clave hash desde tinker:
```ssh
  php artisan tinker
  Hash::make('clave')
```
- Mostrar SQL generado por un migration:
```ssh
  php artisan migrate --pretend
```

[volver al inicio](#notas-y-ayudas)


## MySQl


### Mysql Query a CSV
Guardar un query en un archivo CSV separado por comas ",":
~~~
SELECT * FROM table WHERE id < 100 INTO OUTFILE '/home/usr/archivo.csv' FIELDS ENCLOSED BY '"' TERMINATED BY ',' ESCAPED BY '"' LINES TERMINATED BY '\r\n'; 
~~~
Si devuelve error:
~~~
ERROR 1290 (HY000): The MySQL server is running with the --secure-file-priv option so it cannot execute this statement
~~~
Encontrar la ruta segura con permiso de escritura:
~~~
SELECT @@GLOBAL.secure_file_priv;
~~~
Reemplazar la ruta en el query con la ruta segura: (ejemplo ruta segura: "/var/lib/mysql-files/")
~~~
SELECT * FROM table WHERE id < 100 INTO OUTFILE '/var/lib/mysql-files/archivo.csv' FIELDS ENCLOSED BY '"' TERMINATED BY ',' ESCAPED BY '"' LINES TERMINATED BY '\r\n'; 
~~~

[volver al inicio](#notas-y-ayudas)


### Guia de estilo DB


#### Tablas
Nombre de tablas:
- Minúscula | Snake case | Nombre descriptivo | Plural
- Ejemplos: 
  - usuarios, usuario_tipos, ordenes, orden_items
 
---

#### Campos
- Minúsculas | Snake case | Nombre descriptivo | Singular
  - Ejemplos:
    - nombre
    - password
    - tipo
    - valor
    - obs (observaciones)
- Todas las llaves primarias (primary key) deben llamarse "id"
- Las llaves foráneas (foreign keys) deben empezar con "id" y terminar con el nombre de la tabla relacionada en singular
  - Ejemplos:
    - Tabla usuarios: id, tabla roles: id_usuario
    - Tabla productos: id, table ordenes: id_producto

[volver al inicio](#notas-y-ayudas)


## VIM Cheat Sheet
__Varios__
- Abrir archivo: `vim [file]`
- Ver histórico de comandos: `q:`
- Quitar ajuste de página: `:set nowrap`
- Adicionar ajuste de página: `:set wrap`
- Ir al final del archivo: `shift + G`
- Ir al inicio del archivo: `gg`
- Mostrar los números de línea: `:number`
- Ir a una línea específica (ej: ir a la línea 100): `100G`
- Ocultar los números de línea: `:nonumber` 
- Buscar en el archivo: `? [texto de búsqueda]`
  - Ir al siguiente resultado de búsqueda: `n`
  - Ir a siguiente resultado de búsqueda: `N`
- Guardar: `:w`
- Salir y guardar: `:wq`
- Salir sin guardar: `:q!`

__Copiar - Pegar__
- Copiar una linea: `yy`
- Copiar multiple lineas: `y#y`
    - ejemplo: copiar 5 lineas a partir de la linea actual: `y5y`
- Pegar linea copiada después de la linea actual: `p`
- Pegar linea copiada antes de la linea actual: `P`


__Eliminar__
- Eliminar la linea actual: `dd`
- Eliminar varias lineas: (ej: eliminar 100 líneas a partir de la línea actual): `100dd`
- Eliminar rangos de líneas: `:[start],[end]d`
    - Ejemplos: 
        - Eliminar desde la fila 10 hasta la 20: `:10,20d`
        - Eliminar desde la linea actual a la última linea: `:.,$d`
        - Eliminar desde la linea actual al inicio del archivo: `:.,1d`

__Editar múltiples archivos__
- Mostrar archivos verticalmente: `vim -O fileA.txt fileB.txt`
- Mostrar archivos horizontalmente: `vim -o fileA.txt fileB.txt`
- Para cambiar entre archivos: `Ctrl + w + [h/j/k/l]` (que corresponden a izquierda, abajo, arriba y derecha respectivamente):

__BOOKMARKS__
- Vim copy, paste and delete: https://linuxize.com/post/how-to-copy-cut-paste-in-vim/
- Vim delete: https://linuxize.com/post/vim-delete-line/

[volver al inicio](#notas-y-ayudas)


## GIT


#### COMANDOS BÁSICOS
- Clonar un repositorio: `git clone username@host:/path/to/repository`
- Adicionar un archivo al stage: `git add <filename>`
- Adicionar varios archivos al stage: `git add -A`
- Hacer commit de los archivos adicionados: `git commit -m "Commit message"`
- Enviar los cambios al servidor remoto (rama master): `git push origin master`
- Ver el estatus de los archivos modificados: `git status`
- Crear una nueva rama y cambiarse a ella: `git checkout -b <branchname>`
- Cambiar de rama: `git checkout <branchname>`
- Traer los cambios en el servidor remoto al local: `git pull`
- Crear un tag (versión): `git tag 1.0.0 <commitID>`
- Eliminar un tag (versión): `git tag -d <commitID>`
- Enviar todos los tags al servidor remoto: `git push origin --tags`


#### VARIOS
- Mostrar el último commit de una rama local: **git log -n master**
 > (el modificador -n es la cantidad de registros de log a mostrar y master es el nombre de la rama)
- Mostrar los n commits con hash, tag y comment: **git log -n --pretty=format:"%h %d - %s"**
    - Ejemplo: 
    ```
        git log -1 --pretty=format:"%h %d - %s"
        95eb1565 (tag: 2.1.12) Fix: bug reportado por usuario
    ```    
- Deshacer cambios en un archivo en la rama local (discard changes): **git checkout -- file**
    y para todos los archivos (incluir el punto al final):  **git checkout -- .**

- Deshacer un git pull: **git reset --hard master@{"10 minutes ago"}**


#### ESTRUCTURA DE LOS MARCADORES DE CONFLICTOS:
```
<<<<<<< RAMA_ACTUAL
Cambios de esta rama...
=======
Cambios en la rama desde la que se origina el merge
 >>>>>>> RAMA_ORIGEN_MERGE
 ```

[volver al inicio](#notas-y-ayudas)
