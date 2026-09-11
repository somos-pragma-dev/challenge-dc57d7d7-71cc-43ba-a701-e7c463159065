# Prompt para Mejorar el Codigo Base

Copia y pega el contenido del bloque de abajo en un asistente de IA (Claude, ChatGPT)
para obtener un ZIP con el proyecto completo y arrancable.

Si preferis trabajar en tu editor con un agente local (Claude Code, Cursor, Copilot), usa `AGENTS.md` en vez de este archivo: dice lo mismo pero para que escriba los archivos en disco.

## Las dos reglas que no se negocian

1. **Completa el boilerplate.** Todo lo que el proyecto necesita para compilar y arrancar: manifiesto de dependencias, punto de entrada, configuracion, capa de interfaz, y las capas del patron arquitectonico declarado. Eso es andamiaje y es tu trabajo.
2. **NO resuelvas el reto.** Los entregables de las fases son el trabajo de la persona. El hueco pedagogico se deja como esta: el proyecto arranca, pero lo que el reto pide implementar NO esta implementado.

Dicho de otra forma: si algo impide compilar, arreglalo. Si algo es logica de negocio incompleta, validaciones ausentes, un secreto hardcodeado o un patron mejorable, dejalo exactamente como esta — es lo que la persona tiene que encontrar.

## Como saber que terminaste

```bash
python3 -c "import json; json.load(open('design-tokens.json'))"
```

Ese comando corriendo sin errores es la definicion de "listo".

---

```
## Briefing del reto (autoridad)
Este bloque manda sobre los archivos adjuntos. El stack y el rol salen de AQUÍ, no de un topic genérico ni de markdown placeholder.

### Perfil
Chapter Diseño de soluciones, Especialidad Product Designer, Tecnología Figma, Advanced

### Brecha de conocimiento
Especifica los componentes con todos sus estados y aplica criterios de accesibilidad verificables

### Misión / candidato
Diseñar el flujo de apertura de cuenta

### Reto
- Tema: Diseño de flujo y componentes
- Seniority: advanced-l2
- Tipo: practical
- Título: Diseño de flujo de apertura de cuenta
- Tiempo estimado: 8 horas

### Fases (trabajo del HUMANO — PROHIBIDO completarlas)
No implementes estos entregables. Dejalos como hueco pedagógico. El asistente solo materializa el proyecto arrancable para que el participante pueda trabajar.
- Fase 1: Definición de componentes y estados — objetivo: Identificar y definir todos los componentes y sus estados necesarios para el flujo de apertura de cuenta. — entregable (NO resolver): Documento con la lista de componentes y sus estados, incluyendo criterios de accesibilidad.
- Fase 2: Diseño del flujo de usuario — objetivo: Crear un flujo de usuario que cubra todas las etapas de la apertura de cuenta, incluyendo validaciones y manejo de errores. — entregable (NO resolver): Diagrama de flujo del usuario para la apertura de cuenta, incluyendo validaciones y manejo de errores.
- Fase 3: Revisión y optimización — objetivo: Revisar y optimizar el flujo de usuario y los componentes para asegurar una experiencia de usuario óptima. — entregable (NO resolver): Documento con las mejoras y optimizaciones realizadas al flujo de usuario y los componentes.

Eres un asistente experto en análisis, corrección y generación de archivos de cualquier tipo:
código fuente, documentación, hojas de cálculo, documentos Word, configuraciones, entre otros.
Voy a enviarte una cadena de texto que contiene uno o más archivos. Cada archivo está delimitado por un marcador con el siguiente formato:
// === ARCHIVO: ruta/del/archivo.extension ===
o también puede aparecer como:
## === ARCHIVO: ruta/del/archivo.extension ===
Lo que sigue al marcador puede ser:

El contenido real del archivo (código, texto, YAML, etc.)
Una descripción en lenguaje natural de lo que debe contener el archivo


TU TAREA
PASO 0 — ¿Esto es un proyecto o una carcasa?
Antes de extraer archivos, leé el Briefing (si está) y diagnosticá el adjunto.

Es CARCASA si ocurre CUALQUIERA de estas:
- No hay manifiesto de dependencias del stack del briefing (manifest.json de VTEX IO / package.json / pom.xml / build.gradle / requirements.txt / go.mod / *.tf / *.csproj, según corresponda)
- Hay un "binario" que en realidad es un comentario ("no puede ser mostrado como texto plano", placeholder .fig/.docx vacío)
- Los markdowns ya completan entregables de fases posteriores ("se implementó fade-in", lista de áreas ya resuelta)

Si es CARCASA:
- MATERIALIZÁ un proyecto que arranca en el stack del briefing (VTEX IO Store Framework, Angular, Terraform, pytest, Nest, etc.). Incluí manifiesto, punto de entrada y capa de interfaz reales.
- NO copies los markdowns de "solución" como si fueran el producto. Son ruido de generación.
- NO resuelvas las fases del briefing (están marcadas PROHIBIDO). Dejá el hueco pedagógico: el flujo existe, las microinteracciones/calidad/infra que el reto pide NO están hechas.
- Después seguí al PASO 5 (ZIP).

Si es un proyecto REAL (manifiesto + código que compila o arranca):
- Seguí PASO 1 en adelante. 🔴 compilación sí. 🟡 pedagógico no.

PASO 1 — Detección y extracción
Identifica todos los archivos presentes en la cadena. Para cada archivo extrae:

Su ruta completa (ej: src/main/java/com/pragma/Service.java)
Su contenido o descripción

PASO 2 — Clasificación por tipo
Clasifica cada archivo en una de estas categorías:
A) Código fuente (Java, Python, TypeScript, JavaScript, Kotlin, etc.)
B) Configuración / documentación (YAML, properties, Markdown, JSON, txt, etc.)
C) Excel (.xlsx, .xls, .csv)
D) Word (.docx, .doc)
E) Otro tipo de archivo binario o especial
PASO 3 — Clasificación de errores en código fuente

Objetivo prioritario: que el proyecto compile. No corrijas flujo de negocio ni lógica funcional.

Antes de modificar cualquier archivo de código fuente, clasifica cada problema encontrado en una de estas dos categorías:
🔴 ERROR DE COMPILACIÓN — corregir siempre
Son errores que impiden que el proyecto arranque, sin valor pedagógico:

Import faltante o incorrecto
Clase, método o variable referenciada que no existe en ningún archivo del proyecto
Error de sintaxis
Anotación con atributos inválidos
Dependencia ausente en pom.xml, package.json, etc.
Archivo referenciado que no existe y debe ser creado con implementación mínima

→ CORREGIR estos errores.
🟡 PROBLEMA FUNCIONAL O DE CALIDAD — preservar siempre
Son problemas que no impiden compilar. Pueden ser intencionales para el aprendizaje:

Clave secreta hardcodeada ("secret", "password123")
API deprecada que funciona pero tiene reemplazo moderno
Lógica de negocio incorrecta o incompleta
Código redundante o de baja legibilidad
Falta de validaciones en flujo de negocio
Patrones de diseño incorrectos pero funcionales
Concurrencia no segura
Configuración funcional pero no óptima

→ PRESERVAR tal cual. No corregir, no mejorar, no comentar.
PASO 4 — Procesamiento según tipo de archivo
Tipo A — Código fuente
Aplica únicamente las correcciones clasificadas como 🔴 ERROR DE COMPILACIÓN.
No alteres ningún elemento clasificado como 🟡 PROBLEMA FUNCIONAL O DE CALIDAD.
Si falta un archivo referenciado, créalo con la implementación mínima necesaria para compilar.
Tipo B — Configuración / documentación
Extrae el contenido tal cual, sin modificaciones salvo errores evidentes de sintaxis
(ej: YAML mal indentado).
Tipo C — Excel (.xlsx)
Si viene con contenido real, genera el archivo respetando ese contenido.
Si viene con descripción en lenguaje natural, genera un archivo Excel funcional con:

Fila de encabezados en negrita con color de fondo distintivo
Columnas con ancho ajustado al contenido
Tipos de dato correctos por columna
Validaciones si la descripción lo indica
Hojas nombradas descriptivamente si hay más de una
Filas de ejemplo si no hay datos reales

Tipo D — Word (.docx)
Si viene con contenido real, genera el archivo respetando ese contenido.
Si viene con descripción en lenguaje natural, genera un documento Word funcional con:

Estilos de título (Título 1, Título 2) para jerarquía de secciones
Fuente legible (Calibri o equivalente), tamaño 11-12pt para cuerpo
Márgenes estándar
Tabla de contenido si tiene múltiples secciones
Tablas con encabezados en negrita si aplica

Tipo E — Otro
Genera el archivo con el contenido o estructura más apropiada según la descripción.
PASO 5 — Exportación en ZIP
Empaqueta todos los archivos en un único archivo ZIP descargable respetando exactamente
la estructura de rutas indicada por los marcadores.
El ZIP debe incluir:

Archivos de código con únicamente los errores de compilación corregidos
Archivos de configuración y documentación sin cambios
Archivos nuevos creados para resolver dependencias de compilación faltantes
Archivos Excel y Word generados desde descripción

IMPORTANTE: El ZIP debe estar listo para descargar al finalizar. No preguntes si el usuario
quiere generarlo. Simplemente genera el archivo y proporciona el enlace de descarga; No debes desplegar en el chat el resumen de lo que arreglaste al Zip, solo entregalo.

REGLAS IMPORTANTES

No omitas ningún archivo aunque no tenga errores ni modificaciones
Respeta los nombres y rutas exactas indicadas por los marcadores
Si un archivo no tiene marcador claro, infiere el nombre desde su contenido
Si la cadena contiene solo documentación, placeholders o binarios fake, NO la reproduzcas:
aplicá PASO 0 (materializar el proyecto del briefing). Reproducir la carcasa es un fallo.
No agregues texto después del enlace de descarga del ZIP
No preguntes si el usuario quiere el ZIP: simplemente generalo siempre
Si detectas que falta un archivo de configuración necesario para compilar
(pom.xml, package.json, requirements.txt, build.gradle, etc.), créalo e inclúyelo
inferiendo su contenido desde los imports y frameworks detectados en el código
Nunca corrijas problemas 🟡 aunque parezcan obvios o fáciles de mejorar.
El participante que recibirá este proyecto los debe encontrar y resolver él mismo.


INPUT
Aquí está la cadena con los archivos:

// === ARCHIVO: investigacion/desk-research.md ===
# Desk Research: Flujos de Apertura de Cuenta en Banca Móvil

## Resumen Ejecutivo

La apertura de cuentas bancarias a través de dispositivos móviles representa uno de los mayores desafíos de conversión en la industria fintech. Este documento compila hallazgos de investigación secundaria sobre mejores prácticas, tasas de conversión, puntos de fricción comunes y regulaciones aplicables al diseño de flujos de onboarding en aplicaciones bancarias móviles.

---

## 1. Contexto del Mercado y Estadísticas Clave

### 1.1 Tasas de Conversión en la Industria

Según estudios de Finastra (2024) y Worldpay, las tasas de conversión en flujos de apertura de cuenta bancaria móvil oscilan entre el 15% y el 35%, dependiendo de la complejidad del proceso y el nivel de confianza de la marca. Los datos clave incluyen:

| Métrica | Valor Promedio | Rango |
|---------|---------------|-------|
| Tasa de inicio de flujo | 100% | - |
| Completitud del registro | 45-65% | Depende de longitud |
| Verificación de identidad | 60-80% de quienes completan registro | Mayor fricción |
| Activación de cuenta | 70-90% post-verificación | Mayor Drop-off post-verificación |
| Tasa de conversión final | 15-35% | Benchmark industria |

### 1.2 Factores de Abandonamiento

Un estudio de J.D. Power (2024) identificó los principales motivos de abandono en flujos de apertura de cuenta:

1. **Cantidad de información requerida** (67% de abandonos): Los usuarios abandonan cuando perciben que el proceso es demasiado largo o invasivo.
2. **Tiempo de verificación de identidad** (23%): La verificación biométrica o con documentos falla frecuentemente, causando frustración.
3. **Falta de claridad sobre el uso de datos** (18%): Los usuarios desconfían cuando no se explica claramente para qué se necesitan sus datos.
4. **Errores técnicos durante el proceso** (15%): Carga lenta, pérdida de progreso, errores de validación confusos.

---

## 2. Benchmarks de Mejores Prácticas

### 2.1 Longitud Óptima del Flujo

Investigación de Baymard Institute (2024) establece que el número óptimo de pasos para un flujo de onboarding es entre 4 y 7. Más allá de 7 pasos, la tasa de abandono aumenta exponencialmente. Los flujos exitosos comparten estas características:

- **Progresivo**: La información se solicita solo cuando es necesaria.
- **Estimativo**: Se muestra el progresoremaining (ej: "Paso 2 de 5").
- **Recuperable**: El usuario puede abandonar y continuar luego sin perder progreso.
- **Transparente**: Se explica por qué se solicita cada dato.

### 2.2 Comparativa de Estrategias por Banco

**Banco Digital Tipo A (N26, Revolut):**
- Flujo de 4-5 pasos máximo
- Verificación de identidad por video selfie
- Apertura en menos de 3 minutos
- Tasa de conversión: 28-35%

**Banco Tradicional con App (BBVA, Santander):**
- Flujo de 8-12 pasos
- Verificación con documento físico + selfie
- Proceso de 10-15 minutos
- Tasa de conversión: 18-25%

**Neobanco Regional (Klar, Ualá):**
- Flujo de 5-7 pasos
- Verificación por fotografía de documento
- Proceso de 5-8 minutos
- Tasa de conversión: 22-30%

---

## 3. Marco Regulatorio Aplicable

### 3.1 KYC (Know Your Customer)

La regulación KYC exige que los bancos verifiquen la identidad de sus clientes antes de abrir una cuenta. Los elementos obligatorios típicamente incluyen:

- Nombre completo (legal)
- Fecha de nacimiento
- Dirección de residencia
- Número de identificación oficial (INE, RFC, CURP, etc.)
- En algunos casos: situación fiscal, origen de fondos

### 3.2 AML (Anti-Money Laundering)

Las normas AML requieren verificación de que los fondos no provienen de actividades ilícitas. Esto impacta el diseño del flujo al requerir:

- Declaraciones de origen de fondos
- Screening contra listas de sanciones
- Monitorización posterior a la apertura

### 3.3 GDPR/LGPD y Protección de Datos

El usuario debe ser informado claramente sobre:

- Qué datos se recopilan
- Para qué se utilizan
- Cuánto tiempo se almacenan
- Cómo pueden ejercerse los derechos de acceso, rectificación y supresión

---

## 4. Hallazgos sobre Diseño de Interacciones

### 4.1 Validación en Tiempo Real

Los estudios de Nielsen Norman Group (2024) demuestran que la validación en tiempo real reduce el tiempo de completado en un 22% y los errores de envío en un 35%. Recomendaciones clave:

- Validar email y teléfono inmediatamente tras el input
- Mostrar mensajes de error específicos, no genéricos
- Evitar validación agresiva (no marcar error hasta que el usuario abandone el campo)
- Proporcionar sugerencias de corrección, no solo el error

### 4.2 Manejo de Errores en Verificación de Identidad

La verificación de identidad es el punto de mayor drop-off. Estrategias exitosas incluyen:

- **Instrucciones claras previas**: Mostrar ejemplo de cómo tomar la foto antes de solicitarla.
- **Feedback visual inmediato**: Indicadores de calidad de imagen en tiempo real.
- **Múltiples intentos**: Permitir al menos 3 intentos antes de escalar a soporte humano.
- **Alternativas accesibles**: Offering verificación por llamada telefónica como backup.

### 4.3 Diseño para Confianza

Elementos que incrementan la percepción de seguridad (estudio de Cambridge University, 2023):

- Certificaciones de seguridad visibles (SSL, encryption badges)
- Políticas de privacidad accesibles desde el flujo
- Indicadores de progreso claros
- Lenguaje profesional pero accesible
- Ausencia de clutter visual y advertising excesivo

---

## 5. Consideraciones de Accesibilidad en Investigación

### 5.1WCAG 2.2 Aplicado a Flujos Bancarios

La accesibilidad en flujos financieros tiene implicaciones regulatorias adicionales en algunos países. Los criterios prioritarios incluyen:

- **1.3.1 Información y Relaciones**: La jerarquía del formulario debe ser semánticamente correcta.
- **3.3.1 Identificación de Errores**: Los errores deben identificarse claramente y asociarse al campo correspondiente.
- **3.3.2 Etiquetas o Instrucciones**: Cada campo debe tener label visible y accesible.
- **2.4.7 Foco Visible**: El foco debe ser claramente visible en todo momento.

### 5.2 Adaptaciones para Usuarios con Discapacidad

Estudios de AbilityNet (2024) revelan que el 12% de los usuarios de banca móvil tiene alguna discapacidad que afecta su interacción. Consideraciones:

- Soporte para lectores de pantalla en todos los campos
- Contraste mínimo de 4.5:1 para texto
- Targets táctiles de al menos 44x44 píxeles
- Alternatives textuales para cualquier contenido no textual

---

## 6. Referencias y Fuentes

1. Finastra (2024). "Digital Banking Onboarding Report"
2. J.D. Power (2024). "Banking Mobile App Satisfaction Study"
3. Baymard Institute (2024). "E-Commerce Checkout Usability Research"
4. Nielsen Norman Group (2024). "Form Design Best Practices"
5. Worldpay (2024). "Global Payments Report"
6. Cambridge University (2023). "Trust in Digital Banking"
7. AbilityNet (2024). "Digital Accessibility in Financial Services"
8. WCAG 2.2 W3C Recommendation (October 2023)
9. GDPR Regulation (EU) 2016/679
10. LGPD Law 13.709/2018 (Brazil)

---

## 7. Síntesis para Diseño del Flujo

Los hallazgos de esta investigación secondary sugieren las siguientes directrices para el diseño del flujo de apertura de cuenta:

1. **Mantener entre 4-7 pasos** para optimizar conversión
2. **Validación en tiempo real** para reducir errores y tiempo
3. **Transparencia sobre el uso de datos** para generar confianza
4. **Instrucciones claras para verificación de identidad** para reducir drop-off
5. **Diseño accesible por defecto** para cumplir WCAG 2.2 AA
6. **Múltiples intentos y alternativas** en puntos de fricción crítica
7. **Indicadores de progreso visibles** para gestionar expectativas
8. **Recuperación de progreso** para permitir abandono temporal

// === ARCHIVO: investigacion/user-research.md ===
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


// === ARCHIVO: flujos/flujo-principal.mmd ===
flowchart TD
    subgraph INICIO["Punto de Entrada"]
        A1["Pantalla de Bienvenida"] --> A2["Botón 'Abrir Cuenta'"]
    end

    subgraph REGISTRO["Fase 1: Registro Inicial"]
        B1["Pantalla de Registro"] --> B2["Campo: Correo Electrónico"]
        B2 --> B3["Campo: Contraseña"]
        B3 --> B4["Campo: Confirmar Contraseña"]
        B4 --> B5["Checkbox: Términos y Condiciones"]
        B5 --> B6{"Validación de Criterios"}
        B6 -->|Correo válido| C1
        B6 -->|Correo inválido| E1["Mensaje de Error: Correo inválido"]
        B6 -->|Contraseña débil| E2["Mensaje de Error: La contraseña debe tener al menos 8 caracteres, una mayúscula y un número"]
        B6 -->|Términos no aceptados| E3["Mensaje de Error: Debe aceptar los términos y condiciones"]
        E1 --> B2
        E2 --> B3
        E3 --> B5
    end

    subgraph VERIFICACION_IDENTIDAD["Fase 2: Verificación de Identidad (KYC)"]
        C1["Pantalla: Verificación de Identidad"] --> C2["Captura de Foto de INE/ID"]
        C2 --> C3["Captura de Selfie con verificación biométrica"]
        C3 --> C4["Validación de Documento por IA"]
        C4 --> C5{"Resultado de Verificación"}
        C5 -->|Verificación exitosa| D1
        C5 -->|Documento no legible| E4["Pantalla de Error: Documento no legible. Por favor, tome una foto más clara"]
        C5 -->|Biometría no coincide| E5["Pantalla de Error: La biometricía no coincide con el documento"]
        C5 -->|Tiempo de espera agotado| E6["Pantalla de Error: Tiempo de verificación agotado. Intente de nuevo"]
        E4 --> C2
        E5 --> C3
        E6 --> C1
    end

    subgraph DATOS_PERSONALES["Fase 3: Datos Personales"]
        D1["Pantalla: Datos Personales"] --> D2["Campo: Nombre(s)"]
        D2 --> D3["Campo: Apellido Paterno"]
        D3 --> D4["Campo: Apellido Materno"]
        D4 --> D5["Campo: Fecha de Nacimiento"]
        D5 --> D6["Campo: Género"]
        D6 --> D7["Campo: Nacionalidad"]
        D7 --> D8["Campo: CURP"]
        D8 --> D9["Campo: RFC"]
        D9 --> D10{"Validación de Datos"}
        D10 -->|Datos válidos| F1
        D10 -->|CURP inválido| E7["Error: CURP no válido"]
        D10 -->|RFC inválido| E8["Error: RFC no válido"]
        D10 -->|Menor de edad| E9["Error: Debes ser mayor de 18 años para abrir una cuenta"]
        D10 -->|Campos vacíos| E10["Error: Todos los campos son obligatorios"]
        E7 --> D2
        E8 --> D9
        E9 --> D5
        E10 --> D2
    end

    subgraph DATOS_CONTACTO["Fase 4: Datos de Contacto"]
        F1["Pantalla: Datos de Contacto"] --> F2["Campo: Calle"]
        F2 --> F3["Campo: Número Exterior"]
        F3 --> F4["Campo: Número Interior"]
        F4 --> F5["Campo: Colonia"]
        F5 --> F6["Campo: Ciudad"]
        F6 --> F7["Campo: Estado"]
        F7 --> F8["Campo: Código Postal"]
        F8 --> F9["Campo: Teléfono Móvil"]
        F9 --> F10["Campo: Teléfono Fijo (Opcional)"]
        F10 --> F11{"Validación de Dirección"}
        F11 -->|Dirección válida| G1
        F11 -->|CP no encontrado| E11["Error: Código postal no encontrado en nuestra base de datos"]
        F11 -->|Teléfono inválido| E12["Error: Formato de teléfono inválido"]
        E11 --> F2
        E12 --> F9
    end

    subgraph SELECCION_CUENTA["Fase 5: Selección de Tipo de Cuenta"]
        G1["Pantalla: Selección de Cuenta"] --> G2["Opción 1: Cuenta Básica (sin fees mensuales)"]
        G1 --> G3["Opción 2: Cuenta Premium (beneficios adicionales)"]
        G1 --> G4["Opción 3: Cuenta de Nómina (descuento directo de nómina)"]
        G2 --> G5{"Confirmación de Selección"}
        G3 --> G5
        G4 --> G5
        G5 -->|Usuario selecciona| H1
    end

    subgraph SEGURIDAD["Fase 6: Configuración de Seguridad"]
        H1["Pantalla: Configuración de Seguridad"] --> H2["Establecer PIN de 4 dígitos"]
        H2 --> H3["Confirmar PIN de 4 dígitos"]
        H3 --> H4["Habilitar Biometría (Huella/Face ID)"]
        H4 --> H5["Configurar preguntas de seguridad"]
        H5 --> H6{"Validación de Seguridad"}
        H6 -->|PINs coinciden| I1
        H6 -->|PINs no coinciden| E13["Error: Los PINs no coinciden. Intente de nuevo"]
        H6 -->|Biometría no disponible| E14["Error: Biometría no disponible en este dispositivo"]
        E13 --> H2
        E14 --> H4
    end

    subgraph REVISION["Fase 7: Revisión de Información"]
        I1["Pantalla: Resumen de Solicitud"] --> I2["Sección: Datos Personales"]
        I2 --> I3["Sección: Datos de Contacto"]
        I3 --> I4["Sección: Tipo de Cuenta"]
        I4 --> I5["Sección: Configuración de Seguridad"]
        I5 --> I6{"Usuario Revisa Información"}
        I6 -->|Información correcta| J1
        I6 -->|Información incorrecta| I7["Botón: Editar"]
        I7 -->|Editar datos personales| D1
        I7 -->|Editar contacto| F1
        I7 -->|Editar tipo de cuenta| G1
    end

    subgraph CONFIRMACION["Fase 8: Confirmación y Activación"]
        J1["Pantalla: Confirmación Final"] --> J2["Botón: Confirmar y Enviar Solicitud"]
        J2 --> J3["Procesamiento de Solicitud (Loading)"]
        J3 --> J4{"Resultado del Procesamiento"}
        J4 -->|Solicitud aprobada| K1["Pantalla: Éxito - Cuenta Creada"]
        J4 -->|Solicitud en revisión| K2["Pantalla: Estado Pendiente - Revisión manual requerida"]
        J4 -->|Solicitud rechazada| K3["Pantalla: Solicitud Rechazada"]
        K1 --> K4["Envío de Correo de Confirmación"]
        K2 --> K5["Envío de Correo con Código de Seguimiento"]
        K3 --> K6["Envío de Correo con Motivo de Rechazo"]
        K4 --> K7["Acceso a Banca Móvil"]
        K5 --> K7
        K6 --> K8["Botón: Contactar Soporte"]
    end

    A2 --> B1
    C1 --> D1
    D10 --> F1
    F11 --> G1
    G5 --> H1
    H6 --> I1

    style A1 fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px
    style B1 fill:#e3f2fd,stroke:#1565c0,stroke-width:2px
    style C1 fill:#fff3e0,stroke:#e65100,stroke-width:2px
    style D1 fill:#fce4ec,stroke:#c2185b,stroke-width:2px
    style F1 fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    style G1 fill:#e0f7fa,stroke:#00838f,stroke-width:2px
    style H1 fill:#fff8e1,stroke:#f57f17,stroke-width:2px
    style I1 fill:#efebe9,stroke:#4e342e,stroke-width:2px
    style J1 fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px
    style K1 fill:#c8e6c9,stroke:#1b5e20,stroke-width:3px
    style K2 fill:#fff9c4,stroke:#f9a825,stroke-width:2px
    style K3 fill:#ffcdd2,stroke:#c62828,stroke-width:2px
    style E1 fill:#ffebee,stroke:#c62828,stroke-width:1px
    style E2 fill:#ffebee,stroke:#c62828,stroke-width:1px
    style E3 fill:#ffebee,stroke:#c62828,stroke-width:1px
    style E4 fill:#ffebee,stroke:#c62828,stroke-width:1px
    style E5 fill:#ffebee,stroke:#c62828,stroke-width:1px
    style E6 fill:#ffebee,stroke:#c62828,stroke-width:1px
    style E7 fill:#ffebee,stroke:#c62828,stroke-width:1px
    style E8 fill:#ffebee,stroke:#c62828,stroke-width:1px
    style E9 fill:#ffebee,stroke:#c62828,stroke-width:1px
    style E10 fill:#ffebee,stroke:#c62828,stroke-width:1px
    style E11 fill:#ffebee,stroke:#c62828,stroke-width:1px
    style E12 fill:#ffebee,stroke:#c62828,stroke-width:1px
    style E13 fill:#ffebee,stroke:#c62828,stroke-width:1px
    style E14 fill:#ffebee,stroke:#c62828,stroke-width:1px

// === ARCHIVO: flujos/flujo-errores.mmd ===
flowchart TD
    subgraph ESCENARIOS_ERROR["Escenarios de Error - Apertura de Cuenta"]
        
        subgraph ERRORES_REGISTRO["Errores en Fase de Registro"]
            ER1["Usuario intenta registrarse"] --> ER2{"Validar Correo Electrónico"}
            ER2 -->|Correo ya existe| ERA["Error: Este correo ya está registrado. ¿Desea iniciar sesión o recuperar contraseña?"]
            ER2 -->|Formato inválido| ERB["Error: Ingrese un correo electrónico válido (ej: usuario@dominio.com)"]
            ER2 -->|Dominio bloqueado| ERC["Error: Este dominio de correo no está permitido"]
            
            ER1 --> ER3{"Validar Contraseña"}
            ER3 -->|Menos de 8 caracteres| ERD["Error: La contraseña debe tener al menos 8 caracteres"]
            ER3 -->|Sin mayúscula| ERE["Error: La contraseña debe contener al menos una letra mayúscula"]
            ER3 -->|Sin número| ERF["Error: La contraseña debe contener al menos un número"]
            ER3 -->|Sin carácter especial| ERG["Error: La contraseña debe contener al menos un carácter especial (!@#$%^&*)"]
            ER3 -->|Contraseñas no coinciden| ERH["Error: Las contraseñas no coinciden"]
            
            ER1 --> ER4{"Validar Términos"}
            ER4 -->|No aceptado| ERI["Error: Debe aceptar los Términos y Condiciones y el Aviso de Privacidad"]
            
            ERA --> ER5["Opciones: Iniciar Sesión | Recuperar Contraseña"]
            ERB --> ER6["Campo: Correo marcado como error"]
            ERC --> ER6
            ERD --> ER7["Campo: Contraseña marcado como error"]
            ERE --> ER7
            ERF --> ER7
            ERG --> ER7
            ERH --> ER7
            ERI --> ER8["Checkbox: Términos marcado como error"]
        end

        subgraph ERRORES_KYC["Errores en Verificación de Identidad"]
            EK1["Usuario inicia verificación de identidad"] --> EK2{"Validar Documento de Identidad"}
            EK2 -->|Documento borroso| EKA["Error: La imagen no es clara. Por favor, tome una foto más nítida"]
            EK2 -->|Documento expirado| EKB["Error: El documento está expirado. Por favor, use un documento vigente"]
            EK2 -->|Documento no soportado| EKC["Error: Este tipo de documento no está soportado. Use INE, Pasaporte o Cédula Profesional"]
            EK2 -->|Datos no coinciden| EKD["Error: Los datos del documento no coinciden con la información proporcionada"]
            EK2 -->|Documento fraudulento| EKE["Error: Se detectó posible fraude. Contacte a soporte para verificar su identidad"]
            
            EK1 --> EK3{"Validar Selfie Biometétrico"}
            EK3 -->|Cara no detectada| EKFA["Error: No se detectó un rostro. Asegúrese de estar frente a la cámara"]
            EK3 -->|Múltiples rostros| EKFB["Error: Se detectaron varios rostros. Solo debe aparecer una persona"]
            EK3 -->|Iluminación insuficiente| EKFC["Error: La iluminación es insuficiente. Busque un lugar mejor iluminado"]
            EK3 -->|Iluminación excesiva| EKFD["Error: La luz directa a la cámara dificulta la detección"]
            EK3 -->|Biometría no coincide| EKFE["Error: La cara no coincide con la foto del documento"]
            EK3 -->|Timeout de cámara| EKFF["Error: Tiempo de espera agotado. La cámara no respondió"]
            
            EK1 --> EK4{"Error de Sistema"}
            EK4 -->|Servicio no disponible| EKG["Error: Servicio de verificación temporalmente no disponible. Intente más tarde"]
            EK4 -->|Error de conexión| EKH["Error: Problema de conexión. Verifique su internet e intente de nuevo"]
            EK4 -->|Límite de intentos| EKI["Error: Ha excedido el límite de intentos. Contacte a soporte"]
            
            EKA --> EK5["Reintentar: Captura de documento"]
            EKB --> EK5
            EKC --> EK5
            EKD --> EK5
            EKE --> EK6["Botón: Contactar Soporte"]
            EKFA --> EK7["Reintentar: Captura de selfie"]
            EKFB --> EK7
            EKFC --> EK7
            EKFD --> EK7
            EKFE --> EK7
            EKFF --> EK1
            EKG --> EK1
            EKH --> EK1
            EKI --> EK6
        end

        subgraph ERRORES_DATOS["Errores en Datos Personales y Contacto"]
            ED1["Usuario ingresa datos"] --> ED2{"Validar CURP"}
            ED2 -->|Formato inválido| EDA["Error: El CURP debe tener 18 caracteres"]
            ED2 -->|Checksum inválido| EDB["Error: El CURP no es válido"]
            ED2 -->|Ya registrado| EDC["Error: Ya existe una cuenta con este CURP"]
            
            ED1 --> ED3{"Validar RFC"}
            ED3 -->|Formato inválido| EDD["Error: El RFC debe tener 10 u 11 caracteres"]
            ED3 -->|Checksum inválido| EDE["Error: El RFC no es válido"]
            
            ED1 --> ED4{"Validar Fecha de Nacimiento"}
            ED4 -->|Fecha futura| EDF["Error: La fecha de nacimiento no puede ser futura"]
            ED4 -->|Menor de 18| EDG["Error: Debes ser mayor de 18 años para abrir una cuenta"]
            ED4 -->|Muy antiguo| EDH["Error: La fecha de nacimiento no es válida"]
            
            ED1 --> ED5{"Validar Dirección"}
            ED5 -->|CP no encontrado| EDI["Error: No encontramos ese código postal. Verifique o ingréselo manualmente"]
            ED5 -->|Dirección incompleta| EDJ["Error: Complete todos los campos de dirección"]
            
            ED1 --> ED6{"Validar Teléfono"}
            ED6 -->|Formato inválido| EDK["Error: Ingrese un número de teléfono válido (10 dígitos)"]
            ED6 -->|Teléfono ya registrado| EDL["Error: Este teléfono ya está registrado en otra cuenta"]
            
            EDA --> ED7["Campo: CURP marcado con error"]
            EDB --> ED7
            EDC --> ED7
            EDD --> ED8["Campo: RFC marcado con error"]
            EDE --> ED8
            EDF --> ED9["Campo: Fecha marcado con error"]
            EDG --> ED9
            EDH --> ED9
            EDI --> ED10["Campo: CP marcado con error"]
            EDJ --> ED10
            EDK --> ED11["Campo: Teléfono marcado con error"]
            EDL --> ED11
        end

        subgraph ERRORES_SEGURIDAD["Errores en Configuración de Seguridad"]
            ES1["Usuario configura seguridad"] --> ES2{"Validar PIN"}
            ES2 -->|PINs no coinciden| ESA["Error: Los PINs no coinciden. Intente de nuevo"]
            ES2 -->|PIN con secuencia| ESB["Error: El PIN no puede tener números consecutivos o repetidos (ej: 1234, 1111)"]
            ES2 -->|PIN muy simple| ESC["Error: El PIN es muy simple. Use una combinación más segura"]
            
            ES1 --> ES3{"Validar Biometría"}
            ES3 -->|No disponible| ESD["Error: Biometría no disponible en este dispositivo"]
            ES3 -->|Huella no reconocida| ESE["Error: No se reconoció la huella. Limpie el sensor y intente de nuevo"]
            ES3 -->|Face ID no funciona| ESF["Error: No se reconoció el rostro. Asegúrese de tener buena iluminación"]
            ES3 -->|Demasiados intentos| ESG["Error: Demasiados intentos fallidos. Use el PIN como alternativa"]
            
            ES1 --> ES4{"Validar Preguntas de Seguridad"}
            ES4 -->|Preguntas repetidas| ESH["Error: Seleccione preguntas diferentes"]
            ES4 -->|Respuesta muy corta| ESI["Error: La respuesta debe tener al menos 3 caracteres"]
            ES4 -->|Respuesta con caracteres inválidos| ESJ["Error: La respuesta no puede contener caracteres especiales"]
            
            ESA --> ES5["Reintentar: Ingreso de PIN"]
            ESB --> ES5
            ESC --> ES5
            ESD --> ES6["Omitir biométria y usar solo PIN"]
            ESE --> ES7["Reintentar: Registrar huella"]
            ESF --> ES7
            ESG --> ES6
            ESH --> ES8["Selección de preguntas marquée con error"]
            ESI --> ES9["Campo de respuesta marqué con error"]
            ESJ --> ES9
        end

        subgraph ERRORES_ENVIO["Errores en Envío de Solicitud"]
            EE1["Usuario envía solicitud"] --> EE2{"Procesar Solicitud"}
            EE2 -->|Timeout del servidor| EEA["Error: Tiempo de espera agotado. Su solicitud fue guardada como borrador"]
            EE2 -->|Error de base de datos| EEB["Error: Problema temporal. Intente en unos minutos"]
            EE2 -->|Validación fallida| EEC["Error: Algunos datos no pasaron la validación final. Revise la información"]
            EE2 -->|Cuenta duplicada| EED["Error: Ya existe una cuenta asociada a estos datos"]
            EE2 -->|Riesgo detectado| EEE["Error: No pudimos procesar su solicitud. Contacte a soporte"]
            
            EEA --> EE3["Regresar a pantalla de revisión"]
            EEB --> EE3
            EEC --> EE4["Resaltar campos con problemas"]
            EED --> EE5["Botón: Iniciar sesión con cuenta existente"]
            EEE --> EE6["Botón: Contactar a soporte"]
        end

        subgraph ERRORES_RECHAZO["Escenarios de Rechazo"]
            ERZ1["Solicitud procesada"] --> ERZ2{"Resultado de Análisis"}
            ERZ2 -->|Perfil de riesgo alto| ERZA["Rechazo: Perfil de riesgo no permitido"]
            ERZ2 -->|Documentación insuficiente| ERZB["Rechazo: Documentación insuficiente para verificar identidad"]
            ERZ2 -->|Historial crediticio| ERZC["Rechazo: No cumple con los requisitos de historial crediticio"]
            ERZ2 -->|Lista negra| ERZD["Rechazo: No es posible abrir cuenta por políticas de seguridad"]
            ERZ2 -->|Menor de edad| ERZE["Rechazo: Debe ser mayor de 18 años"]
            
            ERZA --> ERZF["Mensaje: Puede contactar a soporte para más información"]
            ERZB --> ERZF
            ERZC --> ERZF
            ERZD --> ERZF
            ERZE --> ERZF
        end

        subgraph MANEJO_GENERAL["Manejo General de Errores"]
            MG1["Cualquier Error"] --> MG2{"Tipo de Error"}
            MG2 -->|Recuperable| MGA["Mostrar mensaje claro con acción de recuperación"]
            MG2 -->|No recuperable| MGB["Mostrar mensaje con opción de contactar soporte"]
            MG2 -->|Temporal| MGC["Ofrecer reintento automático o manual"]
            
            MGA --> MGD["Botón: Reintentar | Editar | Continuar"]
            MGB --> MGE["Botón: Contactar Soporte | Volver al Inicio"]
            MGC --> MGF["Spinner de carga | Botón de reintento"]
            
            MGD --> MG4["Acción seleccionada por usuario"]
            MGE --> MG4
            MGF --> MG4
        end
    end

    style ERA fill:#ffebee,stroke:#c62828,stroke-width:2px
    style ERB fill:#ffebee,stroke:#c62828,stroke-width:2px
    style ERC fill:#ffebee,stroke:#c62828,stroke-width:2px
    style EKA fill:#ffebee,stroke:#c62828,stroke-width:2px
    style EKB fill:#ffebee,stroke:#c62828,stroke-width:2px
    style EKC fill:#ffebee,stroke:#c62828,stroke-width:2px
    style EKD fill:#ffebee,stroke:#c62828,stroke-width:2px
    style EKE fill:#ffebee,stroke:#c62828,stroke-width:2px
    style EKFE fill:#ffebee,stroke:#c62828,stroke-width:2px
    style EDA fill:#ffebee,stroke:#c62828,stroke-width:2px
    style EDB fill:#ffebee,stroke:#c62828,stroke-width:2px
    style EDG fill:#ffebee,stroke:#c62828,stroke-width:2px
    style ESA fill:#ffebee,stroke:#c62828,stroke-width:2px
    style EEA fill:#ffebee,stroke:#c62828,stroke-width:2px
    style EEE fill:#ffebee,stroke:#c62828,stroke-width:2px
    style ERZA fill:#ffcdd2,stroke:#b71c1c,stroke-width:2px
    style ERZB fill:#ffcdd2,stroke:#b71c1c,stroke-width:2px
    style ERZC fill:#ffcdd2,stroke:#b71c1c,stroke-width:2px
    style ERZD fill:#ffcdd2,stroke:#b71c1c,stroke-width:2px
    style ERZE fill:#ffcdd2,stroke:#b71c1c,stroke-width:2px


// === ARCHIVO: componentes/especificacion-componentes.md ===
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

// === ARCHIVO: componentes/estados-validacion.md ===
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


// === ARCHIVO: tokens/design-tokens.json ===
{
  "$schema": "https://tokens-studio.com/schema/1.0.0.json",
  "tokenSet": {
    "Global": {
      "color": {
        "primary": {
          "50": { "value": "#E3F2FD", "type": "color" },
          "100": { "value": "#BBDEFB", "type": "color" },
          "200": { "value": "#90CAF9", "type": "color" },
          "300": { "value": "#64B5F6", "type": "color" },
          "400": { "value": "#42A5F5", "type": "color" },
          "500": { "value": "#2196F3", "type": "color" },
          "600": { "value": "#1E88E5", "type": "color" },
          "700": { "value": "#1976D2", "type": "color" },
          "800": { "value": "#1565C0", "type": "color" },
          "900": { "value": "#0D47A1", "type": "color" }
        },
        "secondary": {
          "50": { "value": "#E8F5E9", "type": "color" },
          "100": { "value": "#C8E6C9", "type": "color" },
          "200": { "value": "#A5D6A7", "type": "color" },
          "300": { "value": "#81C784", "type": "color" },
          "400": { "value": "#66BB6A", "type": "color" },
          "500": { "value": "#4CAF50", "type": "color" },
          "600": { "value": "#43A047", "type": "color" },
          "700": { "value": "#388E3C", "type": "color" },
          "800": { "value": "#2E7D32", "type": "color" },
          "900": { "value": "#1B5E20", "type": "color" }
        },
        "neutral": {
          "white": { "value": "#FFFFFF", "type": "color" },
          "50": { "value": "#FAFAFA", "type": "color" },
          "100": { "value": "#F5F5F5", "type": "color" },
          "200": { "value": "#EEEEEE", "type": "color" },
          "300": { "value": "#E0E0E0", "type": "color" },
          "400": { "value": "#BDBDBD", "type": "color" },
          "500": { "value": "#9E9E9E", "type": "color" },
          "600": { "value": "#757575", "type": "color" },
          "700": { "value": "#616161", "type": "color" },
          "800": { "value": "#424242", "type": "color" },
          "900": { "value": "#212121", "type": "color" },
          "black": { "value": "#000000", "type": "color" }
        },
        "semantic": {
          "success": {
            "bg": { "value": "#E8F5E9", "type": "color" },
            "text": { "value": "#1B5E20", "type": "color" },
            "border": { "value": "#4CAF50", "type": "color" },
            "icon": { "value": "#2E7D32", "type": "color" }
          },
          "error": {
            "bg": { "value": "#FFEBEE", "type": "color" },
            "text": { "value": "#B71C1C", "type": "color" },
            "border": { "value": "#F44336", "type": "color" },
            "icon": { "value": "#C62828", "type": "color" }
          },
          "warning": {
            "bg": { "value": "#FFF3E0", "type": "color" },
            "text": { "value": "#E65100", "type": "color" },
            "border": { "value": "#FF9800", "type": "color" },
            "icon": { "value": "#EF6C00", "type": "color" }
          },
          "info": {
            "bg": { "value": "#E3F2FD", "type": "color" },
            "text": { "value": "#0D47A1", "type": "color" },
            "border": { "value": "#2196F3", "type": "color" },
            "icon": { "value": "#1565C0", "type": "color" }
          }
        }
      },
      "typography": {
        "font": {
          "family": {
            "primary": { "value": "Inter", "type": "fontFamily" },
            "secondary": { "value": "Roboto", "type": "fontFamily" },
            "monospace": { "value": "JetBrains Mono", "type": "fontFamily" }
          },
          "weight": {
            "regular": { "value": "400", "type": "fontWeight" },
            "medium": { "value": "500", "type": "fontWeight" },
            "semibold": { "value": "600", "type": "fontWeight" },
            "bold": { "value": "700", "type": "fontWeight" }
          }
        },
        "size": {
          "xs": { "value": "12", "type": "dimension" },
          "sm": { "value": "14", "type": "dimension" },
          "base": { "value": "16", "type": "dimension" },
          "lg": { "value": "18", "type": "dimension" },
          "xl": { "value": "20", "type": "dimension" },
          "2xl": { "value": "24", "type": "dimension" },
          "3xl": { "value": "28", "type": "dimension" },
          "4xl": { "value": "32", "type": "dimension" },
          "5xl": { "value": "40", "type": "dimension" }
        },
        "lineHeight": {
          "tight": { "value": "1.2", "type": "lineHeight" },
          "snug": { "value": "1.375", "type": "lineHeight" },
          "normal": { "value": "1.5", "type": "lineHeight" },
          "relaxed": { "value": "1.625", "type": "lineHeight" }
        },
        "letterSpacing": {
          "tight": { "value": "-0.02em", "type": "letterSpacing" },
          "normal": { "value": "0", "type": "letterSpacing" },
          "wide": { "value": "0.02em", "type": "letterSpacing" }
        }
      },
      "spacing": {
        "0": { "value": "0", "type": "dimension" },
        "xs": { "value": "4", "type": "dimension" },
        "sm": { "value": "8", "type": "dimension" },
        "md": { "value": "16", "type": "dimension" },
        "lg": { "value": "24", "type": "dimension" },
        "xl": { "value": "32", "type": "dimension" },
        "2xl": { "value": "48", "type": "dimension" },
        "3xl": { "value": "64", "type": "dimension" },
        "4xl": { "value": "96", "type": "dimension" }
      },
      "borderRadius": {
        "none": { "value": "0", "type": "borderRadius" },
        "sm": { "value": "4", "type": "borderRadius" },
        "md": { "value": "8", "type": "borderRadius" },
        "lg": { "value": "12", "type": "borderRadius" },
        "xl": { "value": "16", "type": "borderRadius" },
        "2xl": { "value": "24", "type": "borderRadius" },
        "full": { "value": "9999", "type": "borderRadius" }
      },
      "shadow": {
        "sm": {
          "value": { "x": "0", "y": "1", "blur": "2", "color": "rgba(0, 0, 0, 0.05)" },
          "type": "boxShadow"
        },
        "md": {
          "value": { "x": "0", "y": "4", "blur": "6", "color": "rgba(0, 0, 0, 0.1)" },
          "type": "boxShadow"
        },
        "lg": {
          "value": { "x": "0", "y": "10", "blur": "15", "color": "rgba(0, 0, 0, 0.1)" },
          "type": "boxShadow"
        },
        "xl": {
          "value": { "x": "0", "y": "20", "blur": "25", "color": "rgba(0, 0, 0, 0.15)" },
          "type": "boxShadow"
        }
      },
      "transition": {
        "duration": {
          "fast": { "value": "150ms", "type": "duration" },
          "normal": { "value": "250ms", "type": "duration" },
          "slow": { "value": "350ms", "type": "duration" }
        },
        "easing": {
          "ease-in": { "value": "cubic-bezier(0.4, 0, 1, 1)", "type": "transition" },
          "ease-out": { "value": "cubic-bezier(0, 0, 0.2, 1)", "type": "transition" },
          "ease-in-out": { "value": "cubic-bezier(0.4, 0, 0.2, 1)", "type": "transition" }
        }
      },
      "component": {
        "button": {
          "primary": {
            "bg": { "value": "{color.primary.600}", "type": "color" },
            "bg-hover": { "value": "{color.primary.700}", "type": "color" },
            "bg-active": { "value": "{color.primary.800}", "type": "color" },
            "bg-disabled": { "value": "{color.neutral.300}", "type": "color" },
            "text": { "value": "{color.neutral.white}", "type": "color" },
            "text-hover": { "value": "{color.neutral.white}", "type": "color" },
            "text-disabled": { "value": "{color.neutral.500}", "type": "color" },
            "border-radius": { "value": "{borderRadius.md}", "type": "borderRadius" },
            "padding-x": { "value": "{spacing.lg}", "type": "dimension" },
            "padding-y": { "value": "{spacing.md}", "type": "dimension" },
            "height": { "value": "48", "type": "dimension" },
            "font-size": { "value": "{typography.size.base}", "type": "dimension" },
            "font-weight": { "value": "{typography.font.weight.semibold}", "type": "fontWeight" }
          },
          "secondary": {
            "bg": { "value": "{color.neutral.white}", "type": "color" },
            "bg-hover": { "value": "{color.neutral.50}", "type": "color" },
            "border": { "value": "{color.primary.600}", "type": "color" },
            "border-hover": { "value": "{color.primary.700}", "type": "color" },
            "text": { "value": "{color.primary.700}", "type": "color" },
            "text-hover": { "value": "{color.primary.800}", "type": "color" },
            "border-radius": { "value": "{borderRadius.md}", "type": "borderRadius" }
          },
          "outline": {
            "bg": { "value": "transparent", "type": "color" },
            "bg-hover": { "value": "{color.primary.50}", "type": "color" },
            "text": { "value": "{color.primary.700}", "type": "color" },
            "border": { "value": "{color.neutral.300}", "type": "color" },
            "border-focus": { "value": "{color.primary.500}", "type": "color" },
            "border-radius": { "value": "{borderRadius.md}", "type": "borderRadius" }
          }
        },
        "input": {
          "default": {
            "bg": { "value": "{color.neutral.white}", "type": "color" },
            "border": { "value": "{color.neutral.300}", "type": "color" },
            "border-hover": { "value": "{color.neutral.400}", "type": "color" },
            "border-focus": { "value": "{color.primary.500}", "type": "color" },
            "text": { "value": "{color.neutral.900}", "type": "color" },
            "placeholder": { "value": "{color.neutral.400}", "type": "color" }
          },
          "error": {
            "border": { "value": "{color.semantic.error.border}", "type": "color" },
            "border-focus": { "value": "{color.semantic.error.border}", "type": "color" },
            "text": { "value": "{color.semantic.error.text}", "type": "color" },
            "bg": { "value": "{color.semantic.error.bg}", "type": "color" }
          },
          "success": {
            "border": { "value": "{color.semantic.success.border}", "type": "color" },
            "text": { "value": "{color.semantic.success.text}", "type": "color" }
          },
          "disabled": {
            "bg": { "value": "{color.neutral.100}", "type": "color" },
            "border": { "value": "{color.neutral.200}", "type": "color" },
            "text": { "value": "{color.neutral.500}", "type": "color" },
            "placeholder": { "value": "{color.neutral.300}", "type": "color" }
          },
          "height": { "value": "48", "type": "dimension" },
          "padding-x": { "value": "{spacing.md}", "type": "dimension" },
          "border-radius": { "value": "{borderRadius.md}", "type": "borderRadius" }
        },
        "card": {
          "bg": { "value": "{color.neutral.white}", "type": "color" },
          "border": { "value": "{color.neutral.200}", "type": "color" },
          "border-radius": { "value": "{borderRadius.lg}", "type": "borderRadius" },
          "padding": { "value": "{spacing.lg}", "type": "dimension" },
          "shadow": { "value": "{shadow.md}", "type": "boxShadow" },
          "shadow-hover": { "value": "{shadow.lg}", "type": "boxShadow" }
        },
        "modal": {
          "overlay": { "value": "rgba(0, 0, 0, 0.5)", "type": "color" },
          "bg": { "value": "{color.neutral.white}", "type": "color" },
          "border-radius": { "value": "{borderRadius.xl}", "type": "borderRadius" },
          "padding": { "value": "{spacing.xl}", "type": "dimension" },
          "max-width": { "value": "480", "type": "dimension" }
        },
        "progress": {
          "track": { "value": "{color.neutral.200}", "type": "color" },
          "fill": { "value": "{color.primary.500}", "type": "color" },
          "height": { "value": "8", "type": "dimension" },
          "border-radius": { "value": "{borderRadius.full}", "type": "borderRadius" }
        },
        "tooltip": {
          "bg": { "value": "{color.neutral.800}", "type": "color" },
          "text": { "value": "{color.neutral.white}", "type": "color" },
          "border-radius": { "value": "{borderRadius.sm}", "type": "borderRadius" },
          "padding-x": { "value": "{spacing.sm}", "type": "dimension" },
          "padding-y": { "value": "{spacing.xs}", "type": "dimension" },
          "font-size": { "value": "{typography.size.sm}", "type": "dimension" }
        }
      },
      "a11y": {
        "focus-ring": {
          "color": { "value": "{color.primary.500}", "type": "color" },
          "width": { "value": "2", "type": "dimension" },
          "offset": { "value": "2", "type": "dimension" }
        },
        "min-contrast-normal": { "value": "4.5", "type": "dimension" },
        "min-contrast-large": { "value": "3.0", "type": "dimension" },
        "touch-target-min": { "value": "44", "type": "dimension" }
      }
    }
  }
}
// === ARCHIVO: tokens/tokens-semanticos.md ===
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

// === ARCHIVO: accesibilidad/criterios-wcag.md ===
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

// === ARCHIVO: accesibilidad/pruebas-accesibilidad.md ===
# Reporte de Pruebas de Accesibilidad

## Información General del Proyecto

- **Proyecto**: Flujo de Apertura de Cuenta Bancaria
- **Fecha de pruebas**: Noviembre 2024
- **Versión evaluada**: 1.0.0
- **Herramientas utilizadas**: axe DevTools Pro, Figma A11y Plugin, Color Contrast Analyzer, NVDA
- **Estándar de referencia**: WCAG 2.2 Nivel AA

---

## Resumen Ejecutivo

Se realizaron pruebas de accesibilidad automatizadas y manuales en las 6 pantallas del flujo de apertura de cuenta. El resultado inicial mostró 23 issues de accesibilidad, de los cuales 18 fueron corregidos antes de la entrega final. Los 5 issues restantes son de baja prioridad y están documentados con justificaciones.

### Estadísticas

| Métrica | Valor |
|---------|-------|
| Total de issues encontrados | 23 |
| Issues críticos | 4 |
| Issues serios | 12 |
| Issues moderados | 5 |
| Issues menores | 2 |
| Issues corregidos | 18 |
| Porcentaje de corrección | 78% |

---

## Detalle de Pruebas por Pantalla

### Pantalla 1: Pantalla de Bienvenida

**Herramienta**: axe DevTools
**Resultado**: 3 issues encontrados, 3 corregidos

#### Issue 1.1: Contraste insuficiente en botón secundario
- **Severidad**: Serio
- **Criterio**: 1.4.3 Contraste mínimo
- **Descripción**: El botón "Inicia sesión" usa color de texto #4A4A4A sobre fondo #F5F5F5 con ratio de 3.8:1
- **Requerido**: 4.5:1 para texto normal
- **Captura de pantalla**: `img/pantalla1-issue-contraste.png` (adjunta)
- **Corrección aplicada**: Cambiado a #1A1A1A sobre #F5F5F5 = 12.6:1
- **Verificación**: ✅ Pasado

#### Issue 1.2: Enlace sin indicador de foco visible
- **Severidad**: Moderado
- **Criterio**: 2.4.7 Foco visible
- **Descripción**: El enlace de términos no tiene estilo de foco definido
- **Corrección aplicada**: Agregado outline 2px dashed #0066CC y background #E6F0FA
- **Verificación**: ✅ Pasado

#### Issue 1.3: Imagen decorativa sin aria-hidden
- **Severidad**: Menor
- **Criterio**: 1.1.1 Contenido no textual
- **Descripción**: Ilustración de bienvenida no identificada como decorativa
- **Corrección aplicada**: Agregado role="img" y aria-hidden="true"
- **Verificación**: ✅ Pasado

---

### Pantalla 2: Selección de Tipo de Cuenta

**Herramienta**: Figma A11y Plugin + axe DevTools
**Resultado**: 5 issues encontrados, 4 corregidos

#### Issue 2.1: Grupo de radio buttons sin etiqueta accesible
- **Severidad**: Crítico
- **Criterio**: 1.3.1 Información y relaciones
- **Descripción**: Las opciones de cuenta no tienen un label asociado al grupo
- **Captura de pantalla**: `img/pantalla2-issue-label.png`
- **Corrección aplicada**: Agregado role="radiogroup" con aria-labelledby="tipo-cuenta-titulo"
- **Verificación**: ✅ Pasado

```html
<!-- Antes -->
<div class="account-options">
  <div class="account-option">...</div>
</div>

<!-- Después -->
<h2 id="tipo-cuenta-titulo">¿Qué tipo de cuenta deseas abrir?</h2>
<div role="radiogroup" aria-labelledby="tipo-cuenta-titulo" class="account-options">
  <div role="radio" aria-checked="false" tabindex="0">...</div>
</div>
```

#### Issue 2.2: Opción de cuenta no navegable por teclado
- **Severidad**: Crítico
- **Criterio**: 2.1.1 Teclado
- **Descripción**: Las tarjetas de cuenta son elementos div sin capacidad de foco
- **Corrección aplicada**: Cambiados a elementos button con tabindex="0", role="radio"
- **Verificación**: ✅ Pasado

#### Issue 2.3: Contraste bajo en texto secundario de opciones
- **Severidad**: Serio
- **Criterio**: 1.4.3 Contraste mínimo
- **Descripción**: Descripción "Ideal para guardar tu dinero" usa #757575 sobre #FFFFFF = 4.2:1
- **Corrección aplicada**: Cambiado a #4A4A4A = 9.2:1
- **Verificación**: ✅ Pasado

#### Issue 2.4: Estado de selección no anunciado
- **Severidad**: Serio
- **Criterio**: 4.1.2 Nombre, rol, valor
- **Descripción**: El lector de pantalla no anuncia qué opción está seleccionada
- **Corrección aplicada**: Agregado aria-checked="true/false" y aria-pressed
- **Verificación**: ✅ Pasado

#### Issue 2.5: Orden de tabulación incorrecto
- **Severidad**: Moderado
- **Criterio**: 2.4.3 Orden del foco
- **Descripción**: El foco va al botón Atrás antes de las opciones
- **Corrección aplicada**: Reordenado en DOM: título → opciones → Continuar → Atrás
- **Verificación**: ⚠️ Pendiente de verificación final

---

### Pantalla 3: Datos Personales

**Herramienta**: axe DevTools + NVDA
**Resultado**: 6 issues encontrados, 5 corregidos

#### Issue 3.1: Campo sin etiqueta asociada
- **Severidad**: Crítico
- **Criterio**: 1.3.1 Información y relaciones
- **Descripción**: El campo de género no tiene label
- **Captura de pantalla**: `img/pantalla3-issue-label-genero.png`
- **Corrección aplicada**: Agregado <label for="genero">Género</label>
- **Verificación**: ✅ Pasado

#### Issue 3.2: Atributo autocomplete ausente
- **Severidad**: Serio
- **Criterio**: 1.3.5 Identificar propósito de entrada
- **Descripción**: Campos sin autocomplete dificultan llenado para usuarios
- **Corrección aplicada**: Agregado autocomplete a todos los campos (name, cc, bday, tel, email)
- **Verificación**: ✅ Pasado

#### Issue 3.3: Error de validación no anunciado
- **Severidad**: Crítico
- **Criterio**: 3.3.1 Identificación de errores
- **Descripción**: El mensaje de error de email no se anuncia automáticamente
- **Captura de pantalla**: `img/pantalla3-issue-error.png`
- **Corrección aplicada**: Agregado role="alert" y aria-live="assertive" al mensaje de error
- **Verificación**: ✅ Pasado

#### Issue 3.4: Checkbox de términos sin texto de error
- **Severidad**: Serio
- **Criterio**: 3.3.2 Etiquetas o instrucciones
- **Descripción**: El checkbox requiere aceptación pero no hay instrucción clara
- **Corrección aplicada**: Agregado aria-describedby con texto de requerimiento
- **Verificación**: ✅ Pasado

#### Issue 3.5: Atributo type incorrecto en campo de teléfono
- **Severidad**: Moderado
- **Criterio**: 1.3.1 Información y relaciones
- **Descripción**: Teléfono usa type="text" en lugar de type="tel"
- **Corrección aplicada**: Cambiado a type="tel"
- **Verificación**: ✅ Pasado

#### Issue 3.6: Placeholder como única referencia
- **Severidad**: Menor
- **Criterio**: 3.3.2 Etiquetas o instrucciones
- **Descripción**: Algunos campos dependen del placeholder como guía
- **Corrección aplicada**: Agregado texto de ayuda visible bajo cada campo
- **Verificación**: ✅ Pasado

---

### Pantalla 4: Información Financiera

**Herramienta**: axe DevTools
**Resultado**: 4 issues encontrados, 3 corregidos

#### Issue 4.1: Select sin opciones accesibles
- **Severidad**: Serio
- **Criterio**: 1.3.1 Información y relaciones
- **Descripción**: Los selects usan opciones sin descripción clara
- **Corrección aplicada**: Agregado aria-label a cada opción
- **Verificación**: ✅ Pasado

#### Issue 4.2: Campo de ingreso sin formato accesible
- **Severidad**: Moderado
- **Criterio**: 1.3.1 Información y relaciones
- **Descripción**: El campo monetario no indica el formato esperado
- **Corrección aplicada**: Agregado inputmode="decimal" y aria-describedby con formato
- **Verificación**: ✅ Pasado

#### Issue 4.3: Mensaje de error ambiguo
- **Severidad**: Serio
- **Criterio**: 3.3.1 Identificación de errores
- **Descripción": "Datos inválidos" no indica qué campo tiene error
- **Corrección aplicada**: Cambiado a mensajes específicos por campo
- **Verificación**: ✅ Pasado

#### Issue 4.4: Instrucciones de declaración confusas
- **Severidad**: Moderado
- **Criterio**: 3.3.2 Etiquetas o instrucciones
- **Descripción**: El checkbox de declaración no indica consecuencias
- **Corrección aplicada**: Agregado tooltip con explicación completa
- **Verificación**: ⚠️ Pendiente de revisión

---

### Pantalla 5: Verificación de Identidad

**Herramienta**: axe DevTools + Color Contrast Analyzer
**Resultado**: 3 issues encontrados, 2 corregidos

#### Issue 5.1: Componente de cámara sin alternativas
- **Severidad**: Serio
- **Criterio**: 1.1.1 Contenido no textual
- **Descripción**: La interfaz de cámara no tiene alternativa para usuarios que no pueden tomar selfie
- **Captura de pantalla**: `img/pantalla5-issue-camera.png`
- **Corrección aplicada**: Agregado botón "Verificación por llamada" como alternativa
- **Verificación**: ✅ Pasado

#### Issue 5.2: Video instructivo sin subtítulos
- **Severidad**: Crítico
- **Criterio**: 1.2.2 Audio descriptivo
- **Descripción**: Video instructivo no tiene subtítulos ni transcripción
- **Corrección aplicada**: Agregado transcript disponible y subtítulos
- **Verificación**: ✅ Pasado

#### Issue 5.3: Indicador de progreso no anunciado
- **Severidad**: Serio
- **Criterio**: 1.3.1 Información y relaciones
- **Descripción**: El progreso de verificación no se anuncia a lectores de pantalla
- **Corrección aplicada**: Agregado role="progressbar" con aria-valuenow
- **Verificación**: ✅ Pasado

---

### Pantalla 6: Confirmación

**Herramienta**: axe DevTools + VoiceOver
**Resultado**: 2 issues encontrados, 1 corregido

#### Issue 6.1: Número de cuenta no anunciado correctamente
- **Severidad**: Serio
- **Criterio**: 1.3.1 Información y relaciones
- **Descripción**: El número de cuenta se muestra agrupado pero no como dato estructurado
- **Captura de pantalla**: `img/pantalla6-issue-cuenta.png`
- **Corrección aplicada**: Agregado aria-label="Número de cuenta: 1234-5678-9012-3456"
- **Verificación**: ✅ Pasado

#### Issue 6.2: Icono de éxito sin descripción
- **Severidad**: Moderado
- **Criterio**: 1.1.1 Contenido no textual
- **Descripción**: El check grande no tiene descripción para lectores de pantalla
- **Corrección aplicada**: Agregado alt="Cuenta creada exitosamente"
- **Verificación**: ✅ Pasado

---

## Resultados de Pruebas con Lectores de Pantalla

### NVDA (Windows)

| Pantalla | Prueba | Resultado |
|----------|--------|-----------|
| Bienvenida | Lectura de título y botón | ✅ Correcto |
| Selección cuenta | Navegación por flechas | ✅ Correcto |
| Datos personales | Anuncio de errores | ⚠️ Requiere mejora |
| Verificación | Instrucciones claras | ✅ Correcto |
| Confirmación | Lectura de número | ✅ Correcto |

**Hallazgo**: En la pantalla de datos personales, cuando hay múltiples errores, NVDA no los lee todos. Se requiere que el usuarioTab entre cada campo para escuchar el error.

**Recomendación**: Agregar botón "Mostrar todos los errores" que presente lista de errores con aria-live="assertive".

### VoiceOver (iOS)

| Pantalla | Prueba | Resultado |
|----------|--------|-----------|
| Bienvenida | Gestos de navegación | ✅ Correcto |
| Selección cuenta | Selector de rotor | ✅ Correcto |
| Datos personales | Formularios | ✅ Correcto |
| Verificación | Cámara | ⚠️ Requiere verificación |
| Confirmación | Elementos interactivos | ✅ Correcto |

### TalkBack (Android)

| Pantalla | Prueba | Resultado |
|----------|--------|-----------|
| Bienvenida | Lectura de contenido | ✅ Correcto |
| Selección cuenta | Navegación | ✅ Correcto |
| Datos personales | Formularios | ⚠️ Problema con fechas |
| Verificación | Alternativas | ✅ Correcto |
| Confirmación | Acciones | ✅ Correcto |

**Hallazgo**: El selector de fecha presenta problemas de navegación en TalkBack.

**Recomendación**: Usar selector nativo type="date" en lugar de componente personalizado.

---

## Capturas de Pantalla de Resultados

### captura-axe-pantalla-1.png
```
axe DevTools - Resultados
✗ 3 issues found
  ⚠ Contraste insuficiente (1)
  ⚠ Foco no visible (1)
  ✓ Decorative image (1)
```

### captura-axe-pantalla-2.png
```
axe DevTools - Resultados
✗ 5 issues found
  ✗ Missing label (2)
  ✗ Keyboard accessible (1)
  ⚠ Contraste (1)
  ⚠ ARIA (1)
```

### captura-axe-pantalla-3.png
```
axe DevTools - Resultados
✗ 6 issues found
  ✗ Form label (1)
  ✗ Autocomplete (1)
  ✗ Error identification (1)
  ⚠ Instructions (2)
  ⚠ Input type (1)
```

### captura-figma-a11y.png
```
Figma A11y Plugin
✓ Contraste: 100%
✓ Etiquetas: 85%
✓ Foco: 90%
⚠ ARIA: 75%
```

---

## Matriz de Correcciones

| ID | Pantalla | Severidad | Criterio | Estado | Fecha Corrección |
|----|----------|-----------|----------|--------|------------------|
| 1.1 | Bienvenida | Serio | 1.4.3 | ✅ Corregido | 2024-11-15 |
| 1.2 | Bienvenida | Moderado | 2.4.7 | ✅ Corregido | 2024-11-15 |
| 1.3 | Bienvenida | Menor | 1.1.1 | ✅ Corregido | 2024-11-15 |
| 2.1 | Selección | Crítico | 1.3.1 | ✅ Corregido | 2024-11-16 |
| 2.2 | Selección | Crítico | 2.1.1 | ✅ Corregido | 2024-11-16 |
| 2.3 | Selección | Serio | 1.4.3 | ✅ Corregido | 2024-11-16 |
| 2.4 | Selección | Serio | 4.1.2 | ✅ Corregido | 2024-11-16 |
| 2.5 | Selección | Moderado | 2.4.3 | ⚠️ Pendiente | - |
| 3.1 | Datos | Crítico | 1.3.1 | ✅ Corregido | 2024-11-17 |
| 3.2 | Datos | Serio | 1.3.5 | ✅ Corregido | 2024-11-17 |
| 3.3 | Datos | Crítico | 3.3.1 | ✅ Corregido | 2024-11-17 |
| 3.4 | Datos | Serio | 3.3.2 | ✅ Corregido | 2024-11-17 |
| 3.5 | Datos | Moderado | 1.3.1 | ✅ Corregido | 2024-11-17 |
| 3.6 | Datos | Menor | 3.3.2 | ✅ Corregido | 2024-11-17 |
| 4.1 | Financiera | Serio | 1.3.1 | ✅ Corregido | 2024-11-18 |
| 4.2 | Financiera | Moderado | 1.3.1 | ✅ Corregido | 2024-11-18 |
| 4.3 | Financiera | Serio | 3.3.1 | ✅ Corregido | 2024-11-18 |
| 4.4 | Financiera | Moderado | 3.3.2 | ⚠️ Pendiente | - |
| 5.1 | Verificación | Serio | 1.1.1 | ✅ Corregido | 2024-11-19 |
| 5.2 | Verificación | Crítico | 1.2.2 | ✅ Corregido | 2024-11-19 |
| 5.3 | Verificación | Serio | 1.3.1 | ✅ Corregido | 2024-11-19 |
| 6.1 | Confirmación | Serio | 1.3.1 | ✅ Corregido | 2024-11-19 |
| 6.2 | Confirmación | Moderado | 1.1.1 | ✅ Corregido | 2024-11-19 |

---

## Issues Pendientes

### Issue 2.5: Orden de tabulación en Selección de Cuenta
- **Severidad**: Moderado
- **Justificación**: El orden actual sigue una lógica de negocio (Atrás siempre al final), cambiarlo afectaría la experiencia de usuarios que esperan ese patrón
- **Alternativa propuesta**: Agregar atajo de teclado (Ctrl+Shift+Tab) para ir directamente a opciones
- **Estado**: Aceptar como riesgo conocido, documentar en release notes

### Issue 4.4: Instrucciones de declaración
- **Severidad**: Moderado
- **Justificación**: El tooltip requiere hover/focus que no está disponible en todos los dispositivos táctiles
- **Alternativa propuesta**: Mostrar texto completo junto al checkbox en lugar de tooltip
- **Estado**: Pendiente de diseño alternativo

---

## Recomendaciones Futuras

1. **Automatización continua**: Integrar pruebas de accesibilidad en el pipeline de CI/CD
2. **Testing con usuarios**: Realizar pruebas con usuarios que utilizan lectores de pantalla
3. **Documentación**: Crear guía de accesibilidad para desarrolladores
4. **Componentes**: Actualizar library de componentes con atributos ARIA por defecto
5. **Monitoreo**: Establecer métricas de accesibilidad en analytics

---

## Referencias

- axe Core: https://www.deque.com/axe/
- WAVE: https://wave.webaim.org/
- NVDA: https://www.nvaccess.org/
- WCAG 2.2 Quick Reference: https://www.w3.org/WAI/WCAG21/quickref/
- Figma A11y Plugin: https://www.figma.com/community/plugin/732603254453395948


// === ARCHIVO: validacion/heuristicas-usabilidad.md ===
# Análisis Heurístico del Flujo de Apertura de Cuenta

## Introducción

Este documento presenta el análisis del flujo de apertura de cuenta bancaria móvil utilizando las 10 heurísticas de usabilidad de Jakob Nielsen. El objetivo es identificar problemas de usabilidad y proponer soluciones concretas que mejoren la experiencia del usuario.

## Contexto del Análisis

El flujo de apertura de cuenta bancaria móvil comprende las siguientes etapas principales: pantalla de bienvenida y selección de tipo de cuenta, ingreso de datos personales (nombre, apellido, correo, teléfono), validación de identidad mediante documento, configuración de credenciales de acceso, verificación de información y confirmación final. Cada una de estas etapas ha sido evaluada contra las heurísticas de Nielsen.

## 1. Visibilidad del Estado del Sistema

**Descripción**: El sistema debe mantener informados a los usuarios sobre lo que está sucediendo, mediante retroalimentación apropiada dentro de un tiempo razonable.

**Análisis del flujo actual**:
- La barra de progreso en la parte superior indica claramente en qué paso se encuentra el usuario (ej: "Paso 2 de 5")
- Los estados de carga durante la validación de documentos muestran un spinner con texto descriptivo
- La validación de campos en tiempo real proporciona feedback inmediato

**Problemas identificados**:
- En el paso de validación de identidad, no se indica claramente cuánto tiempo puede tomar el proceso de verificación
- Cuando hay errores de servidor, el mensaje genérico "Ha ocurrido un error" no especifica qué está pasando
- No hay indicador visual durante la verificación de datos con entidades externas

**Soluciones propuestas**:
- Agregar tiempo estimado de espera en la pantalla de validación de identidad (ej: "Este proceso puede tomar hasta 30 segundos")
- Implementar mensajes de error más específicos que indiquen la causa del fallo y acciones concretas
- Mostrar un indicador de progreso animado durante las verificaciones con terceros

## 2. Relación entre el Sistema y el Mundo Real

**Descripción**: El sistema debe hablar el lenguaje del usuario, con palabras, frases y conceptos familiares, en lugar de términos orientados al sistema.

**Análisis del flujo actual**:
- Los campos de formulario utilizan terminología bancaria estándar que puede resultar confusa para usuarios no familiarizados
- Las etiquetas de los campos son claras (Nombre completo, Número de documento, etc.)

**Problemas identificados**:
- El término "Cuenta de ahorro" puede no ser claro para todos los usuarios; algunos podrían beneficiarse de una explicación breve
- Las validaciones de formato de documento utilizan terminología técnica (ej: "El documento debe tener 8 dígitos")
- Los mensajes de error técnicos no están traducidos a lenguaje cotidiano

**Soluciones propuestas**:
- Incluir tooltips explicativos junto a términos técnicos o productos que requieran contexto
- Reformular mensajes de validación a lenguaje natural (ej: "Ingresa los 8 dígitos de tu documento sin puntos" en lugar de "Formato inválido")
- Agregar ejemplos visuales del documento requerido en el campo de carga

## 3. Control y Libertad del Usuario

**Descripción**: Los usuarios frecuentemente eligen funciones del sistema por error y necesitan marcada claramente una "salida de emergencia" para dejar el estado no deseado.

**Análisis del flujo actual**:
- El botón "Atrás" está disponible en cada paso del flujo
- Existe la opción de guardar el progreso y continuar después
- Los formularios permiten editar información previamente ingresada

**Problemas identificados**:
- Al presionar "Atrás" desde la confirmación de datos, no queda claro qué información se pierde
- No hay botón de cancelación claro que permita salir del flujo sin perder el progreso guardado
- La opción de "Guardar y continuar después" no es visible hasta el tercer paso

**Soluciones propuestas**:
- Implementar un modal de confirmación al presionar "Atrás" que indique qué datos se conservarán
- Hacer visible el botón de "Guardar progreso" desde el primer paso
- Agregar una opción de "Salir" con confirmación clara en la barra de navegación

## 4. Consistencia y Estándares

**Descripción**: Los usuarios no deberían preguntarse si diferentes palabras, situaciones o acciones significan lo mismo. Siga las convenciones de la plataforma.

**Análisis del flujo actual**:
- Los botones de acción primaria mantienen el mismo color a lo largo del flujo
- Los iconos de validación (check, X) son consistentes
- La estructura de las pantallas de formulario sigue un patrón uniforme

**Problemas identificados**:
- En algunos pasos se usa "Continuar" y en otros "Siguiente" como botón primario
- Los mensajes de error aparecen en diferentes ubicaciones según el paso
- La validación en tiempo real aparece en algunos campos y en otros solo al presionar continuar

**Soluciones propuestas**:
- Estandarizar la nomenclatura de botones (recomendación: usar "Siguiente" para avanzar, "Continuar" para acciones de confirmación)
- Mantener la ubicación consistente de los mensajes de error (recomendación: siempre debajo del campo afectado)
- Aplicar validación en tiempo real de manera uniforme o documentar por qué varía

## 5. Prevención de Errores

**Descripción**: Mejor que un buen mensaje de error es un diseño cuidadoso que prevenga un problema antes de que ocurra.

**Análisis del flujo actual**:
- Los campos de fecha tienen selectores que evitan fechas inválidas
- El campo de correo incluye validación de formato en tiempo real
- Los campos de contraseña muestran medidor de fortaleza

**Problemas identificados**:
- No hay validación anticipada de disponibilidad de correo electrónico o número de teléfono
- El selector de tipo de documento no indica qué documentos son aceptados
- No hay límites de caracteres en campos de texto libre que podrían causar problemas de almacenamiento

**Soluciones propuestas**:
- Implementar verificación de disponibilidad en tiempo real para correo y teléfono (con debounce de 500ms)
- Agregar un menú de ayuda que explique qué documentos de identidad son aceptados según el país
- Definir y aplicar límites de caracteres apropiados para cada campo

## 6. Reconocimiento Antes que Recuerdo

**Descripción**: Minimice la carga de memoria del usuario haciendo visibles objetos, acciones y opciones.

**Análisis del flujo actual**:
- Las instrucciones de cada paso son visibles en la parte superior
- Los iconos de ayuda están disponibles junto a campos complejos
- El resumen de información se muestra antes de la confirmación final

**Problemas identificados**:
- Los requisitos de contraseña no están siempre visibles; el usuario debe recordarlos
- La información ingresada en pasos anteriores no se puede consultar sin volver atrás
- Los ejemplos de formato válido solo aparecen después de un error

**Soluciones propuestas**:
- Mantener visibles los requisitos de contraseña cerca del campo, posiblemente como lista colapsable
- Agregar un botón de "Ver resumen" que permita consultar la información sin modificar
- Mostrar ejemplos de formato válido como texto de ayuda, no solo en errores

## 7. Flexibilidad y Eficiencia de Uso

**Descripción**: Los aceleradores, invisibles para el usuario novato, pueden menudo acelerar la interacción para el usuario experto.

**Análisis del flujo actual**:
- Los usuarios expertos pueden navegar entre pasos usando la barra de progreso
- Existe opción de completar el flujo desde web con sesión iniciada
- El autocompletado está disponible para campos de dirección

**Problemas identificados**:
- No hay atajos de teclado para usuarios que acceden desde escritorio
- La opción de subir documento de identidad desde galería no prioriza opciones frecuentes
- No hay modo de completado rápido para usuarios recurrentes

**Soluciones propuestas**:
- Implementar atajos de teclado (Tab para siguiente campo, Enter para continuar)
- Ordenar opciones de carga de documento por frecuencia de uso del usuario
- Ofrecer "Continuar como...” para usuarios con sesiones activas en otros canales

## 8. Diseño Estético y Minimalista

**Descripción**: Los diálogos no deben contener información irrelevante o raramente necesaria.

**Análisis del flujo actual**:
- La interfaz es limpia, con espacio en blanco adecuado
- Los elementos interactivos tienen tamaño apropiado para touch
- La jerarquía visual es clara con un objetivo primario por pantalla

**Problemas identificados**:
- La pantalla de selección de tipo de cuenta muestra información detallada que podría overwhelm al usuario
- Los términos y condiciones están expandidos por defecto, ocupando espacio innecesario
- Hay información promocional que distrae del objetivo principal

**Soluciones propuestas**:
- Simplificar la pantalla de selección a opciones principales con link a detalles
- Mantener términos colapsados con link directo para quienes necesiten leerlos
- Eliminar elementos promocionales del flujo de apertura; mover a pantalla posterior

## 9. Ayuda a Reconocer y Recuperarse de Errores

**Descripción**: Los mensajes de error deben expresarse en lenguaje claro, indicar con precisión el problema y sugerir una solución.

**Análisis del flujo actual**:
- Los errores de validación aparecen junto al campo afectado
- Algunos errores incluyen sugerencia de solución
- El color rojo se usa consistentemente para indicar errores

**Problemas identificados**:
- Los errores de conexión no distinguen entre problemas de red del usuario o del servidor
- Cuando la validación de documento falla, no se indica si es un problema del documento o del sistema
- Los errores de sesión expirada redirigen sin explicación clara

**Soluciones propuestas**:
- Diferenciar mensajes de error de red ("Verifica tu conexión") de errores de servidor ("Intenta más tarde")
- Proporcionar pasos específicos cuando la validación de documento falla (recomendaciones de calidad de imagen, formato)
- Mostrar modal de sesión expirada con opciones claras de acción

## 10. Ayuda y Documentación

**Descripción**: Aunque es mejor que el sistema pueda usarse sin documentación, puede ser necesario proporcionar ayuda. Esta debe ser fácil de buscar, focalizada en las tareas del usuario y no muy extensa.

**Análisis del flujo actual**:
- Los iconos de ayuda (?) están disponibles en campos clave
- Hay sección de preguntas frecuentes accesible desde el menú
- El chat de soporte es accesible durante todo el flujo

**Problemas identificados**:
- La ayuda contextual no se adapta al paso actual del usuario
- Las FAQs no están vinculadas a los puntos de fricción comunes del flujo
- El chat de soporte requiere abandonar el flujo para acceder

**Soluciones propuestas**:
- Implementar ayuda contextual que sugiera artículos basados en el paso actual
- Crear vínculos directos desde errores comunes a la sección relevante de FAQ
- Implementar botón flotante de soporte que abra chat sin perder progreso del formulario

## Matriz de Priorización de Problemas

| Heurística | Problema | Severidad | Impacto |
|------------|----------|-----------|----------|
| Visibilidad | Mensajes de error genéricos | Alta | Alto |
| Mundo real | Terminología técnica | Media | Medio |
| Control | Guardar progreso tardío | Media | Medio |
| Consistencia | Nomenclatura de botones | Baja | Bajo |
| Prevención | Validación de disponibilidad | Alta | Alto |
| Reconocimiento | Requisitos de contraseña | Media | Medio |
| Flexibilidad | Atajos de teclado | Baja | Bajo |
| Estético | Información promocional | Media | Medio |
| Recuperación | Errores de red vs servidor | Alta | Alto |
| Ayuda | Ayuda contextual | Media | Medio |

## Conclusión

El análisis heurístico revela que el flujo de apertura de cuenta presenta una base sólida con áreas de mejora主要集中在 en la comunicación de estados del sistema, la prevención de errores y la recuperación de los mismos. Las soluciones propuestas priorizan cambios de bajo costo que impactan significativamente en la experiencia del usuario, alineándose con las mejores prácticas de diseño móvil financiero.

La implementación de estas mejoras debería resultar en una reducción de la tasa de abandono del flujo y un incremento en la satisfacción del usuario medible a través de pruebas de usabilidad y métricas de producto.

// === ARCHIVO: validacion/metricas-usabilidad.md ===
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
```
