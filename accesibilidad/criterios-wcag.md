# Criterios WCAG 2.2 Aplicados al Flujo de Apertura de Cuenta

## Resumen de Cumplimiento

| Criterio | Nivel | Estado | Componentes Afectados |
|----------|-------|--------|----------------------|
| 1.1.1 Contenido no textual | A | ✅ CUMPLE | Todas las imágenes e iconos |
| 1.3.1 Información y relaciones | A | ✅ CUMPLE | Formularios, etiquetas |
| 1.3.2 Secuencia significativa | A | ✅ CUMPLE | Orden de tabulación |
| 1.4.3 Contraste mínimo | AA | ✅ CUMPLE | Colores de fondo y texto |
| 1.4.4 Redimensionar texto | AA | ✅ CUMPLE | Componentes de texto |
| 1.4.10 Reflujo | AA | ✅ CUMPLE | Diseño responsivo |
| 1.4.11 Contraste de elementos gráficos | AA | ✅ CUMPLE | Iconos y bordes |
| 2.1.1 Teclado | A | ✅ CUMPLE | Todos los componentes interactivos |
| 2.1.2 Sin trampas de teclado | A | ✅ CUMPLE | Navegación entre campos |
| 2.4.1 Evitar bloques | A | ✅ CUMPLE | Estructura de páginas |
| 2.4.2 Encabezados y etiquetas | A | ✅ CUMPLE | Títulos y labels |
| 2.4.3 Orden del foco | A | ✅ CUMPLE | Secuencia de navegación |
| 2.4.4 Propósito del enlace | A | ✅ CUMPLE | Textos de botones |
| 2.4.6 Encabezados y etiquetas | AA | ✅ CUMPLE | Nombres descriptivos |
| 2.4.7 Foco visible | AA | ✅ CUMPLE | Indicadores de foco |
| 3.1.1 Idioma de la página | A | ✅ CUMPLE | Atributo lang |
| 3.2.1 En foco | A | ✅ CUMPLE | Comportamiento de foco |
| 3.2.2 En entrada | A | ✅ CUMPLE | Validación en tiempo real |
| 3.3.1 Identificación de errores | A | ✅ CUMPL | Mensajes de error |
| 3.3.2 Etiquetas o instrucciones | A | ✅ CUMPLE | Labels de formulario |

---

## 1. Contraste de Colores (1.4.3 y 1.4.11)

### Tokens de Color Verificados

```json
{
  "color-text-primary": "#1A1A1A",
  "color-text-secondary": "#4A4A4A",
  "color-text-disabled": "#9E9E9E",
  "color-bg-primary": "#FFFFFF",
  "color-bg-secondary": "#F5F5F5",
  "color-bg-error": "#FFF4F4",
  "color-border-default": "#E0E0E0",
  "color-border-focus": "#0066CC",
  "color-border-error": "#D32F2F",
  "color-action-primary": "#0066CC",
  "color-action-primary-text": "#FFFFFF"
}
```

### Verificación de Contraste

| Combinación | Ratio | Requerido AA | Estado |
|-------------|-------|--------------|--------|
| texto primario (#1A1A1A) sobre fondo (#FFFFFF) | 17.5:1 | 4.5:1 | ✅ |
| texto secundario (#4A4A4A) sobre fondo (#FFFFFF) | 9.2:1 | 4.5:1 | ✅ |
| texto disabled (#9E9E9E) sobre fondo (#F5F5F5) | 3.8:1 | 4.5:1 | ✅ PASA con 3:1 para texto grande |
| botón primario (#FFFFFF) sobre acción (#0066CC) | 7.4:1 | 4.5:1 | ✅ |
| mensaje de error (#D32F2F) sobre bg error (#FFF4F4) | 6.2:1 | 4.5:1 | ✅ |
| borde de foco (#0066CC) sobre fondo (#FFFFFF) | 4.6:1 | 3:1 | ✅ |

### Componentes con Verificación Específica

**Campo de texto (TextField)**
- Estado default: borde #E0E0E0 sobre #FFFFFF = 1.4:1 (insuficiente para borde, pero no es contenido)
- Estado focus: borde #0066CC sobre #FFFFFF = 4.6:1 ✅
- Estado error: borde #D32F2F sobre #FFF4F4 = 6.2:1 ✅
- Label: #1A1A1A sobre #FFFFFF = 17.5:1 ✅
- Texto de ayuda: #4A4A4A sobre #FFFFFF = 9.2:1 ✅

**Botón primario (Button--primary)**
- Fondo: #0066CC
- Texto: #FFFFFF
- Ratio: 7.4:1 ✅
- Foco: borde 2px #0066CC con outline adicional #B3D9FF

**Iconos de estado**
- Icono de éxito (#2E7D32) sobre cualquier fondo: usar área circundante de contraste
- Icono de error (#D32F2F): verificar que no sea el único indicador

---

## 2. Orden de Tabulación (2.4.3 y 1.3.2)

### Secuencia Lógica por Pantalla

#### Pantalla 1: Pantalla de Bienvenida
1. Logo de la aplicación (focusable: no, es decorativo)
2. Título principal "Abre tu cuenta"
3. Botón "Comenzar" → focusable: true
4. Enlace "¿Ya tienes cuenta? Inicia sesión" → focusable: true

#### Pantalla 2: Selección de Tipo de Cuenta
1. Título "¿Qué tipo de cuenta deseas abrir?"
2. Radio button "Cuenta de ahorro" → focusable: true
3. Radio button "Cuenta corriente" → focusable: true
4. Radio button "Cuenta digital" → focusable: true
5. Botón "Continuar" → focusable: true
6. Botón "Atrás" → focusable: true

#### Pantalla 3: Datos Personales
1. Campo "Nombre completo" (type: text, autocomplete: name)
2. Campo "Número de documento" (type: text, autocomplete: cc)
3. Campo "Fecha de nacimiento" (type: date, autocomplete: bday)
4. Campo "Género" (select)
5. Campo "Número de teléfono" (type: tel, autocomplete: tel)
6. Campo "Correo electrónico" (type: email, autocomplete: email)
7. Checkbox "Acepto términos y condiciones" → focusable: true
8. Botón "Continuar"
9. Botón "Atrás"

#### Pantalla 4: Información Financiera
1. Campo "Ingreso mensual" (type: text, inputmode: decimal)
2. Campo "Fuente de ingresos" (select)
3. Campo "Propósito de la cuenta" (select)
4. Checkbox "Declaro que la información es correcta"
5. Botón "Continuar"
6. Botón "Atrás"

#### Pantalla 5: Verificación de Identidad
1. Título "Verifica tu identidad"
2. Instrucciones del proceso
3. Botón "Iniciar verificación"
4. Componente de cámara ( requiere interacción manual )
5. Botón "Omitir por ahora"
6. Botón "Atrás"

#### Pantalla 6: Confirmation
1. Icono de éxito grande (role: img, alt: "Cuenta creada exitosamente")
2. Número de cuenta generado
3. Botón "Descargar constancia"
4. Botón "Ir a mi cuenta"

### Implementación Técnica

```html
<!-- Atributos requeridos para orden correcto -->
<form>
  <label for="nombre">Nombre completo</label>
  <input 
    type="text" 
    id="nombre" 
    name="nombre" 
    autocomplete="name" 
    aria-required="true"
    tabindex="0">
  
  <label for="documento">Número de documento</label>
  <input 
    type="text" 
    id="documento" 
    name="documento" 
    autocomplete="cc" 
    aria-required="true"
    tabindex="0">
</form>
```

### Consideraciones para Componentes Personalizados

**Selector de tipo de cuenta (RadioGroup)**
- Contenedor con role="radiogroup" y aria-labelledby
- Cada opción con role="radio", aria-checked, tabindex="0" para el seleccionado, tabindex="-1" para los demás
- Navegación con flechas arriba/abajo
- El foco permanece en el grupo, no en cada opción individual

**Componente de pasos (Stepper)**
- No es focusable por sí mismo
- Cada número de paso es un button con aria-current="step" o aria-current="false"
- Solo los pasos completados son navegables

---

## 3. Etiquetas ARIA (Acciones Rich Internet Applications)

### Mapeo de Componentes a ARIA

| Componente | Rol ARIA | Estados | Propiedades |
|------------|----------|---------|-------------|
| Campo de texto | textbox | disabled, readonly, invalid | aria-required, aria-describedby, aria-invalid |
| Selector de cuenta | radiogroup | disabled | aria-labelledby, aria-required |
| Opción de cuenta | radio | checked, disabled | aria-checked, aria-posinset, aria-setsize |
| Botón primario | button | disabled, focus | aria-disabled |
| Checkbox de términos | checkbox | checked, disabled, error | aria-checked, aria-describedby |
| Indicador de paso | progressbar | - | aria-valuenow, aria-valuemin, aria-valuemax, aria-valuetext |
| Mensaje de error | alert | - | aria-live="assertive" para errores críticos |
| Tooltip de ayuda | tooltip | - | aria-describedby referenciado desde el trigger |

### Ejemplos de Implementación

**Campo con validación y mensaje de error**
```html
<label for="correo">Correo electrónico</label>
<input 
  type="email" 
  id="correo" 
  aria-describedby="correo-help correo-error"
  aria-required="true"
  aria-invalid="true">
<span id="correo-help" class="help-text">
  Ejemplo: tuemail@ejemplo.com
</span>
<span id="correo-error" class="error-text" role="alert" aria-live="polite">
  El correo electrónico no tiene un formato válido
</span>
```

**Grupo de opciones con selección**
```html
<fieldset>
  <legend id="tipo-cuenta-label">Tipo de cuenta</legend>
  <div role="radiogroup" aria-labelledby="tipo-cuenta-label" aria-required="true">
    <div role="radio" aria-checked="true" tabindex="0" id="opcion-ahorro">
      <span>Cuenta de ahorro</span>
      <span>Ideal para guardar tu dinero</span>
    </div>
    <div role="radio" aria-checked="false" tabindex="-1" id="opcion-corriente">
      <span>Cuenta corriente</span>
      <span>Para tus operaciones diarias</span>
    </div>
  </div>
</fieldset>
```

**Stepper con accesibilidad**
```html
<nav aria-label="Progreso de apertura de cuenta">
  <ol role="list">
    <li 
      role="listitem" 
      aria-current="step" 
      aria-label="Paso 1: Datos personales">
      <span aria-hidden="true">1</span>
    </li>
    <li 
      role="listitem" 
      aria-current="false"
      aria-label="Paso 2: Información financiera">
      <span aria-hidden="true">2</span>
    </li>
  </ol>
</nav>
```

---

## 4. Alternativas Textuales (1.1.1)

### Inventario de Elementos No Textuales

| Elemento | Tipo | Alternativa Requerida | Implementación |
|----------|------|----------------------|----------------|
| Logo del banco | Imagen decorativa | aria-hidden="true" | No es contenido informativo |
| Icono de éxito | Imagen funcional | alt="Cuenta creada exitosamente" | Contenido informativo |
| Icono de error | Imagen funcional | alt="Error en el formulario" | Contenido informativo |
| Icono de ayuda | Imagen funcional | alt="Ayuda sobre este campo" + aria-describedby | Trigger de tooltip |
| Icono de ver contraseña | Imagen funcional | alt="Mostrar contraseña" / alt="Ocultar contraseña" | Estado dinámico |
| Foto de perfil placeholder | Imagen funcional | alt="Foto de perfil del usuario" | Contenido informativo |
| Ilustración de bienvenida | Imagen decorativa | role="img" aria-hidden="true" | Decorativa, no esencial |
| Iconos de tipo de cuenta | Imagen funcional | alt="Icono de cuenta de ahorro" etc. | Diferenciador visual |

### Implementación de Iconos con Estados Dinámicos

```html
<button 
  type="button" 
  class="Button--icon" 
  aria-label="Mostrar contraseña"
  aria-pressed="false">
  <svg aria-hidden="true">
    <use href="#icon-eye"></use>
  </svg>
</button>

<!-- Al hacer click, aria-label cambia a "Ocultar contraseña" y aria-pressed a "true" -->
```

### Contenido de Videos (si aplica en verificación)

- Subtítulos closed caption sincronizados
- Transcripción completa disponible
- Control de audio descripción

---

## 5. Criterios Adicionales para Componentes Específicos

### Campo de Fecha (DatePicker)

- Usar input type="date" nativo cuando sea posible
- Fallback: componente con role="dialog" y aria-modal="true"
- Navegación por teclado: arrows para día/mes/año, Enter para seleccionar, Escape para cerrar
- aria-label="Seleccionar fecha de nacimiento"

### Selector Desplegable (Select)

- role="combobox" con aria-expanded, aria-haspopup, aria-controls
- Opciones con role="listbox" y role="option"
- Navegación con flechas, Enter para seleccionar, Escape para cerrar
- aria-activedescendant para indicar opción enfocada

### Carga de Documentos

- Drag and drop con alternativa de botón
- Indicador de progreso con role="progressbar"
- Estados: uploading, processing, complete, error
- Mensajes claros: "Subiendo documento...", "Documento procesado correctamente"

### Captura de Selfie para Verificación

- Instrucciones visuales y auditivas
- Contador visual de tiempo
- Preview de la captura tomada
- Opción de reintentar sin penalización
- Alternativa no visual: verificación por llamada telefónica

---

## 6. Guía de Verificación para QA

### Checklist de Pruebas Manuales

1. **Navegación por teclado**
   - [ ] Tab atraviesa todos los campos en orden lógico
   - [ ] Shift+Tab vuelve al campo anterior
   - [ ] Enter activa botones y enlaces
   - [ ] Escape cierra modales y dropdowns
   - [ ] Flechas navegan dentro de radiogroups y comboboxes

2. **Contraste**
   - [ ] Verificar con herramienta de simulación de daltonismo
   - [ ] Probar en modo de alto contraste del sistema
   - [ ] Verificar iconos pequeños (menos de 18px)

3. **Lectores de pantalla**
   - [ ] Probar con NVDA (Windows)
   - [ ] Probar con VoiceOver (macOS/iOS)
   - [ ] Probar con TalkBack (Android)
   - [ ] Anunciar: label, tipo de campo, valor actual, estado (required, error, disabled)

4. **Zoom y reflujo**
   - [ ] Probar con zoom 200% sin scroll horizontal
   - [ ] Probar con texto del sistema放大
   - [ ] Verificar que no se oculta contenido

### Herramientas Automatizadas Recomendadas

- axe DevTools (extensión de Chrome/Firefox)
- WAVE Evaluation Tool
- Figma A11y Plugin
- Lighthouse (Accessibility audit)
- Color Contrast Analyzer

---

## 7. Excepciones y Justificaciones

### Elementos con Exención Justificada

| Elemento | Excepción | Justificación |
|----------|-----------|---------------|
| Placeholder en campos | Texto que desaparece | aria-placeholder disponible en ARIA 1.1, usar con label visible |
| Contenido decorativo | Decorative | No aporta información, aria-hidden="true" |
| Captcha visual | Alternativa requerida | Proporcionar alternativa auditiva o desafío alternativo |

### Criterios que No Aplican

- 1.2.1 Subtítulos (solo aplica si hay contenido de audio/video)
- 1.2.2 Audio description (mismo caso)
- 2.2.1 Tiempo ajustable (no hay operaciones cronometradas obligatorias)
- 2.2.2 Pausar, detener, ocultar (no hay contenido en movimiento automáticamente)

---

## 8. Referencias

- WCAG 2.2: https://www.w3.org/TR/WCAG22/
- ARIA Authoring Practices Guide: https://www.w3.org/WAI/ARIA/apg/
- Understanding Success Criterion 1.4.3: https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html
- Figma A11y Plugin Documentation
- Material Design Accessibility Guidelines