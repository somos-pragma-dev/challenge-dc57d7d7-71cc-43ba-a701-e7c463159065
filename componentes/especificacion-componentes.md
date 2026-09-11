# Especificación de Componentes - Apertura de Cuenta Bancaria

## 1. Botones

### Button--primary
**Descripción**: Botón principal de acción para avanzar en el flujo.
**Uso**: Confirmar datos, enviar formulario, continuar al siguiente paso.

| Estado | Propiedades Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | bg: `color-bg-primary`, text: `color-text-on-primary`, border-radius: `radius-md`, padding: `spacing-md` vertical, `spacing-lg` horizontal | role="button", tabindex="0", aria-label="Continuar con la apertura de cuenta" |
| Hover | bg: `color-bg-primary-hover`, transform: scale(1.02), shadow: `shadow-md` | - |
| Focus | outline: `2px solid color-border-focus`, outline-offset: `2px` | focus visible y programático |
| Disabled | bg: `color-bg-disabled`, text: `color-text-disabled`, cursor: not-allowed | aria-disabled="true", tabindex="-1" |
| Loading | bg: `color-bg-primary`, spinner animado, text oculto | aria-busy="true", aria-label="Cargando" |
| Active | bg: `color-bg-primary-active`, transform: scale(0.98) | - |

**Criterios de accesibilidad**:
- Relación de contraste mínimo 4.5:1 para texto sobre fondo
- El foco debe ser visible en todo momento
- El botón tiene mínimo área de toque de 44x44px
- Compatible con navegación por teclado (Enter y Espacio para activar)

### Button--secondary
**Descripción**: Botón alternativo para acciones secundarias.
**Uso**: Cancelar, volver, editar información.

| Estado | Propiedades Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | bg: `color-bg-surface`, border: `1px solid color-border-secondary`, text: `color-text-secondary` | role="button", tabindex="0" |
| Hover | bg: `color-bg-surface-hover`, border-color: `color-border-hover` | - |
| Focus | outline: `2px solid color-border-focus`, outline-offset: `2px` | - |
| Disabled | opacity: 0.5, cursor: not-allowed | aria-disabled="true" |

### Button--text
**Descripción**: Botón sin fondo para acciones inline.
**Uso**: "Ya tengo cuenta", "Olvidé mi contraseña", enlaces de ayuda.

| Estado | Propiedades Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | text: `color-text-link`, text-decoration: none | role="link" |
| Hover | text-decoration: underline, color: `color-text-link-hover` | - |
| Focus | outline: `2px solid color-border-focus`, outline-offset: `2px` | - |

---

## 2. Campos de Texto (Input)

### Input__text--standard
**Descripción**: Campo de entrada de texto para datos simples.
**Uso**: Nombre, apellido, número de identificación.

| Estado | Propiedades Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | bg: `color-bg-input`, border: `1px solid color-border-input`, border-radius: `radius-sm`, padding: `spacing-md`, height: `48px` | aria-label="Nombre completo", aria-required="true" |
| Focus | border: `2px solid color-border-focus`, box-shadow: `0 0 0 3px color-shadow-focus` | aria-focus="true" |
| Filled | bg: `color-bg-input-filled` | - |
| Error | border: `2px solid color-border-error`, bg: `color-bg-error-light` | aria-invalid="true", aria-describedby="error-mensaje-id" |
| Disabled | bg: `color-bg-disabled`, border-color: `color-border-disabled`, opacity: 0.7 | aria-disabled="true", tabindex="-1" |
| Loading | - | aria-busy="true" |

**Componentes internos**:
- Label: posicionado arriba del input, text: `color-text-label`, font-weight: 500
- Helper text: debajo del input, text: `color-text-helper`, font-size: `font-size-sm`
- Error message: debajo del input, text: `color-text-error`, icon: warning

### Input__text--with-icon
**Descripción**: Campo con icono decorativo o funcional.
**Uso**: Búsqueda, visibilidad de contraseña.

| Estado | Propiedades Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | Input estándar + icono a izquierda/derecha, padding-left/right ajustado | aria-label incluye propósito del icono |
| Password toggle | Icono de ojo/ojito交叉 para mostrar/ocultar contraseña | aria-label="Mostrar contraseña", aria-pressed="false" |

### Input__textarea
**Descripción**: Campo de texto multilínea.
**Uso**: Dirección, comentarios adicionales.

| Estado | Propiedades Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | Min-height: `100px`, resize: vertical | - |
| Focus | Igual que Input__text--standard | - |

### Input__currency
**Descripción**: Campo especializado para valores monetarios.
**Uso**: Monto inicial de depósito.

| Estado | Propiedades Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | Prefix: símbolo de moneda, numeric keyboard en móvil | aria-label="Monto a depositar en pesos" |
| Valid | Border success, checkmark icon | - |

---

## 3. Selectores

### Select--dropdown
**Descripción**: Selector desplegable de opciones predefinidas.
**Uso**: Tipo de documento, género, país.

| Estado | Propiedades Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | bg: `color-bg-input`, border: `1px solid color-border-input`, border-radius: `radius-sm`, padding: `spacing-md`, chevron-down icon | role="combobox", aria-expanded="false", aria-haspopup="listbox" |
| Open | border: `2px solid color-border-focus`, dropdown con shadow `shadow-lg`, max-height: `200px` con scroll | aria-expanded="true", aria-activedescendant="opcion-seleccionada" |
| Focused option | bg: `color-bg-option-hover`, text: `color-text-option-selected` | role="option", aria-selected="true" |
| Disabled | opacity: 0.5, cursor: not-allowed | aria-disabled="true" |

**Comportamiento**:
- Click fuera cierra el dropdown
- Navegación con flechas del teclado
- Escape cierra el dropdown
- Búsqueda tipeable para listas largas (>5 items)

### RadioGroup
**Descripción**: Grupo de opciones mutuamente excluyentes.
**Uso**: Género, tipo de cuenta, preferencia de comunicación.

| Estado | Propiedades Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | Radio button custom: `20px`直径, border: `2px solid color-border-radio`, bg: white | role="radiogroup", aria-labelledby="titulo-grupo" |
| Selected | bg: `color-bg-radio-selected`, border-color: `color-border-radio-selected`, inner circle: `8px` | role="radio", aria-checked="true" |
| Hover | border-color: `color-border-radio-hover` | - |
| Focus | outline: `2px solid color-border-focus` | - |
| Disabled | opacity: 0.5 | aria-disabled="true" |

### Checkbox
**Descripción**: Casilla de verificación para opciones múltiples.
**Uso**: Aceptar términos, seleccionar preferencias.

| Estado | Propiedades Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | Custom checkbox: `20px`×`20px`, border: `2px solid color-border-checkbox`, border-radius: `radius-xs` | role="checkbox", aria-checked="false" |
| Checked | bg: `color-bg-checkbox-checked`, checkmark icon white, border-color: `color-border-checkbox-checked` | aria-checked="true" |
| Indeterminate | Square check, minus icon | aria-checked="mixed" |
| Hover | border-color: `color-border-checkbox-hover` | - |
| Focus | outline: `2px solid color-border-focus` | - |
| Disabled | opacity: 0.5 | aria-disabled="true" |

---

## 4. Componentes de Información

### Card--info
**Descripción**: Contenedor para información agrupada.
**Uso**: Datos del usuario, resumen de cuenta, información de seguridad.

| Estado | Propiedades Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | bg: `color-bg-surface`, border: `1px solid color-border-card`, border-radius: `radius-lg`, padding: `spacing-lg`, shadow: `shadow-sm` | role="region", aria-labelledby="titulo-tarjeta" |
| Elevated | shadow: `shadow-md` | - |
| Interactive | cursor: pointer, hover: shadow-md | - |

### ProgressIndicator
**Descripción**: Indicador visual del progreso en el flujo.
**Uso**: Pasos de la apertura de cuenta (1 de 4, 2 de 4, etc.).

| Estado | Propiedades Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | Pasos numerados en línea horizontal, conectores entre pasos | role="progressbar", aria-valuenow="1", aria-valuemin="1", aria-valuemax="4", aria-label="Paso 1 de 4: Información personal" |
| Completed | bg: `color-bg-success`, checkmark icon, línea conectora completada | - |
| Current | bg: `color-bg-primary`, número destacado, línea activa | aria-current="step" |
| Upcoming | bg: `color-bg-disabled`, número en gris | - |

### Alert--info
**Descripción**: Mensaje informativo contextual.
**Uso**: Recordatorios, información importante durante el flujo.

| Estado | Propiedades Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | bg: `color-bg-info-light`, border-left: `4px solid color-border-info`, icon info, padding: `spacing-md`, border-radius: `radius-sm` | role="alert", aria-live="polite" |
| Dismissible | X button a la derecha para cerrar | aria-label="Cerrar mensaje" |

### Alert--success
**Descripción**: Confirmación de acción completada.
**Uso**: Cuenta creada exitosamente, verificación enviada.

| Estado | Propiedades Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | bg: `color-bg-success-light`, border-left: `4px solid color-border-success`, icon check-circle, padding: `spacing-md` | role="alert", aria-live="polite" |

### Tooltip
**Descripción**: Información adicional en hover/focus.
**Uso**: Help text, explicaciones de campos.

| Estado | Propiedades Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | bg: `color-bg-tooltip`, text: `color-text-tooltip`, padding: `spacing-sm` `spacing-md`, border-radius: `radius-sm`, shadow: `shadow-md`, max-width: `250px` | role="tooltip", aria-describedby="elemento-asociado" |
| Visible | Opacity: 1, transition: fade-in 200ms | - |

---

## 5. Componentes de Captura Biométrica

### BiometricPrompt
**Descripción**: Interfaz para autenticación biométrica.
**Uso**: Verificación de identidad con huella o rostro.

| Estado | Propiedades Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | Icono grande de huella/rostro (64px), texto instructivo, botón de alternativa | aria-label="Autenticación biométrica", role="dialog" |
| Scanning | Animación de escaneo, texto "Coloca tu dedo" / "Mira a la cámara" | aria-busy="true" |
| Success | Icono check animado, vibración haptic feedback | - |
| Failed | Icono X, mensaje de error, retry button | aria-live="assertive" |
| Unavailable | Mensaje alternativo, fallback a código manual | - |

---

## 6. Componentes de Captura de Documentos

### DocumentCapture
**Descripción**: Interfaz para fotografiar documentos.
**Uso**: Captura de INE, pasaporte, comprobante de domicilio.

| Estado | Propiedades Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | Área de captura con guía visual (rectángulo de esquinas), ícono de cámara, texto instructivo | role="img", aria-label="Captura de documento de identificación" |
| Scanning | Overlay con animación de escaneo, líneas de guía | aria-busy="true" |
| Captured | Preview de imagen capturada, botones "Retomar" y "Confirmar" | - |
| Processing | Spinner, texto "Verificando documento" | aria-busy="true" |
| Error | Mensaje de error específico (documento ilegible, datos no reconocidos), retry button | aria-live="assertive" |

### SelfieCapture
**Descripción**: Interfaz para captura de selfie con verificación de vida.
**Uso**: Verificación facial para cumplimiento KYC.

| Estado | Parámparos Visuales | Accesibilidad |
|--------|---------------------|---------------|
| Default | Cámara frontal activa, círculo guía facial, instrucciones: "Mira a la cámara" | role="img", aria-label="Selfie para verificación de identidad" |
| Capturing | Countdown (3, 2, 1), flash de confirmación | aria-busy="true" |
| Success | Check overlay, "Verificación exitosa" | - |
| Failed | Mensaje de error, opciones: reintentar o verificación manual | aria-live="assertive" |

---

## 7. Nomenclatura BEM Aplicada

Los componentes siguen la convención BEM para facilitar su implementación en código:

```
Bloque: button, input, select, card, alert
Elemento: button__icon, input__label, select__option, card__header
Modificador: button--primary, input--error, select--disabled, card--elevated
```

**Ejemplos de clases CSS**:
- `.button--primary`
- `.button--secondary__icon`
- `.input__text--error`
- `.select__option--focused`
- `.card--info__header`
- `.alert--success__dismiss`

---

## 8. Tokens de Diseño Relacionados

Cada componente utiliza los siguientes tokens de diseño del sistema:

**Colores**:
- `color-bg-primary`: #2563EB (azul principal)
- `color-bg-primary-hover`: #1D4ED8
- `color-bg-primary-active`: #1E40AF
- `color-bg-surface`: #FFFFFF
- `color-bg-input`: #F9FAFB
- `color-bg-error-light`: #FEF2F2
- `color-bg-success-light`: #F0FDF4
- `color-bg-disabled`: #E5E7EB
- `color-text-primary`: #111827
- `color-text-secondary`: #6B7280
- `color-text-error`: #DC2626
- `color-text-success`: #16A34A
- `color-border-input`: #D1D5DB
- `color-border-focus`: #2563EB
- `color-border-error`: #DC2626

**Espaciado**:
- `spacing-xs`: 4px
- `spacing-sm`: 8px
- `spacing-md`: 16px
- `spacing-lg`: 24px
- `spacing-xl`: 32px

**Radios**:
- `radius-sm`: 4px
- `radius-md`: 8px
- `radius-lg`: 12px
- `radius-xl`: 16px

**Sombras**:
- `shadow-sm`: 0 1px 2px rgba(0,0,0,0.05)
- `shadow-md`: 0 4px 6px rgba(0,0,0,0.1)
- `shadow-lg`: 0 10px 15px rgba(0,0,0,0.1)

---

## 9. Criterios de Verificación de Accesibilidad

Todos los componentes deben pasar las siguientes verificaciones:

1. **Contraste**: Relación mínima 4.5:1 para texto normal, 3:1 para texto grande
2. **Foco visible**: Todo elemento interactivo tiene indicador de foco visible
3. **Navegación por teclado**: Todos los elementos son alcanzables y operables con teclado
4. **ARIA**: Roles, estados y propiedades correctamente implementados
5. **Etiquetas**: Todo input tiene label visible o aria-label
6. **Mensajes de error**: Descritos textualmente, no solo por color
7. **Área de toque**: Mínimo 44x44px en elementos táctiles
8. **Animaciones**: Respectar prefers-reduced-motion