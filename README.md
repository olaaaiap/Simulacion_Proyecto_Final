# Simulación · Proyecto final: carrito de café en Houdini

**Escena animada en Houdini con simulación de fluidos para el agua que gotea y simulaciones pyro para el vapor, renderizada con Karma.**

Es el proyecto final de la asignatura de Simulación del máster. La escena muestra un carrito de café con una taza de la cual sale vapor. Además, la cafetera tiene unos chorros de vapor a presión y unas gotas de agua que caen. La animación dura 10 segundos (240 fotogramas a 24 FPS) y se ve con una cámara que orbita alrededor de la escena.

[![Vídeo de demostración 1](https://img.youtube.com/vi/QhzumJXVIb4/hqdefault.jpg)](https://youtu.be/QhzumJXVIb4)
[![Vídeo de demostración 2](https://img.youtube.com/vi/kBMi9T5wdQg/hqdefault.jpg)](https://youtu.be/kBMi9T5wdQg)

## Enlaces

- 🎥 **Vídeo explicativo:** [youtu.be/QhzumJXVIb4](https://youtu.be/QhzumJXVIb4)
- 🎥 **Vídeo de resultado:** [youtu.be/kBMi9T5wdQg](https://youtu.be/kBMi9T5wdQg)
- 🎬 **Proyecto de Houdini:** [`proyecto_final_olaia_picabea.hipnc`](proyecto_final_olaia_picabea.hipnc)

## Detalle de la escena

### Gotas de agua

- Un **emisor de gotas** genera las partículas iniciales del líquido.
- Una red de dinámicas (DOP) con un **solver FLIP** y **gravedad** simula el movimiento de las partículas.
- A partir de las partículas se genera la **superficie del fluido** (*Particle Fluid Surface*) para poder renderizar el líquido como una malla continua.
- Los resultados se guardan en **caché comprimida** (*Fluid Compress* y *File Cache*) para no tener que volver a simular en cada reproducción.
- El líquido usa un material propio de **líquido**.

### Vapor de la taza (pyro)

- Un **tubo remallado** sobre la taza sirve de fuente del vapor.
- Un **ruido de atributos** (*Attribute Noise*) rompe la uniformidad de la emisión para que el humo sea más natural.
- Los atributos se rasterizan en volúmenes y se simulan con un **Pyro Solver**. La simulación se guarda en caché.

### Vapor a presión (pyro con colisiones)

- Hay dos simulaciones independientes, una a cada lado de la cafetera.
- Cada una emite el vapor desde **puntos dispersos** (*Scatter*) dentro de una esfera.
- Una caja actúa como **fuente de colisión**, para que el vapor reaccione contra la geometría en lugar de atravesarla.

### Escena, materiales y render

- **Modelos:** el carrito de café y la taza se importan en FBX y se combinan en una sola geometría.
- **Materiales:** todos son **MaterialX** (`mtlxstandard_surface`) construidos a partir de sus texturas PBR: color base, metalicidad, rugosidad, oclusión ambiental, opacidad y mapas de normales.
- **Iluminación:** dos luces de área.
- **Cámara:** cámara animada que orbita alrededor del carrito.
- **Render:** con **Karma** a través de USD.

## Tecnologías

- **Houdini 21** (versión no comercial)
- **FLIP** y **Pyro** para las simulaciones de fluidos y humo
- **MaterialX** para los materiales PBR
- **Karma** y **USD** para el render

## Contenido del repositorio

- `proyecto_final_olaia_picabea.hipnc`: proyecto de Houdini con todas las simulaciones, materiales, luces y cámara.
- [`coffee-cart/`](coffee-cart): modelo FBX del carrito de café y sus texturas.
- [`coffee-cup/`](coffee-cup): modelo FBX de la taza y sus texturas.

## Autora

Olaia Picabea
