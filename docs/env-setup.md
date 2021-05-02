# Preparación del entorno de desarrollo

Si eres nuevo en el desarrollo de aplicaciones móvil, la forma más sencilla de comenzar es con Expo CLI. Expo es un conjunto de herramientas construido alrededor de React Native y, si bien tiene muchas [características](https://expo.io/features), la característica más relevante es que permite crear una aplicación de React Native en escasos minutos. Solo necesitarás una versión reciente de Node.js y un teléfono o emulador. Si quieres, también puedes probar React Native directamente en tu navegador web antes de instalar cualquier herramienta, a través de [Snack](https://snack.expo.io/).

Si ya estás familiarizado con el desarrollo móvil, es posible que prefieras utilizar React Native CLI.
Esta opción requiere tener instalados Xcode o Android Studio. Si ya tienes una de estas herramientas instalada, deberías poder empezar a trabajar en unos minutos. Si no tienes ninguna de estas herramientas instalada, tardarás aproximadamente una hora en tener todo instalado y configurado.

En este taller, nos centraremos en Expo CLI, aunque en la [documentación de React Native](https://reactnative.dev/docs/next/environment-setup), puedes ver la guía para utilizar React Native CLI, si prefieres esta opción.

## Preparación del entorno con Expo CLI

En caso de tener la versión de Node 12 LTS o una más reciente, puedes usar npm para instalar el Expo CLI a través de una terminal, ejecutando el siguiente comando:

```
npm  install -g expo-cli
```

Después, con el siguiente comando, crearás un proyecto de React Native llamado "MiProyecto". Elige otro nombre si lo prefieres:

```
expo init AwesomeProject

cd AwesomeProject

npm start # you can also use: expo start
```

Con el primer comando crearemos el proyecto, con el segundo entraremos a la carpeta del mismo, generado con el comando anterior, y con npm start levantaremos un servidor local con nuestra aplicación.
