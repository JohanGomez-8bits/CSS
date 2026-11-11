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

Todo lo declaré en `:root`, al inicio de `styles.css`:

**Colores**

- `--color-cabeza-navegacion` (#ffffff): links del menú del header.
- `--color-primario` (#afafaf): fondo del `main`.
- `--color-secundario` (#d4d4d4): fondo del `aside`.
- `--color-terceario` (#eeeeee): fondo del `footer`.
- `--color-cuaternario` (#1f3a5f): títulos `h2`.
- `--color-base-cabeza` (#7dc2f0): fondo del `header` si la imagen no carga.
- `--color-fuente` (#2b2b2b): texto general.
- `--color-categorias` (#217b81): links de categorías en el `aside`.
- `--color-boton-comprar` (#48ac30): botón de comprar.
- `--color-boton-destacado` (rgb(60, 255, 0)): botón destacado.
- `--color-links` (#5c3ead): links del `footer`.

**Tipografía**

- `--font-size` (20px): tamaño de letra base del `body`.

**Espaciados**

- Todavía no declaré variables de espaciado: los `padding` y `margin` (como `20px` y `15px` en `article`) siguen escritos directo en cada selector.

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