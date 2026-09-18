# Cuaderno de estudio — Civil Domain

> **Status:** DRAFT
> **Editable:** sí; material didáctico derivado incluido en `WORKING_SET.md`
> **Document owner:** coordinación del dominio civil
> **Canonical for:** —
> **Sources:** [guía de estudio](STUDY_GUIDE.md) y fuentes enlazadas en ella
> **Supersedes:** —
> **Last reviewed:** 2026-09-17

## Instrucciones

Resuelve primero sin consultar el repositorio. Los ejercicios abiertos no buscan una
única clase correcta: deben hacer visibles conceptos, relaciones y dudas.

## Bloque A — Conceptos básicos

1. Para `C-101`, separa identidad interna, TAG, ocurrencia, tipo, clasificación y
   propiedades.
2. Da un ejemplo de cambio que conserve la identidad de C-101 y otro que
   razonablemente produzca una nueva ocurrencia.
3. Explica por qué «zapata = sólido de hormigón» es una definición insuficiente.
4. Distingue placement, geometría editable, geometría calculada y representación de
   intercambio con un ejemplo de F-101.
5. ¿Qué problema aparece si se crea una clase interna por cada entidad IFC que
   encontramos?

## Bloque B — Relaciones

6. En el caso EQ-101 → terreno, identifica al menos cinco relaciones distintas que
   el diagrama vertical podría estar ocultando.
7. La columna C-101 está en el área A-10, pertenece a ST-01 y apoya mediante BP-101.
   Explica por qué ninguna de esas frases implica automáticamente ownership.
8. ¿Cuándo bastaría una referencia entre dos objetos y cuándo la conexión podría
   necesitar datos o identidad propia?
9. Propón un ejemplo donde un objeto pertenezca a dos sistemas funcionales sin estar
   compuesto por ellos.
10. Explica por qué un único `parentID` universal haría frágil el modelo.

## Bloque C — Físico y analítico

11. Representa C-101 mediante dos modelos analíticos alternativos. Señala qué datos
    pertenecen a cada modelo y cuáles permanecen en la columna física.
12. Da un caso de mapping uno a varios y otro de varios a uno.
13. ¿Por qué `staadMemberID` no debería ser la identidad principal del elemento
    físico?
14. Distingue relación histórica, alineación técnica y aprobación humana de un
    modelo importado.

## Bloque D — Acciones y resultados

15. Ordena y explica: `Action`, `AppliedLoad`, `LoadCase`, `Combination`, `Envelope`,
    `Result` y `Check`.
16. Una reacción de EQ-101 se aplica a un nodo en STAAD y a una superficie en un
    modelo local. ¿Qué permanece igual y qué cambia?
17. Enumera la información mínima necesaria para interpretar correctamente
    `Fx = 120 kN`.
18. Explica por qué una carga no debería guardarse como propiedad fija de la zapata.

## Bloque E — Caso transversal

19. Analiza este diseño y encuentra al menos seis mezclas conceptuales:

```text
FoundationObject
- code = "F-101-C30-AREA10"
- parentID = "ST-01"
- geometry = importedMesh
- loadN = 1200
- sapNodeID = 448
- valid = true
```

20. Dibuja un mapa para PD-101 que incluya objeto físico, tipo, placement, dos
    representaciones geométricas, materiales, dos relaciones físicas, un modelo
    analítico global y otro local.
21. Decide qué afirmaciones son convergencias `DRAFT` y cuáles serían todavía mera
    especulación:
    - un físico puede tener varios analíticos;
    - toda conexión debe ser entidad;
    - el TAG es la identidad universal;
    - las cargas necesitan procedencia y marco de coordenadas;
    - IFC debe ser nuestra jerarquía interna.
22. Escribe tres preguntas que deberían discutirse cuando llegue la ficha de
    conexiones de Alberto.
23. Elige una simplificación válida para una primera aplicación especializada y
    explica qué límite debe documentarse para no bloquear el dominio futuro.

## Bloque F — Puente con Footings

24. Clasifica `ElementSelectionSet` como objeto físico, sistema, assembly, grupo de
    UI o selección operacional persistente. Explica por qué.
25. Compara `Support.parentElementID` con una interfaz física rica que tenga rigidez,
    reparto entre receptores y geometría propia.
26. Propón una cuestión que Civil Domain deba resolver de forma general y otra que
    Footings deba decidir localmente.

Consulta después las [respuestas razonadas](STUDY_ANSWERS.md).
