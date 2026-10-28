# Catálogo de Productos - Subactividad 1

Página aislada en HTML semántico y CSS para practicar selectores, herencia, cascada y especificidad.

## Cálculo de puntos de especificidad

| Tipo de selector | Puntos |
|------------------|--------|
| Etiqueta         | 1      |
| Clase            | 10     |
| ID               | 100    |

### Ejemplos de este proyecto

| Selector                | Cálculo         | Total |
|-------------------------|-----------------|-------|
| `h2`                    | 1               | 1     |
| `aside ul li a`         | 1+1+1+1         | 4     |
| `footer ul li a`        | 1+1+1+1         | 4     |
| `header nav ul li a`    | 1+1+1+1+1       | 5     |
| `.btn-comprar`          | 10              | 10    |
| `.btn-destacado`        | 10              | 10    |
| `#btn-destacado`        | 100             | 100   |

## Conceptos aplicados

- **Herencia:** `font-family` y `color` declarados en `body` los heredan títulos, párrafos y listas.
- **Selectores combinados:** cada zona (header, aside, footer) pinta sus enlaces sin afectar a las demás.
- **Cascada vs. especificidad:** con un `#id` (100 pts) el color del enlace destacado aplastaba a la clase (10 pts) sin importar el orden.
- **Refactorización:** se eliminaron las reglas por `#id`. Con solo etiquetas y clases, el empate de 10 pts se resuelve por orden de declaración, sin usar `!important`.