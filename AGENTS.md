# Instrucciones para agentes

## Puerta de entrada

1. Abrir primero `docs/WORKING_SET.md` antes de analizar o editar el repositorio.
2. Editar solamente los documentos incluidos en su alcance de trabajo.
3. Tratar el contenido `DRAFT` como hipótesis en discusión, no como definición
   aprobada.
4. No promover contenido a `CANONICAL` sin aprobación humana explícita.

## Crecimiento deliberado del repositorio

La ausencia de una carpeta es intencionada. No crear carpetas vacías ni estructuras
«por si acaso».

Antes de crear una carpeta o una nueva familia de documentos, el agente debe:

1. identificar el artefacto concreto que ya necesita ubicación;
2. comprobar que no pertenece a un documento existente;
3. explicar al equipo qué problema resuelve la carpeta y por qué aparece en ese
   momento;
4. incorporar la creación al alcance de `docs/WORKING_SET.md`;
5. registrar el resultado en `docs/WORK_LOG.md` cuando se cierre el bloque, si el
   cambio es material.

Ejemplos de crecimiento permitido, únicamente cuando exista contenido real:

- crear `docs/canonical/` cuando haya una primera definición aprobada;
- crear `docs/canonical/entities/` cuando una entidad concreta vaya a documentarse
  individualmente;
- crear `docs/decisions/` cuando sea necesario registrar la primera decisión o
  pregunta fuera de su documento de trabajo;
- crear `docs/sources/` al incorporar la primera fuente original que deba preservarse
  sin modificaciones;
- crear `docs/archive/` cuando un documento sea sustituido y deba conservarse;
- crear `schemas/` cuando comience una representación formal o ejecutable del modelo.

Los nombres anteriores son orientativos. Antes de crearlos debe confirmarse que
siguen siendo adecuados para la necesidad real.

## Reglas de conocimiento

- Cada concepto debe tener una única fuente propietaria; otros documentos lo
  enlazan y no duplican su definición.
- Separar hechos confirmados, hipótesis, preguntas y fuentes externas.
- No convertir automáticamente la estructura de IFC, CADMATIC, Tekla, Revit,
  Footings u otro software en el modelo propio. Se utilizan como referencias y
  evidencia comparativa.
- Footings no es autoridad sobre todo el dominio civil. Sus conceptos vigentes son
  una fuente relevante para estudiar la frontera y el posible modelo compartido.
- Mantener separadas la conceptualización del dominio y las decisiones de tablas,
  clases, API o tecnología mientras estas últimas no sean necesarias.
- Cuando aparezcan campos u ownership, mantener coordinadas la definición de la
  entidad y cualquier matriz de datos existente; no crear esa matriz antes de que
  aporte valor real.

## Estados documentales

Se emplearán solo cuando resulten necesarios:

- `DRAFT`: trabajo en curso sin autoridad canónica.
- `CANONICAL`: definición vigente aprobada expresamente.
- `SOURCE`: fuente original preservada y no editable.
- `ARCHIVED`: material histórico sustituido y no editable.

Todo documento mantenido dentro de `docs/` debe indicar al menos estado, condición
de edición, propietario, propósito canónico y fecha de revisión. No se modifican
fuentes originales solo para introducir esta cabecera.

## Registro y publicación

- Durante un bloque se puede editar y validar sin crear commits intermedios.
- «Cerramos bloque», «guárdalo», «súbelo» o una instrucción equivalente autorizan a
  revisar el diff, actualizar `WORK_LOG.md`, crear commits coherentes y publicar en
  `develop` si existe un remoto configurado.
- No incorporar cambios a `main` sin aprobación humana explícita.

