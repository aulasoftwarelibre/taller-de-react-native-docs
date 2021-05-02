# Aplicando estilos a componentes

Con React Native, diseñas tu aplicación usando JavaScript. Todos los componentes principales aceptan una prop llamada `style`. Las propiedades y [valores de](https://reactnative.dev/docs/colors) estilo suelen coincidir con las propiedades de CSS en desarrollo web, excepto que los nombres se escriben en camelCase, por ejemplo, `backgroundColor`en lugar de `background-color`.

La prop `style`puede ser un simple objeto JavaScript. Eso es lo que hemos visto en algunos ejemplos anteriores. También podemos pasar un array de estilos; el último estilo del array tiene prioridad sobre el resto, por lo que puede usarse para heredar estilos.

A medida que un componente crece en complejidad, es recomendable usar `StyleSheet.create`para definir varios estilos en un solo sitio. Observa el siguiente ejemplo:

```
import React from "react";
import { StyleSheet, Text, View } from "react-native";

const LotsOfStyles = () => {
  return (
    <View style={styles.container}>
      <Text style={styles.red}>just red</Text>
      <Text style={styles.bigBlue}>just bigBlue</Text>
      <Text style={[styles.bigBlue, styles.red]}>bigBlue, then red</Text>
      <Text style={[styles.red, styles.bigBlue]}>red, then bigBlue</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    marginTop: 50,
  },
  bigBlue: {
    color: "blue",
    fontWeight: "bold",
    fontSize: 30,
  },
  red: {
    color: "red",
  },
});

export default LotsOfStyles;
```

También podemos hacer que un componente acepte una prop style que afecte a subcomponentes del mismo, lo que se conoce como estilos en cascada.
