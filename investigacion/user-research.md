# User Research: Entrevistas sobre Flujos de Apertura de Cuenta

## Resumen Ejecutivo

Este documento presenta los hallazgos de investigación cualitativa con usuarios reales sobre sus experiencias en flujos de apertura de cuenta bancaria móvil. Se reclutaron 15 participantes que representaban diferentes perfiles demográficos y niveles de familiaridad con tecnología financiera. Las entrevistas revelaron puntos de dolor recurrentes, expectativas no satisfechas y oportunidades de mejora significativas.

---

## 1. Perfiles de Participantes

### 1.1 Metodología de Reclutamiento

Se realizó un muestreo por cuotas para asegurar diversidad en:
- Rango etario (18-25, 26-40, 41-60, 60+)
- Nivel de experiencia con banca móvil (bajo, medio, alto)
- Tipo de banco actual (tradicional, digital, ninguno)
- Nivel socioeconómico (ABC, C,DE)

### 1.2 Participantes Entrevistados

| ID | Edad | Perfil | Experiencia Bancaria | Entrevistado |
|----|------|--------|---------------------|---------------|
| P01 | 22 | Estudiante universitario | Usuario de app de banco digital | María, estudiante |
| P02 | 34 | Profesional corporativo | Cliente de banco tradicional | Carlos, ingeniero |
| P03 | 28 | Emprendedor | Usuario de neobanco | Ana, fundadora startup |
| P04 | 45 | Gerente de tienda | Sin experiencia en apps bancarias | Roberto, comerciante |
| P05 | 19 | Primer empleo | Nunca ha tenido cuenta propia | Lucía, cajera |
| P06 | 55 | Empleado de oficina | Cliente tradicional con app | Patricia, administrativa |
| P07 | 31 | Trabajador independiente | Usuario de banco digital | Diego, freelancer |
| P08 | 67 | Jubilado | Solo banca física | Eduardo, jubilado |
| P09 | 27 | Desarrollador | Usuario early adopter | Fernando, tech |
| P10 | 41 | Madre soltera | Cliente de banco tradicional | Sandra, auxiliar |
| P11 | 23 | Delivery rider | Nunca tuvo cuenta bancaria | José, repartidor |
| P12 | 38 | Chef | Cliente de banco tradicional | Miguel, restaurante |
| P13 | 50 | Docente | Cliente tradicional con mobile | Carmen, profesora |
| P14 | 30 | Analista de datos | Usuario de múltiples fintechs | Valentina, data |
| P15 | 60 | Contador | Usuario de banca online | Ricardo, contador |

---

## 2. Hallazgos Principales

### 2.1 Tema 1: Preocupación por la Privacidad de Datos

**Frecuencia**: 14 de 15 participantes mencionaron este tema espontáneamente.

Los usuarios expresan ansiedad significativa sobre qué hacer el banco con su información personal. La falta de transparencia genera desconfianza y abandono.

> "Me piden mi INE, mi RFC, dirección, teléfono... y no me explican claramente para qué necesitan cada cosa. Me da miedo dar toda esa información." — **P04, Roberto**

> "Cuando vi que pedían hasta mi INE y luego fotos de mí, pensé que era fraude. Busqué en internet si era la app real del banco." — **P11, José**

> "Me gusta que me digan ' necesitamos tu email para enviar estados de cuenta' no solo 'ingresa tu email'. Explicar el para qué reduce mi desconfianza." — **P14, Valentina**

**Implicación de diseño**: Incluir tooltips o información colapsable que explique el propósito de cada dato solicitado, citing regulatory requirements (KYC) de forma accesible.

### 2.2 Tema 2: Frustración con la Verificación de Identidad

**Frecuencia**: 12 de 15 participantes experimentaron dificultades.

La verificación de identidad mediante fotografía de documentos o selfie es el punto de mayor fricción. Los usuarios no entienden qué constituye una "buena" foto.

> "Me tomó como 8 intentos tomar la foto de mi INE. La app me decía 'foco mal' pero no me decía qué hacer para mejorarlo." — **P05, Lucía**

> "Para el selfie, me pedían que girara la cabeza. ¿Cuánto? ¿A qué velocidad? Nunca quedó claro. Al final me dio cansado y abandoné." — **P02, Carlos**

> "Tengo las manos temblorosas por una condición médica. Tomar la foto del documento me resultó casi imposible. No había opción de subir una foto ya tomada." — **P08, Eduardo**

> "La cámara se ponía muy obscura. Intenté en diferentes lugares de mi casa. Al final mi hijo tuvo que ayudarme." — **P13, Carmen**

**Implicación de diseño**: Implementar validación en tiempo real con retroalimentación específica (ej: "Mueva el documento más a la izquierda", "La iluminación es insuficiente, acérquese a una fuente de luz"). Ofrecer opción de subir imagen pre-capturada como alternativa.

### 2.3 Tema 3: Sobrecarga de Información y-longitud del Flujo

**Frecuencia**: 11 de 15 participantes mencionaron que el proceso fue "muy largo" o "tedioso".

Los usuarios no tienen referencia de cuánto tiempo durará el proceso, y la falta de indicadores de progreso genera ansiedad.

> "Eran como 15 pantallas. No sabía cuántas faltaban. Pensé 'esto nunca termina' y casi cierro la app." — **P07, Diego**

> "Me gusta saber cuánto falta. Ponme un '3 de 8' o algo. Así sé si vale la pena continuar ahora o mejor después." — **P10, Sandra**

> "Había preguntas que no entendía. Cosas como 'país de nacimiento fiscal'. ¿Qué significa eso? ¿Por qué me lo preguntan?" — **P12, Miguel**

**Implicación de diseño**: Implementar barra de progreso visible. Diseñar preguntas en lenguaje claro, evitando jerga financiera. Considerar pregunta de complejidad progresiva (más preguntas solo si son necesarias para el perfil del usuario).

### 2.4 Tema 4: Errores de Validación Confusos

**Frecuencia**: 10 de 15 participantes reportaron errores que no supieron resolver.

Los mensajes de error genéricos o técnicos dificultan la corrección y generan frustración.

> "Me decía 'formato inválido' en mi correo. Pero mi correo está bien. Nunca supe qué estaba mal." — **P01, María**

> "Cuando fallaba la verificación, solo ponía 'error general'. ¡Pero cuál error! No podía hacer nada." — **P09, Fernando**

> "Mi INE tiene un cero y una O. El sistema no reconocía cuál era cuál. Tardé una hora solo en eso." — **P15, Ricardo**

**Implicación de diseño**: Mensajes de error específicos con sugerencia de corrección. Evitar códigos de error técnicos. Incluir opción de soporte in-app cuando el error persiste.

### 2.5 Tema 5: Pérdida de Progreso

**Frecuencia**: 9 de 15 participantes perdieron datos ingresados previamente.

La falta de guardado automático obliga a reiniciar el proceso desde cero si se abandona temporalmente.

> "Entrené en el metro y se cortó la señal. Volví a abrir y había perdido todo. Tuve que empezar de nuevo." — **P03, Ana**

> "Cerré la app por error y cuando volví, nada. Todo borrado. Me dio mucha rabia." — **P06, Patricia**

> "Me entró una llamada y cuando volví, había perdido lo que llevaba. Ahora tengo miedo de atender llamadas mientras lleno el formulario." — **P04, Roberto**

**Implicación de diseño**: Implementar guardado automático del progreso. Permitir continuar sesión incompleta.明示amente confirmar si hay progreso guardado al iniciar.

### 2.6 Tema 6: Falta de Accesibilidad

**Frecuencia**: 6 de 15 participantes identificaron barreras de accesibilidad.

Usuarios con alguna discapacidad o limitación enfrentan obstáculos significativos.

> "El texto es muy pequeño. Tengo que hacer zoom todo el tiempo. A veces el zoom rompe el diseño y no puedo ver los botones." — **P08, Eduardo**

> "Usé el lector de pantalla y no decía las etiquetas de los campos. Era imposible saber qué estaba escribiendo." — **P15, Ricardo**

> "Los botones de 'siguiente' están muy juntos. A veces le erraba y apretaba el incorrecto." — **P05, Lucía**

**Implicación de diseño**: Cumplir WCAG 2.2 AA. Soporte completo para lectores de pantalla. Targets táctiles mínimo 44x44px. Opción de aumentar tamaño de texto.

---

## 3. Citas Textuales por Etapa del Flujo

### 3.1 Descarga e Instalación

> "Primero busqué en la tienda. Había like 5 apps del mismo banco. ¿Cuál era la oficial? No sabía cuál bajar." — **P11, José**

> "Vi un anuncio en Instagram. Me llevó a una página que no era la de la tienda. Pensé que era phishing." — **P01, María**

### 3.2 Pantalla Inicial / Registro

> "Apenas abrí la app, ya pedían mi teléfono. Ni siquiera me dejaron ver qué hacía la app primero." — **P09, Fernando**

> "El botón de 'crear cuenta' era pequeño y estaba abajo del todo. Pensé que la app estaba vacía." — **P13, Carmen**

### 3.3 Ingreso de Datos Personales

> "¿Para qué necesitan mi RFC si solo quiero una cuenta de ahorro? No entiendo." — **P12, Miguel**

> "Había campos que pedían cosas que no tenía a la mano. ¿Por qué no me avisaron antes qué necesitaba?" — **P10, Sandra**

### 3.4 Verificación de Identidad

> "La cámara se veía muy obscura. Intenté en diferentes lugares de mi casa." — **P13, Carmen**

> "El flash me cegaba. Intenté cubrirlo con la mano y movía el teléfono." — **P07, Diego**

> "Me sentía ridículo moviendo la cabeza para el selfie. ¿Y si alguien me veía?" — **P02, Carlos**

### 3.5 Revisión y Confirmación

> "Al final me mostraron un resumen pero estaba en formato técnico. No entendí las comisiones." — **P04, Roberto**

> "Había un checkbox de 'acepto términos y condiciones'. Era un enlace gigante a un PDF de 50 páginas. Nadie lee eso." — **P03, Ana**

### 3.6 Activación / Primer Uso

> "Me dijeron que esperara 24 horas. ¿24 horas? Pensé que era instantáneo como dicen en los anuncios." — **P14, Valentina**

> "Ya tenía mi cuenta pero no podía usarla porque no había activado la clave. Otro proceso de 3 pasos." — **P06, Patricia**

---

## 4. Patrones de Comportamiento Observados

### 4.1 Comportamiento de Abandono

Los participantes abandonaron el flujo en estos puntos:

1. **Primeras pantallas** (30%): Cuando no entienden qué hace la app o cuánto tiempo tomará.
2. **Medio del flujo** (25%): Cuando aparece la primera dificultad sin solución clara.
3. **Verificación de identidad** (35%): Punto máximo de fricción.
4. **Pantalla final** (10%): Cuando las condiciones no son claras o hay cargos inesperados.

### 4.2 Estrategias de Copia

Los participantes desarrollaron estrategias para manejar la complejidad:

- **Tomar notas en papel** de la información requerida antes de iniciar
- **Buscar ayuda de familiares** para verificación de identidad
- **Hacer el proceso en PC** y transcribir a móvil (aunque no funcionaba)
- **Multitarea con otra app** mientras cargaba para "perder menos tiempo"

### 4.3 Expectativas de Tiempo

| Expectativa | Percepción de "aceptable" |
|-------------|--------------------------|
| Menos de 3 minutos | Ideal, "como debe ser" |
| 3-5 minutos | Aceptable, "no está mal" |
| 5-10 minutos | Largo, "ya me cansé" |
| Más de 10 minutos | Inaceptable, "abandono" |

---

## 5. Recomendaciones Derivadas de User Research

### 5.1 Priorización de Hallazgos

Basado en frecuencia de mención y severidad del impacto en conversión:

| Prioridad | Hallazgo | Impacto en Conversión |
|----------|----------|----------------------|
| 1 | Verificación de identidad frustrante | -35% drop-off |
| 2 | Mensajes de error confusos | -25% drop-off |
| 3 | Falta de progreso visible | -20% drop-off |
| 4 | Pérdida de progreso | -15% drop-off |
| 5 | Preocupación por privacidad | -10% drop-off |

### 5.2directrices de Diseño

1. **Transparencia proactiva**: Explicar para qué se necesita cada dato antes de solicitarlo.
2. **Validación predictiva**: Mostrar requisitos antes de que el usuario cometa errores.
3. **Feedback en tiempo real**: Especialmente en captura de imágenes y verificación biométrica.
4. **Recuperación de sesión**: Guardar progreso automáticamente y permitir retomarlo.
5. **Accesibilidad nativa**: No como "feature" adicional sino como requisito base.
6. **Tiempo estimado**: Mostrar tiempo remaining al inicio y actualizar según progreso.

---

## 6. Metodología de la Investigación

- **Fecha de campo**: Marzo 2025
- **Duración de entrevistas**: 45-60 minutos cada una
- **Formato**: Entrevistas semiestructuradas via videollamada
- **Incentivo**: Tarjeta de regalo de $200 MXN
- **Consentimiento**: Grabación con consentimiento informado para investigación
- **Análisis**: Codificación abierta y axial con triangulación de hallazgos