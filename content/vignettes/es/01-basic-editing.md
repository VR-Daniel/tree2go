# Lo básico: hacia un árbol listo para publicar

Esta viñeta recorre los pasos principales para editar un árbol en tree2go, desde abrir un conjunto de árboles hasta exportar la figura final. En principio, cubre la mayoría de las opciones básicas para personalizar un árbol y convertirlo en una figura lista para publicar. Otras funciones más específicas se tratan en otras viñetas.

Estos tutoriales son breves y no pretenden explicar cada menú en detalle, sino dar una visión rápida de las opciones disponibles. Para información más detallada, consulta la [guía de referencia de las opciones](https://vr-daniel.github.io/tree2go/#reference).

Como ejemplo, usamos un conjunto de datos simulado que incluye todo lo necesario para mostrar la mayor parte de lo que tree2go puede hacer. Tiene 31 especies de vertebrados: 24 vivas y 7 fósiles. Aunque el ejemplo usa nombres de especies reales, y sus valores se eligieron para parecer razonables desde el punto de vista biológico, todos los datos son ficticios. **Cualquier patrón o conclusión obtenidos de estos datos no tiene significado biológico.**

## 1. Los archivos que necesitamos

Los árboles y las redes filogenéticas provienen de muchos programas y métodos distintos, y en muchas variantes. Para este tutorial, preparamos un conjunto de archivos listos para usar, agrupados en carpetas que siguen las secciones del panel izquierdo de tree2go. Cubren muchos de los tipos y formatos de archivo que puedes encontrar en los análisis filogenéticos, así que también pueden servir más adelante como referencia cuando importes tus propios datos. Los archivos se pueden descargar desde [este enlace](https://github.com/VR-Daniel/tree2go/tree/main/content/examples), y son los siguientes:

```text
vertebrates/
├── Tree/
│   ├── vertebrates_ml.nwk                    Árbol de máxima verosimilitud (Newick), longitudes de rama en sustituciones por sitio
│   ├── vertebrates_mcc.tre                   Árbol MCC (NEXUS), longitudes de rama en tiempo, con una tasa morfológica ficticia
│   └── vertebrates_posterior.trees           10.001 árboles calibrados en el tiempo (NEXUS) de un análisis bayesiano
├── Clades/
│   └── clade_groups.txt                      Clados para resaltar (uno por línea), como Clade={sp1, sp2, …}
├── Phylogenetic networks/
│   └── heliconius_network.nwk                Red de mariposas Heliconius (eNewick), con una especie híbrida y una introgresión
├── Ancestral reconstructions/
│   └── vertebrates_habitat.simmap            100 mapas estocásticos de caracteres para hábitat (formato SIMMAP, como lo escribe phytools)
├── Attachments/
│   ├── regions.csv                           Presencia (1) o ausencia (0) de cada especie en distintas regiones geográficas
│   ├── traits.csv                            Rasgos categóricos y continuos de cada especie
│   ├── vertebrates_traits_heatmap.csv        Cinco rasgos continuos de cada especie
│   └── vertebrates_alignment.fasta           Alineamiento de ADN de 100 pb de las especies vivas (FASTA)
├── Geography/
│   └── fossil_records.csv                    Registros de ocurrencia de los sitios de muestreo de las especies fósiles
└── Tanglegram/
    └── vertebrates_alternative.nwk           El mismo árbol con una topología alternativa (Newick)
```

## 2. Abrir un árbol o un conjunto de árboles

Haz clic en `Open tree` en la sección **Tree** del panel izquierdo. tree2go lee archivos en formato NEXUS y Newick, sea cual sea su extensión. Un archivo con un solo árbol se dibuja de inmediato. Un archivo con muchos árboles, como la muestra posterior de un análisis bayesiano, se lee como un **conjunto de árboles**.

Si el archivo contiene más de 10.000 árboles, se abre una ventana antes de leerlos (Fig. 1A), donde puedes elegir:

- *Burn-in*: el porcentaje de los primeros árboles que se descartan.
- *Keep*: cuántos árboles conservar después del burn-in, como número o como porcentaje.
- *Which trees*: si los árboles conservados están espaciados uniformemente o se eligen al azar (con una semilla, para poder obtener de nuevo la misma muestra).

La misma ventana se abre cuando se eligen varios archivos de árboles a la vez, como los archivos `.t` de las corridas de un análisis de MrBayes. En ese caso, tree2go los lee como un único conjunto de árboles, el burn-in se aplica a cada corrida, se conserva el mismo número de árboles de cada una, y los árboles conservados se combinan. Después, en la sección **Tree**, puedes elegir qué corridas usar (*Runs used*) y ver qué tanto concuerdan (ASDSF).

tree2go también revisa la estructura de las anotaciones de los árboles al leer un archivo. Cuando las llaves o los corchetes no están pareados, algo que puede ocurrir cuando un archivo pasa por varios programas, la app lo detecta en la mayoría de los casos y ofrece repararlo (Fig. 1B). Es un problema real que suele pasar desapercibido, ya que el archivo se abre igualmente, pero que daña en silencio los cálculos y gráficos que dependen de esas anotaciones. tree2go repara solo la estructura de las anotaciones, no puede recuperar valores que otros programas perdieron o cambiaron.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig01-window.png" alt="La ventana que aparece antes de leer un archivo con más de 10.000 árboles, con campos para el burn-in, el número de árboles a conservar y cómo elegirlos"><figcaption><b>Figura 1A.</b> La ventana que aparece antes de leer un archivo con más de 10.000 árboles, con un burn-in y el número de árboles a conservar.</figcaption></figure>
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig01-repair.png" alt="La ventana que avisa de anotaciones cuyas llaves no están pareadas, indica dónde, y ofrece cargar el archivo con la reparación"><figcaption><b>Figura 1B.</b> La ventana que aparece al abrir un archivo cuyas anotaciones tienen llaves sin pareja.</figcaption></figure>
  </div>
</figure>

Para este tutorial, abramos `vertebrates_posterior.trees`, que contiene 10.001 árboles. En la ventana, ponemos un burn-in de `10`% y conservamos 9.000 árboles que quedan después de él (Fig. 1A).

> **Nota.** Cuantos más árboles tiene un archivo, más memoria necesita. tree2go no tiene un límite propio más allá de la memoria que el navegador da a cada pestaña, pero las muestras muy grandes hacen más lenta la app, según el número de puntas y las anotaciones de cada árbol. Como regla general, una muestra de 10.000 árboles es más que suficiente para los árboles resumen.

## 3. Resumir los árboles

Una vez leídos los árboles, la sección **Tree** muestra cuántos se conservaron (Fig. 2). Desde ahí puedes mostrar cualquier árbol del conjunto, o construir un árbol resumen: un consenso (estricto, de mayoría o de máxima compatibilidad), un árbol de máxima credibilidad de clados (MCC) o un árbol de máximo a posteriori (MAP). El árbol MAP necesita además el archivo `.p` de MrBayes o el archivo `.log` de BEAST2, adjuntos en **Attachments**.

Aquí construimos un árbol MCC, que debería ser casi idéntico al de `vertebrates_mcc.tre`. Como ya descartamos el 10% de los árboles al leer el archivo, dejamos el *Burn-in* de esta sección en `0`. Y como los árboles están calibrados en el tiempo, ponemos *Node ages* en `Median`, para que cada nodo tome la mediana de sus edades en la muestra. Luego hacemos clic en `Build summary tree`.

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig02-panel.png" alt="La sección Tree con un conjunto de árboles cargado, Maximum clade credibility elegido como árbol resumen y Median como edades de los nodos">
  <figcaption><b>Figura 2.</b> La sección Tree, construyendo un árbol MCC con las edades medianas de los nodos a partir de la muestra de árboles.</figcaption>
</figure>

La sección **Tree** también tiene una subsección **Reading properties**, con dos opciones que hacen más ligero el trabajo con archivos grandes. Ambas se aplican al siguiente archivo que abras:

- *Significant digits of branch lengths* (de 1 a 10): menos dígitos usan menos memoria, pero pueden redondear las ramas muy cortas.
- *Keep the trees in a compact binary form*: guarda en memoria una copia más ligera de cada árbol. Si está desactivada, los árboles se guardan como texto, lo que hace más lenta la app con archivos muy grandes.

## 4. Organizar el árbol

La sección **Layout** cambia la forma del árbol y su tamaño. Como regla general, cada opción del panel izquierdo cambia todo el árbol a la vez, mientras que un `Right-click` sobre cualquier elemento del lienzo cambia solo ese elemento (o los elementos seleccionados).

Aquí ponemos **Layout** > *Order nodes* en `Decreasing`, para que los clados más grandes queden abajo, y le damos a la raíz una rama corta de `25` px con **Layout** > *Root branch*, que marca dónde empieza el árbol (Fig. 3A–B). Ambas son decisiones puramente estéticas. Siéntete libre de probar las otras formas y opciones. Todos los elementos del lienzo se adaptan a estos cambios.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig03-panel.png" alt="La sección Layout, con Order nodes en Decreasing y una rama de raíz de 25 px"><figcaption><b>Figura 3A.</b> Opciones de Layout.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig03-canvas.png" alt="El árbol con sus clados ordenados por tamaño y una rama de raíz corta"><figcaption><b>Figura 3B.</b> El árbol MCC, con sus clados ordenados por tamaño y una rama de raíz corta.</figcaption></figure>
  </div>
</figure>

Aunque no la usamos en la figura final, la sección **Tree cloud** dibuja todos los árboles del conjunto superpuestos, como hace DensiTree (Fig. 4), para mostrar la incertidumbre en la topología y en las edades. Solo está disponible para conjuntos de árboles.

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig04-cloud.png" alt="Los árboles de la muestra dibujados uno sobre otro detrás del árbol MCC">
  <figcaption><b>Figura 4.</b> Los árboles de la muestra dibujados como una nube de árboles.</figcaption>
</figure>

> **Nota.** Puedes personalizar el aspecto de la nube de árboles: grosor de línea, color, opacidad, cuántos árboles se dibujan y cómo se eligen. Como dibujar muchos árboles puede hacer más lenta la app, recomendamos desactivar **Tree cloud** > *Show the trees of the sample* mientras sigues editando, y volver a activarla antes de exportar. tree2go recuerda tus elecciones en esta sección.

## 5. Ramas

La sección **Branches** define el aspecto de todas las ramas. En árboles con especies vivas y extintas, las ramas de las puntas extintas son discontinuas por defecto, y sus nombres llevan una daga (†). Para cambiar esto solo en algunas ramas, selecciónalas con `Shift` + clic y cambia su aspecto desde su menú de `Right-click`. En árboles solo de especies extintas, o en árboles no calibrados en el tiempo, todas las ramas son continuas por defecto.

Las subsecciones **Color by data** y **Width by data** colorean las ramas, o cambian su grosor, según cualquier valor del árbol (Fig. 5A), sus propias anotaciones o una tabla adjunta en la sección **Attachments**. Los colores pueden elegirse uno a uno (`Custom colors`) o tomarse de una paleta, varias de las cuales son seguras para el daltonismo.

En nuestro ejemplo, ponemos **Branches** > *Line width* en `1.5` px y, en **Color by data**, coloreamos las ramas por `rate_median`, que aquí representa una tasa de evolución morfológica de un análisis bayesiano, con la paleta `Magma` (Fig. 5B).

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig05-panel.png" alt="La subsección Color by data, coloreando las ramas por rate_median con la paleta Magma"><figcaption><b>Figura 5A.</b> Opciones de Color by data.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig05-canvas.png" alt="El árbol con sus ramas coloreadas de oscuro a claro según su tasa evolutiva"><figcaption><b>Figura 5B.</b> Ramas coloreadas según su tasa evolutiva con una paleta segura para el daltonismo.</figcaption></figure>
  </div>
</figure>

> **Nota.** La paleta de toda la sesión se define en `Page settings`, en el encabezado. Cambia los colores que se ofrecen a partir de ese momento, pero no los que ya se dieron a los elementos. El mismo menú tiene `Page settings` > *Color blind preview*, que muestra la figura como se vería con distintas deficiencias en la visión del color. Solo cambia lo que ves en pantalla, la figura conserva sus colores cuando vuelves a la visión normal o la exportas.

## 6. Valores, nodos y su incertidumbre

La sección **Branch values** escribe en cada rama cualquier valor del árbol o de una tabla adjunta, y define su aspecto: posición, alineación, tamaño, color y número de decimales.

La sección **Nodes** añade símbolos a los nodos internos y a las puntas, con el mismo aspecto para todos o con un aspecto definido por un valor del árbol o de una tabla adjunta.

La sección **Node values** reúne los valores que suelen mostrarse en los nodos:

- **Support values**: como números o como símbolos, cuyo color o tamaño cambia con el valor. Para mantener limpia la figura, puedes mostrar solo los valores dentro de un rango que elijas.
- **Other node labels**: cualquier otro valor del árbol o de una tabla adjunta, con varias formas de alinearlo.
- **Node bars**: en árboles calibrados en el tiempo con incertidumbre en sus edades, como nuestro árbol MCC, la incertidumbre de cada nodo puede dibujarse como una barra HPD o como un violín (*Show the ages as*). Su aspecto, tamaño y color pueden cambiarse como los de cualquier otro elemento.

En nuestro ejemplo, primero mostramos los **Support values** como números, dejando el resto de opciones como están. Luego, en **Other node labels**, mostramos (*Show*) `Age, median of the trees` como número, y ponemos *Stack with the support values* en `Below the branch` (Fig. 6A). Siéntete libre de explorar otras opciones que se ajusten al objetivo visual que quieras lograr.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig06-panel.png" alt="La sección Node values, con los valores de soporte como números y las edades medianas de los nodos apiladas debajo de la rama"><figcaption><b>Figura 6A.</b> Valores de soporte y edades de los nodos en la sección Node values.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig06-canvas.png" alt="El árbol con el valor de soporte sobre cada nodo y su edad mediana debajo de la rama, con un círculo rojo alrededor de valores que se superponen"><figcaption><b>Figura 6B.</b> La edad de cada nodo mostrada como un segundo valor, debajo de su soporte.</figcaption></figure>
  </div>
</figure>

En muchos casos, especialmente en clados grandes con ramas cortas, algunos valores terminan uno encima de otro (círculo rojo en la Fig. 6B). Hay varias formas de resolverlo. Una es mover por separado cada etiqueta que se superpone, cambiando su desplazamiento desde su menú de `Right-click`. Otra, la que seguimos aquí, es reemplazar los números por símbolos cuyo tamaño y color den una pista visual de su valor.

Para ello, volvemos a ocultar las edades de los nodos y cambiamos los valores de soporte de `Number` a `Circles`. Luego, en *Which values*, elegimos `By categories`, con tres rangos: negro para soportes menores de 80, azul de 80 a 95, y rojo por encima de 95. También mantenemos un tamaño de círculo distinto para cada rango (Fig. 7A–B).

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig07-panel.png" alt="La subsección Support values, mostrando los soportes como círculos en tres rangos, cada uno con su color y tamaño"><figcaption><b>Figura 7A.</b> Valores de soporte mostrados como símbolos, por categorías.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig07-canvas.png" alt="El árbol con un círculo negro, azul o rojo en cada nodo según su soporte"><figcaption><b>Figura 7B.</b> El árbol con sus valores de soporte mostrados como símbolos.</figcaption></figure>
  </div>
</figure>

A continuación, como nuestro árbol proviene de una muestra de árboles, podemos mostrar la incertidumbre en las edades de los nodos. Algunos programas la escriben en las anotaciones de un solo árbol, como un rango HPD del 95%, que puede dibujarse como una barra. Como tenemos la muestra completa, podemos ir un paso más allá y mostrar cómo se distribuyen las edades dentro de ese rango, como gráficos de violín, desde la subsección **Node bars** (Fig. 8A–B). Como cualquier otro elemento de la app, los gráficos de violín pueden personalizarse por completo en tamaño y color, y también pueden mostrar otros valores, como la media y la mediana.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig08-panel.png" alt="La subsección Node bars, con las edades mostradas como violines"><figcaption><b>Figura 8A.</b> La subsección Node bars, donde las edades pueden mostrarse como una barra HPD o como densidades.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig08-canvas.png" alt="El árbol con un gráfico de violín en cada nodo que muestra la distribución de su edad"><figcaption><b>Figura 8B.</b> El árbol con gráficos de violín en sus nodos, que muestran la incertidumbre de las edades en la muestra.</figcaption></figure>
  </div>
</figure>

> **Nota.** En árboles fechados, la mediana de las barras HPD y de los gráficos de violín debería quedar sobre los nodos. tree2go reconoce a partir de los propios árboles si sus longitudes de rama están en tiempo. En algunos árboles, sin embargo, la estructura es ambigua, y los árboles fechados pueden leerse como no fechados, lo que deja las medianas de las distribuciones fuera de sus nodos. Si esto ocurre, indícale a la app que los árboles están fechados con **Tree** > *Trees in time*.

## 7. Nombres de las puntas

La sección **Tip labels** define el aspecto y la posición de los nombres de las puntas. Aquí activamos *Align labels to the right*, para que todos los nombres terminen en una misma columna (Fig. 9A–B). Esto es especialmente útil en árboles cuyas puntas no llegan todas al presente, como los árboles con fósiles, o en árboles con longitudes de rama en sustituciones por sitio.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig08-canvas.png" alt="El árbol con los nombres de sus puntas fósiles junto al final de sus ramas"><figcaption><b>Figura 9A.</b> Nombres de las puntas sin alinear.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig09-canvas.png" alt="El árbol con todos los nombres de las puntas alineados en una columna, con las puntas fósiles resaltadas en amarillo"><figcaption><b>Figura 9B.</b> Nombres de las puntas alineados en una columna, con las puntas fósiles resaltadas en amarillo para que el cambio se vea mejor.</figcaption></figure>
  </div>
</figure>

Como mencionamos antes, tree2go reconoce automáticamente el tipo de árbol, y con él las ramas que pertenecen a fósiles. Pero si miramos con atención nuestro ejemplo, vemos que *Mammuthus primigenius* (mamut lanudo) y *Smilodon fatalis* (tigre dientes de sable) no tienen ni la rama discontinua ni la daga que los marca como fósiles. No es un error, sino una cuestión de la escala del árbol.

Para distinguir los fósiles de las especies vivas, tree2go admite una pequeña tolerancia, las puntas que terminan a menos del 0,5% de la altura del árbol respecto al presente siguen contando como vivas, para que el redondeo de las longitudes de rama no convierta especies vivas en fósiles. En un árbol que abarca más de 450 millones de años, como el nuestro, ese 0,5% equivale a más de dos millones de años, y ambas especies se extinguieron hace solo unos 12.000 años. La solución es sencilla, reducimos **Fossils** > *Tolerance (% of the tree height)* a un valor muy pequeño, como `0.001` (Fig. 10A–B).

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig10-panel.png" alt="La sección Fossils, con la tolerancia reducida a 0.001%"><figcaption><b>Figura 10A.</b> La sección Fossils y sus opciones.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig10-canvas.png" alt="Las puntas del mamut lanudo y del tigre dientes de sable dibujadas como fósiles, con ramas discontinuas y una daga"><figcaption><b>Figura 10B.</b> Las puntas fósiles después de reducir la tolerancia.</figcaption></figure>
  </div>
</figure>

> **Nota.** Como cualquier otro elemento, los nombres de las puntas pueden editarse uno a uno desde su menú de `Right-click`, o varios a la vez después de seleccionarlos con `Shift` + clic. Renombrar una punta solo cambia el nombre que se muestra. El nombre original se conserva por debajo, así que la punta mantiene su vínculo con los datos adjuntos. Si se renombraron algunas puntas y el árbol se exporta como NEXUS o Newick, tree2go pregunta si escribir los nombres nuevos, tal como aparecen en la figura, o los originales.

## 8. Clados

La sección **Clades** resalta y nombra clados, y define el aspecto de sus resaltados y de sus barras de nombre. Los clados pueden elegirse directamente en el lienzo, con `Select mode` en el encabezado:

- `Element` selecciona un nodo o una rama.
- `Clade` selecciona un nodo con todos sus descendientes.

Los resaltados y los nombres se aplican a la selección, y pueden cubrir todo el clado, solo sus linajes vivos (corona) o solo sus linajes extintos (tallo). Un resaltado puede ser un bloque de color sólido o un degradado, de izquierda a derecha o de derecha a izquierda.

Si ya sabes qué puntas pertenecen a cada grupo, también puedes escribir un archivo de texto plano, como `clade_groups.txt`, con un clado por línea en el formato `Clade={sp1, sp2, …}`. Cada clado necesita al menos dos puntas, escritas como aparecen en el árbol. Con `Highlight clades from a file…` o `Name clades from a file…`, tree2go encuentra el ancestro común más reciente de las puntas de cada clado, y resalta o nombra ese clado por ti (Fig. 11A).

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig11-canvas.png" alt="El árbol rectangular con varios clados principales resaltados y nombrados desde un archivo"><figcaption><b>Figura 11A.</b> El árbol con algunos de sus clados principales resaltados desde un archivo.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig11-canvas_fan.png" alt="El mismo árbol dibujado en abanico, con los mismos clados resaltados y nombrados"><figcaption><b>Figura 11B.</b> El mismo árbol, con sus clados resaltados, en forma de abanico.</figcaption></figure>
  </div>
</figure>

Todos los cambios se conservan cuando cambia la forma del árbol (rectangular, circular, en abanico o sin raíz), salvo que no puedan dibujarse en la forma nueva, como un alineamiento de secuencias en un árbol circular. Además, aunque la app está pensada para adaptarse a todas las formas, algunos elementos que pueden pasar de una forma a otra no resultan prácticos en todas. Por ejemplo, los gráficos de violín en un árbol circular o en abanico se superponen unos a otros hacia la raíz (Fig. 11B).

## 9. Leyendas y colocación de elementos

A medida que añadimos elementos con colores, símbolos o tamaños, tree2go añade sus leyendas en la parte inferior izquierda de la figura. Cada leyenda puede moverse, cambiar de estilo y ocultarse desde su menú de `Right-click` o desde la sección **Legends**. Por defecto, las leyendas están fijas en su lugar, como indica el candado azul en su esquina superior derecha. Un clic en el candado lo vuelve amarillo y libera la leyenda, que entonces puede arrastrarse a cualquier lugar del lienzo, como las imágenes y los gráficos.

Mientras se mueve un elemento, unas guías punteadas muestran los demás elementos a su alrededor, cada uno con su distancia (Fig. 12). Haz clic en la burbuja azul de una distancia para escribir un valor exacto, y el elemento se mueve ahí.

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig12-canvas.png" alt="Una leyenda en movimiento, con guías punteadas y burbujas azules con las distancias a los elementos a su alrededor">
  <figcaption><b>Figura 12.</b> Mover una leyenda libremente, con las guías y las distancias a los elementos a su alrededor.</figcaption>
</figure>

## 10. Eje de tiempo y escala geológica

En árboles calibrados en el tiempo, `Show time axis` en la sección **Time axis** añade un eje de edades debajo del árbol, o encima de él con *Position*. Sus subsecciones definen el eje:

- **Ages**: entre otras opciones, un desplazamiento para árboles solo de fósiles, en los que ninguna especie llega al presente. Cuando este valor cambia, todas las etiquetas que muestran una edad se actualizan automáticamente.
- **Ticks** y **Axis look**: dónde van las marcas y qué aspecto tiene el eje.
- **Geologic time scale**: cajas con los intervalos geológicos, en los colores de la Geological Society of America (GSA Geologic Time Scale v. 6.0), y fondos que sombrean esos intervalos, o rangos propios, detrás del árbol (Fig. 13).

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig13-canvas.png" alt="El árbol con un eje de tiempo y las cajas de la escala geológica debajo de él">
  <figcaption><b>Figura 13.</b> Un eje de tiempo con la escala geológica debajo del árbol.</figcaption>
</figure>

> **Nota.** Como con los demás elementos de la figura, casi todo el aspecto del eje de tiempo y de la escala geológica puede personalizarse. La única excepción son los colores de las cajas geológicas, que siguen una convención internacional. También puedes añadir un segundo eje de tiempo con una escala distinta (**Time axis** > *Show a second axis*), y sombrear intervalos detrás del árbol, ya sean intervalos geológicos estándar o rangos que definas. El eje de tiempo también funciona en árboles circulares y en abanico, como anillos concéntricos, pero las cajas geológicas no se dibujan ahí, porque no encajan en una forma radial.

## 11. Dividir un árbol largo en páginas

Un árbol demasiado alto para una página impresa puede dividirse desde la sección **Split into pages**. tree2go encuentra los clados que van en cada página, según el número de páginas que elijas, y muestra los límites de cada página en el lienzo como recuadros discontinuos (Fig. 14). Para mover un límite, arrástralo.

Cada página tiene el mismo ancho, y puede llevar su propio eje de tiempo o escala geológica. Una miniatura de todo el árbol (el mapa del árbol) muestra, en cada página, dónde están sus clados dentro del árbol. Su posición, colores y resaltado se definen desde su menú de `Right-click`. Al exportar, puedes guardar todo el árbol en un archivo, o cada página como un archivo propio.

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig14-canvas.png" alt="Un árbol dividido en páginas, cada página con una miniatura de todo el árbol">
  <figcaption><b>Figura 14.</b> Un árbol dividido en páginas, cada una con una miniatura de todo el árbol.</figcaption>
</figure>

> **Nota.** Cuando una figura con un eje de tiempo o una escala geológica se divide en páginas, puedes repetir el eje debajo de cada página o mostrarlo solo en la última, con **Split into pages** > *Repeat the time axis under each page*, en su subsección **Look**. El cambio no se ve en el lienzo, solo en los archivos exportados.

## 12. Gráficos de pastel en los nodos

A veces tenemos, para cada nodo, una estimación hecha de proporciones, como las probabilidades de los estados en una reconstrucción de estados ancestrales. tree2go puede dibujarlas como gráficos de pastel en los nodos, para uno o varios caracteres, y colorear las ramas según sus estados más probables.

Para conservar nuestro árbol con su estilo tal como está, primero lo copiamos a una pestaña nueva y empezamos la copia con el aspecto por defecto. Haz `Right-click` en la raíz del árbol y elige `Copy tree to a new tab` (Fig. 15). Una ventana pregunta entonces si la copia conserva el mismo aspecto o empieza con el aspecto por defecto, y aquí elegimos `Default look`. Para reiniciar en cambio el aspecto de la pestaña actual, usa `Reset styles` en `Page settings`. Si haces `Right-click` en cualquier otro nodo en lugar de la raíz, `Extract clade` abre solo ese clado en una pestaña nueva.

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig15-panel.png" alt="El menú de clic derecho de la raíz con Copy tree to a new tab, y la ventana que pregunta si la copia conserva el mismo aspecto o empieza con el aspecto por defecto">
  <figcaption><b>Figura 15.</b> Copiar el árbol a una pestaña nueva.</figcaption>
</figure>

Para renombrar la pestaña nueva, haz doble clic en su nombre. Luego, en la sección **Attachments**, haz clic en `Add file` y elige `vertebrates_habitat.simmap`. Los nodos del árbol se convierten de inmediato en gráficos de pastel. Su aspecto se define en la sección **Ancestral reconstructions** (Fig. 16A), donde las ramas también pueden colorearse por estado con **Ancestral reconstructions** > *Color the branches*, según el estado de máximo a posteriori, según los estados más probables por encima de un umbral, o como un degradado de probabilidad. Como los pasteles ocupan el lugar de los puntos de los nodos, su tamaño y su borde se definen en la sección **Nodes**, como los de cualquier otro punto.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig16-panel.png" alt="La sección Ancestral reconstructions, con pasteles en los nodos y las ramas coloreadas según sus estados más probables"><figcaption><b>Figura 16A.</b> La sección Ancestral reconstructions.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig16-canvas.png" alt="El árbol copiado con un gráfico de pastel del hábitat en cada nodo y sus ramas coloreadas por estado, con un tramo incierto dibujado discontinuo dentro de un círculo rojo"><figcaption><b>Figura 16B.</b> Gráficos de pastel del hábitat en los nodos, y ramas coloreadas según sus estados más probables.</figcaption></figure>
  </div>
</figure>

Para este ejemplo, ponemos **Nodes** > *Node dot size* en `9` px y **Branches** > *Line width* en `3` px, damos a los pasteles un borde negro, movemos la leyenda y renombramos sus estados desde su menú de `Right-click`. También coloreamos las ramas con `Most probable states (threshold-based)`. Esta opción define qué tan dominante debe ser un estado para colorear un tramo de rama, de modo que los tramos donde el estado es incierto destacan como una línea discontinua (círculo rojo en la Fig. 16B).

> **Nota.** Los gráficos de pastel también pueden venir de un archivo, con `Pie charts from a file…` en la subsección **Pie charts** de **Node values**. El archivo puede ser una tabla con los nombres en la primera columna y una columna por categoría, con la proporción de cada una, o un archivo de texto plano con una línea por punta o nodo, como `Name | {A:0.3, B:0.7}`, la notación de los archivos SIMMAP. Los nodos internos se emparejan por sus nombres, así que el árbol necesita nombres en sus nodos internos, escritos como en el archivo.

## 13. Gráficos laterales

Una de las funciones más útiles de tree2go es dibujar gráficos junto a las puntas: gráficos de barras, matrices de categorías (como presencia y ausencia), mapas de calor de valores continuos, e incluso alineamientos de ADN.

Primero, en la sección **Attachments**, haz clic en `Add file` y elige `regions.csv`, `traits.csv`, `vertebrates_traits_heatmap.csv` y `vertebrates_alignment.fasta`, que pueden elegirse juntos (Fig. 17A). Como se describió al principio de este tutorial, estos archivos contienen la distribución geográfica de las especies, algunos de sus rasgos, y secuencias de ADN de las especies vivas. Las tablas son sencillas: una columna con los nombres de las puntas, y una columna para cada valor. Puedes hacerlas en cualquier programa de hojas de cálculo, como Excel, y guardarlas como `.csv`. tree2go encuentra por sí mismo la columna con los nombres de las puntas, y si hace falta puedes elegir otra en su lista *Names in* de **Attachments**.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig17-attachments.png" alt="La sección Attachments con el SIMMAP, el alineamiento y tres tablas cargadas, cada una con el número de puntas con las que coincide"><figcaption><b>Figura 17A.</b> Los archivos adjuntos, cada uno con el número de puntas del árbol con las que coincide.</figcaption></figure>
    <figure><img class="vpanel" src="../../img/vignettes/basic-editing/fig17-sideplots.png" alt="La lista en la parte superior de la sección Side plots, con los gráficos en su orden desde las puntas hacia fuera y un icono de ojo para cada uno"><figcaption><b>Figura 17B.</b> La sección Side plots, con los gráficos en su orden desde las puntas hacia fuera.</figcaption></figure>
  </div>
</figure>

Cada archivo adjunto aparece en la sección **Attachments**, con el número de puntas del árbol con las que coincide. Aquí, la distribución geográfica (`regions.csv`) y los rasgos (`traits.csv` y `vertebrates_traits_heatmap.csv`) coinciden con 31 de las 31 puntas, mientras que el alineamiento coincide solo con 24, lo cual tiene sentido, ya que los 7 fósiles no tienen ADN.

Los gráficos laterales pueden apilarse. Pueden mostrarse varios a la vez, y su orden, desde las puntas hacia fuera, se cambia arrastrándolos en la lista de la parte superior de la sección **Side plots**, donde el icono del ojo muestra u oculta cada uno (Fig. 17B). El aspecto de cada gráfico se define en su subsección de **Side plots**, y algunos elementos también pueden cambiarse uno a uno desde su menú de `Right-click`. Algunos gráficos también pueden tomar el aspecto del árbol, por ejemplo coloreando las barras según el clado nombrado al que pertenece cada punta (**Side plots** > *Color the bars by named clade*).

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig18-canvas.png" alt="El árbol con barras de masa cerebral en escala logarítmica junto a las especies vivas, y un mapa de calor de cinco rasgos continuos">
  <figcaption><b>Figura 18.</b> Barras de masa cerebral en escala logarítmica, y un mapa de calor de cinco rasgos continuos.</figcaption>
</figure>

En este ejemplo, dibujamos barras de masa cerebral (`brain_g`, de `traits.csv`), coloreadas según el clado nombrado de cada punta, y en escala logarítmica (**Side plots** > *Logarithmic scale (log₁₀)*), ya que la masa cerebral va desde una fracción de gramo hasta varios kilogramos. Junto a ellas, dibujamos un mapa de calor de cinco rasgos continuos (`vertebrates_traits_heatmap.csv`): masa corporal, longevidad máxima, tamaño del genoma, temperatura corporal y descendientes por año. Observa que los gráficos laterales dejan vacía una punta cuando no tiene valor. Aquí, los fósiles no tienen barra, ya que su masa cerebral se desconoce, y en el mapa de calor solo muestran su masa corporal (Fig. 18).

Los gráficos laterales también pueden mostrar secuencias de ADN o de proteínas, directamente desde un archivo `.fasta`. Aquí usamos `vertebrates_alignment.fasta`. tree2go da a cada base su propio color, y los colores pueden cambiarse en la subsección **Alignment** de **Side plots**.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig19-bases.png" alt="Las posiciones 15 a 30 del alineamiento junto a las puntas, un cuadro de color por base, con las letras dentro"><figcaption><b>Figura 19A.</b> Las posiciones 15 a 30 del alineamiento, como un cuadro por base.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig19-barcode.png" alt="Todo el alineamiento junto a las puntas como un código de barras, con cada posición marcada donde difiere de su base más común"><figcaption><b>Figura 19B.</b> Todo el alineamiento, como un código de barras.</figcaption></figure>
  </div>
</figure>

La forma en que se dibuja el alineamiento depende de cuántas posiciones se muestran. Cuando caben en el ancho del gráfico (**Side plots** > *Width*, en **Alignment**), cada base se dibuja como un cuadro de color, con su letra dentro cuando hay espacio (Fig. 19A). Cuando no caben, el alineamiento se dibuja como un código de barras, que marca en cada posición, en dos colores contrastantes, las bases que difieren de la más común (Fig. 19B). tree2go calcula cuántas posiciones caben, y la ayuda bajo *Width* te lo indica. También puedes elegir qué posiciones mostrar con *From site* y *To site*.

## 14. Presencia y ausencia en un árbol circular

Dejamos los datos binarios para el final porque, además de dibujarlos como los otros gráficos, los combinaremos con una forma de árbol distinta. Para este ejemplo, ocultamos las barras, el mapa de calor y el alineamiento con sus iconos de ojo en la lista de **Side plots**, y dejamos solo **Categories**, con `regions.csv`. Como los otros gráficos, dibuja una cuadrícula de cuadros, coloreados donde una especie está presente y en gris donde está ausente, y ambos colores pueden cambiarse. Luego, en **Layout**, elegimos la forma `Circular` y damos la vuelta al árbol con **Layout** > *Turn circular and fan trees inside out*. Para aligerar la figura, también quitamos los gráficos de violín y las edades de los nodos, convertimos el árbol en un cladograma desmarcando **Layout** > *Use branch lengths*, y ampliamos el centro con **Layout** > *Inner radius (center gap)*. Por último, con **Side plots** > *Squares follow the circle*, en **Categories**, los cuadros se convierten en cuñas que siguen el círculo, y *Width of the bands* define su ancho (Fig. 20).

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig20-canvas.png" alt="Un cladograma circular invertido, con la presencia y ausencia de cada especie en siete regiones dibujadas como anillos de cuñas de colores dentro del círculo, y un espacio vacío en el centro">
  <figcaption><b>Figura 20.</b> El árbol invertido, con su matriz de presencia y ausencia dentro del círculo.</figcaption>
</figure>

El resultado es una vista especialmente útil en biogeografía, ya que muestra de un vistazo tanto las relaciones entre las especies como su presencia y ausencia en cada región. Y el espacio que abrimos en el centro llevará nuestra figura un paso más allá en la siguiente sección.

## 15. Geografía

Otra función distintiva de tree2go es dibujar mapas con registros de ocurrencia directamente en la app, sin necesidad de un programa de SIG. Esto se hace en la sección **Geography** del panel izquierdo (Fig. 21). Puedes cargar tus propios mapas como shapefiles (`.shp`, o comprimidos en un `.zip`), o descargar contornos básicos de [Natural Earth](https://www.naturalearthdata.com) para mapas actuales, o de [GPlates](https://www.gplates.org) para reconstrucciones paleogeográficas. Descargarlos requiere conexión a internet.

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig21-panel.png" alt="La sección Geography, con sus subsecciones Map, Points y Lines to the tips">
  <figcaption><b>Figura 21.</b> La sección Geography.</figcaption>
</figure>

Para este ejemplo, usamos `fossil_records.csv`, con los sitios de muestreo de los siete fósiles de nuestro árbol. El archivo necesita, como mínimo, una columna con los nombres de las puntas, que pueden repetirse cuando una especie tiene varios registros, y una columna para la longitud y otra para la latitud. Cuando los registros son muchos, tree2go puede agrupar los cercanos. Como nuestros fósiles abarcan un largo periodo de tiempo, mostramos los registros como sitios de muestreo actuales. Con GPlates, las coordenadas pueden colocarse en cambio sobre una reconstrucción paleogeográfica, a partir de varios modelos, lo que también requiere conexión a internet. Esto es más útil cuando los fósiles tienen edades similares y queremos mostrar cómo era su distribución en ese momento.

Primero, en la subsección **Map**, descargamos los contornos `Land` de Natural Earth a `1:110 million`, y ponemos **Geography** > *Projection (maps in degrees)* en `Mollweide (ESRI:54009)`, que da al mapa una forma ovalada. La mejor proyección depende de tus datos y de lo que quieras mostrar. Luego movemos el mapa al centro del círculo, el espacio que abrimos en la sección anterior. Como los demás elementos, el mapa tiene su propio menú de `Right-click`, que cambia no solo su aspecto sino también su extensión y su zoom. Directamente sobre el mapa, `Ctrl` + arrastrar mueve la vista dentro de su marco, y `Ctrl` + rueda acerca y aleja, como en un SIG.

A continuación, con `fossil_records.csv` adjunto en **Attachments**, lo elegimos en **Geography** > *Table*, en la subsección **Points**, y los registros aparecen en el mapa. Con *Size* en `By the number of records`, cada punto crece con el número de registros de su sitio. El tamaño y el color de los puntos también pueden seguir un valor del árbol o de una tabla adjunta, y el color puede seguir los clados nombrados o, como aquí, el resaltado de cada clado (`As the highlight of its clade`). Las Figuras 22A y 22B muestran dos formas de incorporar datos geográficos a un árbol.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig22-canvas.png" alt="El árbol circular invertido con un mapa del mundo en su centro, los registros fósiles como puntos coloreados según el resaltado de su clado, y los anillos de regiones entre el mapa y el árbol"><figcaption><b>Figura 22A.</b> El árbol con un mapa de los registros fósiles en su centro. Los anillos interiores muestran las regiones donde cada especie vive o fue encontrada, y los puntos del mapa están coloreados según el resaltado de su clado.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig22-canvas_alternative.png" alt="Un árbol con un mapa a su lado, que muestra los registros de ocurrencia agrupados por cercanía geográfica y coloreados según los clados del árbol"><figcaption><b>Figura 22B.</b> Una vista alternativa de un mapa dentro de una filogenia. El mapa muestra los registros de ocurrencia agrupados por cercanía geográfica y coloreados según los clados del árbol.</figcaption></figure>
  </div>
</figure>

> **Nota.** La subsección **Lines to the tips** une cada punta con sus puntos (**Geography** > *Join each tip to its points*). Esto ayuda a mostrar de dónde provienen las muestras o las especies, especialmente cuando cada especie tiene uno o unos pocos registros cercanos. Si no, se dibuja una línea desde la punta hasta cada punto.

## 16. Imágenes y elementos visuales

La sección **Images and visual elements** añade elementos propios a la figura:

- `Add image`: una imagen, como una silueta o una foto, en PNG o JPEG.
- `Add label`: un texto libre, que puede alinearse con el árbol.
- `Draw arrow`: una flecha, que puede anclarse a nodos e imágenes, de modo que los sigue cuando el árbol cambia.
- `Add density plot`: la distribución de un valor del árbol, como las tasas.
- `Add LTT plot`: un gráfico de linajes a través del tiempo, para todo el árbol o para clados nombrados.

Como las leyendas, pueden moverse a cualquier lugar, con guías y distancias a los elementos a su alrededor, y cambiar de estilo desde su menú de `Right-click`.

## 17. Tanglegrama

Los tanglegramas son otra figura común en filogenética comparada, dos árboles frente a frente, normalmente con topologías alternativas, con líneas que unen sus puntas correspondientes. En la sección **Tanglegram**, el segundo árbol puede ser cualquier árbol del conjunto (`Open a tree of the set`) o un árbol de un archivo (`Load a tree file in a new tab`). Aquí cargamos `vertebrates_alternative.nwk` (Fig. 23).

<figure class="vfig">
  <img src="../../img/vignettes/basic-editing/fig23-canvas.png" alt="El árbol principal y el árbol alternativo frente a frente, con líneas que unen las mismas especies">
  <figcaption><b>Figura 23.</b> Un tanglegrama del árbol principal y un árbol con una topología alternativa.</figcaption>
</figure>

El segundo árbol se abre en una pestaña propia, y se dibuja con el aspecto de esa pestaña, la alineación de sus nombres, los colores de sus ramas y sus resaltados se definen ahí, como en cualquier otro árbol. Del árbol principal solo toma su tamaño, sus puntas se reparten en la misma altura, y su ancho es el mismo salvo que se defina otro en **Tanglegram** > *Width (0 as this tree)*. Con **Tanglegram** > *Join the highlights of the same clade*, los resaltados de un clado en ambos árboles se unen entre sí. El orden de sus ramas es el suyo propio, y para que las líneas se crucen lo menos posible, el árbol principal ofrece `Untangle (turn the second tree)`, que gira solo los nodos del segundo árbol, y `Untangle both`, que gira los nodos de ambos árboles.

## 18. Guardar y exportar

tree2go conserva tu trabajo de dos maneras. Primero, mientras no se borren los datos del navegador, la app recuerda tu sesión incluso después de cerrarla: la próxima vez que abras tree2go, tus árboles, pestañas, aspecto y archivos adjuntos estarán ahí, exactamente como los dejaste. `Clear session`, en el encabezado, lo borra todo para empezar de nuevo. Sin embargo, una sesión solo existe en ese navegador, así que recomendamos guardar tu trabajo como proyecto de vez en cuando.

Desde `Save` en el encabezado, puedes guardar:

- `Project`: los árboles y todo lo que los acompaña, incluidas las pestañas, el aspecto, las tablas, los alineamientos, los mapas, las imágenes y, si lo eliges, todos los árboles de un conjunto. Se vuelve a abrir más tarde, en cualquier computadora, desde `Import` > `Project`. Al guardarlo, una ventana te permite dejar fuera los archivos adjuntos o los árboles del conjunto, y comprimir el archivo, lo que lo hace mucho más ligero.
- `Style`: solo el aspecto de la figura, sin su árbol ni sus datos. Un estilo puede aplicarse a otro árbol desde `Import` > `Style`, lo que resulta práctico para dar el mismo aspecto a todas las figuras de un artículo.

Por último, exporta la figura desde `Export`, como SVG o PDF, archivos vectoriales que se mantienen nítidos a cualquier tamaño, o como PNG o TIFF, con la resolución y el tamaño que elijas. El mismo menú guarda el árbol tal como está, con sus nombres, su enraizamiento y su orden, en Newick o NEXUS, y, en el caso de un conjunto de árboles, los árboles de la muestra.

## 19. Redes filogenéticas

Aunque no forma parte de nuestro ejemplo de vertebrados, nos queda una sección por explorar: **Phylogenetic networks**. La historia de un grupo no siempre es un árbol: cuando los linajes intercambian genes, por hibridación o introgresión, se representa mejor como una red. tree2go lee redes en Newick extendido (eNewick), como las escriben PhyloNet o SNaQ, donde cada reticulación se marca con una etiqueta como `#H1`.

Como ejemplo, usamos `heliconius_network.nwk`, una pequeña red de mariposas *Heliconius* inspirada en dos casos muy conocidos, con valores ficticios: *H. heurippa*, una especie de origen híbrido entre *H. cydno* y *H. melpomene*, y *H. timareta*, que recibió genes de *H. melpomene* por introgresión. Se abre con `Open tree`, como cualquier árbol.

tree2go reconoce las reticulaciones, y el tipo de cada una, a partir de su etiqueta en el archivo: `#H` para hibridación, `#LGT` para transferencia lateral de genes y `#R` para recombinación, cada una con su propio color en **Phylogenetic networks**. Los dos eventos de nuestro ejemplo son hibridaciones (`#H`). Lo que distingue una especie híbrida de una introgresión es gamma (γ), la proporción del genoma heredada a través de cada progenitor, un valor que puede mostrarse como cualquier otra anotación del árbol.

<figure class="vfig pair">
  <div class="vrow">
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig24-major.png" alt="La red de Heliconius dibujada como su árbol mayor, con dos flechas discontinuas desde la rama de H. melpomene hacia H. heurippa y H. timareta, rotuladas con sus valores de gamma"><figcaption><b>Figura 24A.</b> La red dibujada como su árbol mayor, con cada reticulación como una flecha desde el donante hacia el linaje híbrido.</figcaption></figure>
    <figure><img class="vcanvas" src="../../img/vignettes/basic-editing/fig24-full.png" alt="La misma red dibujada completa, donde cada nodo híbrido une sus dos aristas parentales, con grosores que siguen a gamma"><figcaption><b>Figura 24B.</b> La misma red dibujada completa, con las dos aristas parentales de cada nodo híbrido.</figcaption></figure>
  </div>
</figure>

Las reticulaciones se dibujan como líneas discontinuas desde el linaje donante hasta el nodo híbrido. Por defecto, una flecha apunta del donante al receptor (*Arrows* > `To hybrid`), pero también puede apuntar en sentido contrario, en ambos sentidos o no mostrarse. Con *Show a value on each line*, cada línea muestra su γ, y con *Width from γ*, su grosor lo sigue. *Where on the branches* define dónde empieza y termina cada línea, `Centered` las coloca en el centro de las ramas, mientras que `Lengths` usa las edades escritas en el archivo. Como cualquier otro elemento, cada línea puede seleccionarse con un clic y cambiarse por separado desde su menú de `Right-click`.

Por último, *Style* alterna entre dos vistas de la misma red. `Major tree` dibuja el árbol de las aristas mayores, las que llevan la mayor parte del genoma, con cada arista menor como una línea desde su donante (Fig. 24A), mientras que `Full network` da a cada nodo híbrido un punto propio, donde se unen sus dos aristas parentales (Fig. 24B).
