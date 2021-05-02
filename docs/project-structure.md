# Estructura del proyecto

Si hemos creado nuestro proyecto utilizando Expo CLI, la estructura de carpetas de nuestro proyecto debería ser similar a la siguiente:

![Estructura de un proyecto generado por Expo](https://miro.medium.com/max/247/1*R8ktGDONGT056CyZjIdqNg.png)

Tendremos los siguientes ficheros y carpetas:

- .expo-shared: Carpeta con ficheros de configuración de expo, que no nos interesa tocar de momento.

- assets: Carpeta que contendrá cualquier tipo de recurso (imágenes, audios, fuentes, ...) que necesitemos utilizar en nuestra aplicación.

- node_modules: Carpeta que contiene todas las dependencias de nuestro proyecto. Necesitamos esta carpeta en nuestro proyecto para que todo funcione correctamente. Si instalamos cualquier paquete de terceros (que lo haremos), será aquí donde se aloje.

- .gitignore: Fichero que ayuda a Git a decidir de qué ficheros debe realizar un seguimiento para el control de versiones.
  ¿Aún no sabes qué es Git? ¡Echa un vistazo a nuestro [taller de Git](https://aulasoftwarelibre.github.io/taller-de-git/)! Te aseguro que cuando descubras esta herramienta no podrás despegarte de ella.

- App.js: Este el fichero con el código que muestra nuestra aplicación al ser levantada con el comando start que hemos ejecutado previamente. Inicialmente habrá un componente funcional llamado App que contiene una plantilla (template) de código en JSX.

- app.json: Contiene información sobre nuestro proyecto, su nombre, sus plataformas soportadas, etc.

- package.json: Es el fichero utilizado por node para realizar el seguimiento de las dependencias del proyecto. Si añadimos alguna dependencia al proyecto, se reflejará en este fichero para que, en caso de que alguien se clone el proyecto, pueda instalar estas dependencias con `npm install`, ya que la carpeta _node_modules_ nunca debería subirse a Git.
  Además de las dependencias, este fichero también suele contener scripts que facilitan la ejecución de algunos comandos que suelen ejecutarse frecuentemente.
