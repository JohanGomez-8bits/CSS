# Catálogo de Productos - Subactividad 1

Página aislada en HTML semántico y CSS para practicar selectores, herencia, cascada y especificidad.

## Cálculo de puntos de especificidad

| Tipo de selector | Puntos |
| ---------------- | ------ |
| Etiqueta         | 1      |
| Clase            | 10     |
| ID               | 100    |

### Ejemplos de este proyecto

| Selector             | Cálculo   | Total |
| -------------------- | --------- | ----- |
| `h2`                 | 1         | 1     |
| `aside ul li a`      | 1+1+1+1   | 4     |
| `footer ul li a`     | 1+1+1+1   | 4     |
| `header nav ul li a` | 1+1+1+1+1 | 5     |
| `.btn-comprar`       | 10        | 10    |
| `.btn-destacado`     | 10        | 10    |
| `#btn-destacado`     | 100       | 100   |

## Conceptos aplicados

- **Herencia:** `font-family` y `color` declarados en `body` los heredan títulos, párrafos y listas.
- **Selectores combinados:** cada zona (header, aside, footer) pinta sus enlaces sin afectar a las demás.
- **Cascada vs. especificidad:** con un `#id` (100 pts) el color del enlace destacado aplastaba a la clase (10 pts) sin importar el orden.
- **Refactorización:** se eliminaron las reglas por `#id`. Con solo etiquetas y clases, el empate de 10 pts se resuelve por orden de declaración, sin usar `!important`.

## Hallazgos: El Modelo de Caja:

(1) La diferencia práctica entre Margin y Padding:
El padding es el espacio que hay dentro del elemento, entre el contenido y el borde, y por eso el fondo también se extiende ahí. El margin es el espacio de afuera, entre un elemento y los que tiene al lado, y no tiene color de fondo. Para separar el texto de su caja uso padding, y para separar una caja de otra uso margin.

(2) Por qué es obligatorio usar box-sizing: border-box:
Porque sin esto el padding y el borde se suman al ancho que uno puso, y la caja termina más grande de lo esperado. Por ejemplo, una caja de 200px con 20px de padding queda de 240px. Con border-box el ancho que pongo ya incluye el padding y el borde, así que las medidas me quedan como las planeé y el diseño no se desarma.

(3) Cómo se ven afectados los elementos hermanos cuando le aplicas un margen grande a uno de ellos:
Los hermanos se mueven y se alejan, porque el margen empuja y crea un espacio vacío alrededor del elemento. Si le pongo un margin-bottom grande a uno, el que viene después baja. Además, en vertical los márgenes de dos hermanos pueden "colapsar", o sea que no se suman, sino que se queda el más grande.

## Hallazgos: Centralización de Identidad Visual y Espaciado

### 1. Variables declaradas

Todo lo declaré en `:root`, en `styles.css`, después de los `@import`:

**Colores**

- `--color-cabeza-navegacion` (rgb(255, 255, 255)): links del menú del header.
- `--color-primario` (#f5f5f5): fondo del `.catalogo` (main).
- `--color-secundario` (#f5f5f5df): fondo del `.filtros` (aside), con un poco de transparencia.
- `--color-terceario` (#fafafa): fondo del `.footer` y de la tarjeta destacada; también el texto claro sobre fondos oscuros (hover de enlaces y botones, etiqueta "¡Oferta!").
- `--color-cuaternario` (#1f3a5f): títulos `h2` (`.card__title` y `.filtros__title`), rayita de la tarjeta y fondo del hover en las categorías.
- `--color-base-cabeza` (#7dc2f0): fondo del `.header` si la imagen no carga.
- `--color-fuente` (#2b2b2b): texto general.
- `--color-categorias` (#217b81): links de categorías en `.filtros`.
- `--color-boton-comprar` (#48ac30): botón de comprar.
- `--color-boton-destacado` (hsl(106, 100%, 65%)): botón destacado.
- `--color-boton-hover` (#2e7d1e): fondo del botón al pasar el cursor.
- `--color-boton-active` (#1f5a13): fondo del botón al hacer clic.
- `--color-links` (#5c3ead): links del `.footer`.
- `--color-foco` (usa `--color-cuaternario`): contorno de `:focus` en las categorías.
- `--color-oferta` (#c92a2a): etiqueta "¡Oferta!" y borde de la tarjeta destacada.
- `--color-borde` (#000000): declarada, todavía no la uso en ningún componente.

**Tipografía**

- `--font-size` (20px): tamaño de letra base del `body`.

**Espaciados**

- `--espaciado-enlace` (4px 8px): padding de `.filtros__link`.
- `--espaciado-boton` (6px 14px): padding de `.btn`.
- `--espaciado-medio` (16px): separación (`gap`) entre los enlaces de `.nav__list` y entre el logo y el menú cuando el header se parte en dos líneas.
- `--espaciado-grande` (32px): separación (`gap`) entre los bloques del `.filtros`.
- `--margen-filtro` (8px 4px): declarada, todavía no la uso en ningún componente.
- Los `padding` y `margin` de `.card` (`20px` y `15px`) siguen escritos directo en el selector.

### 2. Ventaja de reutilizar medidas de margin y padding

Si uso siempre las mismas medidas, la página se ve más pareja y ordenada. Además, cambio un solo valor y se actualiza todo, en vez de buscar selector por selector como me pasa ahora con el `20px`.

### 3. Cómo `:root` previene colisiones visuales

Al tener cada color en un solo lugar, evito usar dos tonos casi iguales sin darme cuenta. Todos los selectores toman el valor con `var(--nombre)`, así que no se contradicen cuando la hoja de estilos crece.


## Hallazgos: Pseudoclases y Pseudoelementos

### 1. Diferencia entre pseudoclase y pseudoelemento

Entendí que la pseudoclase es cuando el elemento cambia según lo que hace el usuario. Por ejemplo, `:hover` funciona cuando paso el cursor por encima, `:active` cuando dejo el clic presionado y `:focus` cuando llego a un enlace con la tecla Tab. El elemento sigue siendo el mismo, solo cambia cómo se ve. El pseudoelemento es distinto, porque crea algo nuevo desde el CSS. Con `::before` y `::after` hice la viñeta del menú, la rayita debajo de cada producto y la etiqueta "¡Oferta!", y ninguna de esas cosas está escrita en el HTML.

### 2. Importancia de `:focus` en la accesibilidad

No todas las personas usan mouse, algunas navegan solo con el teclado. Si la página no muestra dónde está el foco, se pierden y no saben en qué enlace están parados. Por eso le puse un contorno visible a los enlaces del `aside`. Además, el color lo saqué de una variable de `:root`, entonces si después cambio los colores de la página, el contorno cambia con ellos sin que yo tenga que hacer nada más.

### 3. Por qué decorar con `::before` y `::after` y no con etiquetas vacías

Si metiera etiquetas vacías en el HTML solo para que se vea bonito, lo llenaría de cosas que no tienen ningún contenido. Con los pseudoelementos el HTML queda limpio y con su significado, y todo lo de la decoración se queda en el CSS. Y si más adelante quiero cambiar la viñeta o quitar la insignia, solo toco una regla, en vez de buscar en las cuatro tarjetas una por una.

## Hallazgos: Arquitectura BEM y Modularidad

### 1. Qué significa BEM y cómo se escribe

BEM significa Bloque, Elemento y Modificador. Es una forma de ponerle nombre a las clases para que se entienda qué es cada cosa. Se escribe así: `bloque__elemento--modificador`.

- **Bloque:** es el componente completo. Ejemplo: `.card`, que es la tarjeta del producto.
- **Elemento:** es una parte del bloque y se une con dos guiones bajos. Ejemplo: `.card__title`, que es el título de la tarjeta.
- **Modificador:** es una variación y se une con dos guiones medios. Ejemplo: `.card--destacado`, que es la tarjeta destacada.

### 2. Por qué dividir el CSS en varios archivos ayuda a trabajar en equipo

Si todo el CSS está en un solo archivo, es difícil encontrar las cosas. Además, si dos personas lo editan al mismo tiempo, en Git salen conflictos. Al dividirlo en archivos como `tarjeta.css`, `botones.css` y `filtros.css`, cada compañero puede trabajar en uno distinto sin dañar el trabajo del otro. También es más fácil encontrar los errores: si algo falla en los botones, solo reviso `botones.css`. El archivo `styles.css` junta todos los módulos con `@import`.

### 3. Cómo BEM evita la guerra de especificidad

Antes tenía selectores largos como `aside ul li a`, que pesa 4 puntos, y otros como `.btn-comprar`, que pesa 10. A veces una regla le ganaba a otra sin que yo quisiera. Con BEM cada elemento tiene su propia clase y todas las reglas pesan lo mismo, 10 puntos. Así ninguna le gana a otra por peso y solo importa el orden en que están escritas (la cascada). Por eso ya no necesito `!important` ni selectores largos. Los `:hover` y `:active` pesan 20 porque suman la clase más la pseudoclase, pero siguen dependiendo de una sola clase.

## Hallazgos: Arquitectura Total con Flexbox

### 1. Por qué fue crucial `min-height: 100vh` y `flex-direction: column` en el contenedor global

Antes el footer quedaba justo debajo del último contenido, y si la página tenía poco contenido se quedaba a mitad de la pantalla. Con `min-height: 100vh` el `.app-layout` mide como mínimo todo el alto de la ventana, y con `flex-direction: column` sus hijos (el header, el `.main-wrapper` y el footer) se apilan de arriba hacia abajo. Como el `.main-wrapper` tiene `flex: 1`, se queda con todo el espacio que sobra y empuja el footer hasta el fondo. Usé `min-height` y no `height` porque así la página puede seguir creciendo cuando hay más productos. También le quité el margen por defecto al `body`, porque con ese margen los 100vh sumaban un scroll de más.

### 2. Cómo la propiedad `gap` reemplazó el uso excesivo de márgenes laterales en los menús

Antes, para separar los enlaces tocaba ponerle `margin-left` o `margin-right` a cada uno, y el primero o el último quedaban con un espacio de sobra en el borde. Con `gap` en `.nav__list` el espacio queda solo entre un enlace y el siguiente, nunca en los extremos, y se define en un solo lugar con `var(--espaciado-medio)`. Lo mismo hice en `.filtros` con `var(--espaciado-grande)` para separar el título de la lista. Por eso en esos contenedores puse `margin: 0` a los hijos: así el único espacio es el del `gap`, y si lo quiero cambiar toco una sola variable.

### 3. Cómo BEM, Custom Properties y Flexbox crean una tarjeta resistente a textos de distinto largo

BEM me da una clase para cada parte de la tarjeta (`.card__desc`, `.card__price-wrapper`, `.card__button`), entonces cada una tiene su propio trabajo sin selectores largos. Las Custom Properties mantienen los colores y los espacios iguales en todas las tarjetas. Flexbox hace el resto: `.card` es una columna y `.card__desc` tiene `flex-grow: 1`, así que se estira y empuja el precio y el botón hacia abajo. Las tarjetas están dentro de `.catalogo__lista`, que es una fila que se parte en líneas con `flex-wrap`, y cada fila se estira sola (`align-items: stretch` por defecto), por eso las tarjetas de una misma fila miden igual y los botones quedan alineados abajo aunque una descripción sea más larga que otra. El precio usa `justify-content: space-between` y `align-items: baseline` para que el precio de oferta, más grande, y el precio original tachado queden sobre la misma línea de texto.

Probé también `height: 100%` en `.card`, pero con el contenedor sin una altura definida esa propiedad impedía que la tarjeta se estirara y las tarjetas de una misma fila quedaban de alturas distintas. Sin esa propiedad quedan iguales, por eso no la dejé.