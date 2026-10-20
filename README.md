# github_skills

Kit reutilizable de instrucciones, skills y configuración para trabajar con agentes de programación (Claude Code, OpenCode y otros) en proyectos personales. Pensado para copiarlo a un proyecto nuevo y arrancar con reglas de seguridad y buenas prácticas desde el primer commit.

## Qué contiene

| Ruta | Para qué sirve |
|---|---|
| `AGENTS.md` | Reglas que siguen los agentes: prioridades, seguridad, aprobaciones obligatorias, flujo de Git y calidad. |
| `CLAUDE.md` | Punto de entrada para Claude Code: indica leer `AGENTS.md` y dónde encontrar el contexto del proyecto. |
| `.gitignore` | Ignora secretos (`.env`, claves, `appsettings.*.local.json`), archivos de IDE/SO y salidas de build de .NET. |
| `.claude/skills/` | Skills reutilizables (ver abajo). |
| `.claude/settings.json.example` | Permisos ejemplo para Claude Code: prohíbe `git push`, `git reset --hard`, `git clean` y leer `.env` reales. |
| `opencode.json.example` | Permisos ejemplo equivalentes para OpenCode. |
| `docs/ai/` | Plantillas de contexto del proyecto: `PROJECT_CONTEXT.md`, `ARCHITECTURE.md` y `DECISIONS.md`. |

## Skills incluidas

- **project-onboarding**: analizar un proyecto desconocido antes de modificar código.
- **dotnet-api-development**: APIs con C#/ASP.NET Core por capas, DTOs, EF Core y manejo de errores.
- **secure-coding**: validación, autenticación/autorización, secretos y dependencias (basada en OWASP).
- **secure-git-workflow**: flujo de Git seguro, mensajes de commit convencionales y revisión de secretos.
- **testing-qa**: casos de prueba, pruebas automatizadas con xUnit y regresión.

## Cómo usarlo en un proyecto nuevo

1. Copiá a la raíz del proyecto nuevo: `AGENTS.md`, `CLAUDE.md` y `.gitignore`.
2. Copiá la carpeta `.claude/` completa si usás Claude Code, o solo `opencode.json.example` como base si usás OpenCode (renombralo a `opencode.json`).
3. Copiá `docs/ai/` y completá las tres plantillas con el contexto del proyecto (qué resuelve, arquitectura y decisiones técnicas).
4. Revisá los archivos `.example` y ajustá los permisos a lo que el proyecto necesite.

## Reglas de seguridad que ya vienen activas

- No se commitean ni se leen secretos (`.env`, claves privadas, configuraciones locales).
- `git push`, `git reset --hard` y `git clean` requieren aprobación explícita del usuario.
- Los ejemplos usan placeholders (`YOUR_API_KEY`), nunca valores reales.

## Licencia

MIT — ver [LICENSE](LICENSE).
