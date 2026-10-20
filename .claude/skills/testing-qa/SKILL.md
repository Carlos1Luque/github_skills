---
name: testing-qa
description: Diseñar y ejecutar pruebas funcionales, de validación, integración, autenticación y regresión. Usar al preparar una matriz de casos de prueba, escribir tests o verificar criterios de aceptación.
---

# Testing and Quality Assurance

## Objetivo
Comprobar que el sistema cumple los requisitos y que los cambios no rompen funcionalidades existentes.

## Procedimiento
1. Leer las historias de usuario y sus criterios de aceptación.
2. Identificar escenarios positivos, negativos y casos límite.
3. Definir precondiciones, datos de prueba y resultados esperados.
4. Diseñar casos reproducibles.
5. Ejecutar pruebas solo cuando exista autorización y un entorno adecuado.
6. Registrar resultados reales, errores y evidencias disponibles.
7. Proponer correcciones y pruebas de regresión.

## Tipos de pruebas
- Funcionales.
- Validaciones de campos.
- Integración entre componentes.
- Autenticación y autorización.
- Manejo de errores.
- Regresión.
- Casos límite.

## Casos de prueba
Cada caso debería incluir:
- ID único.
- Título.
- Módulo.
- Precondiciones.
- Datos de entrada.
- Pasos.
- Resultado esperado.
- Resultado obtenido.
- Estado: pendiente, aprobado o fallido.
- Observaciones o evidencia.

## Reglas
- Cada caso debe ser claro y reproducible.
- No confundir el resultado esperado con el obtenido.
- No marcar pruebas como aprobadas si no se ejecutaron.
- Incluir usuarios sin permisos, entradas inválidas y recursos inexistentes cuando corresponda.
- Evitar depender de datos reales sensibles.
- No ejecutar pruebas destructivas en producción.

## Resultado esperado
Entregar una matriz de pruebas priorizada, los defectos encontrados y las verificaciones pendientes.

---

## Ampliaciones (agregadas, revisar y aceptar o quitar)

### Formato del ID
Usar `TC-<MODULO>-<NNN>`, por ejemplo `TC-AUTH-001`, `TC-PRODUCTOS-014`. El estado inicial de todo caso es `pendiente`.

### Pruebas automatizadas en .NET
- Pruebas unitarias de servicios con **xUnit**, aislando dependencias con interfaces.
- Pruebas de integración de la API con `WebApplicationFactory`, usando una base de datos de prueba aislada (en memoria o SQLite), nunca la real.
- Cada caso del tipo "usuario sin permiso" o "recurso inexistente" debería existir como test automatizado, no solo como caso manual.

### Casos obligatorios de seguridad
Para cada endpoint protegido, incluir al menos:
1. Sin token: debe devolver 401.
2. Token válido pero sin el rol necesario: debe devolver 403.
3. **Usuario A intentando leer o modificar un recurso del usuario B**: debe devolver 403 o 404 (control de acceso por recurso).
4. Campos extra en el body (por ejemplo `isAdmin: true`): deben ignorarse.
5. Entradas inválidas: vacías, demasiado largas, tipos incorrectos.

### Regresión
Cuando se corrige un defecto, agregar primero un test que lo reproduzca y recién después la corrección.
