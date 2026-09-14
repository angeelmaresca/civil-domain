# Registro de trabajo

> **Status:** CANONICAL  
> **Editable:** sí; añadir entradas al cerrar bloques materiales  
> **Document owner:** coordinación del dominio civil  
> **Canonical for:** historial resumido del trabajo realizado  
> **Sources:** historial Git y documentos enlazados por cada entrada  
> **Supersedes:** —  
> **Last reviewed:** 2026-09-14

## Regla de registro

Cada entrada debe resumir el objetivo, el resultado observable, los documentos
afectados, las cuestiones que permanecen abiertas, los commits y la siguiente
acción. No debe copiar aquí el razonamiento que pertenece al documento conceptual.

## Entradas

### 2026-09-14 — Ficha individual de Luis (Zapata)

**Objetivo:** preparar la aportación de Luis a la primera iteración a partir de
las entrevistas del 11 y 14 de septiembre.

**Resultado:** se redactó la [ficha de zapata](FICHA_ZAPATA.md), incluyendo identidad,
tipos, geometría, armado, emplazamiento, encepados y elementos profundos separados.
Se incorporaron métodos de análisis manuales, algorítmicos y de elementos finitos,
y una propuesta transversal de comprobaciones y validación técnica trazable.
La ficha permanece `DRAFT`; su publicación no aprueba el modelo de dominio.

**Documentos afectados:** `docs/FICHA_ZAPATA.md`, `docs/WORKING_SET.md` y este registro.

**Cuestiones abiertas:** las propuestas de clasificación, tipos, asignación
geotécnica y validación se contrastarán con el equipo; los detalles pendientes
permanecen en la ficha.

**Validación:** revisión del contenido, enlaces locales y diff sin errores de
espacios; alcance limitado a la ficha de Luis y documentos de coordinación.

**Commit:** commit de `develop` que contiene esta entrada, autorizado por Luis
mediante «súbelos».

**Siguiente acción:** revisar la ficha con Luis y compararla con las demás
aportaciones de la primera iteración.

### 2026-09-09 — Inicio del dominio e investigación BIM

**Objetivo:** preparar un repositorio compartible para conceptualizar gradualmente
el dominio civil y estructural de una planta industrial.

**Resultado:**

- se establecieron las reglas de trabajo, el working set y el crecimiento deliberado
  del repositorio;
- se creó un inventario preliminar de elementos organizado por ocho grupos de
  exploración;
- se abrió como primera tarea la investigación de referencias BIM, estructurales y
  de plantas industriales;
- se redactó el primer estudio didáctico sobre el núcleo conceptual de IFC;
- se preparó el README como introducción y lectura previa suficiente para el equipo.

**Documentos afectados:** `README.md`, `AGENTS.md` y el conjunto documental inicial
contenido en `docs/`.

**Cuestiones abiertas:** revisar con el equipo los conceptos IFC mediante ejemplos de
pipe rack, viga, equipo y zapata; acordar después el reparto de los siguientes
frentes de investigación.

**Commit:** commit inicial de la rama `develop` que contiene esta entrada.

**Siguiente acción:** realizar la primera sesión de contraste y decidir si IFC
necesita una segunda pasada antes de abrir el frente estructural analítico.

### 2026-09-10 — Preparación de la primera iteración del equipo

**Objetivo:** convertir el estudio inicial de IFC en un ejercicio comparable para
Alberto, Luis, Miguel y Ángel antes de la siguiente reunión.

**Resultado:**

- se definió un caso común desde equipo y estructura hasta cimentación y terreno;
- se creó una batería transversal de preguntas sobre realidad física, identidad,
  tipos, jerarquías, geometría, materiales, conexiones, acciones y modelos
  analíticos;
- se delimitaron focos provisionales para conexiones, zapata, cargas y
  correspondencia físico–analítica;
- se añadió un pedestal resuelto como guía del nivel de detalle esperado;
- se generaron copias PDF del README y del estudio de fundamentos IFC.

**Documentos afectados:** `README.md`, `README.pdf`, `docs/WORKING_SET.md`,
`docs/FIRST_ITERATION.md` y `docs/research/IFC_CORE_CONCEPTS.pdf`.

**Cuestiones abiertas:** contrastar las cuatro fichas, precisar el alcance de cada
frente y decidir qué conceptos requieren investigación adicional.

**Commit:** commit de la rama `develop` que contiene esta entrada.

**Siguiente acción:** preparar las fichas individuales y utilizarlas como entrada de
la próxima reunión, sin diseñar todavía tablas o clases definitivas.

### 2026-09-11 — Ficha individual de Miguel (Acciones y cargas)

**Objetivo:** construir, pregunta a pregunta, la ficha individual del foco
"Acciones y cargas" a partir del ejemplo de un depósito (`EQ-101`) apoyado
sobre la estructura soporte.

**Resultado:**

- se recorrió la batería común aplicada al ejemplo (bloques A, E y F, más
  la pregunta específica de sistema de coordenadas y convenio de signos);
- se fijó la separación entre objeto físico, Acción, agrupación (caso de
  carga) y aplicación analítica, evitando guardar la carga como propiedad
  de un elemento físico;
- se identificaron dos representaciones analíticas alternativas (nodo vs.
  barra) para la misma acción física;
- se registraron 5 conceptos candidatos, 3 dudas para la reunión y un
  ejemplo de simplificación válida frente a un diseño frágil;
- se creó `FICHA_ACCIONES_CARGAS.md` y se incorporó al alcance editable de
  `WORKING_SET.md`.

**Documentos afectados:** `docs/FICHA_ACCIONES_CARGAS.md` (nuevo),
`docs/WORKING_SET.md`.

**Cuestiones abiertas:** las 3 dudas recogidas en la ficha (cambio de TAG
ante revisiones de diseño, dónde vive el convenio de signos, cuándo
ampliar el alcance de un apoyo individual al reparto entre varios apoyos).

**Commit:** commit de la rama `develop` que contiene esta entrada.

**Siguiente acción:** contrastar esta ficha con las de Alberto, Luis y
Ángel en la próxima reunión, según `FIRST_ITERATION.md` sección 7.
