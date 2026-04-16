# Best Practices — Claude Opus 4.7 con Claude Code

Referencia operativa para sacar el máximo de Opus 4.7 en sesiones interactivas, trabajo agéntico, y workflows multi-LLM.

> Fuente: [Anthropic Blog — Best Practices for Using Claude Opus 4.7 with Claude Code](https://claude.com/blog/best-practices-for-using-claude-opus-4-7-with-claude-code)

---

## Filosofía Core

Trata a Claude como **un ingeniero senior al que le delegas**, no como un copiloto que guías línea por línea. Dale el contexto completo upfront y déjalo ejecutar.

---

## 1. Estructurar Sesiones de Coding

### Especificar todo en el primer turno

Incluye en tu primer mensaje:
- **Intent** — Qué quieres lograr
- **Constraints** — Límites técnicos, patrones existentes
- **Acceptance criteria** — Cómo se ve "done"
- **File locations** — Rutas relevantes

> Evita prompts vagos distribuidos en múltiples turnos. Un prompt completo = mejor calidad + menos tokens.

### Reducir interacciones del usuario

Cada turno del usuario agrega overhead de razonamiento. Optimiza:
- Agrupa preguntas en un solo mensaje
- Da contexto suficiente para que el modelo trabaje independiente
- Si necesitas dar seguimiento, dale toda la info de una vez

### Usar Auto Mode

- Disponible en Claude Code Max (toggle: `Shift+Tab`)
- Ideal para tareas con contexto completo y ejecución segura
- Reduce tiempo de ciclo en tareas largas

### Configurar notificaciones

Pide a Claude que reproduzca un sonido al completar tareas, o configura hooks para monitoreo asíncrono.

---

## 2. Effort Levels

El default en Opus 4.7 es **`xhigh`** (nuevo nivel entre `high` y `max`).

| Level | Cuándo usar | Trade-off |
|-------|-------------|-----------|
| `low` / `medium` | Trabajo con scope definido, sensible a costo/latencia | Menos capaz en tareas difíciles pero supera a Opus 4.6 en niveles equivalentes |
| `high` | Balance inteligencia/costo. Sesiones concurrentes | Acepta reducción de calidad por eficiencia |
| **`xhigh`** ⭐ | **Default recomendado. Coding y trabajo agéntico general** | **Fuerte autonomía sin descontrol de tokens** |
| `max` | Problemas genuinamente difíciles que requieren máxima capacidad | Rendimientos decrecientes, tendencia a overthinking |

### Tips de effort
- **Experimenta** con niveles en lugar de portar settings de Opus 4.6
- **Alterna** niveles durante una misma tarea para manejar tokens
- El upgrade al default `xhigh` ocurre automáticamente para usuarios existentes

---

## 3. Adaptive Thinking

**Cambio clave**: Extended Thinking con budget fijo **ya no existe** en Opus 4.7. Ahora el thinking es adaptativo.

### Cómo funciona
- El modelo **decide cuándo pensar** según el contexto
- Responde rápido a queries simples (sin thinking)
- Salta thinking cuando un paso no se beneficia
- Invierte tokens de thinking donde realmente importa

### Controlar el thinking

**Para más thinking** (problemas complejos):
```
Think carefully and step-by-step before responding; this problem is harder than it looks.
```

**Para menos thinking** (respuestas rápidas):
```
Prioritize responding quickly rather than thinking deeply. When in doubt, respond directly.
```
> Nota: Menos thinking ahorra tokens pero puede reducir precisión en pasos difíciles.

---

## 4. Cambios de Comportamiento vs Opus 4.6

### Respuestas más calibradas
- Ya no es verbose por default
- Respuestas cortas en lookups simples
- Respuestas largas en análisis abierto
- **Acción**: Indica preferencias de largo/estilo explícitamente. Usa ejemplos positivos ("hazlo así") en vez de negativos ("no hagas esto").

### Menos uso de herramientas, más razonamiento
- El modelo llama herramientas con menos frecuencia
- Razona más internamente (mejores resultados en muchos casos)
- **Si necesitas más tool use**: Describe explícitamente cuándo y por qué debe usar herramientas (búsquedas más agresivas, lectura de archivos, etc.)

### SubAgents más selectivos
- Menos subagents por default — delega solo cuando realmente aporta
- **Regla clave**:

> "No spawnes un subagent para trabajo que puedes completar directamente en una sola respuesta (e.g., refactorizar una función que ya puedes ver). Spawna múltiples subagents en el mismo turno cuando necesitas fan-out a través de items o leer múltiples archivos."

---

## 5. Tareas Donde Opus 4.7 Brilla

Opus 4.7 rinde significativamente mejor en tareas largas donde la supervisión humana era un cuello de botella:

- **Cambios multi-archivo complejos** — Refactors que cruzan múltiples servicios
- **Debugging ambiguo** — Bugs sin causa raíz clara
- **Code review entre servicios** — Revisión cruzada de PRs con dependencias
- **Trabajo agéntico multi-step** — Pipelines de análisis, deploy, verificación

### Recomendación
Mantén effort en `xhigh` y observa cuánto completa el modelo independientemente en tu primer turno.

---

## 6. Quick Reference para CLAUDE.md

Agrega esto a tu `CLAUDE.md` para optimizar sesiones con Opus 4.7:

```markdown
# Claude Opus 4.7 — Session Config

## Effort & Thinking
- Default effort: xhigh (no cambiar a menos que sea necesario)
- Adaptive thinking: el modelo decide cuándo pensar profundo
- Para problemas complejos, incluir: "Think step-by-step, this is harder than it looks"

## Prompting
- Primer turno: incluir intent, constraints, acceptance criteria, file paths
- Agrupar preguntas — cada turno del usuario cuesta tokens de razonamiento
- Preferir instrucciones positivas ("hazlo así") sobre negativas ("no hagas esto")

## SubAgents
- Solo spawnar subagents para fan-out real (múltiples archivos independientes)
- No delegar trabajo que se puede completar en una sola respuesta
- Cuando delegues, envía todos los subagents en el mismo turno

## Tool Use
- Si necesitas búsquedas agresivas o lecturas de archivos, dilo explícitamente
- El modelo razona más y usa menos herramientas por default — esto es intencional
```

---

## Migración desde Opus 4.6

| Aspecto | Opus 4.6 | Opus 4.7 |
|---------|----------|----------|
| Thinking | Budget fijo configurable | Adaptativo (el modelo decide) |
| Effort default | `high` | `xhigh` |
| Verbosidad | Verbose por default | Calibrada al contexto |
| Tool use | Frecuente | Selectivo (más razonamiento) |
| SubAgents | Agresivo | Selectivo (solo cuando fan-out) |
| Tokenizer | Anterior | Actualizado (afecta conteo) |
| Sesiones largas | Contexto limitado | Mejor manejo de contexto largo |
