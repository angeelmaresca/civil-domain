# Reglas candidatas del dominio civil

> **Status:** DRAFT
> **Editable:** sí; reglas conceptuales dentro de `WORKING_SET.md`
> **Document owner:** equipo de dominio civil
> **Canonical for:** —
> **Sources:** [síntesis de la primera iteración](iteration-01/SINTESIS.md), [ocurrencia de diseño](domain-objects/DESIGN_OCCURRENCE.md) y fichas de la primera iteración
> **Supersedes:** —
> **Last reviewed:** 2026-09-18

## Alcance

Estas reglas permiten probar el modelo conceptual antes de diseñar tablas o clases.
Son candidatas `DRAFT`: expresan consecuencias de las evidencias actuales y deben
contrastarse con casos reales.

## Identidad y revisión

1. El ID interno de una ocurrencia es estable, opaco y no se recicla.
2. TAG, código, GUID externo, geometría, material, posición o pertenencia no son por
   sí solos la identidad de la ocurrencia.
3. Cambiar propiedades produce normalmente otro estado de la misma ocurrencia; una
   división, fusión o sustitución exige decidir explícitamente la continuidad.
4. La ausencia en una revisión de fuente no causa una baja automática. Deben
   comprobarse cobertura, cambio de referencia, sustitución y autoridad de la fuente.
5. Un estado aceptado registra decisión, responsable, fecha, contexto y evidencia;
   no equivale al snapshot más reciente.

## Separación semántica

6. Una representación física no es la ocurrencia que representa.
7. Un objeto analítico no es la ocurrencia física que idealiza.
8. Un tipo declarado no es una agrupación calculada por similitud.
9. Composición física, membresía de sistema, contención espacial, conexión y apoyo
   son relaciones distintas.
10. Una estructura física puede ser una ocurrencia compuesta; un sistema estructural,
    un contenedor espacial, un tipo y un modelo analítico no se convierten en esa
    ocurrencia por compartir el nombre «estructura».

## Procedencia y cambio

11. Toda afirmación importada conserva aplicación, modelo, revisión y referencia
    externas suficientes para reconstruir su procedencia.
12. Datos contradictorios de dos fuentes pueden coexistir hasta una decisión; no se
    sobrescriben silenciosamente.
13. Las relaciones que pueden cambiar deben identificar su contexto o vigencia.
14. La correspondencia físico–analítica conserva cardinalidad, propósito y evidencia.
15. La validación técnica se refiere a estados, entradas, análisis y evidencias
    identificados; no es una propiedad eterna de la ocurrencia.

## Criterio de madurez

Una regla solo podrá proponerse como `CANONICAL` cuando tenga aprobación humana
explícita, ejemplos positivos, al menos un contraejemplo o límite y una fuente
propietaria inequívoca.
