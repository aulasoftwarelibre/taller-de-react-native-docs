# Ancho y alto de un componente

La altura y el ancho de un componente determinan su tamaño en la pantalla.

## Dimensiones fijas

La forma general de establecer las dimensiones de un componente es agregando estilos fijos `width`y `height`. Todas las dimensiones en React Native no tienen unidades y representan píxeles independientes de la densidad, es decir, píxeles que son independientes de las dimensiones de la pantalla.

```
import React from "react";
import { View } from "react-native";

const FixedDimensionsBasics = () => {
  return (
    <View>
      <View
        style={{
          width: 50,
          height: 50,
          backgroundColor: "powderblue",
        }}
      />
      <View
        style={{
          width: 100,
          height: 100,
          backgroundColor: "skyblue",
        }}
      />
      <View
        style={{
          width: 150,
          height: 150,
          backgroundColor: "steelblue",
        }}
      />
    </View>
  );
};

export default FixedDimensionsBasics;
```

Esta forma de indicar el ancho y alto se usa cuando queremos que un componente siempre tenga ese alto y ancho especificados, y que no se calcule en base al tamaño de la pantalla.

## Dimensiones flex (flexibles)

Usa`flex`en el estilo de un componente para que el componente se expanda y encoja dinámicamente según el espacio disponible. Es común usar `flex: 1`, que indica a un componente que llene todo el espacio disponible, compartido uniformemente entre otros componentes con el mismo padre. Cuanto mayor sea el valor de `flex` de un componente, mayor será la proporción de espacio que ocupará este en comparación con sus elementos hermanos.

```
import React from "react";
import { View } from "react-native";

const FlexDimensionsBasics = () => {
  return (
    // Try removing the `flex: 1` on the parent View.
    // The parent will not have dimensions, so the children can't expand.
    // What if you add `height: 300` instead of `flex: 1`?
    <View style={{ flex: 1 }}>
      <View style={{ flex: 1, backgroundColor: "powderblue" }} />
      <View style={{ flex: 2, backgroundColor: "skyblue" }} />
      <View style={{ flex: 3, backgroundColor: "steelblue" }} />
    </View>
  );
};

export default FlexDimensionsBasics;
```

## Dimensiones en porcentajes

Si quieres llenar una cierta proporción de la pantalla, pero prefieres no usar `flex`, puedes usar **valores porcentuales** en el estilo del componente. Al igual que las dimensiones flexibles, las dimensiones porcentuales requieren un padre con un tamaño definido.

```
import React from "react";
import { View } from "react-native";

const PercentageDimensionsBasics = () => {
  // Try removing the `height: '100%'` on the parent View.
  // The parent will not have dimensions, so the children can't expand.
  return (
    <View style={{ height: "100%" }}>
      <View
        style={{
          height: "15%",
          backgroundColor: "powderblue",
        }}
      />
      <View
        style={{
          width: "66%",
          height: "35%",
          backgroundColor: "skyblue",
        }}
      />
      <View
        style={{
          width: "33%",
          height: "50%",
          backgroundColor: "steelblue",
        }}
      />
    </View>
  );
};

export default PercentageDimensionsBasics;
```
