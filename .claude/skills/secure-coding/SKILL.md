---
name: secure-coding
description: Revisar y aplicar seguridad en el código: validación, autenticación, autorización, secretos y dependencias. Usar al crear endpoints, manejar usuarios o credenciales, o antes de dar por terminado un módulo.
---

# Secure Coding

## Objetivo
Incorporar seguridad desde el diseño hasta las pruebas, sin introducir complejidad innecesaria.

## Revisión inicial
- Identificar entradas no confiables.
- Revisar autenticación y autorización.
- Inspeccionar validaciones y manejo de errores.
- Buscar secretos expuestos en código o configuraciones.
- Revisar dependencias y configuraciones sensibles.
- Identificar operaciones con efectos secundarios.

## Reglas fundamentales
1. Validar los datos del lado del servidor.
2. Aplicar el principio de mínimo privilegio.
3. No confiar en la identidad o los permisos enviados por el cliente.
4. Evitar inyección SQL usando consultas parametrizadas o mecanismos seguros del framework.
5. No almacenar contraseñas en texto plano.
6. No exponer tokens, contraseñas ni claves en logs o respuestas.
7. No devolver trazas internas al usuario final.
8. Mantener las dependencias razonablemente actualizadas.
9. Usar HTTPS y configuraciones seguras en los entornos correspondientes.
10. Proteger operaciones sensibles mediante controles de autorización.

## Gestión de secretos
- Utilizar variables de entorno o un gestor de secretos adecuado.
- Mantener archivos `.env` reales fuera de Git.
- Permitir archivos de ejemplo sin valores sensibles.
- Si un secreto queda expuesto, recomendar su revocación y rotación.
- No copiar secretos a documentación, mensajes o reportes.

## Límites de actuación
- No probar exploits contra sistemas sin autorización.
- No desactivar controles de seguridad para hacer pasar una prueba.
- No modificar infraestructura, permisos globales ni configuraciones de producción sin aprobación explícita.
- No afirmar que un sistema es completamente seguro por superar una revisión.

## Resultado esperado
Priorizar los hallazgos por gravedad, explicar su impacto y proponer mitigaciones concretas y verificables.

---

## Ampliaciones (agregadas, revisar y aceptar o quitar)

### Control de acceso por recurso (IDOR)
- Estar autenticado no es estar autorizado. En cada endpoint que reciba un identificador, verificar que el recurso pertenezca al usuario del token o que su rol lo permita.
- La identidad del usuario se toma siempre del token, nunca del body, la URL ni un header que mande el cliente.

### Contraseñas y autenticación
- Guardar contraseñas con un hash lento y salado: ASP.NET Core Identity (`PasswordHasher`) o Argon2/bcrypt. Nunca criptografía propia, ni MD5 ni SHA simple.
- JWT: validar firma, emisor, audiencia y expiración; vida corta; clave larga y fuera del repositorio.
- Rate limiting en login, registro y recuperación de contraseña.
- Mensajes de error de login genéricos ("credenciales inválidas"), sin revelar si el usuario existe.

### Entradas y salidas
- Usar DTOs para evitar *overposting* (ver skill `dotnet-api-development`).
- CORS con orígenes explícitos; no usar `*` junto con credenciales.
- HTTPS obligatorio, HSTS y cabeceras de seguridad en producción.
- Subida de archivos: validar tipo y tamaño, no confiar en el nombre original y guardar fuera de las rutas públicas.
- Logs sin datos personales ni credenciales.

### Dependencias
- Con autorización, revisar vulnerabilidades con `dotnet list package --vulnerable` y desactualizadas con `dotnet list package --outdated`.
- Antes de proponer un paquete NuGet, verificar que exista y que sea el oficial. No sugerir paquetes de memoria sin comprobar el nombre exacto.

### Referencia y cierre
- Usar **OWASP Top 10** y **OWASP ASVS** como checklist.
- Al terminar una revisión, informar qué categorías se revisaron y cuáles quedaron sin revisar.
