# Diseño de flujo de apertura de cuenta

Como diseñador de soluciones, debes diseñar el flujo completo para la apertura de una cuenta bancaria en una aplicación móvil. Debes especificar todos los componentes necesarios, sus estados y aplicar criterios de accesibilidad verificables. El flujo debe cubrir desde la solicitud inicial hasta la confirmación final, incluyendo validaciones y manejo de errores.

## Informacion General

| Campo | Valor |
|-------|-------|
| **Tema** | Diseño de flujo y componentes |
| **Nivel** | advanced-l2 |
| **Tipo** | practical |
| **Tiempo estimado** | 8 horas |

## Fases del Reto

### Fase 0: Configuración del Proyecto

**Objetivo:** Obtener el proyecto base funcional enviando el Código Base a un asistente de IA, que lo analizará, corregirá errores y generará un ZIP listo para usar.

**Tiempo estimado:** 15-30 minutos

**Instrucciones:**

- Asegúrate de tener instalado para ejecutar el proyecto: Un IDE o editor de código.
- Copia todo el contenido del campo **Código Base** de este reto — incluyendo el texto de instrucciones que aparece al inicio.
- Abre un asistente de IA (Claude en claude.ai, ChatGPT o Gemini — se recomienda Claude), pega el contenido copiado en el chat y envíalo.
- El asistente analizará los archivos, corregirá errores y generará un archivo ZIP descargable. Descárgalo y extráelo en la carpeta donde quieras trabajar.
- Verifica que el proyecto arranca sin errores.

**Entregable:** El proyecto compila/arranca sin errores.

<details>
<summary>Pistas de conocimiento</summary>

- Copia el Código Base completo incluyendo el texto de instrucciones al inicio — esas instrucciones le indican al asistente exactamente qué hacer con los archivos.
- Si el asistente no genera el ZIP automáticamente al terminar el análisis, escríbele: "genera el ZIP ahora".
- Si el proyecto tiene errores al arrancar, comparte el mensaje de error con el mismo asistente para que lo corrija.

</details>

### Fase 1: Definición de componentes y estados

**Objetivo:** Identificar y definir todos los componentes y sus estados necesarios para el flujo de apertura de cuenta.

**Tiempo estimado:** 2 horas

**Instrucciones:**

- Enumera todos los componentes (ej. botones, campos de texto, indicadores de progreso) y describe sus estados (ej. normal, hover, disabled).
- Aplica criterios de accesibilidad a cada componente (ej. contraste de colores, etiquetas adecuadas).

**Entregable:** Documento con la lista de componentes y sus estados, incluyendo criterios de accesibilidad.

<details>
<summary>Pistas de conocimiento</summary>

- Considera las interacciones posibles del usuario con cada componente.
- Revisa las guías de accesibilidad para aplicaciones móviles.

</details>

### Fase 2: Diseño del flujo de usuario

**Objetivo:** Crear un flujo de usuario que cubra todas las etapas de la apertura de cuenta, incluyendo validaciones y manejo de errores.

**Tiempo estimado:** 3 horas

**Instrucciones:**

- Diseña el flujo de usuario desde la solicitud inicial hasta la confirmación final.
- Incluye validaciones en cada paso (ej. verificación de datos, confirmación de términos y condiciones).
- Maneja posibles errores y proporciona retroalimentación al usuario.

**Entregable:** Diagrama de flujo del usuario para la apertura de cuenta, incluyendo validaciones y manejo de errores.

<details>
<summary>Pistas de conocimiento</summary>

- Considera las posibles interacciones del usuario en cada paso del flujo.
- Piensa en cómo manejar los errores de forma amigable para el usuario.

</details>

### Fase 3: Revisión y optimización

**Objetivo:** Revisar y optimizar el flujo de usuario y los componentes para asegurar una experiencia de usuario óptima.

**Tiempo estimado:** 3 horas

**Instrucciones:**

- Revisa el flujo de usuario y los componentes diseñados en las fases anteriores.
- Identifica áreas de mejora y optimiza el flujo y los componentes.
- Asegura que todos los criterios de accesibilidad se hayan aplicado correctamente.

**Entregable:** Documento con las mejoras y optimizaciones realizadas al flujo de usuario y los componentes.

<details>
<summary>Pistas de conocimiento</summary>

- Considera la usabilidad y la accesibilidad en cada paso del flujo.
- Piensa en cómo puedes optimizar la experiencia del usuario.

</details>

## Dimensiones Evaluadas

- **queEs**: ¿Qué son los componentes y estados necesarios para el flujo de apertura de cuenta?
- **paraQueSirve**: ¿Para qué sirve cada componente y estado en el flujo de apertura de cuenta?
- **comoSeUsa**: ¿Cómo se usan los criterios de accesibilidad en los componentes del flujo de apertura de cuenta?
- **erroresComunes**: ¿Qué errores comunes pueden ocurrir en el flujo de apertura de cuenta y cómo se manejan?
- **queDecisionesImplica**: ¿Qué decisiones implica el diseño del flujo de apertura de cuenta?

## Criterios de Evaluacion

- Identificación y definición de todos los componentes y sus estados necesarios para el flujo de apertura de cuenta.
- Aplicación de criterios de accesibilidad a cada componente.
- Diseño del flujo de usuario que cubre todas las etapas de la apertura de cuenta, incluyendo validaciones y manejo de errores.
- Revisión y optimización del flujo de usuario y los componentes para asegurar una experiencia de usuario óptima.

## Como trabajar con un asistente de IA

Hay dos caminos, elegi uno:

- **AGENTS.md** (recomendado) — instrucciones nativas del repo. Abri esta carpeta con tu agente local (Claude Code, Cursor, Codex, Copilot, Gemini) y las carga solo. Sabe que archivos faltan y con que comando se verifica, y completa el scaffold escribiendo en disco.
- **PROMPT_MEJORA.md** — para copiar y pegar en un chat (claude.ai, ChatGPT). Devuelve un ZIP con el proyecto. Sirve si no tenes un agente en el IDE.

Ninguno de los dos resuelve las fases del reto: eso es tu trabajo.

## Verificacion

El proyecto esta listo para trabajar cuando este comando corre sin errores:

```bash
python3 -c "import json; json.load(open('design-tokens.json'))"
```

---

*Reto generado automaticamente por Challenge Generator - Pragma*
