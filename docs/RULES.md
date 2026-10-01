# Reglas candidatas del dominio civil

> **Status:** DRAFT
> **Editable:** sí; reglas conceptuales dentro de `WORKING_SET.md`
> **Document owner:** equipo de dominio civil
> **Canonical for:** —
> **Sources:** [síntesis de la primera iteración](iteration-01/SINTESIS.md), [ocurrencia de diseño](domain-objects/DESIGN_OCCURRENCE.md), [sistema de ingeniería](domain-objects/ENGINEERING_SYSTEM.md) y fichas de la primera iteración
> **Supersedes:** —
> **Last reviewed:** 2026-10-01

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

## Versiones de conjuntos y cargas — propuesta para contraste

Fuente: [sesión del 23 de septiembre](iteration-02/ENUNCIADO.md#11-sesión-del-23-de-septiembre-conjuntos-y-versiones).
Reglas `DRAFT` para los casos tratados, pendientes del equipo.

16. Versión de diseño y revisión documental de emisión son conceptos distintos;
    no se presupone correspondencia uno a uno.
17. Estructura y cimentación se versionan como conjuntos completos; sus piezas se
    describen dentro de esa versión sin exigir ciclos independientes por pieza.
18. Los módulos, y estructura frente a cimentación, pueden versionarse de forma
    independiente. Un cambio requiere evaluar dependencias, no incrementar todos
    los números de versión automáticamente.
19. Cada receptor de cargas debe identificar la versión concreta proveedora usada
    como base. La aceptación sin cambios frente a una nueva versión debe quedar
    explícita; el mecanismo y la autoridad están por definir.
20. El cierre exige resolver dependencias por actualización o aceptación sin cambios.
    Igualar números no prueba coherencia ni sustituye validación técnica.
21. En la remodularización descrita bastan modelos completos históricos sin vínculo
    pieza a pieza. No extender esta simplificación a todos los casos.
22. Reutilizar TAG no equivale a reutilizar identidad interna; decidir continuidad
    del módulo es distinto de conservar su código.

## Sistemas, modelos y conciliación — hipótesis para la quinta iteración

Fuente: [quinta iteración](iteration-05/ENUNCIADO.md). Reglas `DRAFT` que deben
intentarse refutar con modelos globales, fronteras compartidas y pertenencia múltiple.

23. Un modelo de ingeniería tiene identidad, propósito y revisiones propios; no
    pertenece a una ocurrencia individual aunque pueda representarla.
24. Una ocurrencia aparece en un modelo mediante una representación contextualizada.
    El objeto o referencia del modelo no sustituye su identidad interna.
25. Asociar un modelo o una ocurrencia a un sistema de ingeniería no implica
    ownership exclusivo. No se fijará cardinalidad uno-a-muchos sin resolver los
    casos de cobertura global y sistemas compartidos.
26. Un caso de conciliación identifica propósito, alcance, modelos y revisiones,
    aspectos comparables, políticas aplicadas y responsables de las decisiones.
27. Una diferencia entre modelos solo es discrepancia si incumple una expectativa
    declarada de cobertura, equivalencia, tolerancia o autoridad para ese alcance.
28. Una vista resuelta conserva fuentes, revisiones, aspecto, política y momento de
    resolución; no duplica silenciosamente valores técnicos en la ocurrencia.
29. `SistemaDeIngeniería` permanece como frontera conceptual candidata. No se declara
    agregado raíz hasta que existan decisiones explícitas de consistencia,
    transacción e implementación.

## Criterio de madurez

Una regla solo podrá proponerse como `CANONICAL` cuando tenga aprobación humana
explícita, ejemplos positivos, al menos un contraejemplo o límite y una fuente
propietaria inequívoca.
