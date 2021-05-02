# Diseño con Flexbox

Un componente puede especificar el diseño de sus hijos usando el algoritmo Flexbox. Flexbox está diseñado para proporcionar un diseño uniforme en diferentes tamaños de pantalla.

Es normal que se utilice una combinación de `flexDirection`, `alignItems`y `justifyContent`para lograr la disposición correcta. Veamos que significan estas propiedades.

## Flex Direction

[`flexDirection`](https://reactnative.dev/docs/layout-props#flexdirection) establece la dirección en la que se distribuyen los elementos secundarios de un nodo padre. También se conoce como el eje principal. El eje transversal es el eje perpendicular al eje principal. Esta propiedad tiene los siguientes posibles valores:

- `column`( **valor por defecto** ) Alinea a los hijos de arriba a abajo.
- `row`Alinea a los hijos de izquierda a derecha.
- `column-reverse`Alinea a los hijos de abajo hacia arriba.
- `row-reverse`Alinea a los hijos de derecha a izquierda.

## Layout Direction

`direction` especifica la dirección en la que se deben distribuir los elementos secundarios y el texto en una jerarquía de elementos. También afecta a qué se refieren los valores `start`y `end`. De forma predeterminada, React Native tiene la dirección LTR. Con este valor, `start`se refiere a la izquierda y `end`a la derecha.

- `LTR`( **valor por defecto** ) El texto y los elementos secundarios se distribuyen de izquierda a derecha. El margen y el relleno aplicados al inicio de un elemento se aplican en el lado izquierdo.
- `RTL`El texto y los elementos secundarios se distribuyen de derecha a izquierda. El margen y el relleno aplicados al inicio de un elemento se aplican en el lado derecho.

## Justify Content

[`justifyContent`](https://reactnative.dev/docs/layout-props#justifycontent) indica cómo alinear a los hijos dentro del eje principal de su contenedor. Por ejemplo, puedes usar esta propiedad para centrar a un hijo horizontalmente dentro de un contenedor que tiene la propiedad`flexDirection`establecida en `row`, o verticalmente dentro de un contenedor con la propiedad `flexDirection`establecida en `column`.

- `flex-start`( **valor predeterminado** ) Alinea los elementos secundarios de un contenedor al inicio del eje principal del contenedor.
- `flex-end` Alinea los hijos de un contenedor al final del eje principal del contenedor.
- `center` Alinea los hijos de un contenedor en el centro del eje principal del contenedor.
- `space-between` Separa uniformemente a los hijos a lo largo del eje principal del contenedor, distribuyendo el espacio restante **entre los hijos**.
- `space-around`Separa uniformemente a los hijos a lo largo del eje principal del contenedor, distribuyendo el espacio restante **alrededor de los hijos**. En comparación con `space-between`, al usar `space-around` se distribuirá el espacio antes del primer hijo y después del último hijo.
- `space-evenly`Distribuye uniformemente a los hijos dentro del contenedor de alineación a lo largo del eje principal. El espacio entre cada par de elementos adyacentes, el espacio entre el inicio y el primer elemento, y el espacio entre el final y el último elemento, es exactamente el mismo.

## Align Items

[`alignItems`](https://reactnative.dev/docs/layout-props#alignitems) indica cómo alinear a los hijos a lo largo del eje transversal de su contenedor. Es muy similar a `justifyContent` pero en lugar de aplicarse al eje principal, se aplica al eje transversal.

- `stretch`( **valor predeterminado** ) Estira los elementos secundarios de un contenedor para que coincidan con el `height` del eje transversal del contenedor.

- `flex-start` Alinea los hijos de un contenedor al inicio del eje transversal del contenedor.

- `flex-end` Alinea los hijos de un contenedor al final del eje transversal del contenedor.

- `center` Alinea los hijos de un contenedor en el centro del eje transversal del contenedor.

- `baseline`Alinea los hijos de un contenedor a lo largo de una línea de base común. Se puede establecer que los hijos individuales sean la línea de base de referencia para sus padres.

## Align Self

[`alignSelf`](https://reactnative.dev/docs/layout-props#alignself) tiene las mismas opciones y efectos que `alignItems`, pero en lugar de afectar a los hijos dentro de un contenedor, puede aplicarse esta propiedad a un solo hijo para cambiar su alineación dentro de su padre. `alignSelf`anula cualquier opción establecida por el padre con `alignItems`.

## Flex Wrap

La propiedad [`flexWrap`](https://reactnative.dev/docs/layout-props#flexwrap) se establece en los contenedores y controla lo que sucede cuando los hijos desbordan el tamaño del contenedor a lo largo del eje principal. De forma predeterminada, los niños se ven obligados a entrar en una sola línea (lo que puede encoger elementos). Si se permite el envoltorio o wrapping, los elementos se envuelven en varias líneas a lo largo del eje principal si es necesario.

Al envolver líneas, se puede utilizar `alignContent` para especificar cómo se colocan las líneas en el contenedor.

## Align Content

[alignContent](https://reactnative.dev/docs/layout-props#aligncontent) indica la distribución de las líneas a lo largo del eje transversal. Esto solo tiene efecto cuando los elementos se envuelven en varias líneas usando `flexWrap`.

- `flex-start`( **valor por defecto** ) Alinea las líneas envueltas al inicio del eje transversal del contenedor.
- `flex-end` Alinea las líneas envueltas al final del eje transversal del contenedor.
- `stretch` Estira las líneas envueltas para que coincidan con la altura del eje transversal del contenedor.
- `center` Alinea las líneas envueltas en el centro del eje transversal del contenedor.
- `space-between` Las líneas envueltas se distribuyen uniformemente a través del eje transversal del contenedor, distribuyendo el espacio restante entre las líneas.
- `space-around`Las líneas envueltas se distribuyen uniformemente a través del eje transversal del contenedor, distribuyendo el espacio restante alrededor de las líneas. A diferencia de `space-between`, al usar `space-around`el espacio se distribuirá al principio de la primera línea y al final de la última línea.

Echa un vistazo al [Playground de Yoga Layout](https://yogalayout.com/playground), donde puedes probar todas estas propiedades y sus posibles valores.

Existen algunas propiedades más de Flexbox que pueden ser de utilidad en determinados casos, puedes obtener más información sobre estas en la [documentación oficial](https://reactnative.dev/docs/flexbox).
