
## VERSION DE GIT
cuando va con un guión(-) es porque irá con la abreviación(1 o 2 letras)

```bash
git --version
```


## AYUDA DE GIT


```bash
git help
git -h
# Documentación de un comando en especifico
git help [comando]
```

## CONFIGURACIÓN GLOBAL EN GIT

- Registrar usuario y correo
    ```bash
    git config --global user.name "[name]"
    git config --global user.email "[email@email.com]"
    ```
- Consultar usuario y correo
    ```bash
    git config user.name
    git config user.email
    git config --global --list
    ```

- Abrir archivo de configuración global de Git y edita

    ```bash
    git config --global -e
    ```
  
## INCIALIZAR UN PROYECTO
```bash
git config user.name
```

- configuración global de la rama por defecto
    ```bash
    git config --global init.defaultBranch <name>
    ```

## SEGUMIENTO *
Muestra el estado del árbol de trabajo y del área de ensayo (también conocido como índice). Te permite inspeccionar archivos modificados, preparados y sin rastrear para que decidas qué hacer a continuación.

```bash
git status
```


regresa a la ultima versión de git que se le hace seguimeinto
```bash
git checkout --.
```

ver cuales son las ramas y vemos en que rama estamos

## RAMAS
###  1. LISTAR RAMAS
```bash
# Ramas remotas
git branch

# Ramas remotas
git branch -r

# Ramas locales
git branch -a
```

###  2. CREAR Y BORRAR
```bash
# Crear una nueva rama
git branch <name>

# Borrar rama de forma segura, git no te dejara si tiene cambios pendientes
git branch -d <name>

# Borrar una rama a la fuerza.
git branch -D <name>
```

### 3. MODIFICA RAMAS
```bash
# Renombra el nombre de la rama en la que estoy
git branch -m <new-name>

# Renombra ramas locales
git branch -m <old-name> <new-name>
```

### 4. FILTRAR E INSPECCIONAR
```bash
# Ramas integradas a mi rama actual
git branch --merged

# Lista las ramas que tienen código nuevo que aún no has fusionado
git branch --no-merged

# Muestra las ramas locales detalladas, incluyendo su último commit y si están sincronizadas, adelantadas o atrasadas respecto a las ramas del servidor remoto
git branch -vv
```

## ANATOMÍA DE UN COMANDO DE GIT
```markdown
| [programa base] | [subcomando] | [flag] | [argument/object] |
|:----------------|:-------------|:-------|:------------------|
| git             | branch       | -d     | feature-login     |
```

### TABLA DE FLAGS PARA `git branch`
| Opción Corta | Opción Larga | Significado | ¿Se puede Forzar? | 
|:-------------|:-------------|:------------|:------------------|
| -d | --delete | Delete | SI (-D / --delete --force) |
| -m | --move | Modify / Move | SI (-M / --move --force) |
| -a | --all | All | NO Aplica |
| -r | --remotes | Remote | NO Aplica |
| -v | --verbose| Verbose | No fuerza duplica detalle (-vv / --verbose -- verbose) |


## AGREGAR ARCHIVOS AL ESCENARIO
Para agregar contenido de archivos al área de almacenamiento provisional.
```bash
git add <field-name1> <field-name2>

# Todos los archivos según tipo de archivo 
git add *.html

# staging todos los archivos dentro de una carpeta
git add <name-field>/*.gitkeep

# Todo lo que se modifico  en el working area pasara al Staging area
git add .
```

## CAMBIOS EN LOS ARCHIVOS

```bash
git diff

git diff -stage
```


```bash
git commit -m "[message]"
```

```bash
git checkout --."
```

Después de haber preparado algunos cambios para su confirmación, puede guardar el trabajo en una instantánea ejecutando el comando


ermite ver información sobre las confirmaciones anteriores. Cada confirmación tiene un mensaje adjunto (un mensaje de confirmación), y el comando git log permite imprimir información sobre las confirmaciones más recientes, como su marca de tiempo, el autor y un mensaje de confirmación