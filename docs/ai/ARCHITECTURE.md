# Arquitectura

> Completar y actualizar cuando cambie la estructura.

## Capas
- `Controllers/`: reciben la request y devuelven la respuesta HTTP. Sin lógica de negocio.
- `Services/`: reglas de negocio.
- `Repositories/` o acceso a datos (EF Core): persistencia.
- `Dtos/`: modelos de entrada y salida de la API.
- `Models/` o `Entities/`: modelos de base de datos. Nunca se exponen directamente.

## Límites
- Los controladores no acceden a la base de datos.
- Las entidades no salen de la capa de servicios hacia el cliente.

## Autenticación y autorización
(Mecanismo elegido, dónde se valida y cómo se verifica la propiedad de cada recurso)

## Configuración y secretos
(Qué variables usa; los valores nunca van en el repositorio)
