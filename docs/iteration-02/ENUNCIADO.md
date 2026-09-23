# Segunda iteración — reflexión sobre la ocurrencia de diseño

> **Status:** DRAFT
> **Editable:** sí mientras figure como documento activo en `WORKING_SET.md`
> **Document owner:** equipo de dominio civil
> **Canonical for:** —
> **Sources:** [`OcurrenciaDeDiseño`](../domain-objects/DESIGN_OCCURRENCE.md), [síntesis de la primera iteración](../iteration-01/SINTESIS.md), [estudio IFC](../research/IFC_CORE_CONCEPTS.md), documentación oficial IFC 4.3.2.0 enlazada en este documento y conversación del equipo del 2026-09-18
> **Supersedes:** —
> **Last reviewed:** 2026-09-23

## 1. Propósito de esta iteración

Este documento conserva las conclusiones provisionales alcanzadas al comenzar a
definir `OcurrenciaDeDiseño` y las compara expresamente con IFC. No plantea un
ejercicio individual ni exige devolver una ficha. Su finalidad es que la próxima
sesión pueda revisar la propuesta sin olvidar separaciones que IFC ya ha tenido que
resolver y sin copiar decisiones de IFC que respondan solo al intercambio.

La definición extensa de la entidad continúa teniendo una única fuente propietaria:
[`DESIGN_OCCURRENCE.md`](../domain-objects/DESIGN_OCCURRENCE.md). Aquí se documentan
el razonamiento comparativo, los riesgos de desalineación y las cuestiones que
podrían obligar a ajustar esa definición.

## 2. Reflexión de partida

Conviene comenzar el modelo por `OcurrenciaDeDiseño` porque columna, zapata y equipo
necesitan una identidad estable mientras cambian sus datos y representaciones. No
conviene convertirla en una raíz universal de todo el CDM.

La hipótesis actual restringe el concepto a un **individuo físico proyectado**:

- existe como intención concreta del proyecto, aunque aún no esté construido;
- conserva identidad a través de varios estados de diseño;
- no se identifica mediante TAG, código externo, geometría o posición;
- puede estar compuesto por otras ocurrencias o relacionarse con ellas;
- puede tener varias representaciones físicas y analíticas;
- no equivale a la pieza fabricada ni al activo instalado.

Esta decisión es útil porque delimita el problema demostrado por las fichas, pero
también crea una diferencia terminológica respecto de IFC: IFC utiliza «occurrence»
para muchas cosas que no son individuos físicos. Esa diferencia debe ser consciente,
documentada y revisable.

## 3. Qué hace realmente IFC

### 3.1. `IfcObject` no significa «objeto físico»

El núcleo de IFC separa definiciones de objetos, propiedades y relaciones:

```text
IfcRoot
├── IfcObjectDefinition
│   ├── IfcContext
│   ├── IfcObject                 ocurrencias en sentido IFC
│   │   ├── IfcProduct
│   │   ├── IfcGroup
│   │   ├── IfcProcess
│   │   ├── IfcControl
│   │   ├── IfcResource
│   │   └── IfcActor
│   └── IfcTypeObject             definiciones comunes de tipo
├── IfcPropertyDefinition
└── IfcRelationship
```

[`IfcObjectDefinition`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcObjectDefinition.htm)
abarca una cosa o proceso tratado semánticamente, como tipo o como ocurrencia.
[`IfcObject`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcObject.htm)
es la rama de ocurrencias e incluye productos, grupos, procesos, controles, recursos
y actores. IFC considera ocurrencias tanto una viga como un espacio, una retícula,
una tarea, un coste o una persona.

**Consecuencia para el CDM:** `OcurrenciaDeDiseño` no es equivalente a `IfcObject`.
Es una especialización conceptual mucho más estrecha. Si el CDM necesita en el
futuro una raíz común para objetos físicos, sistemas, procesos o actores, deberá
justificarse por casos propios; no debe llamarse automáticamente
`OcurrenciaDeDiseño` por imitación de IFC.

### 3.2. `IfcProduct` tampoco es sinónimo de producto físico

[`IfcProduct`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcProduct.htm)
representa cualquier objeto relacionado con un contexto geométrico o espacial. Bajo
esa rama aparecen elementos físicos, elementos espaciales y también objetos no
físicos como retículas, puertos, anotaciones, acciones estructurales y objetos de
análisis.

Placement y representación son opcionales. Un producto puede existir semánticamente
antes de disponer de geometría, y un mismo producto puede tener distintas
representaciones.

**Consecuencia para el CDM:** ser ubicable o representable no basta para ser una
ocurrencia física. El adaptador IFC deberá inspeccionar el significado del subtipo y
el contexto, no mapear todo `IfcProduct` a `OcurrenciaDeDiseño`.

### 3.3. IFC separa ocurrencia y tipo

[`IfcTypeObject`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcTypeObject.htm)
conserva información común a varias ocurrencias. `IfcRelDefinesByType` asigna el
tipo y una propiedad declarada específicamente en la ocurrencia puede prevalecer
sobre la propiedad común del tipo.

Esta separación apoya que:

- `C-101` y un perfil o tipo de columna no sean el mismo objeto;
- dos zapatas iguales no compartan necesariamente un tipo intencional;
- un tipo pueda existir antes de tener ocurrencias asignadas;
- clasificación externa, tipo declarado y agrupación derivada por similitud sigan
  siendo conceptos distintos.

**Punto que el CDM debe resolver:** IFC asigna normalmente un tipo a la ocurrencia,
pero nuestro tipo de zapata puede cambiar entre estados sin cambiar la identidad.
Debemos decidir si el tipado pertenece a `OcurrenciaDeDiseño`, a `EstadoDeDiseño` o
a una relación con vigencia. No conviene copiar la cardinalidad de IFC antes de
resolver el modelo temporal propio.

### 3.4. Assembly físico y sistema funcional son patrones diferentes

[`IfcElementAssembly`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcElementAssembly.htm)
representa un conjunto físico complejo agregado a partir de elementos. Puede tener
identidad y placement propios; su geometría puede derivarse de sus componentes y no
necesita duplicarse. IFC cita cerchas y pórticos como ejemplos de assemblies.

[`IfcGroup`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcGroup.htm)
es, en cambio, una colección lógica sin placement ni forma propios. Un objeto puede
pertenecer a cero, uno o varios grupos; la membresía no tiene que ser jerárquica y
no implica dependencia. [`IfcSystem`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcSystem.htm)
especializa ese patrón para una combinación funcional de productos que persiguen
un propósito común.

**Consecuencia para `ST-01`:** hay al menos dos lecturas válidas que no deben
colapsarse:

```text
ST-01-FIS    conjunto físico con identidad y partes
SYS-ST-01    agrupación funcional de elementos resistentes
```

Puede bastar una de ellas o pueden ser necesarias ambas. Que compartan nombre en el
lenguaje cotidiano no demuestra que compartan identidad, geometría, lifecycle ni
cardinalidades.

### 3.5. Composición y agrupación tienen consecuencias distintas

En IFC, `IfcRelAggregates` expresa una relación todo–parte no ordenada con
dependencia. El modelo general restringe una parte a una única descomposición
principal para mantener una estructura jerárquica. La asignación a grupos no tiene
esa dependencia y admite pertenencia múltiple.

**Lección útil:** no representar composición, sistema, conexión, apoyo y localización
con un único `parent`.

**Precaución:** la restricción IFC de una sola descomposición principal sirve a su
estructura de intercambio, pero no se adopta automáticamente en el CDM. Debemos
probar cimentaciones, assemblies compartidos, conexiones y módulos antes de decidir
si nuestra composición física necesita la misma cardinalidad.

### 3.6. La estructura espacial forma otra jerarquía

El concepto IFC de
[`Spatial Structure`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/concepts/Object_Connectivity/Spatial_Structure/content.html)
crea una jerarquía de emplazamiento —por ejemplo sitio, instalación, planta o
espacio— distinta de la composición del producto. Un elemento físico tiene un
contenedor espacial principal, aunque puede referenciar otros contextos espaciales.

**Consecuencia para el CDM:** área, unidad, nivel o instalación no deben convertirse
en el padre físico de una columna solo porque sirven para localizarla. Tampoco debe
deducirse que toda «estructura» nombrada por una aplicación sea un contenedor
espacial.

### 3.7. El modelo analítico es una ocurrencia IFC, pero no un producto físico

[`IfcStructuralAnalysisModel`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcStructuralAnalysisModel.htm)
es subtipo de `IfcSystem`. Agrupa miembros y conexiones estructurales, referencia
cargas y resultados y establece un placement compartido para la topología del
modelo. IFC permite además componer modelos analíticos parciales.

[`IfcStructuralItem`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcStructuralItem.htm)
representa miembros y conexiones analíticos, es decir, idealizaciones de elementos
del modelo construido. IFC admite una relación explícita entre el elemento físico y
su idealización analítica.

**Consecuencia para el CDM:** una barra, placa o nodo analítico puede tener identidad
dentro de su modelo y revisión, pero no es una `OcurrenciaDeDiseño` física. Debemos
mantener `ModeloAnalitico`, `ObjetoAnalitico` y la correspondencia físico–analítica
como conceptos separados.

Existe además una diferencia deliberada: Luis ha descrito cálculos manuales y
formulaciones algorítmicas sin malla. Por ello el CDM no puede exigir que todo
análisis adopte la topología de `IfcStructuralAnalysisModel`.

### 3.8. IFC da identidad a las relaciones

[`IfcRelationship`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcRelationship.htm)
es una rama propia de `IfcRoot`. IFC objetiva relaciones de tipado, agregación,
asignación, asociación, conexión y contención en lugar de esconder toda la semántica
en atributos de los extremos.

**Consecuencia para el CDM:** una relación con vigencia, evidencia, geometría,
transformación, autoridad o propiedades propias no debe reducirse a un ID desnudo.
Esto no obliga a copiar una clase IFC por relación, pero sí a conservar el significado
que se perdería con `parentId` o `relatedIds`.

## 4. Correspondencias y diferencias deliberadas

| Tema | Patrón IFC | Propuesta actual del CDM | Riesgo que vigilar |
|---|---|---|---|
| Ocurrencia | `IfcObject` cubre objetos físicos y no físicos, procesos, actores y grupos. | `OcurrenciaDeDiseño` se limita provisionalmente al individuo físico proyectado. | Creer que ambos términos son equivalentes. |
| Producto | `IfcProduct` reúne todo lo situado o representable, no solo lo material. | La condición física se decide por significado del dominio. | Importar como físico cualquier `IfcProduct`. |
| Tipo | `IfcTypeObject` aporta información común a ocurrencias. | Tipo intencional separado de clasificación y similitud calculada. | Fijar el tipo a la identidad cuando puede variar por estado. |
| Conjunto físico | `IfcElementAssembly` se compone de elementos. | Una estructura física puede ser una ocurrencia compuesta. | Crear un assembly para cualquier agrupación visible. |
| Sistema | `IfcSystem` es una agrupación funcional. | `SistemaFuncional` separado del conjunto físico. | Usar sistema como propietario de sus miembros. |
| Espacio | Jerarquía espacial y contención principal. | `ContextoEspacial` separado de composición y sistema. | Confundir ubicación con pertenencia física. |
| Analítico | Modelo como sistema; items como idealizaciones. | Modelo, objetos, ejecución y correspondencia separados del físico. | Tratar barra y columna como el mismo objeto o exigir malla a todo cálculo. |
| Relaciones | Relaciones objetivadas y tipadas. | Relaciones semánticas con contexto cuando aporte valor. | Copiar toda la taxonomía IFC o reducir todo a referencias genéricas. |
| Revisión | IFC conserva identidad e historial de intercambio, pero no define nuestro proceso de aceptación longitudinal. | Estados de diseño aceptados, snapshots de fuente y decisiones separados. | Suponer que GUID o última exportación resuelven identidad y autoridad. |

## 5. Qué significa «estructura» en esta reflexión

La palabra no identifica una entidad única:

| Uso | Naturaleza propuesta | ¿`OcurrenciaDeDiseño`? | Patrón IFC orientativo |
|---|---|---|---|
| Estructura soporte física `ST-01-FIS` | Todo físico compuesto con identidad propia | Sí, si supera la prueba de continuidad y utilidad | Producto agregado / assembly |
| Sistema resistente `SYS-ST-01` | Agrupación funcional | No | `IfcSystem` / `IfcGroup` |
| Área, módulo o instalación espacial | Contexto espacial | No por ser espacio | `IfcSpatialElement` / facility part |
| Modelo estructural `AM-01` | Modelo analítico con hipótesis y revisión propias | No | `IfcStructuralAnalysisModel` |
| Pipe rack tipo `TYPE-ST-A` | Definición reutilizable | No | `IfcTypeObject` o clasificación, según significado |

La decisión pendiente no es elegir una fila para todos los usos, sino comprobar qué
filas existen realmente en el CDM y cómo se relacionan sin duplicar identidad.

## 6. Aspectos en los que podríamos estar desalineándonos sin querer

1. **Usar «ocurrencia» con un alcance distinto sin hacerlo explícito.** Es válido
   restringirla a lo físico, pero los adaptadores y la documentación deben conocer
   la diferencia respecto de IFC.
2. **Buscar una única raíz demasiado pronto.** Que IFC tenga `IfcObject` no obliga
   a crear ahora `DomainObject` o `DomainOccurrence`. Solo debe aparecer si varios
   conceptos propios necesitan de verdad las mismas reglas.
3. **Confundir `IfcProduct` con materialidad.** Espacios, retículas y objetos
   analíticos también pueden ser productos IFC.
4. **Convertir todo conjunto en una ocurrencia física.** Un grupo de consulta o un
   sistema funcional no adquiere cuerpo, placement o lifecycle de assembly.
5. **Copiar cardinalidades de intercambio.** La descomposición única o el tipo único
   de IFC pueden no cubrir estados históricos y relaciones temporales del CDM.
6. **Confiar en el GUID como identidad empresarial.** Un identificador IFC identifica
   una instancia intercambiada; no demuestra por sí solo continuidad entre fuentes,
   revisiones o reconstrucciones independientes.
7. **Usar el último modelo como verdad.** El CDM necesita separar snapshot, estado
   aceptado, autoridad y decisión de baja.
8. **Forzar todo análisis al patrón de elementos finitos.** IFC describe muy bien
   topologías analíticas; el CDM también debe admitir formulaciones sin nodos,
   barras o placas.
9. **Copiar entidades IFC como clases internas.** IFC es evidencia y contrato de
   intercambio; las fronteras del CDM deben proceder de responsabilidades y casos
   propios.

## 7. Puntos a investigar en la próxima sesión

Estas preguntas son una agenda de conversación, no una ficha que deba entregarse:

### Alcance de ocurrencia

- ¿Queremos mantener `OcurrenciaDeDiseño` como término explícitamente físico o sería
  más claro llamarla `OcurrenciaFisicaDeDiseño`?
- ¿Necesitamos una abstracción superior para sistemas, espacios, modelos o procesos,
  o todavía no existe un comportamiento común que la justifique?
- ¿Qué ejemplos no físicos necesitan identidad y lifecycle propios en el CDM?

### Estructura física y sistema

- ¿`ST-01` tiene continuidad propia cuando se sustituye una columna o solo es el
  nombre de una agrupación funcional?
- ¿Necesitamos simultáneamente `ST-01-FIS` y `SYS-ST-01`? Si existen ambos, ¿qué
  relación los conecta y quién gobierna cada uno?
- ¿La cimentación compone la estructura física, la apoya, pertenece al mismo sistema
  resistente o depende del contexto de uso?

### Partes y granularidad

- ¿Qué distingue una ocurrencia hija de un detalle descrito dentro del estado del
  padre?
- ¿Pernos, barras de armadura, insertos y capas necesitan identidad siempre o solo
  cuando existe fabricación, montaje, inspección o sustitución individual?
- ¿Puede una ocurrencia ser parte física de dos todos simultáneamente o ese caso
  revela que una relación es realmente sistema, conexión o apoyo?

### Estado, tipo y tiempo

- ¿El tipo se asigna a la ocurrencia completa o a cada estado de diseño?
- ¿Cómo representamos que la composición, pertenencia o ubicación cambian sin borrar
  la relación anterior?
- ¿Qué constituye continuidad tras traslado, desmontaje, división, fusión o
  reconstrucción?

### Interoperabilidad IFC

- ¿Qué subtipos IFC se mapearían normalmente a ocurrencias físicas y cuáles deben
  excluirse explícitamente?
- ¿Cómo conservamos el `GlobalId` IFC como referencia de fuente sin convertirlo en
  el ID interno del CDM?
- ¿Cómo representamos mappings `1:1`, `1:N`, `N:1` y ambiguos entre IFC, otros
  modelos físicos y modelos analíticos?
- ¿Qué restricciones IFC queremos adoptar como invariantes propios y cuáles solo
  deben validarse en el adaptador de exportación?

## 8. Criterios que podrían obligar a ajustar la definición

La definición actual debe revisarse si aparece alguno de estos resultados:

- un concepto no físico necesita las mismas reglas de continuidad, estado y baja;
- no podemos representar una estructura sin duplicar identidad entre todo físico y
  sistema funcional;
- el tipo no puede cambiar de forma trazable entre estados;
- una parte relevante necesita múltiples composiciones físicas simultáneas;
- el modelo no permite reconstruir por qué dos fuentes se conciliaron o separaron;
- un intercambio IFC válido no puede mapearse sin afirmar identidades falsas;
- los cálculos sin topología quedan forzados artificialmente a objetos analíticos
  discretos.

Si ocurre alguno, primero se corrige la frontera conceptual y después, si hace
falta, se incorpora otra entidad. No se amplía `OcurrenciaDeDiseño` únicamente para
evitar crear un concepto nuevo.

## 9. Estructura documental durante la iteración

La estructura actual sigue siendo suficiente:

```text
docs/
├── domain-objects/       una fuente propietaria por objeto del dominio
├── iteration-01/         evidencia y síntesis de la ronda anterior
├── iteration-02/         reflexión y agenda activa
├── research/             estudios de referencias externas
├── study/                material didáctico derivado
├── VOCABULARY.md         índice de términos
├── RELATIONSHIPS.md      semántica de relaciones
├── RULES.md              invariantes candidatos
├── WORKING_SET.md        estado operativo
└── WORK_LOG.md            historial de bloques cerrados
```

No se crean por ahora carpetas independientes para relaciones, reglas, decisiones,
fuentes o esquemas. Se revisará esta decisión cuando exista un artefacto concreto
que ya no encaje con claridad, no para anticipar una estructura vacía.

## 10. Resultado buscado de la próxima sesión

No se espera una ficha. Se busca una revisión conjunta que deje explícito:

- qué partes de la definición actual se sostienen;
- qué diferencias respecto de IFC son deliberadas;
- qué riesgo de interoperabilidad necesita una regla o prueba adicional;
- qué preguntas permanecen abiertas y quién puede aportar evidencia;
- si procede ajustar `OcurrenciaDeDiseño`, `RELATIONSHIPS.md`, `RULES.md` o
  `VOCABULARY.md`.

Mientras no exista ese contraste, todas las conclusiones conceptuales permanecen
`DRAFT`.

## 11. Sesión del 23 de septiembre: conjuntos y versiones

**Fuente:** conversación de trabajo con Luis. Sus respuestas se conservan como
aportación `DRAFT` para contraste, no como aprobación canónica del equipo.

### Identidad, alcance y códigos

- ST-01 conserva identidad aunque se cambien o sustituyan componentes. Habitualmente
  designa solo la estructura metálica; su cimentación puede llamarse FDN-ST-01.
  Tiene ubicación y función resistente, generalmente soportar tuberías y transmitir
  cargas a cimentación; esto no obliga a crear tres entidades distintas.
- Los equipos sobre estructuras tienen TAG propios y la estructura no hereda el
  del equipo. Para un equipo apoyado a suelo aparece, por ejemplo, FDN-V-005 como
  cimentación de V-005. Son prácticas de denominación, no reglas de identidad.
- El TAG suele llevar prefijo de unidad, como 210-ST-01. La unidad puede delimitar
  zona o proceso; en una zona pueden coexistir TAG de distintas unidades.
- Piping define módulos como PR-05-M03 y puede cambiar sus alineaciones durante el
  diseño. Si un pórtico pasa de M03 a M02, los módulos pueden conservar identidad.
  Si el cambio hace desaparecer un módulo, se elimina y puede sustituirse por otro.
  Los TAG se reutilizan. La magnitud del cambio orienta el juicio; no se fijó umbral
  ni responsable de decidir continuidad.
- Luis no da por resuelta la identidad del pórtico y sus piezas trasladadas: en
  STAAD puede necesitar eliminar y crear objetos, cargas y parámetros de diseño de
  acero; prevé algo similar en generación automática de maqueta. Para este caso
  **basta conservar versiones completas anteriores de los modelos**, sin vínculo
  histórico pieza a pieza. No se establece que toda recreación analítica deba crear
  obligatoriamente una nueva identidad física.

### Pipe rack y modularización

En oferta o FEED, PR-05 puede ser continuo. Al modularizarse, **PR-05 sigue siendo
el mismo objeto de proyecto y los módulos pasan a formar parte de él**. Como
conjunto, PR-05 incluye sus cimentaciones. Esto no amplía automáticamente el alcance
habitual de ST-01 ni determina el alcance de cada módulo.

Los módulos y sus cimentaciones pueden llevar versiones independientes. Actualmente
no se necesita identificar una configuración global como «M01 v03, M02 v07, M03
v02»; podría interesar en el futuro. Sí se prevén consultas de cantidades o ratios
del PR-05, por ejemplo m³ o kg de acero por volumen. Magnitudes, denominadores y
reglas de agregación no se han definido todavía.

### Versiones y dependencias de cargas

Luis precisa que **versión** describe los estados sucesivos del diseño. Reserva
**revisión documental** para emisiones oficiales al cliente, relacionadas con
estados como IFR o IFC. Las respuestas previas utilizaban ambas palabras
indistintamente. Aquí IFC como estado de emisión no significa formato de intercambio.

Se versiona el conjunto completo de estructura o cimentación, no cada columna,
viga o zapata independientemente. Sus interacciones y el plano o memoria del conjunto
motivan este criterio. Aunque las zapatas no cambien geométricamente, pueden responder
a una nueva versión de cargas y pertenecer a una nueva versión del conjunto.

Estructura y cimentación tienen ciclos independientes. Un cambio de estructura
normalmente afecta a cimentación, pero puede aceptarse sin modificarla si el impacto
es pequeño. Un descentramiento de zapata por una tubería o la incorporación de SPSs
son ejemplos aportados de cambios de cimentación que no obligan a cambiar estructura.
No se desarrolló el significado de SPSs ni se afirma que cualquier cambio de
cimentación carezca de impacto estructural.

**Práctica actual:** la aceptación sin cambio de cimentación no suele registrarse.
**Necesidad expresada por Luis:** debe registrarse y cada receptor debe referirse a
la versión concreta que proporciona sus cargas. Cimentación v05 puede estar referida
o aceptada frente a estructura v06. Esto se extiende a todos los elementos receptores.

El diseño estaría completo si sus últimas versiones tienen resueltas esas referencias,
por actualización o aceptación sin cambios. Equipo v02, estructura ST-04 v05 y
cimentación v06 pueden ser coherentes: no se exige igualar números. Esta condición
de dependencias no sustituye las comprobaciones ni la aprobación técnica.

**Propuesta del asistente por concretar:** distinguir la versión efectivamente
utilizada para obtener cargas de la aceptación posterior frente a otra versión,
conservando ambas referencias. No se decidió dónde vive esa aceptación, sus datos
mínimos, su autoridad ni si crea una versión o un registro separado.

### Pendientes para el equipo

1. **Aplazado expresamente por Luis:** si PR-05-M03 incluye su cimentación o identifica
   solo estructura metálica y la cimentación es otro conjunto dentro de PR-05.
2. **Pregunta sin responder:** si una cimentación puede apoyar varios módulos o
   estructuras y cómo se identifica y organiza en ese caso.
3. Quién decide continuidad o sustitución al remodular y con qué criterio.
4. Cómo representar estados de piezas dentro de versiones del conjunto sin imponer
   ciclos de versiones independientes por pieza.
5. Cómo registrar aceptación sin cambios y conservar las referencias de cargas;
   relación entre versiones técnicas y emisiones documentales.
6. Cuándo será necesaria una configuración global y cómo agregar cantidades sin
   mezclar versiones ni contar dos veces componentes compartidos.

Consecuencias candidatas en [ocurrencia](../domain-objects/DESIGN_OCCURRENCE.md),
[relaciones](../RELATIONSHIPS.md) y [reglas](../RULES.md). Esta sección es la evidencia
propietaria de la conversación; no se crean nuevas familias documentales.
