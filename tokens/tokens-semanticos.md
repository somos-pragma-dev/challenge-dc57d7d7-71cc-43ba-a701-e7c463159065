# Tokens Semánticos del Sistema de Diseño

## Propósito y Arquitectura

Este documento describe la semántica y aplicación de cada token de diseño en el sistema, estableciendo la fuente única de verdad para todas las decisiones de estilo en la aplicación de apertura de cuenta bancaria. Los tokens siguen un nomenclatura semántica que describe su propósito funcional, no su apariencia visual, facilitando el mantenimiento y la consistencia a través de cambios de marca o temas.

---

## 1. Tokens de Color

### 1.1 Paleta Primaria

La paleta primaria representa la identidad de marca y se utiliza para acciones principales, elementos de navegación clave y estados de énfasis.

| Token | Aplicación | Relación WCAG |
|-------|------------|---------------|
| `color.primary.500` | Color principal de botones CTA, iconos de marca | Ratio 4.62:1 sobre blanco |
| `color.primary.600` | Fondo de botones primarios activos | Ratio 5.35:1 sobre blanco |
| `color.primary.700` | hover de botones primarios | Ratio 6.32:1 sobre blanco |
| `color.primary.900` | Texto sobre fondos claros en áreas de énfasis | Ratio 15.89:1 sobre blanco |

**Ejemplo de implementación en componente:**
```css
.btn--primary {
  background-color: var(--color-primary-600);
  color: var(--color-neutral-white);
}
.btn--primary:hover {
  background-color: var(--color-primary-700);
}
```

### 1.2 Paleta Secundaria

La paleta secundaria complementa la primaria para acciones secundarias, estados de éxito y elementos decorativos que requieren distinción visual de la acción principal.

| Token | Aplicación | Notas |
|-------|------------|-------|
| `color.secondary.500` | Indicadores de éxito, estados completados | Verde banco tradicional |
| `color.secondary.700` | Texto de confirmación en estados de éxito | Alto contraste |
| `color.secondary.900` | Iconos de verificación, badges de completado | Visibilidad máxima |

### 1.3 Tokens Semánticos de Estado

Los tokens semánticos comunican estados de retroalimentación al usuario de manera consistente en toda la aplicación.

#### Estado de Éxito (`color.semantic.success`)

- **Propósito:** Confirmar completitud, operaciones exitosas, validaciones aprobadas
- **Contraste mínimo:** 4.5:1 contra fondo
- **Uso en flujos de apertura de cuenta:**
  - Validación de documentos exitosa
  - Confirmación de datos verificados
  - Estado "cuenta creada" en pantalla final

#### Estado de Error (`color.semantic.error`)

- **Propósito:** Comunicar fallos, datos inválidos, acciones bloqueadas
- **Contraste mínimo:** 4.5:1 contra fondo
- **WCAG 2.2 AA:** El color rojo no debe ser el único medio de indicar error; siempre acompañar de icono y texto
- **Aplicaciones en el flujo:**
  - Campo de documento inválido
  - Contraseña que no cumple requisitos
  - Error de conexión con servicio
  - Límite de intentos excedido

```css
/* Componente de input con estado error */
.input--error {
  border-color: var(--color-semantic-error-border);
  background-color: var(--color-semantic-error-bg);
}
.input--error .input__message {
  color: var(--color-semantic-error-text);
}
```

#### Estado de Advertencia (`color.semantic.warning`)

- **Propósito:** Situaciones que requieren atención sin sererror
- **Aplicaciones:**
  - Sesión por expirar
  - Documentación próxima a vencer
  - Información adicional requerida

#### Estado Informativo (`color.semantic.info`)

- **Propósito:** Comunicar información contextual sin urgencia
- **Aplicaciones:**
  - Tooltips explicativos
  - Pasos completados en indicador de progreso
  - Información de ayuda contextual

---

## 2. Tokens de Tipografía

### 2.1 Familia Tipográfica

| Token | Uso | Justificación |
|-------|-----|----------------|
| `typography.font.family.primary` | Inter | Legibilidad en pantallas, soporte extenso de idiomas |
| `typography.font.family.secondary` | Roboto | Backup system, compatibilidad legacy |
| `typography.font.family.monospace` | JetBrains Mono | Números de cuenta, códigos de verificación |

### 2.2 Sistema de Escala Tipográfica

La escala sigue una progresión armónica basada en 4px, optimizada para lectura en dispositivos móviles.

| Token | Tamaño | Uso en Apertura de Cuenta |
|-------|--------|---------------------------|
| `typography.size.xs` | 12px | Labels helper, información secundaria |
| `typography.size.sm` | 14px | Texto de ayuda, captions, timestamps |
| `typography.size.base` | 16px | Cuerpo de texto principal, inputs |
| `typography.size.lg` | 18px | Subtítulos, valores destacados |
| `typography.size.xl` | 20px | Títulos de sección |
| `typography.size.2xl` | 24px | Encabezados de pantalla |
| `typography.size.3xl` | 28px | Títulos principales de paso |
| `typography.size.4xl` | 32px | Números grandes (monto a abrir) |

### 2.3 Line Height y Letter Spacing

```css
/* Títulos: línea ajustada para densidad */
h1, h2, h3 {
  line-height: var(--typography-line-height-tight);
  letter-spacing: var(--typography-letter-spacing-tight);
}

/* Cuerpo: línea cómoda para lectura */
p, span, label {
  line-height: var(--typography-line-height-normal);
  letter-spacing: var(--typography-letter-spacing-normal);
}

/* Texto monospace para datos financieros */
.account-number, .verification-code {
  font-family: var(--typography-font-family-monospace);
  letter-spacing: var(--typography-letter-spacing-wide);
}
```

---

## 3. Tokens de Espaciado

### 3.1 Sistema de Espaciado

La escala de espaciado sigue múltiplos de 4px para consistencia visual y alineación con grid de 4px.

| Token | Valor | Aplicación |
|-------|-------|------------|
| `spacing.xs` | 4px | Entre labels y contenido relacionado |
| `spacing.sm` | 8px | Padding interno de elementos pequeños |
| `spacing.md` | 16px | Padding estándar de componentes, gap entre elementos de formulario |
| `spacing.lg` | 24px | Separación entre secciones, márgenes de cards |
| `spacing.xl` | 32px | Separación entre grupos de contenido mayor |
| `spacing.2xl` | 48px | Márgenes de pantalla, separación de header/footer |

### 3.2 Aplicación en Formularios de Apertura de Cuenta

```css
.form-group {
  margin-bottom: var(--spacing-lg);
}

.form-label {
  margin-bottom: var(--spacing-xs);
}

.form-help-text {
  margin-top: var(--spacing-xs);
}

.form-actions {
  gap: var(--spacing-md);
  margin-top: var(--spacing-xl);
}
```

---

## 4. Tokens de Componentes

### 4.1 Botones

Los tokens de botón definen el comportamiento visual completo para cada variante, incluyendo todos los estados de interacción.

#### Botón Primario

```css
.btn--primary {
  background-color: var(--component-button-primary-bg);
  color: var(--component-button-primary-text);
  border-radius: var(--component-button-primary-border-radius);
  padding: var(--component-button-primary-padding-y) var(--component-button-primary-padding-x);
  height: var(--component-button-primary-height);
  font-size: var(--component-button-primary-font-size);
  font-weight: var(--component-button-primary-font-weight);
  transition: background-color var(--transition-duration-fast) var(--transition-easing-ease-out);
}

.btn--primary:hover {
  background-color: var(--component-button-primary-bg-hover);
}

.btn--primary:disabled {
  background-color: var(--component-button-primary-bg-disabled);
  color: var(--component-button-primary-text-disabled);
  cursor: not-allowed;
}

.btn--primary:focus-visible {
  outline: var(--a11y-focus-ring-width) solid var(--a11y-focus-ring-color);
  outline-offset: var(--a11y-focus-ring-offset);
}
```

**Estados del botón primario en el flujo de apertura:**

| Estado | Condición de activación | Feedback visual |
|--------|------------------------|-----------------|
| Default | Pantalla cargada, datos válidos | Fondo primary-600 |
| Hover | Cursor sobre botón | Fondo primary-700, cursor pointer |
| Active | Clic en proceso | Fondo primary-800, escala 0.98 |
| Disabled | Formulario inválido o proceso en curso | Fondo neutral-300, texto neutral-500 |
| Loading | Envío en progreso | Spinner animado, texto oculto |

### 4.2 Inputs de Formulario

Los tokens de input manejan la complejidad de validación visual necesaria para el flujo de apertura de cuenta bancaria.

```css
.input {
  background-color: var(--component-input-default-bg);
  border: 1px solid var(--component-input-default-border);
  border-radius: var(--component-input-border-radius);
  height: var(--component-input-height);
  padding: 0 var(--component-input-padding-x);
  color: var(--component-input-default-text);
  transition: border-color var(--transition-duration-fast) var(--transition-easing-ease-out);
}

.input:hover {
  border-color: var(--component-input-default-border-hover);
}

.input:focus {
  border-color: var(--component-input-default-border-focus);
  outline: none;
  box-shadow: 0 0 0 3px rgba(33, 150, 243, 0.15);
}

.input:disabled {
  background-color: var(--component-input-disabled-bg);
  border-color: var(--component-input-disabled-border);
  color: var(--component-input-disabled-text);
}

.input--error {
  border-color: var(--component-input-error-border);
  background-color: var(--component-input-error-bg);
}

.input--error:focus {
  border-color: var(--component-input-error-border-focus);
  box-shadow: 0 0 0 3px rgba(244, 67, 54, 0.15);
}
```

### 4.3 Card

```css
.card {
  background-color: var(--component-card-bg);
  border: 1px solid var(--component-card-border);
  border-radius: var(--component-card-border-radius);
  padding: var(--component-card-padding);
  box-shadow: var(--component-card-shadow);
  transition: box-shadow var(--transition-duration-normal) var(--transition-easing-ease-out);
}

.card:hover {
  box-shadow: var(--component-card-shadow-hover);
}
```

### 4.4 Progress Indicator

El indicador de progreso comunica visualmente el avance en el flujo de apertura de cuenta.

```css
.progress-bar {
  height: var(--component-progress-height);
  background-color: var(--component-progress-track);
  border-radius: var(--component-progress-border-radius);
  overflow: hidden;
}

.progress-bar__fill {
  height: 100%;
  background-color: var(--component-progress-fill);
  border-radius: var(--component-progress-border-radius);
  transition: width var(--transition-duration-slow) var(--transition-easing-ease-in-out);
}
```

---

## 5. Tokens de Accesibilidad

### 5.1 Anillo de Enfoque

WCAG 2.2 requiere indicadores de foco visibles para usuarios de teclado. El token `a11y.focus-ring` define un anillo de enfoque consistente en toda la aplicación.

```css
*:focus-visible {
  outline: var(--a11y-focus-ring-width) solid var(--a11y-focus-ring-color);
  outline-offset: var(--a11y-focus-ring-offset);
}
```

**Especificaciones:**
- Color: Primary-500 (azul brillante de alto contraste)
- Ancho: 2px
- Offset: 2px (separa el anillo del elemento)

### 5.2 Requisitos de Contraste

| Contexto | Ratio mínimo | Tokens aplicables |
|----------|--------------|-------------------|
| Texto normal | 4.5:1 | `a11y.min-contrast-normal` |
| Texto grande (18px+ bold o 24px+ regular) | 3.0:1 | `a11y.min-contrast-large` |
| Componentes UI | 3.0:1 | Bordes, fondos, iconos |

### 5.3 Targets Táctiles

WCAG 2.2 establece un tamaño mínimo de 44x44 píxeles para áreas de clic en dispositivos táctiles.

```css
button, a, input[type="checkbox"], input[type="radio"] {
  min-height: var(--a11y-touch-target-min);
  min-width: var(--a11y-touch-target-min);
}
```

---

## 6. Guía de Implementación

### 6.1 Orden de Precedencia

Al aplicar tokens en componentes, seguir este orden:

1. Tokens de componente específicos (mayor especificidad)
2. Tokens globales de color, tipografía, espaciado
3. Tokens de accesibilidad (siempre presentes)

### 6.2 Patrones de Uso

**Correcto:**
```css
.btn {
  background-color: var(--component-button-primary-bg);
  color: var(--component-button-primary-text);
  border-radius: var(--component-button-primary-border-radius);
}
```

**Incorrecto:**
```css
.btn {
  background-color: #1E88E5; /* Valor hardcodeado */
  color: #FFFFFF;
  border-radius: 8px;
}
```

### 6.3 Validación Automatizada

Integrar en pipeline CI/CD:
- Plugin de tokens de Figma para sincronización
- Linter que verifique uso de tokens (no valores hardcodeados)
- Tests de regresión visual con Axe para contraste
- Verificación de targets táctiles en componentes

---

## 7. Referencias

- WCAG 2.2: https://www.w3.org/TR/WCAG22/
- Figma Tokens Plugin: https://tokens-studio.com/
- Nielsen Norman Group - Usability Heuristics: https://www.nngroup.com/articles/ten-usability-heuristics/
- Material Design 3 Color System: https://m3.material.io/styles/color