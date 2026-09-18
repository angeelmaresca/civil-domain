# Respuestas razonadas — Civil Domain

> **Status:** DRAFT
> **Editable:** sí; material didáctico derivado incluido en `WORKING_SET.md`
> **Document owner:** coordinación del dominio civil
> **Canonical for:** —
> **Sources:** [guía](STUDY_GUIDE.md), [fundamentos IFC](../research/IFC_CORE_CONCEPTS.md), [síntesis](../iteration-01/SINTESIS.md) y fichas de la primera iteración
> **Supersedes:** —
> **Last reviewed:** 2026-09-17

## Regla de lectura

Las respuestas muestran un razonamiento posible. No aprueban entidades ni cierran
las preguntas que el equipo debe revisar.

## Bloque A

### 1. C-101

- identidad interna: clave estable del objeto en nuestro dominio;
- TAG/código: etiqueta visible o externa, potencialmente revisable;
- ocurrencia: la columna física concreta C-101;
- tipo: definición reutilizable de perfil/material/reglas, si realmente se comparte;
- clasificación: códigos IFC, bSDD o corporativos asociados;
- propiedades: longitud, fase, resistencia, acabado u otros datos de ocurrencia o tipo.

### 2. Continuidad de identidad

Cambiar perfil durante una revisión de diseño puede conservar la ocurrencia si sigue
representando la misma columna funcional. Sustituirla por otra columna construida en
una intervención posterior puede justificar nueva identidad. La decisión depende del
lifecycle, no solo de que cambie un valor.

### 3. Zapata y sólido

El sólido describe forma y material, pero no función, identidad, contacto con
terreno, relación con la estructura, armadura, lifecycle ni modelos analíticos. Dos
sólidos iguales podrían cumplir funciones distintas.

### 4. Cuatro planos geométricos

Placement sitúa F-101 en coordenadas del proyecto. La geometría editable contiene
dimensiones de intención. La calculada puede incluir chaflanes, canto resultante o
armadura. La representación de intercambio traduce una de ellas a IFC, DWG u otro
formato con posible pérdida.

### 5. Copiar IFC

Importaría complejidad de intercambio, herencia y compatibilidad que puede no
responder a nuestro lenguaje ni lifecycle. IFC sirve para descubrir separaciones;
las clases propias requieren casos funcionales.

## Bloque B

### 6. Relaciones ocultas

Son posibles ownership del modelo, contención espacial, pertenencia a estructura o
sistema, composición placa-pernos, conexión columna-placa, contacto grout-pedestal,
apoyo pedestal-zapata, interfaz zapata-terreno y transmisión de acciones. La línea
vertical por sí sola no elige una.

### 7. Área, sistema y apoyo

Área responde a ubicación, ST-01 a pertenencia funcional y BP-101 a conexión/apoyo.
Ownership responde a quién controla creación, sustitución y borrado. Pueden coincidir
en una aplicación, pero no por significado.

### 8. Conexión rica

Una referencia puede bastar si solo necesitamos conocer extremos. Si debemos guardar
posición, superficie, rigidez, holgura, capacidad, componentes, estado o revisión, la
relación necesita un modelo explícito. La entidad exacta sigue pendiente del frente
de conexiones.

### 9. Varios sistemas

Una viga puede pertenecer al sistema resistente de un pipe rack y al sistema de
soporte de una línea. Ninguno tiene por qué poseerla ni componerla físicamente.

### 10. Parent universal

Forzaría cardinalidad y borrado comunes para relaciones que no los comparten. También
haría imposible expresar varios sistemas, dos endpoints, mappings N:M o conexiones
con datos propios sin excepciones.

## Bloque C

### 11. Dos modelos de C-101

Modelo global: una barra con eje local, offsets y releases. Modelo local: superficies
o sólidos con contactos. Perfil, material físico, placement e identidad permanecen
en C-101; nodos, malla, releases y condiciones de contorno pertenecen a cada modelo.

### 12. Cardinalidades

Uno a varios: una columna física representada por dos barras y un nodo rígido.
Varios a uno: varios componentes físicos simplificados como una única barra o masa
equivalente en un análisis global.

### 13. ID de STAAD

Depende de una herramienta, fichero y revisión. Puede cambiar al regenerar el modelo
y puede haber varios modelos simultáneos. Debe conservarse como identidad externa en
un mapping, no reemplazar la identidad física.

### 14. Tres evaluaciones

Relación histórica indica qué snapshot originó el modelo. Alineación técnica evalúa
si sigue correspondiendo al físico actual. Aprobación humana declara que una persona
aceptó su uso para un propósito. Ninguna implica automáticamente las otras.

## Bloque D

### 15. Secuencia de cargas

`Action` representa el fenómeno o acción con procedencia. `LoadCase` agrupa una
hipótesis. `AppliedLoad` proyecta la acción sobre un objeto analítico. `Combination`
combina casos; el análisis produce `Result`; `Envelope` selecciona extremos relevantes
y `Check` evalúa un criterio usando esos resultados. La secuencia real puede variar,
pero los significados no deben colapsarse.

### 16. Dos aplicaciones

Puede mantenerse origen, magnitud física y propósito. Cambian objeto analítico,
distribución espacial, transformación de coordenadas y quizá nivel de aproximación.
Ambas aplicaciones deben poder remontarse a la misma acción.

### 17. Fx = 120 kN

Como mínimo: unidad, sistema de coordenadas, convenio de signos, punto o región de
aplicación, caso/hipótesis, origen, revisión y si es valor característico, de cálculo
o resultado. Sin contexto, el número es ambiguo.

### 18. Carga fija en zapata

Las cargas varían por caso, revisión, modelo y combinación; pueden proceder de varios
objetos. Guardarlas como propiedades fijas mezcla fuente, aplicación y derivado con
el objeto físico.

## Bloque E

### 19. Diseño frágil

El código compuesto mezcla identidad con clasificación, material y ubicación;
`parentID` no declara la relación; `importedMesh` confunde objeto con representación;
`loadN` fija una acción variable; `sapNodeID` liga el físico a una idealización;
`valid` mezcla vigencia, traducción, convergencia y aprobación.

### 20. Mapa de pedestal

Debe parecerse al ejemplo resuelto del
[enunciado](../iteration-01/ENUNCIADO.md#6-ejemplo-resuelto--pedestal-pd-ex-01): una
identidad física, definición/tipo provisional, placement, representación paramétrica
y detallada, hormigón y armadura, apoyo inferior e interfaz superior, y mappings
separados a modelos global y local.

### 21. Grado de certeza

Las fichas convergen en que un físico puede tener varios analíticos y que las cargas
requieren procedencia y marco. «Toda conexión es entidad», «TAG universal» e «IFC
como jerarquía interna» no están apoyadas; las dos últimas contradicen el enfoque
del repositorio.

### 22. Preguntas para conexiones

Ejemplos: qué distingue contacto, apoyo, anclaje y conexión; cuándo la interfaz tiene
identidad; cómo localizarla; qué propiedades pertenecen a la relación; cómo mapea a
conexiones analíticas; cómo se revisa sin sustituir sus extremos.

### 23. Simplificación válida

Una aplicación puede conservar una geometría paramétrica única y generar el sólido
detallado, siempre que documente que no representa todas las geometrías posibles y
que la identidad no depende de ese formato.

## Bloque F

### 24. ElementSelectionSet

Es una selección operacional persistente. Puede solaparse, no posee placement ni
transmite cargas y su borrado no elimina miembros. Llamarlo assembly o sistema
añadiría semántica física inexistente.

### 25. Parent frente a interfaz rica

El parent ordinario expresa un receptor físico `0..1`. Una interfaz con rigidez,
geometría, reparto N:M o estado tiene datos y cardinalidad propios y no debería
reducirse a esa FK.

### 26. General y local

Civil Domain puede estudiar el significado general de interfaz física y mapping
físico–analítico. Footings puede decidir localmente políticas como atomicidad de una
traslación en lote o qué subtipos participan en un reporte concreto.

## Autoevaluación final

Puedes considerar completado este bloque si eres capaz de explicar:

1. ocurrencia, tipo, clasificación y propiedad sin usar sinónimos;
2. por qué el dominio civil necesita grafos y no una única jerarquía;
3. cómo un físico conserva identidad con varios analíticos;
4. el recorrido desde acción hasta check;
5. por qué procedencia, vigencia y aprobación son dimensiones distintas.
