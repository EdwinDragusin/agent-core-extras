# Agent Core Extras

[![Licencia](https://img.shields.io/badge/licencia-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-success.svg)](plugin.json)
[![Estandar](https://img.shields.io/badge/standard--readme-conforme-success.svg)](https://github.com/RichardLitt/standard-readme)

Plugin complementario de gobernanza avanzada que provee el pipeline SDLC en 5 fases, 8 subagentes especializados, protocolo de servidores MCP (Obsidian, Codebase Memory y Playwright) y un catalogo de 6 skills tecnicas.

Este repositorio fue separado a partir del commit base `13739dc` de `agent-core-skills` (registrado en `.origen-commit`).

---

## Tabla de Contenidos

- [Requisitos](#requisitos)
- [Contenido](#contenido)
- [Instalacion](#instalacion)
- [Uso](#uso)
- [Contribucion](#contribucion)
- [Licencia](#licencia)

---

## Requisitos

Requiere tener instalado previamente el plugin nucleo `agent-core-skills` (v3.0.0 o superior), el cual aporta los modos globales de operacion (Ponytail, Caveman, regla anti-emojis y compuertas base).

Servidores MCP opcionales segun la fase del SDLC:
- `codebase-memory-mcp` (analisis estructural de codigo)
- `playwright` (pruebas de interfaz y navegacion real)
- `obsidian` (gestion de bovedas documentales arc42 y Diataxis)

---

## Contenido

El plugin provee:
- **8 subagentes** (`agents/`): `product-architect`, `system-architect`, `core-builder`, `ui-builder`, `qa-reviewer`, `release-engineer`, `software-doc-architect` y `ux-auditor`.
- **6 skills** (`skills/`):
  - `browser-testing-with-devtools`: Pruebas E2E en navegador.
  - `codebase-memory-mastery`: Navegacion sobre grafos de conocimiento de codigo.
  - `docs-governance-mastery`: Gobernanza documental arc42, Diataxis y Living Knowledge Graph.
  - `interview-me`: Protocolo de entrevistas estructuradas pre-fase.
  - `obsidian-markdown`: Formato y enlazado bidireccional en bovedas Obsidian.
  - `spec-driven-development`: Especificacion funcional rigurosa de Casos de Uso.
- Protocolo de compuertas SDLC y configuracion de servidores en `mcp_config.json`.

---

## Instalacion

### Google Antigravity

```bash
agy plugin install C:/Users/edenr/Documents/agent-core-extras
```

### Claude Code

Declarar la dependencia en `.claude-plugin/plugin.json` o instalar mediante:

```bash
claude plugin add agent-core-extras
```

---

## Uso

Una vez instalado, el orquestador delega tareas a los subagentes segun la fase SDLC activa:

```bash
# Ejemplo: invocar el arquitecto documental para diseno pre-codigo
invoke_subagent --name software-doc-architect --task "Modelar caso de uso y contratos DTO"
```

Los subagentes emitiran un plan pre-fase `[PLAN_PRE_FASE]` para autorizacion antes de realizar cualquier cambio en el repositorio de trabajo.

---

## Contribucion

Las contribuciones siguen el flujo Conventional Commits en espanol, en minusculas, sin acentos y sin emojis. Toda modificacion debe validar la suite de gobernanza:

```powershell
pwsh ./scripts/plugin-lint.ps1
```

---

## Licencia

Distribuido bajo la licencia MIT. Consultar el archivo [LICENSE](LICENSE) para mas detalles.
