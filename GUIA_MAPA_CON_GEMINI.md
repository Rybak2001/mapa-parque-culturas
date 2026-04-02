# Guía: Crear Mapa del Parque de las Culturas — Por Capas con Gemini AI

## Resumen
Crear un mapa ilustrado (estilo del mapa promo) del **Parque de las Culturas y de la Madre Tierra** trabajando **por capas de imagen (JPG/PNG)** con Gemini AI. Cada capa se genera, se refina a mano, y luego se le pasa de vuelta a Gemini para continuar.

### Herramientas que necesitas
- **Gemini AI** — generar imágenes por capa
- **Editor de imagen** — para refinar cada capa a mano:
  - **GIMP** (gratis) o **Photoshop** — ideal, trabaja con capas .PSD/.XCF
  - **Photopea** (gratis en navegador, abre PSD) — alternativa rápida
  - **Paint.NET** (gratis Windows) — más simple pero funcional
- **Google Earth Pro** (gratis) — para obtener coordenadas GPS

### Tamaño estándar para TODAS las capas
> **1400 x 700 píxeles, fondo transparente (PNG)** cuando sea posible.
> Si Gemini da JPG, úsalo igual y recorta el fondo en tu editor.

---

## FASE 0: Preparación

### 0.1 Obtener Coordenadas GPS
1. Abre **Google Earth Pro** (gratis) o Google Maps
2. Busca el parque (Bolivia)
3. Haz clic derecho → "¿Qué hay aquí?" en cada punto clave
4. Anota lat/lon de al menos las 4 esquinas + los 11 puntos de interés

### 0.2 Tabla de coordenadas (llenar)
| # | Punto | Lat | Lon |
|---|-------|-----|-----|
| 1 | Ingreso | | |
| 2 | Boleterías | | |
| 3 | Chiwiña | | |
| 4 | Cafetería | | |
| 5 | Teatro Galpón | | |
| 6 | Aguas Danzantes | | |
| 7 | Mirador | | |
| 8 | Escenario Principal | | |
| 9 | Anfiteatro | | |
| 10 | Parrillero | | |
| 11 | Área de Picnik | | |
| - | Esquina NW | | |
| - | Esquina NE | | |
| - | Esquina SW | | |
| - | Esquina SE | | |

### 0.3 Preparar archivo base en tu editor
1. Crea un archivo nuevo de **1400 x 700 px** en GIMP/Photoshop
2. Crea estas capas vacías (de abajo hacia arriba):
   - `00_fondo` (color beige/crema: #D4C9A8)
   - `01_terreno`
   - `02_caminos`
   - `03_edificios`
   - `04_arboles`
   - `05_detalles` (agua, juegos, bancas)
   - `06_iconos_servicios`
   - `07_numeros_poi`
   - `08_leyenda`
   - `09_texto_titulo`
3. Guárdalo como `mapa_parque.psd` (o `.xcf` en GIMP)

---

## FASE 1: CAPA DE TERRENO (silueta y zonas de suelo)

### Prompt para Gemini (adjuntar original.png + mapa_promo):
```
Estoy creando un mapa ilustrado de un parque por capas. Te adjunto:
- Imagen 1: ortofoto aérea real tomada con dron (esta es la FORMA REAL)
- Imagen 2: mapa promocional ilustrado (este es el ESTILO que quiero copiar)

Necesito que generes la PRIMERA CAPA: solo el terreno.

ESPECIFICACIONES TÉCNICAS:
- Formato: imagen JPG
- Tamaño: 1400 x 700 píxeles
- Fondo: beige claro (#D4C9A8)

QUÉ DIBUJAR — Copia la FORMA de la ortofoto, pero con el ESTILO del mapa promo:

1. SILUETA del parque: forma de medialuna/riñón vista desde arriba.
   El borde izquierdo es más estrecho (zona de ingreso), se ensancha 
   hacia el centro, y la parte derecha sube formando una loma con bosque.
   Bordes CURVOS y orgánicos, nada rectangular.

2. ZONAS DE COLOR (planas, sin textura, sin gradiente):
   - Zona de plaza/tierra (centro-izquierda): marrón arena (#C4A882)
   - Zona de césped (disperso): verde claro (#8DB564)
   - Zona de bosque (todo el lado derecho, ~40% del mapa): verde medio 
     (#5D8A3C) como mancha plana de color. NO dibujes árboles individuales.
   - Estacionamiento (franja larga horizontal en la parte inferior): 
     gris (#9E9E9E), forma rectangular alargada
   - Zona de desnivel/colina (arriba izquierda): marrón claro (#D4B896)

3. ESTILO: Flat design idéntico al mapa promo adjunto:
   - Colores 100% sólidos y planos
   - SIN sombras, SIN gradientes, SIN texturas fotográficas
   - SIN efectos 3D ni relieve
   - Bordes limpios entre zonas de color

PROHIBIDO en esta capa (esto irá en capas posteriores):
❌ Edificios o estructuras
❌ Árboles individuales
❌ Caminos o senderos
❌ Texto, números, íconos, flechas
❌ Personas, vehículos, animales
❌ Nubes, sol, decoraciones
❌ Elementos fuera de la silueta del parque

SOLO genera la silueta del terreno con zonas de color plano.
```

### Tu trabajo manual después:
1. **Descarga** la imagen que genera Gemini
2. **Abre** tu archivo `mapa_parque.psd` en GIMP/Photoshop
3. **Pega** la imagen de Gemini en la capa `01_terreno`
4. **Compara** con la ortofoto `original.png`:
   - ¿La silueta coincide con la forma real? Si no, usa la herramienta de **selección libre/lazo** para recortar y ajustar el borde
   - ¿Las proporciones son correctas? El bosque debe ser ~40% del lado derecho
   - ¿El estacionamiento está en el lugar correcto? (franja inferior)
5. **Corrige colores** si no coinciden con el estilo del mapa promo:
   - Usa Bote de pintura o Relleno para cambiar colores de zonas
6. **Guarda** la capa corregida como `capas/01_terreno_v1.png` (exportar PNG)

### Prompt de refinamiento (adjuntar tu versión corregida):
```
Te adjunto MI versión corregida de la capa de terreno. Hice estos 
cambios que DEBES mantener exactamente:

[LLENAR — Describe qué cambiaste, ej:]
- Recorté el borde izquierdo para que sea más curvo como en la ortofoto
- Moví el estacionamiento 50px más abajo
- Agrandé la zona de bosque (ahora ocupa más del lado derecho)
- Cambié el color de la plaza de marrón a marrón arena más claro

Lo que necesito que MEJORES (sin cambiar lo que yo corregí):
[LLENAR — ej:]
- Suaviza los bordes de la silueta, se ven dentados
- La transición entre la zona de césped y la zona de bosque se ve 
  muy brusca, hazla más gradual
- El estacionamiento debe tener esquinas redondeadas

ESPECIFICACIONES: misma imagen JPG de 1400x700, mismos colores, 
mismo estilo flat. Respeta MIS posiciones y formas, solo mejora lo 
que te pido.
```

---

## FASE 2: CAPA DE CAMINOS Y SENDEROS

### Prompt para Gemini (adjuntar tu terreno corregido + original.png):
```
Estoy creando un mapa ilustrado por capas. Te adjunto:
- Imagen 1: mi capa de terreno ya corregida (ESTA es la forma correcta 
  del parque, usa esta como referencia de posición)
- Imagen 2: la ortofoto aérea real (para ver dónde están los caminos reales)

Necesito la SEGUNDA CAPA: solo caminos y senderos.

ESPECIFICACIONES TÉCNICAS:
- Formato: imagen JPG
- Tamaño: exactamente 1400 x 700 píxeles (MISMO tamaño que mi terreno)
- Fondo: BLANCO PURO (#FFFFFF) — yo voy a recortar el fondo después

QUÉ DIBUJAR:

1. CAMINO PRINCIPAL (el más ancho, ~12-15px de grosor):
   - Color: gris (#BDBDBD)
   - Recorre el parque de izquierda a derecha siguiendo la forma 
     visible en la ortofoto
   - Tiene curvas suaves, NO es recto

2. CAMINOS SECUNDARIOS (grosor ~8-10px):
   - Color: gris más claro (#D5D5D5)
   - Conectan las diferentes zonas del parque entre sí
   - Van del camino principal hacia arriba (a la zona del mirador) 
     y hacia las zonas de juegos

3. SENDEROS DEL BOSQUE (grosor ~4-6px):
   - Color: gris terroso (#C5B9A5)
   - Líneas curvas y sinuosas que serpentean por la zona boscosa 
     (lado derecho del mapa)
   - Conectan las casitas y zonas de juegos dentro del bosque

4. ESCALINATAS/RAMPAS:
   - Donde hay desniveles (visible en la ortofoto como cambios de 
     nivel), dibujar líneas transversales cortas que representen 
     escalones

IMPORTANTE — Las posiciones de los caminos deben COINCIDIR con mi capa 
de terreno. Si mi terreno tiene la plaza en el centro-izquierda, los 
caminos deben pasar por ahí.

ESTILO: Líneas limpias, bordes definidos, flat design. Sin textura, 
sin sombra, sin 3D.

PROHIBIDO:
❌ Terreno, colores de fondo (solo fondo blanco)
❌ Edificios, árboles, vegetación
❌ Texto, números, íconos
❌ Cualquier elemento que no sea camino/sendero
```

### Tu trabajo manual después:
1. **Descarga** la imagen de Gemini
2. En GIMP/Photoshop:
   - **Selecciona** el fondo blanco con la Varita Mágica → Eliminar (para hacer transparente)
   - **Pega** en la capa `02_caminos` sobre el terreno
3. **Verifica alineación**: ¿Los caminos caen donde deberían según la ortofoto?
   - Usa **Mover** (tecla M) para reposicionar
   - Usa **Transformar/Escalar** si el tamaño no coincide
4. **Dibuja caminos faltantes** a mano con la herramienta Pincel (brocha dura, color gris)
5. **Borra caminos incorrectos** con el Borrador
6. **Guarda** como `capas/02_caminos_v1.png`

### Prompt de refinamiento (adjuntar terreno+caminos juntos):
```
Te adjunto mi mapa con terreno + caminos superpuestos. La capa de 
caminos tiene estos problemas:

[LLENAR con lo que veas mal, ej:]
- El camino principal no coincide con la ortofoto — debería curvarse 
  más hacia la derecha en la zona central
- Falta un sendero que va desde [punto A] hasta [punto B]
- El camino de la zona del bosque es demasiado recto, debería 
  serpentear más
- Hay un camino que no existe en la realidad — bórralo
- Los caminos son muy delgados, hazlos 2px más gruesos

Genera una nueva versión de SOLO la capa de caminos:
- JPG 1400x700, fondo blanco
- Mantén los caminos que están bien
- Corrige SOLO los problemas que te indiqué
- Mismos colores y grosor que la versión anterior (a menos que 
  te pida cambiarlo)
```

---

## FASE 3: CAPA DE EDIFICIOS Y ESTRUCTURAS

### ⚠️ El problema de los dos contornos diferentes
La imagen promocional (mapa_promo) tiene un contorno artístico distorsionado 
que NO coincide con la silueta real de la ortofoto satelital. Si le pasas 
ambas imágenes a Gemini y le dices "pon los edificios en su lugar", se va 
a confundir porque las geometrías no coinciden.

**La solución: separar ESTILO de POSICIÓN.**
- Del mapa promo → Gemini solo debe copiar la **apariencia** de cada edificio
- De tu mapa en progreso (terreno+caminos) → tú defines la **posición**
- Genera edificios **uno por uno**, no todos juntos

### PASO 3.0 — Crear imagen de referencia con posiciones marcadas
Antes de pedirle nada a Gemini, prepara una **imagen guía de posiciones**:

1. Abre tu mapa en progreso (terreno + caminos) en GIMP/Photoshop
2. Crea una capa nueva llamada `GUIA_posiciones` (temporal, no es para el mapa final)
3. Con la herramienta **Texto** o **Pincel rojo**, marca con cruces rojas (+) 
   y números dónde va cada edificio, comparando con la ortofoto real:
   - Cruz roja + "1" donde va el Ingreso
   - Cruz roja + "2" donde van las Boleterías
   - Cruz roja + "3" donde va la Chiwiña (el edificio más grande)
   - ... y así con los 9 edificios
4. Exporta esta imagen guía como `capas/03_guia_posiciones.png`
5. Oculta/borra la capa `GUIA_posiciones` después (es solo de referencia)

> **¿Por qué esto ayuda?** Porque ahora tú le dices a Gemini EXACTAMENTE 
> dónde poner cada edificio con marcas visuales sobre TU contorno correcto, 
> en vez de que Gemini trate de adivinar la correspondencia entre dos contornos diferentes.

### PASO 3.1 — Generar edificios UNO POR UNO (estrategia recomendada)
En lugar de pedir todos los edificios en una imagen (donde Gemini se 
confundirá con las posiciones), genera cada edificio por separado como 
un "sticker" que tú pegas en su lugar.

### Prompt para CADA edificio (adjuntar SOLO el mapa_promo como referencia de estilo):

**Edificio 3 — Chiwiña (el más importante, empezar por este):**
```
Te adjunto un mapa ilustrado promocional de un parque. Fíjate en el 
edificio marcado como #3 "Chiwiña" — es un domo geodésico grande con 
techo de triángulos en colores azul-verde y turquesa.

Genera SOLO ese edificio aislado, con fondo blanco, en el MISMO estilo 
flat/ilustrado del mapa. Vista en perspectiva isométrica leve (3/4, 
como se ve en el mapa promo). Tamaño de la imagen: 250x200 píxeles.

IMPORTANTE: Solo genera el edificio como un objeto aislado, sin terreno, 
sin suelo, sin contexto alrededor. Como un sticker recortable.
```

**Repetir con cada edificio (cambiar la descripción):**

| Edificio | Descripción para el prompt | Tamaño sugerido |
|----------|---------------------------|-----------------|
| #1 Ingreso | Estructura de entrada/pórtico del parque, arco o portal | 150x120 px |
| #2 Boleterías | Caseta pequeña de venta de boletos, junto al ingreso | 100x80 px |
| #3 Chiwiña | Domo geodésico grande, techo triangulado azul-verde/turquesa | 250x200 px |
| #4 Cafetería | Edificio rectangular, techo naranja/marrón | 180x130 px |
| #5 Teatro Galpón | Galpón con techo a dos aguas, estructura alargada | 200x140 px |
| #8 Escenario Principal | Estructura abierta tipo tinglado/tarima grande con techo | 220x150 px |
| #9 Anfiteatro | Semicírculo con graderías/escalones | 200x150 px |
| Casitas Taypi | 3-4 casitas pequeñas estilo rústico agrupadas | 200x120 px |
| Casitas Macroregiones | 3-4 casitas dispersas, similares a Taypi | 200x120 px |

### Prompt modelo (copiar y adaptar para cada edificio):
```
Te adjunto un mapa ilustrado promocional de un parque. Fíjate en el 
edificio [NOMBRE Y NÚMERO] — [DESCRIPCIÓN DEL EDIFICIO].

Genera SOLO ese edificio aislado, fondo blanco, mismo estilo flat/ilustrado 
del mapa promo. Vista isométrica leve (3/4). Tamaño: [ANCHO x ALTO] píxeles.
Contornos definidos, colores sólidos planos. Como un sticker recortable, 
sin suelo ni contexto alrededor.
```

### PASO 3.2 — Tu trabajo manual: ARMAR EL ROMPECABEZAS

Este es el paso clave donde TÚ controlas las posiciones (no Gemini):

1. **Descarga** todos los edificios generados
2. **Abre** tu archivo `mapa_parque.psd` con todas las capas anteriores
3. **Pon la ortofoto `original.png` como capa semitransparente** (opacidad ~40%)
   encima de todo — esta es tu referencia de dónde va cada cosa en la realidad
4. **Para CADA edificio**:
   a. Abre el PNG del edificio generado por Gemini
   b. Quita el fondo blanco (Varita Mágica → Eliminar)
   c. Copia y pega en la capa `03_edificios`
   d. **Muévelo** (tecla M) a su posición correcta mirando la ortofoto
   e. **Escálalo** (Herramienta Escalar) al tamaño apropiado para el mapa
   f. Si queda mal → genera solo ese edificio de nuevo con Gemini
5. **Oculta** la capa de la ortofoto cuando termines de posicionar
6. **Verifica** que los edificios no tapen caminos importantes — si lo hacen, 
   muévelos ligeramente o borra la parte que sobra

> **TIP**: Pon cada edificio en su propia sub-capa dentro de `03_edificios` 
> (en GIMP: clic derecho en la capa → "Nuevo grupo de capas" → pegar cada 
> edificio como capa separada dentro del grupo). Así puedes mover y escalar 
> cada uno independientemente sin afectar los demás.

### PASO 3.3 — Alternativa: Generar TODOS juntos (solo si te animas)
Si prefieres intentar generar todos en una sola imagen, usa este prompt 
mejorado que separa claramente la referencia de estilo vs. posición:

```
Te adjunto 3 imágenes:
1. "mapa_progreso" — mi mapa en progreso con terreno y caminos ya correctos. 
   ESTA es la geometría/contorno correcto del parque.
2. "guia_posiciones" — el mismo mapa pero con cruces rojas numeradas donde 
   debe ir cada edificio.
3. "mapa_promo" — un mapa promocional ilustrado. Este tiene otro contorno 
   diferente (está distorsionado artísticamente), pero los EDIFICIOS tienen 
   el estilo visual que quiero copiar.

INSTRUCCIÓN CLAVE: 
- Las POSICIONES de los edificios deben seguir la imagen "guia_posiciones" 
  (las cruces rojas numeradas). NO uses las posiciones del mapa_promo porque 
  su contorno es diferente.
- El ESTILO VISUAL de cada edificio (colores, forma, perspectiva) debe 
  copiarse del mapa_promo.

Genera una imagen JPG de 1400x700 con FONDO BLANCO con SOLO los edificios 
en las posiciones marcadas con cruces rojas en mi guía.

Edificios:
1. Cruz #1 → Ingreso/pórtico
2. Cruz #2 → Boleterías (caseta pequeña)
3. Cruz #3 → Chiwiña (domo geodésico, el más grande)
4. Cruz #4 → Cafetería (techo naranja)
5. Cruz #5 → Teatro Galpón (techo a dos aguas)
6. Cruz #8 → Escenario Principal (tinglado grande)
7. Cruz #9 → Anfiteatro (semicírculo con graderías)
8. Zona marcada "Taypi" → casitas pequeñas rústicas
9. Zona marcada "Macro" → más casitas dispersas

Estilo flat design, perspectiva isométrica leve, contornos definidos.
NO incluyas: terreno, caminos, árboles, texto, números.
```

> **NOTA**: Este enfoque "todo junto" es más rápido pero Gemini probablemente 
> meterá la pata con varias posiciones. Vas a tener que recortar y mover 
> edificios igual que en el PASO 3.2. La ventaja del enfoque "uno por uno" 
> es que cada edificio sale mejor y tú controlas 100% la posición.

### PASO 3.4 — Si un edificio queda feo, pide variantes
```
El edificio "Chiwiña" que generaste no se parece al del mapa promo. 
Te adjunto nuevamente SOLO la sección del mapa promo donde aparece ese 
edificio (recorté solo esa parte).

Genera 3 variantes diferentes del domo geodésico Chiwiña:
- Variante A: más redondeado
- Variante B: más angular/geométrico  
- Variante C: más similar al del mapa promo

Mismo estilo flat, fondo blanco, 250x200 px cada uno. Ponlos en fila.
```

### PASO 3.5 — Integrar edificios al mapa (que no se vean "pegados")

Los edificios generados por Gemini probablemente se ven "pegados" sobre 
el mapa — no combinan con el terreno/caminos. Hay dos caminos: arreglarlo 
a mano o pedirle a Gemini que los redibuje integrados.

#### Opción A: Prompt para Gemini — Redibujar edificio integrado al mapa
Adjunta tu mapa en progreso CON el edificio ya posicionado:
```
Te adjunto mi mapa en progreso del Parque de las Culturas. Ya tengo los
edificios posicionados en su lugar correcto, pero se ven "pegados" y no
se integran con el estilo del terreno y caminos.

Necesito que REDIBUJES SOLO el edificio [NOMBRE] (el que está en [POSICIÓN])
manteniendo EXACTAMENTE la misma posición y tamaño, pero:

1. Adapta su paleta de colores a estos tonos del mapa:
   - Techos: naranja cálido (#D4874E) o marrón (#8B6538)
   - Paredes: beige (#E8D5B7) o blanco hueso (#F5F0E1)
   - Domo geodésico (Chiwiña): azul-verde (#4ABFB2) y turquesa (#2E9E8F)
   - Contornos: marrón oscuro (#4A3728), grosor 2-3px

2. Agrega un contorno marrón oscuro (#4A3728) alrededor del edificio,
   consistente con el estilo flat design del mapa promo.

3. Agrega una sombra sutil: una elipse gris oscuro semi-transparente
   debajo y ligeramente detrás del edificio (como si el sol viniera
   del noroeste).

4. En la base del edificio, haz una transición suave con el color del
   terreno que hay debajo — no debe haber un corte recto entre edificio
   y suelo.

Genera la imagen completa de 1400x700 con FONDO BLANCO mostrando SOLO
ese edificio redibujado (para que yo lo pegue en mi mapa).
```

#### Opción B: Prompt para Gemini — Integrar TODOS los edificios de golpe
Si prefieres hacer todos a la vez, adjunta tu mapa completo en progreso:
```
Te adjunto mi mapa en progreso del Parque de las Culturas con terreno,
caminos y edificios. Los edificios están en las posiciones correctas pero
NO se integran bien con el estilo del mapa — se ven "pegados".

Necesito que generes una nueva versión de SOLO la capa de edificios
(imagen JPG 1400x700, fondo blanco) donde TODOS los edificios:

1. Estén en las MISMAS posiciones y tamaños que en mi mapa actual
2. Tengan esta paleta de colores unificada:
   - Contornos: marrón oscuro (#4A3728), grosor consistente 2-3px
   - Techos: naranja cálido (#D4874E), marrón (#8B6538), o naranja
     teja (#C4662B) dependiendo del edificio
   - Paredes: beige claro (#E8D5B7), blanco hueso (#F5F0E1)
   - Chiwiña (domo geodésico): triángulos azul-verde (#4ABFB2),
     turquesa (#2E9E8F), verde agua (#3BBFA0)
   - Ventanas/puertas: marrón medio (#6B4226) o gris azulado (#7B8FA1)
3. Tengan sombra sutil (elipse gris, opacidad 20%, debajo de cada uno)
4. Perspectiva isométrica leve uniforme (3/4 vista, todos mirando
   hacia la misma dirección)
5. Estilo FLAT DESIGN con colores sólidos planos, sin gradientes,
   sin texturas fotográficas

Los edificios son:
- Ingreso (#1): pórtico/arco de entrada
- Boleterías (#2): caseta pequeña
- Chiwiña (#3): domo geodésico grande (el más importante)
- Cafetería (#4): edificio rectangular, techo naranja
- Teatro Galpón (#5): galpón alargado, techo a dos aguas
- Escenario Principal (#8): estructura abierta con techo/tinglado
- Anfiteatro (#9): semicírculo con graderías
- Casitas Taypi: 3-4 casitas rústicas en zona boscosa
- Casitas Macroregiones: casitas dispersas extremo derecho

IMPORTANTE: Mantén las posiciones EXACTAS de mi mapa. Solo cambia
el estilo visual para que sean uniformes y se integren al mapa.
```

#### Opción C: Arreglarlo a mano en GIMP/Photoshop (más control)
Si prefieres no depender de Gemini para esto:

1. **Unificar colores** — Selecciona cada edificio → Colores → Tono/Saturación:
   - Tono: ajustar hacia naranjas/marrones cálidos
   - Saturación: bajar a ~60-70% (los colores planos no son muy saturados)
   - Luminosidad: ajustar para que no sea ni muy brillante ni muy oscuro

2. **Agregar contornos** — Para cada edificio:
   - Varita Mágica en el fondo → Invertir selección (ahora tienes el edificio seleccionado)
   - Seleccionar → Crecer → 2px
   - Crear capa NUEVA debajo del edificio
   - Editar → Rellenar selección con marrón oscuro (#4A3728)
   - Resultado: borde marrón consistente como en el mapa promo

3. **Agregar sombras** — Para cada edificio:
   - Duplicar la capa del edificio
   - En la copia: Colores → Tono/Saturación → Luminosidad a -100 (todo negro)
   - Herramienta Escalar: reducir SOLO la altura al 25-30%
   - Mover la sombra debajo y ligeramente hacia abajo-derecha
   - Opacidad de la capa sombra: 15-20%
   - Filtros → Desenfocar → Desenfoque Gaussiano → 4px

4. **Suavizar bases** — Con pincel suave (opacidad 30%), color del terreno
   (#C4A882), pinta la zona donde el edificio toca el suelo

### Guardar resultado:
- **Guarda** como `capas/03_edificios_v1.png`
- Si pusiste cada edificio en sub-capa, también exporta `capas/03_chiwina.png`, 
  `capas/03_cafeteria.png`, etc. por si necesitas regenerar uno solo

---

## FASE 4: CAPA DE ÁRBOLES Y VEGETACIÓN

### Prompt para Gemini (adjuntar tu mapa actual + mapa_promo):
```
Estoy creando un mapa ilustrado por capas. Te adjunto:
- Imagen 1: mi mapa en progreso (terreno + caminos + edificios ya puestos)
- Imagen 2: mapa promocional de referencia (FÍJATE cómo están dibujados 
  los árboles — son triángulos verdes simples estilizados)

Necesito la CUARTA CAPA: solo árboles y vegetación.

ESPECIFICACIONES TÉCNICAS:
- Formato: imagen JPG
- Tamaño: exactamente 1400 x 700 píxeles
- Fondo: BLANCO PURO (#FFFFFF)

CÓMO DEBEN VERSE LOS ÁRBOLES (copia el estilo del mapa promo):
- Forma: triángulos simples apilados (2-3 triángulos por árbol) con 
  un tronco fino rectangular marrón (#6B4226) abajo
- NO realistas, NO fotográficos — son formas geométricas planas
- Sin sombras, sin gradientes, sin detalles internos
- Contorno fino marrón oscuro (#4A3728) opcional

PALETA DE COLORES para los árboles (usar TODOS, mezclar):
- Verde oscuro: #2D5016 (árboles del fondo/más lejanos)
- Verde bosque: #4A7A2E (árboles medianos)
- Verde esmeralda: #3D8B37 (árboles del frente)
- Verde claro: #6BAF49 (árboles jóvenes/pequeños)
- Verde azulado: #2E7D5B (variación para que no sea monótono)

DISTRIBUCIÓN EN EL MAPA:

1. ZONA DERECHA — BOSQUE DENSO (~40% del ancho del mapa):
   - Llenar densamente con árboles de diferentes tamaños
   - Los árboles se superponen ligeramente entre sí
   - TAMAÑOS VARIADOS: grandes (40-50px alto) en primer plano, 
     medianos (25-35px) en medio, pequeños (15-20px) atrás
   - DEJAR HUECOS/CLAROS donde van los senderos (mira mi mapa 
     de progreso para ver dónde están los caminos)
   - DEJAR HUECOS donde van las casitas de Taypi y Macroregiones

2. ZONA IZQUIERDA — ÁRBOLES DISPERSOS:
   - Solo 5-8 árboles individuales sueltos
   - Tamaño mediano-pequeño
   - Cerca de los bordes/perímetro del parque
   - NO poner árboles encima de los edificios ni de la plaza

3. ZONA CENTRAL — ARBUSTOS:
   - Algunos arbustos pequeños (círculos verdes de 8-12px) a lo 
     largo de los caminos
   - Macetas/jardineras como rectángulos verdes pequeños

IMPORTANTE: Mira mi mapa de progreso para ver dónde están los 
edificios y caminos. NO pongas árboles encima de ellos.

PROHIBIDO:
❌ Edificios, caminos, terreno de fondo
❌ Texto, números, íconos
❌ Árboles con hojas detalladas o estilo realista
❌ Sombras o gradientes en los árboles
```

### Tu trabajo manual después:
1. **Quita el fondo blanco**
2. **Pega** sobre tus capas anteriores
3. **Problema común**: Gemini pondrá árboles donde van edificios o caminos
   - **Borra** árboles que tapan edificios con el Borrador
   - **Borra** árboles que bloquean caminos
4. **Agrega árboles faltantes**: 
   - Selecciona un árbol que te guste → Copiar → Pegar → Mover
   - Repite para llenar huecos del bosque
   - Cambia el tono verde (Tono/Saturación) para dar variedad
5. **Escala árboles**: Los del fondo más pequeños, los del frente más grandes
6. **Guarda** como `capas/04_arboles_v1.png`

### Prompt de refinamiento:
```
Te adjunto mi mapa con todas las capas hasta ahora. La capa de 
árboles tiene estos problemas específicos:

[LLENAR, ej:]
- La esquina superior derecha tiene muy pocos árboles — necesito 
  el doble de densidad ahí
- Todos los árboles son del mismo tamaño (~30px) — necesito variación: 
  grandes (50px), medianos (30px), pequeños (15px)
- Hay árboles encima del edificio #8 (Escenario Principal) — elimínalos
- Los árboles del lado izquierdo son demasiados — deja solo 4-5 sueltos
- El color es muy uniforme — usa más variedad de verdes
- Falta un claro/hueco en el bosque donde va el sendero principal

Genera una NUEVA capa de vegetación completa que:
- CORRIJA los problemas que te indiqué
- MANTENGA los árboles que ya están bien posicionados
- Use el MISMO estilo (triángulos planos, flat design)
- JPG 1400x700, fondo blanco
```

### Prompt extra — Generar árboles sueltos para copiar-pegar:
```
Genera una HOJA DE SPRITES de árboles estilizados para un mapa ilustrado.
Imagen JPG de 800x400, fondo blanco.

Dibuja 20 árboles sueltos organizados en 4 filas de 5, con espacio 
entre ellos para recortar. Cada árbol debe ser diferente:

Fila 1 — ÁRBOLES GRANDES (50-60px alto):
5 árboles tipo pino/conífera, triángulos verdes, diferentes tonos 
de verde (#2D5016, #4A7A2E, #3D8B37, #6BAF49, #2E7D5B)

Fila 2 — ÁRBOLES MEDIANOS (30-40px alto):
5 árboles más pequeños, mismos estilos pero proporcionalmente menores

Fila 3 — ÁRBOLES PEQUEÑOS (15-25px alto):
5 arbolitos para el fondo/lejanía

Fila 4 — ARBUSTOS Y MATORRALES (10-15px alto):
5 arbustos redondeados/ovalados verdes para decorar bordes de caminos

Estilo: flat design, colores sólidos, tronco fino marrón, SIN sombras.
Cada árbol bien separado del siguiente para poder recortarlos.
```

---

## FASE 5: CAPA DE AGUA, JUEGOS Y DETALLES

### Prompt para Gemini (adjuntar tu mapa actual + mapa_promo):
```
Estoy creando un mapa ilustrado por capas. Te adjunto:
- Imagen 1: mi mapa en progreso (terreno + caminos + edificios + árboles)
- Imagen 2: mapa promocional de referencia

Necesito la QUINTA CAPA: elementos de detalle.

ESPECIFICACIONES TÉCNICAS:
- Formato: imagen JPG
- Tamaño: exactamente 1400 x 700 píxeles
- Fondo: BLANCO PURO (#FFFFFF)

ELEMENTOS A DIBUJAR (cada uno en su posición según mi mapa):

1. AGUAS DANZANTES — Fuente/piscina decorativa:
   - Posición: zona central del parque
   - Forma: rectángulo redondeado o forma orgánica
   - Color: azul agua (#4FC3F7) con 2-3 líneas curvas blancas 
     adentro simulando ondas
   - Borde: azul más oscuro (#2196F3), 2px
   - Tamaño: aprox 80x50px

2. TELEFÉRICO — Sistema de cable aéreo:
   - Posición: esquina superior izquierda, cruzando diagonalmente
   - Dibujar: una línea negra fina (2px) que representa el cable
   - Colgar 3 cabinas del cable: rectángulos redondeados de 20x15px 
     en rojo (#E74C3C) con ventanas blancas
   - Una torre/poste en cada extremo del cable (líneas grises finas)

3. APACHETA — Montículo de piedras ritual:
   - Posición: junto al mirador (arriba izquierda)
   - Forma: pirámide pequeña de piedras circulares apiladas
   - Colores: grises (#888, #AAA, #CCC) alternando
   - Tamaño: aprox 30x25px

4. ZONAS DE JUEGOS — Áreas resaltadas semitransparentes:
   - NO son objetos sólidos, son manchas de color tenue que 
     resaltan una zona del mapa
   - Tierras Altas: óvalo naranja tenue (#E67E22, opacidad 25%) 
     arriba izquierda
   - Tierras Medias: óvalo naranja tenue (#F39C12, opacidad 25%) 
     centro del mapa
   - Tierras Bajas: óvalo naranja claro (#F5B041, opacidad 25%) 
     abajo centro
   - Taypi: óvalo gris tenue (#95A5A6, opacidad 25%) centro-derecha
   - Cada zona ~150x100px aproximadamente

5. BANCAS/MOBILIARIO (opcional):
   - Pequeños rectángulos marrones (#8B6538) de 10x5px dispersos 
     junto a los caminos, representando bancas

ESTILO: Flat design, colores sólidos, sin sombras, sin gradientes.

PROHIBIDO:
❌ Terreno, caminos, edificios, árboles
❌ Texto, números
❌ Elementos fuera de la silueta del parque
```

### Tu trabajo manual después:
1. Quita fondo blanco, pega en capa `05_detalles`
2. Posiciona cada elemento en su lugar correcto
3. Ajusta la transparencia/opacidad de las zonas de juego (~30-40%) para que se vean como áreas resaltadas
4. El teleférico puede necesitar redibujarse: usa la herramienta Línea para el cable y copia las cabinas
5. **Guarda** como `capas/05_detalles_v1.png`

---

## FASE 6: CAPA DE ÍCONOS DE SERVICIOS

### Prompt para Gemini:
```
Genera una imagen JPG de 700x200 píxeles con fondo BLANCO PURO.

Dibuja 7 íconos de servicios para un mapa de parque, organizados en 
una fila horizontal con 80px de espacio entre cada uno.

Cada ícono debe:
- Ser de 50x50 píxeles exactos
- Estar dentro de un círculo de fondo blanco con borde fino (2px)
- Tener diseño flat/minimalista, MÁXIMO 2 colores por ícono
- Ser reconocible incluso si se reduce a 25x25px

Los 7 íconos de izquierda a derecha:

1. BAÑOS: Silueta clásica hombre+mujer (el símbolo universal de WC).
   Color: azul (#2196F3). Borde círculo: azul oscuro (#1565C0).

2. BAÑO FAMILIAR: Silueta de adulto+niño juntos.
   Color: azul (#2196F3). Borde: azul oscuro (#1565C0).

3. ACCESO DISCAPACITADOS: Símbolo internacional de silla de ruedas.
   Color: azul (#2196F3). Borde: azul oscuro (#1565C0).

4. POSTA DE SALUD: Cruz médica simple (cruz griega gruesa).
   Color: rojo (#E53935). Borde: rojo oscuro (#B71C1C).

5. KIOSCO: Letra "K" grande bold centrada.
   Color: marrón (#795548). Borde: marrón oscuro (#4E342E).
   Fondo del círculo: crema (#FFF8E1).

6. PARQUEO VEHICULAR: Letra "P" grande bold centrada.
   Color: blanco. Fondo del círculo: azul (#1976D2).

7. PARQUEO BICICLETAS: Silueta simplificada de bicicleta (2 círculos 
   para ruedas + líneas para marco).
   Color: verde (#388E3C). Borde: verde oscuro (#1B5E20).

Sin texto debajo de los íconos. Sin sombras. Sin gradientes.
Cada ícono bien separado y centrado en su espacio para poder 
recortarlo fácilmente.
```

### Tu trabajo manual después:
1. **Recorta cada ícono** individualmente
2. **Guarda** cada ícono por separado en `assets/iconos/`:
   - `icono_bano.png`, `icono_salud.png`, etc.
3. En tu mapa, crea la capa `06_iconos_servicios`
4. **Coloca** cada ícono en su posición según el mapa promo:
   - Hay baños en varias ubicaciones
   - Los kioscos (K) están en 2 ubicaciones
   - etc.
5. Si un ícono quedó feo, **dibújalo tú** — son formas simples
6. **Guarda** como `capas/06_iconos_v1.png`

---

## FASE 7: CAPA DE NÚMEROS Y POIs

### Prompt para Gemini:
```
Genera una imagen JPG de 800x200 píxeles con fondo BLANCO PURO.

Dibuja 2 filas de marcadores circulares para un mapa:

FILA 1 — MARCADORES GRANDES (40x40px cada uno, separados 20px):
11 círculos numerados del 1 al 11.
- Fondo de cada círculo: naranja (#E67E22)
- Número adentro: blanco (#FFFFFF), fuente bold sans-serif, centrado
- Borde exterior: blanco (#FFFFFF), grosor 3px
- Los números de 2 dígitos (10, 11) deben tener fuente más pequeña 
  para que quepan dentro del círculo

FILA 2 — MARCADORES PEQUEÑOS (25x25px cada uno, separados 15px):
5 círculos de colores SIN número adentro (solo color sólido):
- Círculo 1: naranja oscuro (#D35400) — representa "Tierras Altas"
- Círculo 2: naranja medio (#E67E22) — representa "Tierras Medias"
- Círculo 3: naranja claro (#F5B041) — representa "Tierras Bajas"
- Círculo 4: gris claro (#95A5A6) — representa "Taypi"
- Círculo 5: verde (#27AE60) — representa "Macroregiones"
Cada uno con borde blanco de 2px.

Estilo FLAT: colores 100% sólidos, sin gradiente, sin sombra, sin brillo.
Círculos perfectamente redondos (no ovalados).
```

### Tu trabajo manual:
1. **Recorta** cada marcador
2. **Es más fácil hacerlos tú mismo**: 
   - Herramienta Elipse → círculo de 40px → relleno naranja → borde blanco 2px
   - Herramienta Texto → número blanco centrado → fuente bold
3. **Coloca** cada número en su posición del mapa:
   - 1 (Ingreso) → extremo izquierdo
   - 2 (Boleterías) → junto al ingreso
   - 3 (Chiwiña) → sobre el domo geodésico
   - 4 (Cafetería) → arriba centro-izquierdo
   - 5 (Teatro Galpón) → junto a cafetería
   - 6 (Aguas Danzantes) → centro, sobre la fuente
   - 7 (Mirador) → punto más alto, arriba izquierda
   - 8 (Escenario Principal) → centro-derecho
   - 9 (Anfiteatro) → abajo derecha
   - 10 (Parrillero) → arriba derecha, en el bosque
   - 11 (Área Picnik) → derecha, en el bosque
4. **Guarda** como `capas/07_numeros_v1.png`

---

## FASE 8: CAPA DE LEYENDA Y TEXTO

### Prompt para Gemini (adjuntar mapa promo):
```
Te adjunto el mapa promocional de referencia. Fíjate en la leyenda 
que tiene en la parte inferior izquierda — necesito algo similar.

Genera una imagen JPG de 600x350 píxeles que sea la leyenda del mapa.

DISEÑO:
- Fondo: rectángulo redondeado color crema (#F5F0E1) con borde fino 
  marrón (#8B6538)
- Dividido en 3 columnas

COLUMNA 1 — LUGARES (título bold):
Lista vertical con número en círculo naranja (#E67E22) + texto:
  1  Ingreso
  2  Boleterías
  3  Chiwiña
  4  Cafetería
  5  Teatro Galpón
  6  Aguas Danzantes
  7  Mirador
  8  Escenario Principal
  9  Anfiteatro
  10 Parrillero
  11 Área de Picnik

COLUMNA 2 — JUEGOS (título bold):
Lista vertical con punto de color + texto:
  ● Tierras Altas      (punto naranja oscuro #D35400)
  ● Tierras Medias     (punto naranja #E67E22)
  ● Tierras Bajas      (punto naranja claro #F5B041)
  ● Taypi              (punto gris #95A5A6)
  ● Macroregiones      (punto verde #27AE60)

COLUMNA 3 — SERVICIOS (título bold):
Lista vertical con ícono pequeño + texto:
  🚻 Baños
  👨‍👩‍👧 Baño Familiar
  ♿ Acceso Discapacitados
  ➕ Posta de Salud
  K  Kioscos
  🅿 Parqueo Vehicular
  🚲 Parqueo Bicicletas

TIPOGRAFÍA: sans-serif (tipo Arial/Helvetica), color texto marrón 
oscuro (#4A3728). Títulos en bold, items en regular.
Tamaño legible, buena separación entre items.

ATENCIÓN CON LA ORTOGRAFÍA — Copia EXACTAMENTE estos textos en español:
- "Boleterías" (con tilde en la i)
- "Chiwiña" (con ñ)
- "Cafetería" (con tilde en la i)
- "Galpón" (con tilde en la o)
- "Área" (con tilde en la A)
```

> **NOTA IMPORTANTE**: Gemini probablemente va a equivocarse con los 
> acentos y la ñ. Es **mucho más eficiente hacer la leyenda 100% a mano** 
> con la herramienta Texto de GIMP/Photoshop. Usa los marcadores que 
> generaste en la Fase 7 como referencia visual.

### Tu trabajo manual:
1. **Honestamente, la leyenda es mejor hacerla 100% a mano** porque Gemini 
   va a equivocarse con los textos/acentos. Usa la Herramienta Texto de GIMP/Photoshop
2. Si usas la de Gemini: corrige errores de texto, alinea columnas
3. Agrega el título "BIENVENIDOS al Parque de las Culturas y de la Madre Tierra" 
   arriba del mapa (fuente grande, bold)
4. Agrega la mascota del parque (el oso hormiguero) si tienes el recurso
5. **Guarda** como `capas/08_leyenda_v1.png`

---

## FASE 9: EXPORTAR MAPA FINAL + MAPA INTERACTIVO

### 9.1 Exportar mapa ilustrado
1. En GIMP/Photoshop, asegúrate de que todas las capas estén visibles y bien posicionadas
2. **Exportar como JPG** de alta calidad: `mapa_final.jpg` (calidad 95%)
3. **Exportar como PNG** si necesitas transparencia: `mapa_final.png`
4. También guarda el archivo de capas `.psd` / `.xcf` para ediciones futuras

### 9.2 Mapa interactivo con coordenadas (Leaflet.js)
Usa este prompt en Gemini:
```
Genera un archivo HTML completo y funcional que muestre un mapa 
interactivo del Parque de las Culturas y de la Madre Tierra usando 
Leaflet.js (cargado desde CDN, sin instalar nada).

REQUISITOS TÉCNICOS:
- El archivo HTML debe funcionar abriéndolo directamente en el navegador
- Cargar Leaflet.js y su CSS desde CDN (unpkg o cdnjs)
- La imagen del mapa "mapa_final.jpg" está en la misma carpeta que el HTML
- Diseño responsive que funcione en desktop y móvil

MAPA BASE:
- Tile layer: OpenStreetMap estándar
- Centro inicial: [INSERTAR LAT, LON DEL CENTRO DEL PARQUE]
- Zoom inicial: 17 (nivel de manzana/edificio)
- Zoom mínimo: 15, máximo: 19

OVERLAY DE IMAGEN:
- Superponer "mapa_final.jpg" como L.imageOverlay
- Esquinas del overlay (bounds):
  - Esquina suroeste (SW): [LAT_SW, LON_SW]
  - Esquina noreste (NE): [LAT_NE, LON_NE]
- Opacidad inicial: 0.85
- Agregar un slider HTML para controlar la opacidad del overlay (0 a 1)

MARCADORES — Usar L.divIcon con círculo naranja y número blanco:
[PEGAR TU TABLA DE COORDENADAS AQUÍ, formato:]
{ nombre: "Ingreso", lat: -XX.XXXX, lon: -XX.XXXX, numero: 1,
  descripcion: "Entrada principal del parque" },
{ nombre: "Boleterías", lat: -XX.XXXX, lon: -XX.XXXX, numero: 2,
  descripcion: "Venta de boletos de ingreso" },
[...continuar con los 11 puntos...]

Cada marcador al hacer clic muestra un popup con:
- Nombre del lugar en bold
- Descripción corta
- Número entre paréntesis

CONTROL DE CAPAS (L.control.layers):
- Capa base: OpenStreetMap (siempre visible)
- Overlays checkbox:
  ☑ Mapa ilustrado (la imagen overlay)
  ☑ Puntos de interés (1-11)
  ☑ Zonas de juegos
  ☑ Servicios

ESTILOS CSS INLINE (dentro del mismo HTML):
- El control de opacidad debe estar en la esquina inferior derecha
- Los popups con fondo blanco y bordes redondeados
- Los marcadores (divIcon) como círculos naranjas de 30px con 
  número blanco centrado

El código debe estar limpio, comentado en español, y listo para 
usar sin modificaciones (excepto insertar las coordenadas reales).
```

---

## FLUJO DE TRABAJO VISUAL (Resumen)

```
CAPA 1: TERRENO          CAPA 2: CAMINOS         CAPA 3: EDIFICIOS
┌──────────────┐         ┌──────────────┐         ┌──────────────┐
│ Gemini genera│         │ Gemini genera│         │ Gemini genera│
│ imagen JPG   │         │ imagen JPG   │         │ imagen JPG   │
└──────┬───────┘         └──────┬───────┘         └──────┬───────┘
       ▼                        ▼                        ▼
┌──────────────┐         ┌──────────────┐         ┌──────────────┐
│ TÚ corriges  │         │ TÚ corriges  │         │ TÚ corriges  │
│ en GIMP/PS   │         │ en GIMP/PS   │         │ en GIMP/PS   │
│ - Recortas   │         │ - Alineas    │         │ - Posicionas │
│ - Recoloreas │         │ - Dibujas    │         │ - Escalas    │
│ - Ajustas    │         │   los que    │         │ - Redibujas  │
│   silueta    │         │   faltan     │         │   los malos  │
└──────┬───────┘         └──────┬───────┘         └──────┬───────┘
       ▼                        ▼                        ▼
┌──────────────┐         ┌──────────────┐         ┌──────────────┐
│ Gemini refina│         │ Gemini refina│         │ Gemini refina│
│ con TUS      │         │ con TUS      │         │ con TUS      │
│ correcciones │         │ correcciones │         │ correcciones │
└──────┬───────┘         └──────┬───────┘         └──────┬───────┘
       │                        │                        │
       └────────────┬───────────┴────────────────────────┘
                    ▼
         ┌───────────────────┐
         │ REPETIR con capas:│
         │ 4.Árboles         │
         │ 5.Detalles        │
         │ 6.Íconos          │
         │ 7.Números         │
         │ 8.Leyenda/Texto   │
         └────────┬──────────┘
                  ▼
         ┌───────────────────┐
         │  GIMP/Photoshop   │
         │  Unir todas las   │
         │  capas → Exportar │
         │  mapa_final.jpg   │
         └────────┬──────────┘
                  ▼
         ┌───────────────────┐
         │  HTML + Leaflet   │
         │  Mapa interactivo │
         │  con coordenadas  │
         └───────────────────┘
```

---

## TIPS CLAVE

### Para que Gemini genere mejores imágenes:
- **Siempre adjunta tu versión más reciente** del mapa como referencia
- **Sé MUY específico** con colores (usa códigos hex), tamaños (en píxeles), posiciones
- **Pide UNA capa a la vez**, nunca todo junto
- **Pide fondo blanco** para poder recortar fácilmente
- Si la imagen es mala, **no insistas con el mismo prompt** — reformúlalo

### Para tu edición manual:
- **Trabaja con zoom al 200-300%** para detalles
- **Usa capas con nombres claros** — nunca trabajes todo en una sola capa
- **Guarda versiones**: cada vez que una capa quede bien, exporta PNG con nombre versionado
- **La ortofoto es tu referencia real** — pon `original.png` como capa semitransparente para verificar posiciones
- **Ctrl+Z es tu amigo** — experimenta sin miedo

### Para pasar correcciones a Gemini:
- Siempre adjunta la imagen que TÚ editaste, no la que Gemini generó antes
- Di exactamente qué cambiaste: "moví el edificio 3 más a la izquierda", "borré los árboles del centro"
- Di exactamente qué falta mejorar: "necesito más árboles arriba a la derecha"

### Estructura de archivos:
```
MAPA/
├── original.png                 (ortofoto drone)
├── mapa_promo.png               (mapa ilustrado referencia)
├── mapa_parque.psd              (archivo master con TODAS las capas)
├── mapa_final.jpg               (exportación final)
├── mapa_interactivo.html        (versión web con Leaflet)
├── coordenadas.json             (coordenadas GPS)
├── capas/                       (capas individuales exportadas)
│   ├── 01_terreno_v1.png
│   ├── 01_terreno_v2.png        (después de correcciones)
│   ├── 02_caminos_v1.png
│   ├── 03_edificios_v1.png
│   ├── 04_arboles_v1.png
│   ├── 05_detalles_v1.png
│   ├── 06_iconos_v1.png
│   ├── 07_numeros_v1.png
│   └── 08_leyenda_v1.png
└── assets/
    └── iconos/                  (íconos recortados individuales)
        ├── icono_bano.png
        ├── icono_salud.png
        └── ...
```
