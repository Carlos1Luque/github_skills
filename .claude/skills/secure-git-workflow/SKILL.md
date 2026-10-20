---
name: secure-git-workflow
description: Flujo de Git seguro: revisar estado, ramas, diffs y secretos antes de commitear; operaciones que requieren aprobación. Usar antes de cualquier commit, push, merge o cuando hay conflictos.
---

# Secure Git Workflow

## Objetivo
Mantener un historial claro y reducir el riesgo de perder trabajo, publicar secretos o introducir cambios no revisados.

## Antes de modificar
1. Ejecutar `git status`.
2. Revisar la rama actual.
3. Examinar los cambios existentes.
4. Confirmar que no se van a sobrescribir modificaciones del usuario.
5. Verificar `.gitignore` y los archivos que se pretenden agregar.

## Durante el trabajo
- Crear ramas para cambios relevantes cuando corresponda.
- Realizar cambios pequeños y coherentes.
- Revisar `git diff` antes de confirmar.
- No agregar archivos sensibles.
- No incluir archivos generados o dependencias innecesarias.
- No sobrescribir cambios ajenos sin autorización.

## Antes de un commit
Verificar:
- Que los archivos preparados sean los esperados.
- Que no haya secretos.
- Que las diferencias sean comprensibles.
- Que se hayan realizado las verificaciones pertinentes.
- Que el mensaje del commit describa el cambio real.

Comandos de revisión útiles:

```
git status
git diff
git diff --cached
git diff --cached --check
git log -5 --oneline
```

## Operaciones que requieren aprobación explícita
- `git push`, especialmente a ramas compartidas o protegidas.
- `git push --force`.
- `git reset --hard`.
- `git clean -fd` y variantes destructivas.
- Reescribir historial compartido.
- Eliminar ramas o etiquetas importantes.
- Publicar versiones o desplegar en producción.

No ejecutar estas operaciones automáticamente.

## Si aparece un conflicto
- No descartar cambios para resolverlo rápidamente.
- Identificar qué modificaciones pertenecen a cada parte.
- Explicar las opciones de resolución.
- Solicitar aprobación cuando exista riesgo de pérdida de datos.

## Resultado esperado
Un flujo de trabajo revisable, con cambios trazables, commits coherentes y ninguna publicación realizada sin la autorización necesaria.

---

## Ampliaciones (agregadas, revisar y aceptar o quitar)

### Relación con AGENTS.md
Esta skill describe *cómo* trabajar con Git; no autoriza a hacer commit ni push. Se sigue `AGENTS.md`: no se confirman cambios ni se publican salvo pedido o autorización expresa del usuario.

### Mensajes de commit
Usar prefijos convencionales: `feat:`, `fix:`, `docs:`, `test:`, `refactor:`, `chore:`. Un commit, un cambio coherente. Ejemplo: `fix: validar que el pedido pertenezca al usuario autenticado`.

### Revisión de secretos antes de commitear
- Leer `git diff --cached` buscando claves, tokens, cadenas de conexión y contraseñas.
- Confirmar que ningún `.env` real, `.pfx`, `.key` ni `appsettings.*.local.json` esté preparado.
- Si hay una herramienta de escaneo de secretos instalada y el usuario la autoriza, ejecutarla antes del commit.

### Si un secreto ya se subió
1. **Rotar o revocar el secreto de inmediato.** Es el paso que realmente cierra el riesgo.
2. Recién después, evaluar limpiar el historial. Reescribirlo no alcanza: el secreto pudo haber sido copiado o indexado mientras estuvo público, y requiere aprobación explícita por afectar historial compartido.
