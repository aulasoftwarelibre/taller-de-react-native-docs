# React Navigation

Antes de entrar en materia con la navegación a través de nuestra aplicación, la cual conseguiremos utilizando React Navigation, es de gran utilidad tener claro cómo funciona la navegación en un navegador web.

En un navegador web, nuestro historial de navegación actúa como una pila de URLs. Los enlaces se crean con la etiqueta de anclaje (`<a>`) en HTML. Cuando el usuario hace clic en un enlace, la URL en la que nos encontrábamos se envía a la pila del historial del navegador y navegamos a la página enlazada. Si el usuario presiona el botón Atrás, el navegador mostrará el elemento de la parte superior de la pila del historial, por lo que la página activa pasará a ser la página visitada anteriormente.

React Native no tiene una idea incorporada de un historial global o pila de URLs como lo hace un navegador web; y es aquí donde React Navigation entra en escena.

## Instalación de dependencias

Antes de nada, debemos instalar las dependencias esenciales para que React Navigation funcione correctamente. En la carpeta del proyecto, ejecuta el siguiente comando:

```
expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view
```

Esto instalará las versiones de estas librerías compatibles con la versión de React Native en la que se encuentre nuestro proyecto.

En React Navigation existen distintos tipos de navigators, pero en este taller nos centraremos en el Stack Navigator, que es el más similar al de un navegador web.

## Stack Navigator

El Stack Navigator de React Navigation nos provee de un mecanismo para navegar entre las distintas vistas de nuestra aplicación y gestionar un historial de navegación.

Si tu aplicación utiliza un único stack navigator, sería conceptualmente similar a la forma en la que un navegador gestiona su estado de navegación - tu aplicación mete o saca elementos de su pila de navegación a medida que el usuario interactúa con esta, y esto resulta en el usuario viendo distintas vistas.

La diferencia respecto a un navegador web es que el stack navigator de React Navigation está provisto de los gestos y animaciones que verías en una aplicación de Android o iOS al navegar entre rutas.

Para diferenciar entre los navigators de React Navigation, y un navegador web, no se traducirá el concepto navigator cuando estemos hablando del primero de estos.

### Instalación de la librería del stack navigator

Las librerías que hemos instalado hasta ahora son los cimientos del resto de navigators, y cada navigator en React Navigation tiene su propia librería.

Para utilizar el stack navigator, necesitaremos instalar [`@react-navigation/stack`](https://github.com/react-navigation/react-navigation/tree/main/packages/stack), ejecutando el siguiente comando.

```
npm  install @react-navigation/stack
```

### Creación de un Stack Navigator

`createStackNavigator` es una función que devuelve un objeto que contiene 2 propiedades: `Screen` y `Navigator`. Ambos son componentes de React que se utilizan para configurar el navigator. El `Navigator` debe contener elementos `Screen` como elementos hijo para definir la configuración de rutas.

`NavigationContainer` es un componente que administra nuestro árbol de navegación y contiene el [estado de navegación](https://reactnavigation.org/docs/navigation-state). Este componente debe envolver la estructura de todos los navigators. Por lo general, renderizamos este componente en la raíz de nuestra aplicación, que suele ser el componente exportado desde `App.js`.

```
// App.js

import * as React from 'react';
import { View, Text } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';

function HomeScreen() {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>Home Screen</Text>
    </View>
  );
}

const Stack = createStackNavigator();

function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen name="Home" component={HomeScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

export default App;
```

![Preview de App.js](https://reactnavigation.org/assets/images/basic_stack_nav-7388d409c412d0c728a0903301338433.png)

Si ejecutas este código, verás una pantalla con una barra de navegación vacía y un área de contenido gris que contiene el componente `HomeScreen`, definido justo antes de App. Los estilos de la barra de navegación y el área de contenido son la configuración predeterminada para un stack navigator, y aprenderemos cómo configurarlos más adelante.

El primer componente Screen que pasemos a nuestro stack navigator será la **ruta inicial**. Prueba a crear un componente `Details`, que sea igual a `Home` pero cambiando el texto del contenido para diferenciarlos. A continuación, crea un componente Screen y pasa el componente Details como prop. Ahora, prueba a poner este `Screen` en primer lugar, guarda el fichero y tu aplicación debería mostrar la vista de `Details`.

### Especificando opciones al navigator

Cada vista en el navigator puede tener sus opciones específicas, como el título que se renderiza en el encabezado. Estas opciones pueden pasarse como una prop _options_ para cada componente `Screen`:

```
<Stack.Screen
  name="Home"
  component={HomeScreen}
  options={{ title: 'Overview' }}
/>
```

A veces nos interesará especificar las mismas opciones para todas las vistas del navigator. Para ello, podemos pasar una prop _screenOptions_ al navigator.

### Pasando props adicionales

En caso de querer pasar props personalizadas a una vista, podemos conseguirlo de dos formas:
Sometimes we might want to pass additional props to a screen. We can do that with 2 approaches:

- Utilizar [React context](https://reactjs.org/docs/context.html) y envolver el navigator con un provider de contexto para pasar datos a las vistas (recomendado).
- Utilizar un callback de renderizado en lugar de pasar un componente como prop:

```
<Stack.Screen name="Home">
  {props => <HomeScreen {...props} extraData={someData} />}
</Stack.Screen>
```

## Navegación entre vistas

Todo bien pero...¿Cómo consigo navegar entre rutas de mi aplicación? Vamos a ello.

En la sección anterior, hemos definido un stack navigator con dos rutas ( `Home`y `Details`), pero no hemos aprendido cómo conseguir que un usuario navegue de `Home`a `Details` (aunque sí aprendimos cómo cambiar la ruta _inicial_ en nuestro código, pero obligar a nuestros usuarios a clonar nuestro repositorio y cambiar la ruta en el código para ver otra pantalla es posiblemente una de las peores experiencias de usuario que uno podría imaginar).

Si este fuera un navegador web, podríamos escribir algo como esto:

```
<a href="details.html">Go to Details</a>
```

O esto:

```
<a
  onClick={() => {
    window.location.href = 'details.html';
  }}
>
  Go to Details
</a>
```

Haremos algo similar, pero en lugar de utilizar un objeto global `window.location`, usaremos el prop `navigation` del cual disponen nuestros componentes `Screen` de manera automática.

Observa el siguiente ejemplo:

```
import * as React from 'react';
import { Button, View, Text } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';

function HomeScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>Home Screen</Text>
      <Button
        title="Go to Details"
        onPress={() => navigation.navigate('Details')}
      />
    </View>
  );
}

// ... código de la sección anterior
```

Veamos esto con detalle:

- navigation: El prop navigation es pasado en cada uno de los componentes screen del stack navigator.
- navigate('Details') - llamamos a la función _navigate_ de la prop _navigation_ (los nombres son algo confusos al principio) con el nombre de la ruta a la que queremos navegar.

> Si llamamos a `navigation.navigate` con un nombre de ruta que no hemos definido en un navigator, imprimirá un error en las builds (compilaciones) de desarrollo y no pasará nada en las builds de producción. Dicho de otra manera, solo podemos navegar a rutas que hayan sido definidas en nuestro navegador, no podemos navegar a un componente arbitrario.

Entonces, ahora tenemos una pila con dos rutas: 1) la ruta `Home` 2) la ruta `Details`. ¿Qué pasaría si volviéramos a navegar a la ruta `Details`, desde la vista `Details`?

Pongamos que el código de nuestro componente Details fuera el siguiente:

```
function DetailsScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>Details Screen</Text>
      <Button
        title="Go to Details... again"
        onPress={() => navigation.navigate('Details')}
      />
    </View>
  );
}
```

Si ejecutas este código, notarás que cuando tocas "Go to Details...again", ¡no hace nada! Esto se debe a que ya estamos en la ruta de Details. La función `navigate` significa, en realidad, "ir a esta ruta", y si ya estás ahí, tiene sentido que no haga nada.

Supongamos que realmente queremos agregar otra vista de Details. Esto es bastante común en casos en los que se pasa algún dato único a cada ruta (más adelante explicaremos cómo hacerlo). Para hacer esto, podemos cambiar `navigate` a `push`. Esto nos permite expresar la intención de agregar otra ruta, independientemente del historial de navegación existente.

```
<Button
  title="Go to Details... again"
  onPress={() => navigation.push('Details')}
/>
```

Cada vez que llamamos a _push_, se añade una nueva ruta a la pila de navegación. Cuando llamamos a _navigate_ intenta encontrar una ruta existente con el nombre especificado, y solo pushea una nueva ruta en caso de no encontrarla en la pila.

El encabezado proporcionado por el stack navigator incluirá automáticamente un botón de retroceso cuando sea posible volver desde la pantalla activa (si solo hay una pantalla en la pila de navegación, no hay nada a lo que se pueda volver, por lo que no hay botón de retroceso).

En caso de necesitar este comportamiento en algún otro sitio, puedes usar `navigation.goBack();`

```
function DetailsScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>Details Screen</Text>
      <Button
        title="Go to Details... again"
        onPress={() => navigation.push('Details')}
      />
      <Button title="Go to Home" onPress={() => navigation.navigate('Home')} />
      <Button title="Go back" onPress={() => navigation.goBack()} />
    </View>
  );
}
```

Otro caso de uso común es querer retroceder varias pantallas, por ejemplo, si tienes varias pantallas en una pila y quieres descartarlas todas para volver a la primera pantalla. Si quisiéramos volver a `Home`, podríamos hacerlo usando `navigate('Home')`( ¡no uses _push_! Pruébalo y mira la diferencia). Otra alternativa sería utilizar `navigation.popToTop()`, que te devuelve a la primera pantalla de la pila.

```
function DetailsScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>Details Screen</Text>
      <Button
        title="Go to Details... again"
        onPress={() => navigation.push('Details')}
      />
      <Button title="Go to Home" onPress={() => navigation.navigate('Home')} />
      <Button title="Go back" onPress={() => navigation.goBack()} />
      <Button
        title="Go back to first screen in stack"
        onPress={() => navigation.popToTop()}
      />
    </View>
  );
}
```

## Pasar parámetros a rutas

Ahora que sabemos cómo crear un stack navigator con algunas rutas, pasemos a ver cómo podemos pasar datos a las rutas cuando navegamos hacia ellas.

Hay dos pasos clave para esto:

1.  Pasar los parámetros a una ruta, contenidos en un objeto, como segundo parámetro de la función `navigation.navigate`:

```
navigation.navigate('RouteName', { /* los parámetros irían aquí here */ })
```

2.  Leer los parametros en el componente de la pantalla utilizando `route.params`.

```
function HomeScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>Home Screen</Text>
      <Button
        title="Go to Details"
        onPress={() => {
          /* 1. Navigate to the Details route with params */
          navigation.navigate('Details', {
            itemId: 86,
            otherParam: 'anything you want here',
          });
        }}
      />
    </View>
  );
}

function DetailsScreen({ route, navigation }) {
  /* 2. Get the param */
  const { itemId, otherParam } = route.params;
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>Details Screen</Text>
      <Text>itemId: {JSON.stringify(itemId)}</Text>
      <Text>otherParam: {JSON.stringify(otherParam)}</Text>
      <Button
        title="Go to Details... again"
        onPress={() =>
          navigation.push('Details', {
            itemId: Math.floor(Math.random() * 100),
          })
        }
      />
      <Button title="Go to Home" onPress={() => navigation.navigate('Home')} />
      <Button title="Go back" onPress={() => navigation.goBack()} />
    </View>
  );
}
```

![Ejemplo de parámetros en una ruta](https://reactnavigation.org/assets/images/passing_params-69f71caabd25eb4226631c1fff19d8ef.png)

Las pantallas también pueden actualizar sus parámetros, al igual que pueden actualizar su estado. el método `navigation.setParams` permite actualizar los parámetros de una pantalla.

```
navigation.setParams({
  query: 'someText',
})
```

Consulta la [documentación oficial](https://reactnavigation.org/docs/navigation-prop#setparams) para obtener más información sobre setParams.

También puedes pasar parámetros iniciales a una pantalla. Si no especificas ningún parámetro al navegar a esta pantalla, se utilizarán los parámetros iniciales. También se añadirán a cualquier parámetro que pases a una pantalla. Los parámetros iniciales se pueden especificar con la prop `initialParams`:

```
<Stack.Screen
  name="Details"
  component={DetailsScreen}
  initialParams={{ itemId: 42 }}
/>
```

### ¿Qué debería pasar en los parámetros a una pantalla?

Es importante comprender qué tipo de datos deben incluirse en los parámetros. Los parámetros son como opciones para una pantalla. Solo deben contener información para configurar lo que se muestra en la pantalla. Evita pasar todos los datos que se mostrarán en la misma (por ejemplo, puedes un ID de usuario en lugar de un objeto de User). Evita también pasar datos que son utilizados por múltiples pantallas, dichos datos deberían estar en una [store global](https://es.reactjs.org/docs/context.html).

```
// ¡No hagas esto!
navigation.navigate('Profile', {
  user: {
    id: 'jane',
    firstName: 'Jane',
    lastName: 'Done',
    age: 25,
  },
});
```

Esto puede parecer conveniente y permite acceder a los objetos de usuario `route.params.user` sin ningún trabajo adicional.

Sin embargo, esto se trata de un anti-patrón. Los datos, como los objetos de usuario, deberían estar en una store global en lugar de en el estado de navegación. De lo contrario, tendrás los mismos datos duplicados en varios sitios. Esto puede generar errores, como que la pantalla de perfil muestre datos desactualizados, incluso si el objeto del usuario ha cambiado después de la navegación.
