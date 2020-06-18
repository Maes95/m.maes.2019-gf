# Práctica 1 - Solución 
### Repositorios y modelos de desarrollo

A continuación se detalla como se ha resuelto la práctica utilizando Git Flow

### Paso 1: Creación y clonado del repositorio en GitHub

Desde la interfaz web https://github.com/ creamos un nuevo repositorio llamado `m.maes.2019-gf`

Una vez creado, inicializamos un nuevo proyecto git usando git flow y sincronizamos con GitHub:
```
$ mkdir m.maes.2019-gf
$ cd m.maes.2019-gf
$ git flow init -d 
$ git remote add origin https://github.com/Maes95/m.maes.2019-gf.git
$ git push -u origin develop
```

### Paso 2: Desarrollo de la Feature 1

En primer lugar, ese necesario crar una nueva rama para la feature 1

```
$ git flow feature start feature-1
```

Añadidmos 3 nuevos commits, cada uno creando los ficheros A, B y C respectivamente.

```
$ echo "'A' file content" > a.txt
$ git add a.txt
$ git commit -m "feature/feature-1 - Add file A"
```

```
$ echo "'B' file content" > b.txt
$ git add b.txt
$ git commit -m "feature/feature-1 - Add file B"
```

```
$ echo "'C' file content" > c.txt
$ git add c.txt
$ git commit -m "feature/feature-1 - Add file C"
```

Subimos estos cambios al repositorio remoto:

```
$ git push -u origin feature/feature-1
```

Finalizamos la feature 1:

```
$ git flow feature finish feature-1 -k
```

Esto mergeará la rama feature/feature-1 con develop, por lo que en siguiente paso es subir los cambios de develop:

```
$ git push -u origin develop
```

A contiuación creamos la Release 1.0.0:

```
$ git flow release start 1.0.0
$ git push -u origin release/1.0.0
$ git flow release finish 1.0.0
```

Esto mergeará la rama release/1.0.0 con master y le asignará un tag.

Subimos todos los cambios al repositorio remoto:

```
$ git push -u origin develop
$ git push -u origin master 
$ git push --tags
```


### Paso 3: Desarrollo de la Feature 2

Creamos una nueva rama con Git Flow para la Feature 2:

```
$ git flow feature start feature-2
```

Añadidmos 2 nuevos commits, el primero añadiendo el fichero D y el segundo modificando A:

```
$ echo "'D' file content" > d.txt
$ git add d.txt
$ git commit -m "feature/feature-2 - Add file D"
```

```
$ echo -e "F2-CHANGE $(cat a.txt)" > a.txt 
$ git add a.txt 
$ git commit -m "feature/feature-2 - Change first line of A"
```

Subimos estos cambios al repositorio remoto:

```
$ git push -u origin feature/feature-2
```

No cerramos aún la feature-2.

### Paso 4: Desarrollo de la Feature 3

Creamos una nueva rama con Git Flow para la Feature 3 (trabajamos en paralelo a la feature 2):

```
$ git flow feature start feature-3
```

Añadimos 2 nuevos commits, el primero añadiendo el fichero E y el segundo modificando A:

```
$ echo "'E' file content" > e.txt
$ git add e.txt
$ git commit -m "feature/feature-3 - Add file E"
```

```
$ echo -e "F3-CHANGE $(cat a.txt)" > a.txt 
$ git add a.txt 
$ git commit -m "feature/feature-3 - Change first line of A"
```

Subimos estos cambios al repositorio remoto:

```
$ git push -u origin feature/feature-3
```

### Paso 5: Damos por finalizada la feature 2 y publicamos release

Finalizamos la feature-2 (se mergea a develop) y actualizamos la rama develop
```
$ git flow feature finish feature-2 -k
$ git push -u origin develop
```

Realizamos la release 1.1.0:

```
$ git flow release start 1.1.0
$ git push -u origin release/1.1.0
$ git flow release finish 1.1.0
```

Actualizamos master y las tags:

```
$ git push -u origin develop
$ git push -u origin master 
$ git push --tags
```

### Paso 6: Corregimos el bug

Creamos una rama de hotfix
```
$ git flow hotfix start 1.1.1
```

Añadimos un nuevo commit con el fix (añadir fichero F):

```
$ echo "AWESOME FIX" > f.txt 
$ git add f.txt 
$ git commit -m "BUGFIX - Hotfix to solve a bug in production"
```

Subimos el hotfix y lo damos por finalizado:

```
$ git push -u origin hotfix/1.1.1
$ git flow hotfix finish 1.1.1
```

OJO: Incluirá este cambio en develop, dejandonos en esa rama.

Actualizamos master y las tags:

```
$ git push -u origin develop
$ git push -u origin master 
$ git push --tags
```

### Paso 7: Damos por finalizada la feature 3 y publicamos release

Finalizamos la feature-3 (se mergea a develop) y actualizamos la rama develop
```
$ git flow feature finish feature-3 -k
```

En este punto, el merge fallara, deberemos solucionar el conflicto a mano.

Una vez solucionado, creamos a mano el commit de merge:

```
$ git add a.txt
$ git commit -am "Solve conflict between develop and F3"
```

Volvemos a intentar cerrar la feature-3 y actualizamos develop

```
$ git flow feature finish feature-3 -k
$ git push -u origin develop
```

Realizamos la release 1.2.0:

```
$ git flow release start 1.2.0
$ git push -u origin release/1.2.0
$ git flow release finish 1.2.0
```

Actualizamos master y las tags:

```
$ git push -u origin master 
$ git push --tags
```
