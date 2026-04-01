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
Te adjunto una ortofoto aérea real de un parque y su mapa promocional 
ilustrado. Necesito que generes una IMAGEN JPG de 1400x700 píxeles con 
fondo beige claro (#D4C9A8) que muestre SOLO la silueta/forma del terreno 
del parque, sin edificios, sin árboles, sin texto, sin personas.

Lo que debe incluir esta capa:
- La silueta del perímetro del parque (forma de medialuna/riñón)
- Zonas de tierra/plaza en color marrón arena (#C4A882)
- Zonas de césped en verde claro (#8DB564)
- El estacionamiento largo en la parte inferior en gris (#9E9E9E)
- Las zonas donde irá bosque (lado derecho) en verde medio (#5D8A3C) 
  como mancha de color plana, SIN dibujar árboles individuales

Estilo: flat design, colores sólidos y planos, sin sombras, sin texturas 
fotográficas. Similar al estilo del mapa promocional adjunto.

NO incluyas: edificios, árboles individuales, texto, números, íconos, 
personas, nubes, decoraciones. Solo la forma del terreno con zonas de color.
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
Te adjunto mi versión corregida de la capa de terreno del mapa. 
Necesito que la mejores manteniendo MIS correcciones:

[Describe qué corregiste, por ejemplo:]
- Ajusté la silueta del borde izquierdo para que sea más curva
- El estacionamiento ahora está más abajo
- La zona de bosque es más grande

Genera una nueva versión JPG de 1400x700 que mantenga estos cambios 
y mejore: [lo que quieras mejorar, ej: "suaviza los bordes", 
"hazla más similar al mapa promo"]
```

---

## FASE 2: CAPA DE CAMINOS Y SENDEROS

### Prompt para Gemini (adjuntar tu terreno corregido + original.png + mapa_promo):
```
Te adjunto 2 imágenes:
1. Mi capa de terreno ya corregida del parque
2. La ortofoto aérea real (original.png)

Genera una imagen JPG de 1400x700 con FONDO BLANCO que muestre 
SOLAMENTE los caminos y senderos del parque. Esta imagen la voy a 
superponer sobre la capa de terreno.

Debe incluir:
- Camino principal que cruza el parque de izquierda a derecha (gris claro #BDBDBD)
- Caminos secundarios que conectan las zonas (gris más claro #D5D5D5)
- Senderos en la zona boscosa (derecha) como líneas curvas más delgadas
- Las escalinatas/rampas que conectan niveles (el parque tiene desniveles)

Los caminos deben coincidir con las posiciones visibles en la ortofoto.
Estilo flat, líneas limpias, sin texturas. Las líneas deben tener grosor 
visible (como en el mapa promo donde se ven los caminos).

NO incluyas: terreno, edificios, árboles, texto, íconos. 
Solo caminos sobre fondo blanco.
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
Te adjunto cómo quedó mi mapa con la capa de terreno + caminos superpuestos.
[Describe problemas, ej: "el camino principal debería curvarse más hacia 
la derecha", "falta un sendero que conecta el mirador con la cafetería"]

Genera una versión mejorada de SOLO la capa de caminos (fondo blanco, 
1400x700) con estas correcciones.
```

---

## FASE 3: CAPA DE EDIFICIOS Y ESTRUCTURAS

### Prompt para Gemini (adjuntar tu mapa actual + mapa_promo):
```
Te adjunto mi mapa en progreso (terreno + caminos) y el mapa promocional 
de referencia del Parque de las Culturas.

Genera una imagen JPG de 1400x700 con FONDO BLANCO que muestre SOLO los 
edificios y estructuras del parque, en estilo flat/ilustrado como el mapa 
promo. Cada edificio debe estar en la posición correcta según mi mapa.

Edificios a incluir (con su estilo del mapa promo):
1. Chiwiña (#3) — el domo geodésico grande, techo triangulado azul-verde/turquesa
2. Cafetería (#4) — edificio rectangular, techo naranja/marrón
3. Teatro Galpón (#5) — galpón con techo a dos aguas, junto a cafetería
4. Escenario Principal (#8) — estructura abierta tipo tinglado grande
5. Anfiteatro (#9) — semicírculo/graderías, parte inferior derecha
6. Boleterías (#2) — caseta pequeña junto al ingreso
7. Casitas zona Taypi — varias casitas pequeñas estilo rústico en la zona del bosque
8. Casitas zona Macroregiones — más casitas dispersas en el extremo derecho
9. Estructura del Ingreso (#1) — entrada/pórtico del parque

Estilo: flat design, contornos definidos, colores sólidos del mapa promo.
Vista: perspectiva isométrica leve (como se ve en el mapa promo, los 
edificios se ven ligeramente en 3/4, no solo desde arriba).

NO incluyas: terreno, caminos, árboles, texto, números. 
Solo edificios sobre fondo blanco.
```

### Tu trabajo manual después:
1. **Quita el fondo blanco** (Varita Mágica → Eliminar)
2. **Recorta cada edificio por separado** si es posible:
   - Selecciona un edificio → Cortar → Pegar como nueva capa
   - Así puedes mover cada edificio individualmente
3. **Posiciona cada edificio** comparando con la ortofoto:
   - Pon la ortofoto como capa semi-transparente de referencia
   - Arrastra cada edificio a su posición correcta
4. **Escala** edificios que estén muy grandes o pequeños (Herramienta Escalar)
5. **Redibuja** partes que Gemini haya hecho mal:
   - Usa el Pincel para corregir contornos
   - Usa el Bote de pintura para corregir colores
6. Si un edificio quedó muy mal, **genera solo ese edificio** con Gemini:

### Prompt para un edificio individual:
```
Genera SOLO el edificio "Chiwiña" del parque — es un domo geodésico grande 
con techo de triángulos en colores azul-verde y turquesa. Vista en perspectiva 
isométrica leve. Estilo flat design. Fondo blanco. Tamaño: 200x150 píxeles.
Usa como referencia el edificio #3 del mapa promocional adjunto.
```

7. **Guarda** como `capas/03_edificios_v1.png`

---

## FASE 4: CAPA DE ÁRBOLES Y VEGETACIÓN

### Prompt para Gemini (adjuntar tu mapa actual + mapa_promo):
```
Te adjunto mi mapa en progreso y el mapa promocional de referencia.

Genera una imagen JPG de 1400x700 con FONDO BLANCO que muestre SOLO 
árboles y vegetación en estilo flat/ilustrado como el mapa promo.

ZONA DERECHA (BOSQUE DENSO ~40% del mapa):
- Muchos árboles tipo conífera/pino estilizados (triángulos verdes)
- Diferentes tamaños: grandes, medianos, pequeños
- Diferentes tonos: verde oscuro (#2D5016), verde medio (#4A7A2E), 
  verde esmeralda (#3D8B37), verde claro (#6BAF49)
- Deben estar agrupados densamente, superponiéndose ligeramente
- Dejar espacios para senderos y casitas (que irán en otra capa)

ZONA IZQUIERDA (ÁRBOLES SUELTOS):
- Algunos árboles individuales dispersos
- Más pequeños que los del bosque

ZONA CENTRAL:
- Arbustos pequeños decorativos a lo largo de caminos
- Manchas de césped/pasto

Estilo exactamente como el mapa promo: árboles como triángulos simples 
con tronco fino, no realistas. Colores sólidos planos.

NO incluyas: edificios, caminos, terreno, texto. Solo vegetación 
sobre fondo blanco.
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
Te adjunto cómo quedó mi mapa con todas las capas hasta ahora 
(terreno + caminos + edificios + árboles). 

Problemas que veo:
- [ej: "Hay muy pocos árboles en la esquina superior derecha"]
- [ej: "Los árboles son todos del mismo tamaño"]

Genera SOLO una nueva capa de vegetación (fondo blanco, 1400x700) 
que corrija estos problemas. Mantén el mismo estilo y posiciones 
que ya están bien.
```

---

## FASE 5: CAPA DE AGUA, JUEGOS Y DETALLES

### Prompt para Gemini (adjuntar tu mapa actual):
```
Te adjunto mi mapa en progreso del Parque de las Culturas.

Genera una imagen JPG de 1400x700 con FONDO BLANCO que muestre SOLO 
estos elementos de detalle:

1. AGUAS DANZANTES (#6) — fuente/piscina decorativa en la zona central, 
   color azul agua (#4FC3F7) con efecto de ondas simples
2. TELEFÉRICO — cable con cabinas rojas en la esquina superior izquierda 
   (como se ve en el mapa promo, las cabinas cuelgan de un cable)
3. APACHETA — estructura de piedras apiladas junto al mirador (arriba izquierda)
4. ZONAS DE JUEGOS — representadas como áreas de color:
   - Tierras Altas: zona naranja tenue arriba izquierda  
   - Tierras Medias: zona naranja tenue centro
   - Tierras Bajas: zona naranja tenue abajo centro
   - Taypi: zona gris tenue centro-derecha

Estilo flat, colores suaves. Solo estos elementos sobre fondo blanco.
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
Genera un SET de íconos individuales para un mapa de parque, estilo flat 
design, cada uno de 50x50 píxeles, todos sobre FONDO BLANCO, en una 
cuadrícula. Los íconos son:

1. 🚻 Baños — símbolo hombre/mujer clásico, azul
2. 👨‍👩‍👧 Baño Familiar — símbolo familia, azul  
3. ♿ Acceso Discapacitados — símbolo silla de ruedas, azul
4. ➕ Posta de Salud — cruz, rojo
5. K Kiosco — letra K en círculo marrón
6. P Parqueo Vehicular — letra P en cuadrado azul
7. 🚲 Parqueo Bicicletas — bicicleta simplificada, verde

Cada ícono debe tener contorno definido y ser legible en tamaño pequeño.
Ponlos todos en una sola imagen como cuadrícula para que yo los recorte.
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
Genera 11 marcadores circulares numerados del 1 al 11 para un mapa.
Cada marcador es un círculo naranja (#E67E22) con el número en blanco 
adentro, con borde blanco fino. Tamaño: 40x40 píxeles cada uno.
También genera 5 marcadores más pequeños (25x25) en estos colores:
- Naranja oscuro (#D35400)
- Naranja medio (#E67E22)  
- Naranja claro (#F39C12)
- Gris claro (#95A5A6)
- Verde (#27AE60)

Ponlos todos en una fila sobre fondo blanco.
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
Genera una imagen JPG de la leyenda del mapa, similar a la del mapa 
promocional adjunto. Tamaño: 500x300 píxeles, fondo crema semitransparente.

SECCIÓN 1 — LUGARES (con números naranjas):
1 Ingreso, 2 Boleterías, 3 Chiwiña, 4 Cafetería, 5 Teatro Galpón,
6 Aguas Danzantes, 7 Mirador, 8 Escenario Principal, 9 Anfiteatro,
10 Parrillero, 11 Área de Picnik

SECCIÓN 2 — JUEGOS (con puntos de color):
● Tierras Altas, ● Tierras Medias, ● Tierras Bajas, ● Taypi, ● Macroregiones

SECCIÓN 3 — SERVICIOS (con íconos simples):
Baños, Baño Familiar, Acceso Discapacitados, Posta de Salud, Kioscos,
Parqueo Vehicular, Parqueo Bicicletas

Fuente sans-serif, texto en español. Estilo limpio y legible.
```

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
Genera un archivo HTML completo con Leaflet.js que muestre un mapa 
interactivo del Parque de las Culturas y de la Madre Tierra.

Características:
1. Usa mi imagen "mapa_final.jpg" como overlay sobre OpenStreetMap
2. Centro del mapa: [INSERTAR LAT, LON]
3. Esquinas del overlay:
   - Esquina NW: [lat, lon]
   - Esquina SE: [lat, lon]

4. Marcadores para cada punto de interés con popup:
[PEGAR TABLA DE COORDENADAS AQUÍ]

5. Control de capas para mostrar/ocultar:
   - Mapa ilustrado (overlay)
   - Puntos de interés
   - Servicios

Genera el HTML completo que funcione abriendo el archivo directamente 
en el navegador. La imagen mapa_final.jpg estará en la misma carpeta.
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
