## Paso 3: Agregar Features

Se puede personalizar aún más el codespace agregando features de container, extensiones de VS Code, configuraciones de VS Code, requisitos del host y mucho más.

Agreguemos el GitHub CLI, extensiones para ejecutar el programa python usando VS Code, y un script personalizado para instalar algunos paquetes al crear el Codespace por primera vez.

### ⌨️ Actividad: Agregar soporte para Python

1. En VS Code, abrir la Paleta de Comandos (Command Palette) (`CTRL`+`SHIFT`+`P`) y seleccionar el siguiente comando.

   ```txt
   Codespaces: Add Dev Container Configuration Files...
   ```

   <img width="350" alt="vs code configure dev container command" src="../images/configure-dev-container-command.png" />

1. Seleccionar la opción `Modify your active configuration...`.

1. En la lista de features, buscar y seleccionar `Python` de `devcontainers`.

   - En lugar de los valores predeterminados, elegir `Configure Options`.
   - Dejar `Install Tools` configurado en `true`.
   - Seleccionar versión de Python: `3.10`

1. Navegar y abrir el archivo `.devcontainer/devcontainer.json`.

1. Verificar que se agregó una nueva entrada similar a la siguiente.

   ```json
   "features": {
      "ghcr.io/devcontainers/features/python:1": {
         "installTools": true,
         "version": "3.10"
      }
   },
   ```

### ⌨️ Actividad: Agregar extensiones de VS Code

1. En la navegación izquierda, seleccionar la pestaña **Extension** (Extensiones).

   <img width="200" alt="vs code extensions tab" src="../images/vs-code-extensions-tab.png" />

1. Buscar `python` y encontrar las entradas para `Python` y `Python Debugger`.

   <img width="250" alt="python extensions for vs code" src="../images/python-extensions.png" />

1. Hacer clic derecho en cada entrada y seleccionar la opción `Add to devcontainer.json`.

   <img width="250" alt="add to devcontainer config button" src="../images/add-to-devcontainer-button.png" />

1. Navegar y abrir el archivo `.devcontainer/devcontainer.json`.

1. Verificar que se agregó una nueva entrada similar a la siguiente.

   ```json
   "customizations": {
      "vscode": {
         "extensions": [
            "ms-python.python",
            "ms-python.debugpy"
         ]
      }
   },
   ```

### ⌨️ Actividad: Agregar un script personalizado

La especificación Dev Container proporciona múltiples ubicaciones para ejecutar [scripts de ciclo de vida](https://containers.dev/implementors/json_reference/#lifecycle-scripts) para personalizar aún más el Codespace. Agreguemos el `postCreateCommand` que se ejecuta una sola vez después de la construcción inicial (o reconstrucción).

1. Usar el explorador de archivos de VS Code para crear un archivo de script con el siguiente nombre.

   ```txt
   .devcontainer/postCreate.sh
   ```

   Alternativamente, ejecutar el siguiente comando de terminal para crearlo.

   ```bash
   touch .devcontainer/postCreate.sh
   ```

1. Hacer el script ejecutable ejecutando el siguiente comando de terminal.

   ```bash
   chmod +x .devcontainer/postCreate.sh
   ```

1. Abrir el archivo `.devcontainer/postCreate.sh` y agregar el siguiente código, que instalará una animación de una locomotora de vapor.

   ```bash
   #!/bin/bash

   sudo apt-get update
   sudo apt-get install sl
   echo "export PATH=\$PATH:/usr/games" >> ~/.bashrc
   echo "export PATH=\$PATH:/usr/games" >> ~/.zshrc
   ```

1. Navegar y abrir el archivo `.devcontainer/devcontainer.json`.

1. Crear la entrada `postCreateCommand` al mismo nivel (_nivel superior_) que `features` y `customizations`.

   ```json
   "postCreateCommand": ".devcontainer/postCreate.sh"
   ```

1. Con nuestra nueva configuración terminada, hagamos commit de los cambios. Usar las herramientas de control de código de VS Code o el siguiente comando de terminal.

   ```shell
   git add '.devcontainer/devcontainer.json'
   git add '.devcontainer/postCreate.sh'
   git commit -m 'feat: Add features, extensions, and postCreate script'
   git push
   ```

1. Abrir la Paleta de Comandos (Command Palette) de VS Code (`CTRL`+`Shift`+`P`) y ejecutar el comando `Codespaces: Rebuild Container`. Seleccionar la opción **Rebuild** (Reconstruir). No es necesaria una construcción completa.

   <img width="350" alt="rebuild codespace command" src="../images/rebuild-codespace-command.png"/>

1. Esperar unos minutos para que el Codespace se reconstruya y VS Code se reconecte.

1. Con las personalizaciones confirmadas, Mona comenzará a revisar el trabajo. Darle un momento para proporcionar retroalimentación y los siguientes pasos de aprendizaje.

> [!TIP]
> También se puede configurar la cuenta para [instalar dotfiles](https://docs.github.com/en/codespaces/setting-your-user-preferences/personalizing-github-codespaces-for-your-account), permitiendo combinar configuraciones personales con la configuración del proyecto.

### ⌨️ Actividad: (opcional) Verificar nuestras personalizaciones

Ahora que se ha reconstruido el codespace, verifiquemos que la extension de python, la versión de python y el script personalizado se ajustaron correctamente en el Codespace.

1. Asegurarse de estar en el Codespace.

1. En la barra lateral izquierda, hacer clic en la pestaña de extensiones (extensions) y verificar que las extensiones de Python estén instaladas y habilitadas.

   <img width="250" alt="python extensions for vs code" src="../images/python-extensions.png" />

1. En la barra lateral izquierda, seleccionar la pestaña **Run and Debug** (Ejecutar y Depurar) y luego presionar el icono **Start Debugging** (Iniciar Depuración). VS Code abrirá el panel inferior y mostrará los logs de ejecución.

   <img width="250" alt="run and debug tab pointing to start button" src="../images/run-and-debug-start-button.png"/>

1. En el panel inferior, cambiar a la pestaña **TERMINAL**.

1. Ejecutar el siguiente comando para mostrar la versión instalada de Python. Notar que las otras no están instaladas.

   ```bash
   node --version
   dotnet --version
   python --version
   gh --version
   ```

1. Ejecutar el siguiente comando para mostrar la animación de la locomotora de vapor.

   ```bash
   sl
   ```
