# Fundamentos básicos de React

React Native se ejecuta en React, una librería de código abierto muy popular, utilizada para la creación de interfaces de usuario con JavaScript, y de la cual tenemos un pequeño taller en el canal. Para sacar el máximo provecho de React Native, necesitamos entender conceptos básicos de React. Cubriremos brevemente los siguientes conceptos fundamentales de React:

- Componentes
- JSX
- Props
- State (estado)

Si quieres adentrarte más en estos y otros conceptos de React, echa un vistazo a la [ documentación oficial](https://reactjs.org/docs/getting-started.html).

## JSX

React y React Native utilizan JSX, una sintáxis que permite escribir elementos dentro de JavaScript, como el siguiente ejemplo:

```
const AnyCat = () => {
  return (
    <Text>Hello, I am a cat!</Text>
  );
}
```

JSX es al fin y al cabo JavaScript, por lo que puede usar variables dentro de este. En el siguiente ejemplo, declararemos un _name_ para un gato.

```
const Cat = () => {
  const name = "Maru";
  return (
    <Text>Hello, I am {name}!</Text>
  );
}
```

Los dos ejemplos anteriores son lo que se conocen como componentes, en los que indagaremos a continuación.

## Componentes

Los componentes son piezas de código independientes y reutilizables que funcionan de manera similar a funciones de JavaScript, aceptando entradas arbitrarias llamadas Props, y devolviendo a React elementos que describen lo que debería aparecer por pantalla. Estos componentes se dividen en Componentes de Clase y Componentes Funcionales. El siguiente ejemplo, se trata de un componente funcional.

```
import React from 'react';
import { Text } from 'react-native';

const Cat = () => {
  return (
    <Text>Hello, I am your cat!</Text>
  );
}
export default Cat;
```

Los componentes de clase tienden a ser algo más detallados de lo necesario.

```
import React, { Component } from 'react';
import { Text } from 'react-native';

class Cat extends Component {
  render() {
    return (
      <Text>Hello, I am your cat!</Text>
    );
  }
}

export default Cat;
```

Como se puede observar, en ambos casos necesitamos importar React, que nos permitirá utilizar código JSX.

## Props

Props es la abreviatura de **propiedades**. Las props te permiten personalizar componentes de React. En el siguiente ejemplo, pasaremos una propiedad _name_ al componente Cat a través de un componente Cafe.

```
import React from 'react';
import { Text, View } from 'react-native';

const Cat = (props) => {
  return (
    <View>
      <Text>Hello, I am {props.name}!</Text>
    </View>
  );
}
const CatsCafe = () => {
  return (
    <View>
      <Cat name="Maru" />
      <Cat name="Jellylorum" />
      <Cat name="Spot" />
    </View>
  );
}

export default CatsCafe;
```

El componente Cafe consta de una vista que renderiza tres gatos, cada uno con su propio nombre.

La mayoría de componentes core de React Native también disponen de props para personalizarlos a tu gusto. Por ejemplo, el componente _Image_ dispone de una propiedad _source_ para indicar la imagen que debe mostrar.

```
<Image
	source={{uri: "https://reactnative.dev/docs/assets/p_cat1.png"}}
	style={{width: 200, height: 200}}
/>
```

_Image_ tiene un gran número de propiedades, incluyendo _style_, que acepta un objeto de JavaScript que contiene pares **propiedad-valor** relacionados con el diseño del elemento.

> Echa un vistazo a la propiedad style y a las llaves dobles que contienen a las propiedades width and height. En JSX, los valores de JavaScript son referenciados con `{}`. Esto es muy útil cuando estamos pasando algo distinto de un string como una propiedad, como un array o un número. `<Cat food={["fish", "kibble"]} age={2} />`.
> Sin embargo, los objetos de JavaScript también son marcados utilizando llaves: `{width: 200, height: 200}`. Por ello, para pasar un objeto de JS en JSX, debes contener el objeto en otro par de llaves, como en el ejemplo anterior.

Puedes construir muchísimas cosas utilizando props y los componentes core de React Native, como `Text`,`Image` o `View`, pero para crear algo interactivo, necesitarás un state o estado.

## State

El state de un componente funciona como su almacén de datos personal. Es útil para manejar datos que cambian a lo largo del tiempo, o que dependen de una interacción del usuario. ¡El state brinda a tus componentes de su propia memoria!

> Como regla general, usa props para configurar el renderizado de un componente. Utiliza el state para realizar un seguimiento de cualquier dato en un componente que esperas que cambie a lo largo del tiempo.

Observa el siguiente ejemplo de un componente de clase con state:

```
import React, { Component } from "react";
import { Button, Text, View } from "react-native";

class Cat extends Component {
  state = { isHungry: true };

  render() {
    return (
      <View>
        <Text>
          I am {this.props.name}, and I am
          {this.state.isHungry ? " hungry" : " full"}!
        </Text>
        <Button
          onPress={() => {
            this.setState({ isHungry: false });
          }}
          disabled={!this.state.isHungry}
          title={
            this.state.isHungry ? "Pour me some milk, please!" : "Thank you!"
          }
        />
      </View>
    );
  }
}
```

En resumen, se trata de un componente Cat con un state booleano _isHungry_ cuyo valor por defecto es true.
Cuando pulsamos en el botón, se ejecuta la función indicada en la prop _onPress_ del mismo, estableciendo la propiedad a false, cambiando el valor de las props _title_ y _disabled_.

¿Por qué se ha utilizado un componente de clase para el ejemplo del estado? ¿No eran menos legibles y demasiado detallados? Esto es correcto, pero tiene su explicación.

Hasta la llegada de los hooks de React, los componentes de clase eran los únicos que nos permitían manejar un estado y un ciclo de vida en nuestros componentes. Sin embargo, desde la aparición de estos, es posible tener un estado en componentes funcionales, cuya semántica es mucho más simple y limpia.

Un hook es una pequeña función que permite a un componente "engancharse" ("hook into") a características de React. Por ejemplo, _useState_ es un Hook que te permite añadir state a un componente funcional. El siguiente ejemplo, es exactamente igual al anterior, pero utilizando un componente funcional:

```
import React, { useState } from "react";
import { Button, Text, View } from "react-native";

const Cat = (props) => {
  const [isHungry, setIsHungry] = useState(true);

  return (
    <View>
      <Text>
        I am {props.name}, and I am {isHungry ? "hungry" : "full"}!
      </Text>
      <Button
        onPress={() => {
          setIsHungry(false);
        }}
        disabled={!isHungry}
        title={isHungry ? "Pour me some milk, please!" : "Thank you!"}
      />
    </View>
  );
}
```

Al llamar al hook useState, hacemos dos cosas:

- Crear una variable de state con un valor inicial. En el ejemplo anterior, la variable es _isHungry_ y su valor inicial es _true_.
- Crea una función para reestablecer el valor de esa variable, _setIsHungry_.

En este taller, por tanto, nos centraremos en los componentes funcionales, ya que, además de sus ventajas frente a los componentes de clase, haremos uso de algún otro Hook de React.
