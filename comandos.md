### POWER SHELL

- Crear archivo vacío

    - Opción 1:
        ```shell
        New-Item [name].md -ItemType File
        ```
    - Opción 2:
        ```shell
        ni [name].md
        ```

- Crear archivo con contenido
  - Opción 1:
    ```shell
    "# Mi primer archivo Markdown" | Out-File [name].md    
    ```

  - Opción 2:
    ```shell
    @"
    # Título
    Este es un archivo Markdown creado desde PowerShell.
    - Item 1
    - Item 2
    "@ | Out-File [name].md
    ```
---
### BASH
- Crear archivo vacío
  - Opción 1: 
  
    ```bash
    touch archivo.md
    ```
  
  - Opción 2:
    
    ```bash
    echo "# Mi primer archivo Markdown" > [name].md
    ```

- Crear archivo con contenido
  - Opción 1:
    ```bash
    cat <<EOF > [name].md
    # Título
    Este es un archivo Markdown creado desde Bash.
    - Item 1
    - Item 2
    EOF
    ``
    ```

---

### ABRIR ARCHIVO
- POWERSHELL

  ```shell
  # APERTURA RÁPIDA
  notepad [name].md
  # ABRIR CON EL EDITOR POR DEFECTO
  start [name].md
  ```

- BASH

  ```shell
  nano archivo.md
  # o
  code archivo.md
  ```




