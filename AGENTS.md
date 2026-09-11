# AGENTS.md

Instrucciones para el agente de IA que abra este repositorio (Claude Code, Cursor, Codex, Copilot, Gemini). Se cargan solas: no hay que pegar nada en ningun chat.

## Que es este repositorio

Es el codigo base de un reto de aprendizaje de Pragma: **Diseño de flujo de apertura de cuenta**.

| | |
|---|---|
| Tema | Diseño de flujo y componentes |
| Nivel | advanced-l2 |
| Chapter | Diseño de Soluciones |
| Especialidad | Product Design |
| Stack | Figma / Atomic Design + Design Tokens |
| Patron arquitectonico | Design Thinking con doble diamante + sistema de diseño basado en componentes |
| Tiempo estimado | 8 horas |

## Tu tarea

Dejar este conjunto de artefactos en estado **verificable**: que el comando de verificacion corra sin errores. Escribi los archivos en disco, en este repositorio. No generes ZIPs ni archivos adjuntos.

En orden:

1. Corre `python3 -c "import json; json.load(open('design-tokens.json'))"` y mira que falla.
2. Completa lo que falte de la lista de abajo: manifiesto de dependencias, punto de entrada, capa de interfaz y las capas del patron declarado.
3. Arregla SOLO los errores que impiden compilar o arrancar.
4. Volve a correr `python3 -c "import json; json.load(open('design-tokens.json'))"` hasta que pase.
5. Pará ahí.

## Regla dura: las fases son trabajo del humano

**PROHIBIDO implementar los entregables de las fases.** El valor del reto esta en que la persona los resuelva. Tu trabajo es que tenga un proyecto que arranca; el hueco pedagogico se queda como esta.

No resuelvas nada de esto:

- **Fase 1 — Definición de componentes y estados**: Documento con la lista de componentes y sus estados, incluyendo criterios de accesibilidad.
- **Fase 2 — Diseño del flujo de usuario**: Diagrama de flujo del usuario para la apertura de cuenta, incluyendo validaciones y manejo de errores.
- **Fase 3 — Revisión y optimización**: Documento con las mejoras y optimizaciones realizadas al flujo de usuario y los componentes.

Distincion operativa:

- **Arreglar** (si): import faltante, tipo que no existe, dependencia sin declarar, error de sintaxis, archivo referenciado que no existe.
- **No tocar** (no): logica de negocio incompleta, validaciones ausentes, secretos hardcodeados, APIs deprecadas que funcionan, concurrencia insegura, patrones mejorables. Eso es lo que la persona tiene que encontrar.

## Lo que falta y tenes que completar

No se detectaron huecos: estan los archivos declarados, el boilerplate del stack y ninguna referencia quedo colgando. Igual corre el comando de verificacion — que los archivos existan no garantiza que compilen.

### Presentes (12)

- `investigacion/desk-research.md`
- `investigacion/user-research.md`
- `flujos/flujo-principal.mmd`
- `flujos/flujo-errores.mmd`
- `componentes/especificacion-componentes.md`
- `componentes/estados-validacion.md`
- `tokens/design-tokens.json`
- `tokens/tokens-semanticos.md`
- `accesibilidad/criterios-wcag.md`
- `accesibilidad/pruebas-accesibilidad.md`
- `validacion/heuristicas-usabilidad.md`
- `validacion/metricas-usabilidad.md`

### Capas del patron declarado

Cada una tiene que existir como directorio real con al menos un archivo. Codigo plano en la raiz no satisface el patron.

- `investigacion`
- `flujos`
- `componentes`
- `tokens`
- `accesibilidad`
- `validacion`

## Verificacion

```bash
python3 -c "import json; json.load(open('design-tokens.json'))"
```

Ese comando pasando es la definicion de "terminado" para vos.

## Convenciones que tenes que respetar

- Un solo ecosistema: no declares librerias de otro lenguaje ni mezcles gestores de paquetes.
- Toda libreria que uses tiene que estar declarada en el manifiesto de dependencias.
- Todo import declarado tiene que usarse; todo tipo usado tiene que existir o venir de una dependencia declarada.
- El patron es **Design Thinking con doble diamante + sistema de diseño basado en componentes**: los contratos (interfaces, puertos) los define la capa interna y los implementa la externa, nunca al revés.
- Los archivos que crees llevan implementacion real, no stubs: sin `TODO`, sin cuerpos vacios, sin `// getters y setters`.

## Contexto del candidato

Sirve para calibrar el nivel del codigo, no para resolver las fases.

- Perfil: Chapter Diseño de soluciones, Especialidad Product Designer, Tecnología Figma, Advanced
- Brecha que el reto ataca: Especifica los componentes con todos sus estados y aplica criterios de accesibilidad verificables
- Mision: Diseñar el flujo de apertura de cuenta

---

*Generado por Challenge Generator — Pragma. `README.md` tiene el enunciado completo del reto para la persona. `PROMPT_MEJORA.md` es la variante para pegar en un chat, si se prefiere ese flujo.*
