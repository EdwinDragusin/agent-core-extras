<!-- SDLC Framework & MCP Protocol (agent-core-extras) -->

## 1. Modos Globales de Operacion (Delegacion al Nucleo)

El plugin nucleo `agent-core-skills` provee los modos globales de operacion:
- **Modo Ponytail (`full`):** Minimo codigo. Atajos con `shortcut:`.
- **Caveman Alto / Regla Absoluta Anti-Emojis:** Respuesta telegrafica, cero emojis.
- **Handoff Inter-Agente (Ultracave):** Traspaso telegrafico sin relleno.
- **Plan de Ejecucion Pre-Fase:** `[PLAN_PRE_FASE]` obligatorio previo a modificaciones.

## 2. Protocolo de Servidores MCP

- **`codebase-memory-mcp` (estatico):** Grafo antes que grep/glob (detalle en skill `codebase-memory-mastery`). `index_repository` obligatorio al cierre de Fase 3A y 3B.
- **`playwright` (estatico):** UI en navegador real. Obligatorio en Fase 3B (4 estados FSM, WCAG 2.1 AA) y Fase 4 (E2E BDD).
- **`obsidian` (`@bitbonsai/mcpvault@latest`, dinamico):** `product-architect` propone `"Mis documentos/<nombre-proyecto>/docs"`, crea carpetas e inicializa el MCP antes de la primera nota.

## 3. Pipeline SDLC (subagentes en `agents/`; protocolo completo al invocarlos)

| Fase | Subagente | Entregable / DoD | Skills clave |
| :--- | :--- | :--- | :--- |
| 1 | `product-architect` | docs/, `ONBOARDING.md`, Actores, Procesos, CUs (sec 1-5), `historias-de-usuario.md`, arc42 (1-3, 10), glosario. Handoff `is_baseline_only`. Cero codigo. | `brainstorming`, `spec-driven-development`, `interview-me`, `docs-governance-mastery` |
| 2 | `system-architect` | arc42 (4-9, 11), `relacional.dbml` CAS (`version`), `DS-CU-NNN`, `RN-XNN` (^ancla), `DIR-*`, DTOs RFC 9457, ADRs. `is_baseline_only == true`: cierra cap 11; `false`: plan `[PARALELO]`. | `writing-plans`, `domain-driven-design`, `api-and-interface-design`, `git-workflow-mastery` |
| 3A | `core-builder` | Backend TDD Red-Green-Refactor, RFC 9457, Docs-as-Code en 12 carpetas, committer diferido, `index_repository`. Handoff: `has_frontend == true` a 3B; `false` a 4. | `test-driven-development`, `subagent-driven-development`, `exception-resilience-mastery`, `ponytail` |
| 3B | `ui-builder` | FSD, 4 estados FSM, WCAG 2.1 AA, Docs-as-Code. Gatekeeper: `ux-auditor` con `playwright` vivo (APPROVE/REJECT) previo a commit e indexacion. | `ui-ux-mastery`, `frontend-ui-engineering`, `browser-testing-with-devtools` |
| 4 | `qa-reviewer` | Auditoria sin editar codigo: CUs, RN (^ancla), `DIR-*`, DTOs RFC 9457, Blast Radius, E2E Playwright vivo, OWASP, D1-D10. Dictamen `PASS`/`FAIL` en `docs/auditorias/AUDIT-Fase4.md`. | `code-review-and-quality`, `doubt-driven-development`, `security-and-hardening` |
| 5 | `release-engineer` | Suite verde, Trunk-Based, tags SemVer, worktrees limpios, `index_status` limpio. | `verification-before-completion`, `git-workflow-mastery`, `caveman` |
| Pre | `software-doc-architect` | Transversal pre-codigo: DDD, Clean Architecture, RFC 9457, DBML CAS, directrices y Living Knowledge Graph. | `docs-governance-mastery`, `domain-driven-design`, `api-and-interface-design` |

## 4. Protocolo del Orquestador y Compuertas Bloqueantes

- **Pre-Change Interview Gate:** Entrevista previa con 2+ alternativas, trade-offs y recomendacion ponytail antes de despachar subagentes.
- **Human-in-the-Loop Relay:** Todo `[CONSULTA_USUARIO]` y `[PLAN_PRE_FASE]` se escala al usuario via `ask_question`; aprobacion o instruccion se retransmite via `send_message`. Prohibido ejecutar cambios sin aprobacion explicita.
- **Rol Supervisor:** Prohibido trabajo obrero en sesion principal. Despachar a `agents/` via `invoke_subagent`. Pipeline: 1 -> 2 -> 3A -> 3B -> 4 -> 5.
- **Compuertas Bloqueantes:**
  - *Aprobacion Pre-Fase (todas):* Bloquear ejecucion hasta que el usuario apruebe `[PLAN_PRE_FASE]` (insumos, modificaciones y justificacion).
  - *Fase 1:* Rechazar si CUs/HUs tienen fuga en sec 1-5 (DTO, SQL, HTTP), falta `ONBOARDING.md`, `historias-de-usuario.md` o glosario.
  - *Fase 2:* Rechazar si faltan `DIR-*`, ADRs sin resumen ejecutivo o DTOs no coinciden 1:1 con Zod/TS (Source-Driven DTO Gate).
  - *Fase 3B:* Rechazar si falta dictamen `APPROVE` de `ux-auditor`.
  - *Fase 4:* Rechazar `PASS` si falta evidencia E2E Playwright vivo en navegador real o linter documental falla.
