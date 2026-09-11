# Métricas de Usabilidad para el Flujo de Apertura de Cuenta

## Introducción y Marco Conceptual

Este documento establece el framework de métricas de usabilidad para evaluar el diseño del flujo de apertura de cuenta bancaria móvil. Las métricas propuestas permiten medir tanto la eficiencia del proceso como la satisfacción del usuario, proporcionando datos cuantificables para iteraciones de diseño futuras y validación contra los criterios de éxito del proyecto.

Las métricas se organizan en cuatro categorías principales: métricas de rendimiento (eficacia y eficiencia), métricas de errores, métricas de satisfacción y métricas de accesibilidad. Cada categoría incluye indicadores específicos con metodología de medición y umbrales de aceptación.

## 1. Métricas de Rendimiento

### 1.1 Tasa de Finalización (Conversion Rate)

**Definición**: Porcentaje de usuarios que inician el flujo de apertura de cuenta y lo completan exitosamente hasta la confirmación final.

**Fórmula**: (Usuarios que completan el flujo / Usuarios que inician el flujo) × 100

**Umbral de aceptación**: >= 65% para la versión inicial, objetivo >= 75%

**Metodología de medición en producción**:
- Implementar tracking de eventos en cada paso del flujo (evento "flow_started", evento "flow_completed", evento "flow_abandoned")
- Utilizar herramienta de analytics (Firebase Analytics, Amplitude o similar) para capturar el funnel completo
- Segmentar por fuente de tráfico, dispositivo y tipo de usuario (nuevo vs recurrente)
- Calcular tasa semanal con ventana móvil de 7 días para identificar tendencias

**Análisis de funnels**:
- Generar reporte de funnel que muestre conversión entre cada paso
- Identificar pasos con mayor caída (drop-off) y analizar causas raíz
- Comparar tasas de conversión entre versiones de diseño mediante tests A/B

### 1.2 Tiempo Promedio de Completado

**Definición**: Tiempo medio que tarda un usuario en completar todos los pasos del flujo desde el inicio hasta la confirmación final.

**Fórmula**: Sumatoria(tiempo_fin - tiempo_inicio) / Número de completaciones

**Umbral de aceptación**: <= 5 minutos para flujo completo, objetivo <= 3.5 minutos

**Metodología de medición en producción**:
- Registrar timestamps en cada transición de paso del flujo
- Excluir tiempo de inactividad mayor a 30 segundos (considerado como abandono temporal)
- Calcular percentiles: P50 (mediana), P90 para identificar usuarios que requieren más tiempo
- Segmentar por tipo de dispositivo (iOS vs Android) y por experiencia previa del usuario

**Factores de contexto**:
- Medir también tiempo por paso individual para identificar cuellos de botella
- Comparar tiempo entre usuarios que completan en primer intento vs usuarios que cometen errores
- Registrar tiempo de carga de cada pantalla para identificar problemas de rendimiento

### 1.3 Tasa de Abandonos por Paso

**Definición**: Porcentaje de usuarios que abandonan el flujo en cada paso específico, sin completarlo ni retomarlo en 24 horas.

**Fórmula**: (Usuarios que abandonan en paso N / Usuarios que llegan al paso N) × 100

**Umbral de aceptación**: <= 15% por paso, con máximo 25% en pasos de validación de identidad

**Metodología de medición en producción**:
- Crear evento de "step_entered" para cada paso del flujo
- Definir abandono como usuario que no completa el siguiente paso en 24 horas
- Utilizar dashboards de analytics con visualización de embudo
- Alertas automáticas cuando la tasa de abandono exceda el umbral en 20%

**Pasos críticos a monitorear**:
- Paso 1: Selección de tipo de cuenta (tasa esperada < 5%)
- Paso 2: Ingreso de datos personales (tasa esperada < 10%)
- Paso 3: Validación de identidad (tasa esperada < 20%)
- Paso 4: Configuración de credenciales (tasa esperada < 8%)
- Paso 5: Confirmación y términos (tasa esperada < 5%)

### 1.4 Velocidad de Carga por Pantalla

**Definición**: Tiempo que tarda cada pantalla del flujo en estar completamente interactiva.

**Umbral de aceptación**: < 2 segundos para carga inicial, < 500ms para transiciones entre pasos

**Metodología de medición en producción**:
- Utilizar Web Vitals (LCP, FID, CLS) para web mobile
- Implementar Firebase Performance o Crashlytics para aplicaciones nativas
- Medir desde que el usuario toca el botón hasta que la pantalla responde
- Registrar condiciones de red (4G, 3G, WiFi) para análisis de rendimiento real

## 2. Métricas de Errores

### 2.1 Tasa de Errores por Paso

**Definición**: Número promedio de errores que comete un usuario en cada paso del flujo.

**Fórmula**: Total de errores en paso N / Usuarios que completaron el paso N

**Umbral de aceptación**: < 0.5 errores por usuario por paso, objetivo < 0.2

**Metodología de medición en producción**:
- Registrar evento de "validation_error" cada vez que el sistema rechaza un ingreso
- Categorizar errores por tipo: formato, obligatoriedad, validación de negocio
- Crear dashboard de heatmap de errores por campo del formulario
- Analizar correlación entre errores y tiempo de completación

**Categorías de errores a trackear**:
- Errores de formato (email inválido, teléfono mal formado)
- Errores de validación (documento ya registrado, correo duplicado)
- Errores de longitud (campo muy corto o muy largo)
- Errores de carga de documentos (imagen borrosa, formato no soportado)

### 2.2 Tasa de Reintentos

**Definición**: Porcentaje de usuarios que deben intentar más de una vez una acción específica.

**Umbral de aceptación**: < 10% para acciones simples, < 25% para carga de documentos

**Metodología de medición en producción**:
- Trackear intentos de carga de documento de identidad
- Registrar intentos de validación de rostro/biometría
- Medir intentos de ingreso de credenciales (para flujos con login)
- Comparar tasas de reintento entre métodos de autenticación

### 2.3 Tiempo de Recuperación de Error

**Definición**: Tiempo promedio que tarda un usuario en resolver un error y continuar con el flujo.

**Fórmula**: Sumatoria(tiempo_resolución) / Número de errores resueltos

**Umbral de aceptación**: < 30 segundos para errores simples, < 60 segundos para errores complejos

**Metodología de medición en producción**:
- Medir tiempo desde que aparece el mensaje de error hasta que el usuario realiza una nueva acción
- Identificar si el usuario requiere ayuda externa (chat, llamada) para resolver
- Analizar si errores recurrentes indican problemas de diseño del formulario

### 2.4 Tasa de Abandono Post-Error

**Definición**: Porcentaje de usuarios que abandonan el flujo después de recibir un mensaje de error.

**Fórmula**: (Usuarios que abandonan tras error / Usuarios que reciben error) × 100

**Umbral de aceptación**: < 15%, objetivo < 8%

**Metodología de medición en producción**:
- Cruzar eventos de error con eventos de abandono
- Segmentar por tipo de error para identificar los más problemáticos
- Comparar tasas entre versiones de mensajes de error

## 3. Métricas de Satisfacción

### 3.1 System Usability Scale (SUS)

**Definición**: Escala estandarizada de 10 preguntas para medir la usabilidad percibida del sistema.

**Umbral de aceptación**: Score >= 68 (por encima de la media de 68 puntos), objetivo >= 75

**Metodología de aplicación**:
- Enviar encuesta SUS vía email within 48 horas después de completar el flujo
- Ofrecer incentivo (descuento en primera mensualidad) para aumentar tasa de respuesta
- Target de respuestas: mínimo 100 respuestas por versión para validez estadística
- Calcular score usando metodología estándar de Brooke (1996)

**Preguntas SUS a incluir**:
1. Creo que me gustaría usar este sistema frecuentemente
2. Encontré el sistema innecesariamente complejo
3. Pensé que el sistema era fácil de usar
4. Creo que necesitaría ayuda de una persona técnica para usar este sistema
5. Encontré que las diversas funciones del sistema estaban bien integradas
6. Pensé que había demasiadas inconsistencias en el sistema
7. Imagino que la mayoría de las personas aprenderían a usar este sistema rápidamente
8. Encontré el sistema muy difícil de usar
9. Me sentí muy seguro usando el sistema
10. Necesité aprender mucho antes de poder comenzar con este sistema

### 3.2 Net Promoter Score (NPS)

**Definición**: Métrica de lealtad del cliente que mide la probabilidad de recomendar el servicio.

**Umbral de aceptación**: NPS >= 30, objetivo >= 45

**Metodología de aplicación**:
- Pregunta: "En una escala de 0 a 10, ¿qué tan probable es que recomiendes esta app a un amigo o familiar?"
- Segmentar respuestas: Detractores (0-6), Pasivos (7-8), Promotores (9-10)
- Calcular: NPS = % Promotores - % Detractores
- Enviar junto con encuesta SUS para reducir fatiga del usuario

### 3.3 Customer Satisfaction (CSAT)

**Definición**: Medida directa de satisfacción con puntos específicos del proceso.

**Umbral de aceptación**: >= 4.0 sobre 5.0 en cada paso medido

**Metodología de aplicación**:
- Pregunta de satisfacción tras cada paso principal del flujo
- Escala: 1 (Muy insatisfecho) a 5 (Muy satisfecho)
- Incluir pregunta abierta opcional: "¿Qué podríamos mejorar?"
- Analizar correlación entre CSAT por paso y tasa de abandono

### 3.4 Indicador de Esfuerzo del Usuario (UEQ)

**Definición**: Métrica que mide la facilidad percibida de uso del sistema.

**Umbral de aceptación**: Score >= 0.8 en escala de -3 a +3, objetivo >= 1.5

**Metodología de aplicación**:
- Utilizar el cuestionario UEQ (User Experience Questionnaire)
- Evaluar seis dimensiones: atractividad, perspicuidad, eficiencia, dependabilidad, Stimulation, novelidad
- Aplicar tras completación del flujo con máximo 12 preguntas

## 4. Métricas de Accesibilidad

### 4.1 Contraste de Color

**Definición**: Relación de contraste entre texto y fondo en todos los elementos del flujo.

**Umbral de aceptación**: Ratio mínimo 4.5:1 para texto normal, 3:1 para texto grande (WCAG 2.1 AA)

**Metodología de medición**:
- Auditoría automática con axe DevTools o Lighthouse
- Verificación manual con herramienta de simulación de daltonismo
- Testear en modo de alto contraste del sistema operativo
- Documentar áreas que no cumplen y planificar corrección

### 4.2 Navegación por Teclado

**Definición**: Capacidad de completar todo el flujo usando únicamente teclado.

**Umbral de aceptación**: 100% de los elementos interactivos accesibles por teclado

**Metodología de medición**:
- Testing manual: navegar todo el flujo con Tab, Shift+Tab, Enter, Escape
- Verificar orden lógico de enfoque (de izquierda a derecha, arriba abajo)
- Asegurar indicador de foco visible en todos los elementos
- Auditoría automatizada con axe-core o Accessibility Insights

### 4.3 Compatibilidad con Lectores de Pantalla

**Definición**: Capacidad de completar el flujo usando tecnologías de asistencia.

**Umbral de aceptación**: Sin errores críticos en VoiceOver (iOS) y TalkBack (Android)

**Metodología de medición**:
- Testing con VoiceOver en iOS y TalkBack en Android
- Verificar que todos los campos tengan etiquetas asociadas
- Confirmar que los mensajes de error se anuncien correctamente
- Probar con diferentes velocidades de voz

### 4.4 Tamaño de Objetivos Táctiles

**Definición**: Área de interacción mínima para elementos tocables.

**Umbral de aceptación**: Mínimo 44x44 píxeles (WCAG 2.1 SC 2.5.5)

**Metodología de medición**:
- Auditoría con Accessibility Inspector en Xcode / uiautomatorviewer en Android
- Verificar espaciado entre objetivos táctiles (mínimo 8px entre elementos)
- Testing con dispositivos reales de diferentes tamaños

## 5. Dashboard y Monitoreo

### 5.1 KPIs Principales

| Métrica | Frecuencia | Responsable | Alerta |
|---------|------------|-------------|--------|
| Tasa de finalización | Diaria | Product Manager | < 50% |
| Tiempo promedio | Semanal | UX Researcher | > 6 min |
| Tasa de errores | Diaria | Developer | > 20% |
| SUS Score | Quincenal | UX Lead | < 60 |
| NPS | Mensual | Product Manager | < 20 |
| Accesibilidad | Por release | Accessibility Lead | 0 errores críticos |

### 5.2 Herramientas Recomendadas

- **Analytics**: Firebase Analytics, Amplitude o Mixpanel
- **Heatmaps**: Hotjar o Microsoft Clarity
- **Testing de accesibilidad**: axe DevTools, Accessibility Insights, WAVE
- **Encuestas**: Typeform, Google Forms o SurveyMonkey
- **Dashboards**: Looker, Data Studio o Power BI

## 6. Plan de Implementación

### Fase 1 (Semanas 1-2): Setup de tracking
- Implementar eventos de analytics en cada paso del flujo
- Configurar dashboards iniciales
- Definir líneas base de las métricas

### Fase 2 (Semanas 3-4): Medición inicial
- Recolectar datos durante 2 semanas
- Calcular métricas de línea base
- Identificar áreas críticas

### Fase 3 (Semanas 5-8): Iteración
- Priorizar mejoras según datos
- Implementar cambios de diseño
- Medir impacto con tests A/B

### Fase 4 (Semanas 9-12): Optimización continua
- Monitoreo semanal de métricas
- Ajustes finos basados en feedback
- Documentar aprendizajes

## Conclusión

El framework de métricas propuesto proporciona una visión completa del rendimiento del flujo de apertura de cuenta desde múltiples perspectivas. La combinación de métricas cuantitativas (tasa de conversión, tiempo de completado, errores) con métricas cualitativas (SUS, NPS, CSAT) permite tomar decisiones de diseño basadas en evidencia y medir el impacto de las iteraciones de manera objetiva.

Es fundamental establecer un proceso de revisión de métricas con frecuencia mínima semanal para métricas de rendimiento y mensual para métricas de satisfacción, asignando responsables claros para cada área de mejora identificada.