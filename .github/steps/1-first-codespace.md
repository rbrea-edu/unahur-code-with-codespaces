## Paso 1: Iniciar un codespace y enviar código

### ¿Cuál es la ventaja de los Codespaces?

Un **codespace** es un entorno de desarrollo alojado en la nube, definido por archivos de configuración en el repository. Esto crea un entorno de desarrollo repetible adaptado específicamente al proyecto, que simplifica la incorporación de desarrolladores y evita la famosa frase "¡Funciona en mi máquina!" 😎

Cada codespace sigue la [especificación Dev Container](https://containers.dev/implementors/spec/) y es alojado por GitHub como un [contenedor de Docker](https://code.visualstudio.com/docs/devcontainers/containers).

¡Pero no preocuparse! ¡No es necesario conocer Docker ni siquiera tenerlo instalado en la máquina!

> [!TIP]
> Dado que la configuración del Dev Container es parte del repository, ¡también se puede usar localmente con el propio host de Docker! ¡Excelente!

Un Codespace tiene varias ventajas/características en comparación con el desarrollo local. Por mencionar algunas:

- Iniciar un codespace directamente desde la página del repository.
- Desarrollar en el navegador. No se requiere instalación de IDE.
  - Opción de usar una instalación local de VS Code para conectar al Codespace remoto.
- Preconfigurar todo lo necesario para ejecutar el proyecto:
  - Agregar **[features](https://containers.dev/features)** para instalar necesidades comunes de desarrollo.
  - Ejecutar scripts en varias etapas del ciclo de vida del codespace _(por ejemplo, instalar paquetes python/npm)_.
  - Configurar ajustes y extensiones de VS Code para coincidir con las necesidades del proyecto.
- Acceso rápido a internet (ya que el container está en el datacenter).

> [!TIP]
> Los Codespaces son incluso útiles en situaciones de corta duración como revisar un pull request. No es necesario verificar que se tenga la configuración correcta para probar los cambios de código entrantes.

¡Comencemos! Iniciaremos un Codespace, ejecutaremos la aplicación, haremos un cambio y lo enviaremos. ¡Como el desarrollo normal! 🤓

### ⌨️ Actividad: Iniciar un codespace

1. Abrir una segunda pestaña y navegar a este repository. Asegurarse de estar en la pestaña **Code** (Código).

1. Sobre la lista de archivos a la derecha, hacer clic en el botón verde **<> Code** (Código).

   <img width="300" alt="green code button" src="https://github.com/rbrea-edu/unahur-code-with-codespaces/blob/main/.github/images/green-code-button.png?raw=true" />

1. Seleccionar la pestaña **Codespaces** y hacer clic en el botón **Create codespace on main** (Crear codespace en main). Se abrirá una nueva ventana ejecutando VS Code y se conectará al Codespace remoto. Esperar unos minutos para que se cree el codespace.

1. Mirar en la parte inferior izquierda de la ventana de VS Code para ver la conexión remota.

   <img width="350" alt="remote connection status in VS Code" src="https://github.com/rbrea-edu/unahur-code-with-codespaces/blob/main/.github/images/remote-connection-status.png?raw=true"/>

> [!TIP]
> GitHub usa la imagen de Codespace [universal](https://github.com/devcontainers/images/tree/main/src/universal) si el repository no incluye una configuración. Incluye varias herramientas útiles y comúnmente usadas.

### ⌨️ Actividad: Ejecutar la aplicación

1. Asegurarse de estar en el Codespace de VS Code.

1. En la barra lateral izquierda, seleccionar la pestaña **Explorer** (Explorador) y abrir el archivo `src/hello.py`.

   <img width="250" alt="vs code explorer tab" src="https://github.com/rbrea-edu/unahur-code-with-codespaces/blob/main/.github/images/vs-code-explorer-tab.png?raw=true" />

1. En el panel inferior, seleccionar la pestaña **TERMINAL**.

   <img width="350" alt="vs code terminal tab" src="https://github.com/rbrea-edu/unahur-code-with-codespaces/blob/main/.github/images/vs-code-terminal-tab.png?raw=true" />

1. Pegar el siguiente comando en el terminal remoto del Codespace para mostrar las versiones instaladas de varias herramientas. Anotar las versiones para comparar más adelante.

   ```bash
   node --version
   dotnet --version
   python --version
   gh --version
   ```

1. Pegar el siguiente comando para ejecutar el programa Python en el terminal remoto del Codespace.

   ```bash
   python src/hello.py
   ```

### ⌨️ Actividad: Enviar cambios al repository desde el codespace

1. Reemplazar el contenido del archivo `src/hello.py` con lo siguiente y guardar el archivo.

   ```py
   print("Hello World!")
   ```

1. Con el mensaje actualizado, hacer commit del cambio y enviarlo a GitHub. Usar las herramientas de control de código de VS Code o los siguientes comandos de terminal.

   ```bash
   git add 'src/hello.py'
   git commit -m 'fix: incomplete hello message'
   git push
   ```

1. (opcional) De vuelta en el navegador web, abrir el archivo `src/hello.py` para verificar que el cambio fue actualizado.

1. Con el cambio enviado a GitHub, Mona comenzará a revisar el trabajo. Darle un momento para proporcionar retroalimentación y los siguientes pasos de aprendizaje.
