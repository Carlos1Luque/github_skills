---
name: dotnet-api-development
description: Desarrollar o modificar APIs con C# y ASP.NET Core (controladores, servicios, DTOs, CRUD, EF Core). Usar al crear endpoints, implementar un CRUD o revisar una API .NET.
---

# .NET API Development

## Objetivo
Desarrollar APIs mantenibles, comprensibles y seguras utilizando C# y ASP.NET Core.

## Antes de programar
1. Revisar la versión de .NET y el archivo `.csproj`.
2. Inspeccionar la estructura actual y los controladores existentes.
3. Identificar modelos, DTO, servicios, persistencia y configuración.
4. Confirmar los requisitos funcionales antes de elegir una implementación.

## Principios de desarrollo
- Mantener las convenciones existentes del proyecto.
- Utilizar nombres descriptivos y responsabilidades claras.
- Aplicar correctamente los verbos HTTP: GET, POST, PUT, PATCH y DELETE según corresponda.
- Devolver códigos HTTP apropiados.
- Validar entradas del usuario.
- Evitar duplicar lógica entre controladores.
- No agregar paquetes innecesarios.
- No introducir patrones complejos si el proyecto no los necesita.

## CRUD
Al implementar un CRUD, verificar:
- Crear recursos con validaciones.
- Consultar uno o varios recursos.
- Actualizar recursos existentes.
- Eliminar recursos según las reglas del negocio.
- Manejar identificadores inexistentes y datos inválidos.
- Evitar exponer información interna en los errores.

## Seguridad
- No guardar contraseñas en texto plano.
- No incluir secretos en el código.
- No confiar en los datos recibidos desde el cliente.
- Aplicar autenticación y autorización cuando los requisitos lo exijan.
- No considerar que ocultar un endpoint equivale a protegerlo.

## Verificación
1. Revisar los cambios realizados.
2. Ejecutar `dotnet build` cuando esté autorizado.
3. Ejecutar las pruebas existentes.
4. Probar los casos exitosos y los errores esperados.
5. Informar los comandos ejecutados y sus resultados reales.

## Resultado esperado
Entregar código coherente con el proyecto, explicar las decisiones relevantes y enumerar las verificaciones pendientes.

---

## Ampliaciones (agregadas, revisar y aceptar o quitar)

### Arquitectura por capas
- **Proyecto nuevo:** la base es por capas, `Controller -> Service -> Repository` (o acceso a datos con EF Core), con cada capa en su responsabilidad. Esto precisa la regla de "no patrones complejos": por capas es el punto de partida, no un patrón avanzado.
- **Proyecto existente:** se respeta la estructura que ya tiene; no se reorganiza sin pedido explícito.
- Los controladores solo reciben la request, llaman al servicio y devuelven la respuesta HTTP. La lógica de negocio vive en los servicios.

### DTOs separados de las entidades
- Nunca recibir ni devolver la entidad de base de datos directamente.
- Usar DTOs de entrada y de salida distintos. Esto evita el *overposting* (que el cliente envíe campos como `IsAdmin` o `Id` y se guarden) y evita filtrar campos internos.

### Manejo de errores
- Devolver errores con `ProblemDetails`, sin trazas ni mensajes de excepciones internas.
- Un manejo global de excepciones (middleware) en vez de `try/catch` repetido en cada controlador.
- Códigos correctos: 400 datos inválidos, 401 sin autenticar, 403 sin permiso, 404 no existe, 409 conflicto.

### Rendimiento y buenas prácticas
- Endpoints asíncronos (`async/await`) y `CancellationToken` en las operaciones de base de datos.
- Paginación en todo listado que pueda crecer.
- `AsNoTracking()` en consultas de solo lectura.
- Consultas con EF Core o parámetros; nunca armar SQL concatenando texto del cliente.
