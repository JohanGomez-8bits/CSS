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
