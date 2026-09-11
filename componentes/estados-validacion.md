# Estados de Validación y Retroalimentación - Apertura de Cuenta

## 1. Flujo de Validación en Tiempo Real

### Validación de Campos Individuales

La validación se ejecuta en tres momentos:
1. **On blur**: Cuando el usuario sale del campo
2. **On input**: Para campos con validación instantánea (email, teléfono)
3. **On submit**: Validación completa del formulario

#### Campo de Email

| Escenario | Estado | Retroalimentación Visual | Mensaje | Acción Usuario |
|-----------|--------|-------------------------|---------|----------------|
| Vacío | Default | Borde gris | - | - |
| Válido | Success | Borde verde, check icon | - | - |
| Formato inválido | Error | Borde rojo, bg-error-light | "Ingresa un correo electrónico válido" | Corregir formato |
| Dominio no permitido | Error | Borde rojo | "Este dominio no está permitido" | Usar otro email |
| Ya registrado | Error | Borde rojo | "Este correo ya está registrado. ¿Ya tienes cuenta?" | Iniciar sesión o recuperar contraseña |

#### Campo de Teléfono

| Escenario | Estado | Retroalimentación Visual | Mensaje | Acción Usuario |
|-----------|--------|-------------------------|---------|----------------|
| Vacío | Default | Borde gris | - | - |
| Válido | Success | Borde verde, check icon | - | - |
| Formato inválido | Error | Borde rojo | "El teléfono debe tener 10 dígitos" | Ingresar 10 dígitos |
| Ya registrado | Error | Borde rojo | "Este teléfono ya está registrado" | Usar otro o recuperar |

#### Campo de Contraseña

| Escenario | Estado | Retroalimentación Visual | Mensaje | Acción Usuario |
|-----------|--------|-------------------------|---------|----------------|
| Vacío | Default | Borde gris, tooltip con requisitos | "La contraseña debe tener: 8+ caracteres, 1 mayúscula, 1 número, 1 símbolo" | - |
| Muy débil | Warning | Borde naranja | "Contraseña débil. Agrega más caracteres" | Fortalecer |
| Débil | Warning | Borde amarillo | "Mejora la contraseña" | Fortalecer |
| Fuerte | Success | Borde verde, check icon | "Contraseña segura" | - |
| Cumple requisitos pero común | Warning | Borde naranja | "Esta contraseña es común. Elige otra" | Cambiar |

**Medidor de Fortaleza de Contraseña**:
```
Nivel 0 (rojo): Menos de 6 caracteres
Nivel 1 (rojo): 6-7 caracteres, sin mayúsculas ni números
Nivel 2 (naranja): 8+ caracteres, 1 tipo de carácter
Nivel 3 (amarillo): 8+ caracteres, 2 tipos de carácter
Nivel 4 (verde): 8+ caracteres, 3+ tipos de carácter + no común
```

#### Campo de Número de Identificación (INE/Pasaporte)

| Escenario | Estado | Retroalimentación Visual | Mensaje | Acción Usuario |
|-----------|--------|-------------------------|---------|----------------|
| Vacío | Default | Borde gris | - | - |
| Válido | Success | Borde verde, check icon | - | - |
| Formato inválido | Error | Borde rojo | "El formato no coincide con el tipo de documento" | Verificar formato |
| Documento vencido | Warning | Borde amarillo | "Tu documento está vencido. ¿Deseas continuar?" | Confirmar o cambiar documento |
| No legible en OCR | Error | Borde rojo, imagen del documento | "No pudimos leer el documento. Toma otra foto más clara" | Retomar foto |

---

## 2. Estados de Carga (Loading)

### Loading en Botones

Cuando una acción requiere procesamiento:

| Componente | Estado | Visual | Accesibilidad |
|------------|--------|--------|---------------|
| Button--primary | Loading | Spinner white (20px), texto oculto, bg se mantiene | aria-busy="true", aria-label="Procesando" |
| Button--secondary | Loading | Spinner primary color, texto "Procesando..." | aria-busy="true" |

**Transiciones**:
- El spinner aparece inmediatamente (no hay delay)
- El botón se deshabilita para evitar doble clic
- El cursor cambia a wait

### Loading en Campos

| Componente | Estado | Visual | Accesibilidad |
|------------|--------|--------|---------------|
| Input__text | Loading | Spinner pequeño a la derecha, border cambia a gris | aria-busy="true" |
| Select | Loading | Spinner dentro del select, opciones deshabilitadas | aria-busy="true" |
| DocumentCapture | Processing | Overlay semi-transparente, spinner central, texto "Verificando..." | aria-busy="true", aria-live="polite" |

### Skeleton Loading (Contenido que carga)

Para secciones que cargan datos:

| Componente | Visual | Uso |
|------------|--------|-----|
| Skeleton--text | Líneas grises con animación shimmer | Cargar datos del usuario |
| Skeleton--avatar | Círculo gris animado | Foto de perfil |
| Skeleton--card | Rectángulo con shimmer | Resumen de cuenta |

**Implementación**:
```css
.skeleton {
  background: linear-gradient(90deg, #E5E7EB 25%, #F3F4F6 50%, #E5E7EB 75%);
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
}
```

---

## 3. Estados de Error

### Error de Validación de Formulario

Cuando el usuario intenta enviar un formulario con errores:

| Visual | Comportamiento |
|--------|----------------|
| Scroll automático al primer campo con error | El campo recibe foco |
| Borde rojo en cada campo inválido | Primer error visible sin scroll |
| Mensajes de error debajo de cada campo | Descritos textualmente |
| Toast o banner superior | "Por favor, corrige los errores marcados" | aria-live="assertive" |

### Error de Conexión / Servidor

| Escenario | Visual | Mensaje | Acción |
|-----------|--------|---------|--------|
| Timeout | Alert--error, retry button | "Tiempo de espera agotado. Verifica tu conexión" | Botón "Reintentar" |
| Error 500 | Alert--error | "Error del servidor. Intenta más tarde" | Botón "Reintentar", opcional "Contactar soporte" |
| Sin conexión | Alert--error, icono offline | "Sin conexión a internet" | Auto-retry al detectar conexión |

### Error de Verificación Biométrica

| Escenario | Visual | Mensaje | Acción |
|-----------|--------|---------|--------|
| Huella no reconocida | Icono huella X, vibración | "No reconocimos tu huella. Intenta de nuevo" | Retry button |
| Demográficos intentos | Icono warning | "Demasiados intentos. Verifica tu identidad de otra forma" | Botón "Verificación manual" |
| Rostro no coincide | Selfie con overlay X | "El rostro no coincide con el documento" | Retry o verificar manualmente |

### Error de Captura de Documento

| Escenario | Visual | Mensaje | Acción |
|-----------|--------|---------|--------|
| Foto borrosa | Preview con indicador de calidad | "La foto está borrosa. Asegúrate de que el documento esté firme" | Botón "Retomar" |
| Documento incompleto | Guía de裁切 en rojo | "Captura todo el documento, incluyendo las esquinas" | Botón "Retomar" |
| Reflejo/Glare | Preview con área de brillo resaltada | "Hay un brillo en el documento. Evita la luz directa" | Botón "Retomar" |
| Datos no leídos | OCR con campos resaltados | "No pudimos leer algunos datos. Verifica que el texto sea legible" | Revisar y reintentar |

---

## 4. Estados de Éxito / Confirmación

### Confirmación de Campo Válido

| Componente | Visual | Timing |
|------------|--------|--------|
| Input__text | Borde verde, check icon, helper text verde | Inmediato al validar |
| Input__currency | Borde verde, formato con separadores | On blur |
| Checkbox | Checkmark animado, color success | On check |

### Confirmación de Paso Completado

| Escenario | Visual | Animación |
|-----------|--------|-----------|
| Paso completado en progress | Check icon animado, línea conecta completada | Scale + fade in 300ms |
| Verificación de documento | Success overlay con check grande | Confetti sutil, haptic feedback |
| Biometría exitosa | Check animado, texto "Verificado" | Fade in 200ms |
| Cuenta creada | Pantalla de éxito completa | Animación de celebración sutil |

### Pantalla de Éxito Final

```
┌─────────────────────────┐
│     ✓                   │
│   ¡Cuenta creada!       │
│                         │
│  Tu cuenta XXX123      │
│  está lista para usar  │
│                         │
│  [Ir a mi cuenta]       │
│                         │
│  ¿Enviar datos por     │
│  correo? [Sí] [No]     │
└─────────────────────────┘
```

**Elementos**:
- Icono check grande (64px), color success
- Título: "¡Cuenta creada!" o "¡Bienvenido!"
- Número de cuenta (parcial: XXX123)
- CTA principal: "Ir a mi cuenta"
- Acción secundaria: envío de confirmación por email

---

## 5. Micro-interacciones

### Feedback Táctil (Haptic)

| Evento | Tipo de Vibración | Uso |
|--------|-------------------|-----|
| Error de validación | Error (3 vibraciones cortas) | Campo inválido |
| Éxito de verificación | Success (1 vibrate) | Biometría, documento verificado |
| Botón presionado | Light impact | Cualquier botón |
| Selección | Selection changed | Checkbox, radio, select |

### Animaciones de Transición

| Transición | Duración | Easing | Descripción |
|------------|----------|--------|-------------|
| Error shake | 400ms | ease-in-out | Campo se sacude horizontalmente (3px cada lado) |
| Success pulse | 300ms | ease-out | Checkmark escala de 0.8 a 1.0 |
| Loading spinner | 1000ms | linear | Rotación continua |
| Fade in | 200ms | ease-out | Opacity 0 a 1 |
| Slide up | 300ms | ease-out | TranslateY 20px a 0 |

### Transiciones entre Pasos

| Escenario | Transición | Detalle |
|-----------|------------|----------|
| Avanzar | Slide left | Contenido actual sale a la izquierda, nuevo entra desde derecha |
| Retroceder | Slide right | Contenido actual sale a la derecha, anterior entra desde izquierda |
| Error en submit | Shake | Contenido actual sacude, focus en primer error |

---

## 6. Manejo de Estados Edge

### Sesión Expirada durante el Flujo

| Escenario | Visual | Comportamiento |
|-----------|--------|----------------|
| Sesión expirada | Modal con overlay | "Tu sesión expiró. Guarda tu progreso" |
| | | Botones: "Continuar después" / "Iniciar de nuevo" |
| Auto-save | Toast info | "Progreso guardado" cada 30 segundos |

### Validación de Duplicados

| Escenario | Visual | Mensaje |
|-----------|--------|---------|
| Email ya existe | Error en campo + link | "¿Ya tienes cuenta?" → "Iniciar sesión" |
| Teléfono ya existe | Error en campo + link | "Recuperar acceso" |
| CURP ya registrada | Error + banner | "Esta persona ya tiene una cuenta" |

### Límite de Intentos

| Escenario | Visual | Comportamiento |
|-----------|--------|----------------|
| 3 intentos de verificación fallidos | Modal warning | "Demasiados intentos. Te enviamos un código por SMS" |
| 5 intentos de contraseña incorrectos | Lockout 5 min | "Intenta de nuevo en X minutos" |

---

## 7. Accessibility en Estados de Validación

### Requisitos WCAG 2.2 AA

1. **Identificación de errores** (3.3.1): Los errores son identificados textualmente
2. **Etiquetas o instrucciones** (3.3.2): Los campos tienen labels claros
3. **Sugerencia de errores** (3.3.3): Los mensajes sugieren la corrección
4. **Prevención de errores** (3.3.4): Validación proactiva cuando es posible

### Implementación de ARIA

```html
<!-- Campo con error -->
<input 
  aria-invalid="true" 
  aria-describedby="error-email"
  aria-required="true"
/>
<span id="error-email" role="alert" aria-live="polite">
  Ingresa un correo electrónico válido
</span>

<!-- Botón con loading -->
<button aria-busy="true" aria-label="Creando cuenta...">
  <span class="sr-only">Creando cuenta, por favor espera</span>
</button>

<!-- Progress con estados -->
<div role="progressbar" aria-valuenow="2" aria-valuemin="1" aria-valuemax="4" aria-label="Paso 2 de 4">
```

### Orden de Lectura

Cuando hay errores múltiples:
1. El foco se mueve al primer campo con error
2. El mensaje de error se announce mediante aria-live
3. El usuario puede navegar entre errores con Tab

### Contrase y Foco

- Los errores siempre tienen color de contraste mínimo 4.5:1
- El indicador de foco no depende solo del color
- Los iconos de error tienen aria-label

---

## 8. Tokens de Diseño para Estados

### Colores de Estados

```json
{
  "color-state-default": "#D1D5DB",
  "color-state-focus": "#2563EB",
  "color-state-error": "#DC2626",
  "color-state-error-light": "#FEF2F2",
  "color-state-success": "#16A34A",
  "color-state-success-light": "#F0FDF4",
  "color-state-warning": "#D97706",
  "color-state-warning-light": "#FFFBEB",
  "color-state-disabled": "#E5E7EB"
}
```

### Mensajes de Validación

```json
{
  "message-required": "Este campo es obligatorio",
  "message-email-invalid": "Ingresa un correo electrónico válido",
  "message-password-weak": "La contraseña es muy débil",
  "message-password-requirements": "Usa 8+ caracteres con mayúsculas, números y símbolos",
  "message-phone-length": "El teléfono debe tener 10 dígitos",
  "message-document-expired": "El documento está vencido",
  "message-connection-error": "Error de conexión. Verifica tu internet",
  "message-server-error": "Error del servidor. Intenta más tarde",
  "message-biometric-failed": "No reconocimos tu biometric. Intenta de nuevo",
  "message-try-again": "Intentar de nuevo"
}
```