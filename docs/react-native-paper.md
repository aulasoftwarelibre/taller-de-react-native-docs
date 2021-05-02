# React Native Paper

Los componentes core de React Native están muy bien y son suficientes para construir una aplicación funcional con todo tipo de características. Sin embargo, flaquean en algo que hay que tener muy en cuenta, y es que el estilo de estos componentes suele ser plano y poco llamativo, y para alguien que no haya tocado CSS lo suficiente, puede ser bastante tedioso estilar cada uno de los componentes de su aplicación para intentar conseguir un resultado más vistoso.

¿La solución? React Native Paper.

## ¿Qué es React Native Paper?

React Native Paper es una colección de componentes personalizables, multiplataforma y listos para ser usados con React Native, que siguen la guía de diseño Material Design de Google.

Esta librería nos provee de todo tipo de componentes, desde el más simple botón hasta una especie de carta con información e imágenes en ella. ¿Lo mejor? Que todos los componentes disponen de varias props que permiten personalizarlos a tu gusto.

## Instalación de dependencias y uso

Al igual que en casos anteriores, instalaremos la librería con un simple comando:

```
npm install react-native-paper
```

En caso de haber usado React Native CLI para la creación del proyecto, necesitamos instalar también el pack de iconos MaterialCommunityIcons, debido a que son usados por algunos de los componentes de Paper. Como en este taller hemos utilizado Expo CLI, no es necesario que instalemos estos iconos.

En caso de que tengamos un fichero _babel.config.js_ o _.babelrc_, necesitaremos añadir el preset _babel-preset-expo_ y el plugin _react-native-paper/babel_.

Para más información sobre la instalación y configuración inicial, visita la [documentación oficial de React Native Paper](https://callstack.github.io/react-native-paper/getting-started.html).

Envuelve el componente raíz del proyecto en un `Provider`de `react-native-paper`. Si has creado un proyecto vanilla de React Native, suele ser recomendado agregar el Provider en el componente que se pasa a `AppRegistry.registerComponent`, que por lo general, está en el archivo `index.js`. En nuestro caso, que hemos creado el proyecto con Expo, añadiremos el Provider en el fichero `App.js`.

```
import * as React from "react";
import { AppRegistry } from "react-native";
import { Provider as PaperProvider } from "react-native-paper";
import { name as appName } from "./app.json";
import App from "./src/App";

export default function Main() {
  return (
    <PaperProvider>
      <App />
    </PaperProvider>
  );
}

AppRegistry.registerComponent(appName, () => Main);
```

El componente PaperProvider provee a todos los componentes del proyecto del tema de React Native Paper, y actúa como portal para componentes que deben renderizarse en el nivel más alto.

### Personalizando el Tema por defecto

Como hemos mencionado en la sección previa, hemos envuelto a nuestra aplicación con un PaperProvider para dotar a los componentes del tema por defecto de Paper. Pero, ¿y si queremos cambiar este tema?

Para esto, el Provider dispone de una prop `theme` a la que podemos pasarle un tema definido previamente, tal que así:

```
import * as React from "react";
import { DefaultTheme, Provider as PaperProvider } from "react-native-paper";
import App from "./src/App";

const theme = {
  ...DefaultTheme,
  roundness: 2,
  colors: {
    ...DefaultTheme.colors,
    primary: "#3498db",
    accent: "#f1c40f",
  },
};

export default function Main() {
  return (
    <PaperProvider theme={theme}>
      <App />
    </PaperProvider>
  );
}
```

Echa un vistazo a la [documentación de React Native Paper](https://callstack.github.io/react-native-paper/theming.html) para ver todas las propiedades por defecto en un tema.

Además de las propiedades por defecto, podemos crear propiedades personalizadas, extendiendo el tema por defecto. Podemos hacer esto simplemente añadiendo una nueva propiedad en el objeto _theme_.

```
const theme = {
  ...DefaultTheme,
  // Propiedad personalizada
  myOwnProperty: true,
  // Propiedad personalizada en objeto anidado
  colors: {
    myOwnColor: "#BADA55",
  },
};
```

En caso de tener un proyecto en TypeScript, no funcionará correctamente con esta configuración, pero podemos aprovechar la _[global augmentation](https://www.typescriptlang.org/docs/handbook/declaration-merging.html#global-augmentation)_ y especificar las propiedades que hemos añadido al tema.

```
/// App.js
import * as React from "react";
import { DefaultTheme, Provider as PaperProvider } from "react-native-paper";
import App from "./src/App";

declare global {
  namespace ReactNativePaper {
    interface ThemeColors {
      myOwnColor: string;
    }

    interface Theme {
      myOwnProperty: boolean;
    }
  }
}
/// ... Resto del código anterior
```

## Componentes, iconos y fuentes

Ya tenemos todo listo para usar React Native Paper en nuestro proyecto, echa un vistazo a la variedad de componentes que ofrece la librería y sustituye los componentes en alguna de las vistas que hemos realizado anteriormente. El cambio es bastante notorio, y la aplicación tiene un aspecto mucho más moderno.

<img src="https://callstack.github.io/react-native-paper/gallery/button.png" width="300px" />
<img src="https://callstack.github.io/react-native-paper/gallery/card.png" width="300px" />
<img src="https://callstack.github.io/react-native-paper/gallery/list-accordion.png" width="300px" />
