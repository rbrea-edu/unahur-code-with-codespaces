## Paso 2: Usar una image personalizada en el codespace

No se especificó ninguna configuración para el codespace que acabamos de crear, por lo que GitHub usó una image de Docker predeterminada. Si bien esto es muy útil, no será consistente y no bloquea la versión de nuestro entorno de ejecución. Especificar la configuración es importante para mantener el entorno de desarrollo repetible.

Hagamos eso ahora proporcionando una image de container de Docker específica.

### ¿Cómo configurar un Codespace?

La configuración se proporciona directamente en el repository a través del archivo `.devcontainer/devcontainer.json`. ¡Incluso se pueden agregar múltiples configuraciones!

Creemos este archivo y establezcamos algunas de las configuraciones más comunes. Para otras opciones como configurar VS Code, reenviar puertos y ejecutar scripts de ciclo de vida, ver la [documentación de Codespaces](https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces) en GitHub.

### ⌨️ Actividad: Personalizar el codespace

1. Asegurarse de estar en el Codespace de VS Code.

1. Usar el explorador de archivos de VS Code para crear el archivo de configuración.

   ```txt
   .devcontainer/devcontainer.json
   ```

   Alternativamente, ejecutar el siguiente comando de terminal para crearlo.

   ```bash
   mkdir -p .devcontainer
   touch .devcontainer/devcontainer.json
   ```

1. Abrir el archivo `.devcontainer/devcontainer.json` y agregar el siguiente contenido. Comencemos con una image básica.

   ```json
   {
     "name": "Basic Dev Environment",
     "image": "mcr.microsoft.com/vscode/devcontainers/base:debian"
   }
   ```

   > 💡 **Consejo**: El nombre es opcional pero ayudará a identificar la configuración al crear un codespace en GitHub, si hay múltiples opciones.

1. Después de guardar, VS Code probablemente mostró una notificación indicando que detectó un cambio de configuración. Se puede **Aceptar** esa opción para reconstruir el container de desarrollo o manualmente usar la Paleta de Comandos (Command Palette) (`CTRL`+`Shift`+`P`) y ejecutar el comando `Codespaces: Rebuild Container`. Seleccionar la opción **Rebuild** (Reconstruir). No es necesaria una construcción completa.

   <img width="350" alt="rebuild codespace command" src="../images/rebuild-codespace-command.png"/>

1. Esperar unos minutos para que el Codespace se reconstruya y VS Code se reconecte.

1. Expandir el panel inferior y seleccionar la pestaña **TERMINAL**.

1. Usar el siguiente comando para verificar las versiones de las herramientas nuevamente. ¡Notar que ahora ninguna está instalada!

   ```bash
   node --version
   dotnet --version
   python --version
   gh --version
   ```

1. ⚠️ Actualmente hay un bug con Codespaces que espera que [Git-LFS](https://git-lfs.com/) esté instalado. Ejecutar el siguiente comando para eliminar los hooks de Git afectados.

   ```bash
   rm .git/hooks/post-checkout
   rm .git/hooks/post-commit
   rm .git/hooks/post-merge
   rm .git/hooks/pre-push
   ```

1. Con nuestra nueva configuración verificada, hagamos commit de los cambios. Usar las herramientas de control de código de VS Code o el siguiente comando de terminal.

   ```bash
   git add '.devcontainer/devcontainer.json'
   git commit -m 'feat: Add codespace configuration'
   git push
   ```

1. Con nuestra configuración de dev container confirmada, Mona comenzará a revisar el trabajo. Darle un momento para proporcionar retroalimentación y los siguientes pasos de aprendizaje.
