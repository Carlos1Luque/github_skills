---
name: project-onboarding
description: Analizar un proyecto desconocido o recién abierto antes de modificar código. Usar al empezar a trabajar en un repositorio, antes de proponer cambios medianos o grandes, o cuando se pide entender la estructura del proyecto.
---

# Project Onboarding

## Objetivo
Comprender un proyecto antes de modificar código, evitando cambios innecesarios y respetando las decisiones existentes.

## Procedimiento
1. Revisar `AGENTS.md`, `CLAUDE.md`, README y la documentación disponible.
2. Identificar lenguaje, framework, estructura de carpetas, dependencias y puntos de entrada.
3. Reconocer módulos, responsabilidades y relaciones principales.
4. Revisar configuración, variables de entorno y manejo de secretos sin revelar sus valores.
5. Identificar pruebas existentes, comandos de ejecución y herramientas de calidad.
6. Detectar riesgos, inconsistencias y documentación desactualizada.
7. Presentar un resumen y un plan de trabajo antes de modificar archivos.

## Reglas
- Comenzar en modo de lectura.
- No asumir que una tecnología o dependencia está instalada sin verificarlo.
- No ejecutar scripts, instalar paquetes ni modificar archivos sin autorización cuando corresponda.
- No inventar resultados de pruebas.
- Diferenciar hechos comprobados, hipótesis y recomendaciones.

## Resultado esperado
Entregar:
- Resumen del proyecto.
- Tecnologías y estructura.
- Archivos importantes.
- Riesgos detectados.
- Pruebas recomendadas.
- Plan de próximos pasos priorizado.

## Criterio de finalización
El proyecto se considera analizado cuando existe una descripción clara de su estructura, sus principales convenciones y los pasos seguros para continuar.

---

## Ampliaciones (agregadas, revisar y aceptar o quitar)

### Plantilla fija para el informe final
Usar siempre este orden, para que la salida sea comparable entre proyectos:

1. **Resumen del proyecto** (qué problema resuelve, en 3 a 5 líneas).
2. **Tecnologías y estructura** (versión de .NET u otro runtime, carpetas, puntos de entrada).
3. **Archivos importantes** (con una línea de explicación cada uno).
4. **Riesgos detectados** (ordenados por gravedad).
5. **Pruebas recomendadas** (qué existe y qué falta).
6. **Plan de próximos pasos** (priorizado, con lo que requiere aprobación marcado).

Etiquetar cada afirmación relevante como `[Hecho]` (lo vi en un archivo o salida real), `[Hipótesis]` o `[Recomendación]`.

### Secretos
- Listar solo los **nombres** de las variables de entorno y dónde se usan, nunca sus valores.
- No abrir `.env` reales; usar `.env.example` como referencia.
