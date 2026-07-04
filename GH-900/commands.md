
## VERSION DE GIT
```bash
git --version
```


## AYUDA DE GIT

```bash
git help
```

## CONFIGURACIÓN DE GIT

- Registrar usuario y correo
    ```bash
    git config --global user.name "[name]"
    git config --global user.email "[email@email.com]"
    ```
- Consultar usuario y correo
    ```bash
    git config user.name
    git config user.email
    ```

- Abrir archivo de configuración global de Git y edita

    ```bash
    git config --global -e
    ```

- configuración global de la rama por defecto
    ```bash
    git config --global init.defaultBranch <name>
    ```

## SEGUMIENTO

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
```bash
git add <field-name1> <field-name2>

# Todos los archivos según tipo de archivo 
git add *.html

# staging todos los archivos dentro de una carpeta
git add <name-field>/*.gitkeep
```

## CAMBIOS EN LOS ARCHIVOS

```bash
git diff

git diff -stage
```
