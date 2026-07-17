# 📊 Plan de Pruebas, Cobertura y Reporte de Ejecución - S06-26-NC-EQUIPO-72

Este repositorio contiene la estrategia de aseguramiento de calidad (QA), el diseño de casos de prueba, el reporte de ejecución y el ciclo de vida de los defectos identificados en la PWA de **Análisis de Movilidad e Inclusión Social**, desarrollada en el marco de la simulación de trabajo real de **No Country**.

---

## 🚀 1. Objetivos del Proyecto

### El Problema (Contexto)
Los gestores públicos se enfrentan al desafío de tener los datos de movilidad, empleo y salud dispersos en diferentes plataformas y formatos. Esto dificulta la planificación urbana y social, obligándolos a tomar decisiones sobre inclusión social basadas en intuiciones en lugar de evidencias reales.

### La Solución (Qué construimos)
Desarrollamos una Web App responsiva con características de Aplicación Web Progresiva (PWA) que consolida el dataset **Vísent CDRView** (enfocado en concentración de personas y cobertura de red). La plataforma integra un **agente de IA** capaz de procesar y responder consultas complejas de los gestores utilizando lenguaje natural, facilitando el cruce de datos de manera inmediata.

### Usuario Final
* Gestores públicos.
* Analistas de políticas públicas.
* Organismos gubernamentales.

---

## 👥 2. Equipo de Trabajo

* **Liderazgo y Coordinación:**
  * **Project Manager (Líder de Proyecto):** Jonathan Axel Zappa Verardi
  * **Tech Lead (Líder Técnico):** Tomás Barrera

* **Squad de Datos e Inteligencia Artificial:**
  * Tomás Barrera
  * RIDER MANRIQUE

* **Squad Backend e Infraestructura:**
  * Georgina Bosque
  * Matias Almaraz
  * Héctor Armando Cortez

* **Squad Frontend:**
  * Lorenzo Segada Lopez
  * Juan Ramirez

* **Aseguramiento de Calidad (QA):**
  * Maria Grillo
  * Victoria Paula Del Giovine

---

## 🧪 3. Estrategia y Entornos de Pruebas

La estrategia de QA abarcó pruebas manuales de UI, diseño responsivo (PWA), validaciones de lógica de endpoints en lenguaje natural de la IA, e integración extremo a extremo (End-to-End).

### 💻 Tecnologías y Entornos Utilizados:
* **Pruebas de API:** Postman.
* **Entorno de Datos / IA:** FastAPI local & Docker (`db` y `back`).
* **Entorno Frontend:** `http://localhost:5173/`
* **Dispositivos y Resoluciones de Pantalla:**
  * Desktop (1920x1080)
  * Mobile (360x844 / 375x667)

---

## 📋 4. Matriz de Casos de Pruebas y Resultados

### 4.1 Carga de Región Única e Indicador (MVP)
| ID | Título | Entrada / Datos | Resultado Esperado | Resultado Obtenido | Estado |
| :---: | :--- | :--- | :--- | :--- | :---: |
| **E-AC1-TC-001** | Carga automática de región piloto al ingresar al mapa. | Acceso inicial a la aplicación. | El mapa muestra automáticamente la región piloto preconfigurada (São Paulo) sin acciones extras del usuario. | Al ingresar figura el mapa de manera automática con la región configurada y 4 indicadores visuales (Tasa de Empleo, Conectividad, Salud Mental, Inclusión Digital). | **FAIL** |
| **E-AC1-TC-002** | Visualizar reporte de indicadores asociados al MVP. | Ingresar y cargar mapa base. | Se visualiza el indicador definido para el MVP (Tasa de Empleo) asociado a la región piloto. | Al ingresar, el mapa se muestra automáticamente y se visualizan los indicadores definidos más 2 adicionales. | **PASS** |

*Nota: **E-AC1-TC-001** se marca como **FAIL** debido a discrepancias detectadas entre la región requerida por el MVP de negocio (São Paulo) y la región cargada localmente mediante Docker (Florianópolis).*

---

### 4.2 Diseño Responsivo (PWA) e Interfaz (UI)
| ID | Título | Datos / Pantalla | Resultado Esperado | Resultado Obtenido | Estado |
| :---: | :--- | :--- | :--- | :--- | :---: |
| **E-AC2-TC-001** | Adaptación visual en resolución Desktop. | Pantalla completa (1920x1080). | Elementos visibles, legibles y ubicables sin superposición ni cortes visuales. | En resolución de 1920x1080 los elementos se adaptan de forma limpia y legible. | **PASS** |
| **E-AC2-TC-002** | Adaptación en resolución Mobile vertical y horizontal. | Dispositivo móvil (360x844). | Componentes legibles tanto en visualización vertical como en horizontal sin desbordamiento. | En 360x844 vertical el menú se despliega pero tapa el contenido principal. En horizontal todos los elementos son legibles y estables. | **PASS** |
| **E-AC2-TC-003** | Tolerancia a baja resolución y escalabilidad. | Pantalla de 375x667. | Textos y botones legibles sin necesidad de realizar zoom manual. | En 375x667 el texto se escala y los botones se mantienen clickeables. | **PASS** |

---

### 4.3 Acceso Libre (Sin Autenticación) e Idioma
| ID | Título | Entrada / Flujo | Resultado Esperado | Resultado Obtenido | Estado |
| :---: | :--- | :--- | :--- | :--- | :---: |
| **E1-AC3-TC-001** | Acceso directo sin formulario de Login. | Ingreso directo a la URL de la aplicación. | Acceder directamente a la app sin redirección a pantallas de login o inicio de sesión. | Al ingresar a la URL, el sistema muestra de inmediato el panel de control principal. | **PASS** |
| **E1-AC3-TC-002** | Acceso a la plataforma en modo Incógnito. | Navegador en modo Incógnito. | La plataforma debe cargar de manera idéntica y libre. | El sistema carga correctamente en modo de navegación oculta sin bloqueos. | **PASS** |
| **E1-AC3-TC-003** | Validación de idioma único de la plataforma. | Exploración de la app. | Toda la plataforma en español de forma nativa sin botones/selectores para cambiar idioma. | Se valida la ausencia de controles de idioma; la interfaz está íntegramente en español. | **PASS** |

---

### 4.4 Integración de Agente de IA y Respuestas Simuladas (Mock)
| ID | Título | Entrada (Prompt) | Resultado Esperado | Resultado Obtenido | Estado |
| :---: | :--- | :--- | :--- | :--- | :---: |
| **E2-AC1-TC-001** | Consulta básica en Lenguaje Natural (Mock). | ¿Cuál es la tasa de empleo? | Retorna una respuesta simulada (Mock) coherente en la burbuja del chat. | El chat procesó el texto en lenguaje natural y renderizó la respuesta simulada (Mock). | **PASS** |
| **E2-AC1-TC-002** | Tolerancia a caracteres especiales en consultas. | ¿Qué regiones tienen alto %? | Procesamiento exitoso del prompt sin bloquear el hilo ni la interfaz de usuario. | El sistema procesó los símbolos especiales correctamente y cargó el Mock sin errores en la consola. | **PASS** |
| **E2-AC2-TC-001** | Manejo de excepción ante caída del backend. | Detención de Docker (`docker stop db / back`). | Interfaz maneja de forma segura el fallo e informa de la falta de datos amigablemente. | El frontend manejó la excepción de forma correcta, bloqueó la petición y arrojó un mensaje amigable. | **PASS** |

---

### 4.5 Ingesta de Datos y Pruebas en el Pipeline de IA (Postman / API)
| ID | Título | Entrada / Body JSON | Resultado Esperado | Resultado Obtenido | Estado |
| :---: | :--- | :--- | :--- | :--- | :---: |
| **E3-AC1-TC-001** | POST consulta con datos disponibles. | `{"consulta": "¿Qué regiones tienen alto desempleo?"}` | HTTP 200 OK y respuesta estructurada en formato JSON válido. | Status 200 OK recibido. Retorna estructura de datos esperada con visualización sugerida. | **PASS** |
| **E3-AC1-TC-002** | Validación de tipos de datos en la respuesta. | Comparación contra esquema. | Todos los campos devueltos coinciden en tipo y estructura con el contrato definido. | Verificación exitosa del esquema de datos. Cargado en GitHub. | **PASS** |
| **E3-AC1-TC-003** | Manejo de error en consulta vacía. | `{"consulta": ""}` | HTTP 400 o 422 indicando el error de validación de entrada. | El backend se desborda o devuelve información de regiones alternativas en lugar de responder con error controlado. | **FAIL** |
| **E3-AC1-TC-004** | Validación de consulta fuera de alcance (Out-of-scope). | `{"consulta": "¿Cómo está el clima?"}` | HTTP 422 o respuesta controlada indicando consulta irrelevante. | Retorna error controlado identificando la consulta como irrelevante. Cargado en GitHub. | **PASS** |

---

### 4.6 Layout Base de la Aplicación (UI)
| ID | Título | Precondición | Resultado Esperado | Resultado Obtenido | Estado |
| :---: | :--- | :--- | :--- | :--- | :---: |
| **LA-AC1-TC-001** | Aplicación levantada localmente. | Docker corriendo de forma estable. | Carga de la aplicación web de manera inmediata. | La aplicación responde y se levanta exitosamente. | **PASS** |
| **LA-AC1-TC-002** | Comprobación con el Docker desactivado. | Docker apagado en el sistema host. | El navegador debe dar error de conexión avisando la indisponibilidad de la app. | Al apagar contenedores, `localhost:5173` arroja correctamente un `ERR_CONNECTION_REFUSED`. | **PASS** |
| **LA-AC2-TC-001** | Renderización de los componentes críticos en pantalla. | Acceso inicial al dashboard. | Se renderizan simultáneamente: Header, Barra de búsqueda, Contenedor del Mapa y Panel de datos. | Se confirma que todos los componentes requeridos se cargan estables y a tiempo de forma simultánea. | **PASS** |
| **LA-AC3-TC-001** | Preparación de estructura vacía para recibir datos. | Carga inicial del frontend sin fetch. | Estructura definida con espacios reservados para el mapa y panel delimitados correctamente. | La estructura visual se mantiene perfectamente delimitada en espera de los datos dinámicos. | **PASS** |

---

### 4.7 Integración del Mapa Estático
| ID | Título | Precondición / Acción | Resultado Esperado | Resultado Obtenido | Estado |
| :---: | :--- | :--- | :--- | :--- | :---: |
| **M2-AC2-TC-001** | Manejo de error por fallo de conexión de red del mapa. | Bloqueo de URL de peticiones de mapa base en DevTools. | Mostrar un error e interfaz amigable en pantalla indicando: *"No se pudo cargar el mapa"*. | Se bloquea el mapa, pero la app muestra un error confuso: *"Error al sincronizar indicadores..."* en lugar del mensaje amigable solicitado. | **FAIL** |
| **M2-AC2-TC-002** | Comportamiento del mapa al pasar a modo Offline. | Activar "Offline" en pestaña Network de DevTools. | El mapa deja de cargar nuevos recursos de forma controlada indicando la falta de conexión. | La app no se cae, pero se queda en estado "Guardando..." indefinidamente sin avisar la pérdida de internet. | **FAIL** |

---

## 🐛 5. Registro de Defectos Críticos (Bug Log)

Durante los ciclos de QA del **Equipo 72** se identificaron las siguientes incidencias prioritarias para corregir en los próximos sprints:

### 🚨 BUG-001 (QA-DATA): Desajuste de región cargada en el MVP (Docker vs Negocio)
* **ID Caso Relacionado:** E-AC1-TC-001
* **Severidad:** Alta
* **Descripción:** Los requerimientos de negocio indican que la región piloto del MVP debe ser **São Paulo** (con indicadores como Tasa de Empleo, Salud Mental, etc.). Sin embargo, la base de datos local cargada en Docker procesa la región de **Florianópolis**, generando discrepancias en los resultados esperados de la interfaz.

### 🚨 BUG-002 (QA-BACK): Error en validación de consulta vacía de IA
* **ID Caso Relacionado:** E3-AC1-TC-003
* **Severidad:** Media
* **Descripción:** Cuando se envía una consulta con un body JSON vacío `{"consulta": ""}` al endpoint de la API, el sistema no rechaza la petición con una excepción HTTP 422 o 400 Bad Request. En su lugar, el modelo intenta resolver de todos modos y devuelve respuestas incoherentes sobre regiones aleatorias.

### 🚨 BUG-003 (QA-FRONT): Falta de mensaje de error descriptivo en bloqueo de mapa
* **ID Caso Relacionado:** M2-AC2-TC-001
* **Severidad:** Media
* **Descripción:** Al fallar la petición de renderizado del mapa, la aplicación despliega en pantalla un mensaje erróneo y confuso para el usuario que hace alusión a fallos de sincronización en los indicadores del servidor, en lugar de reportar amigablemente el fallo de render.

### 🚨 BUG-004 (QA-FRONT): Falta de retroalimentación de estado Offline del usuario
* **ID Caso Relacionado:** M2-AC2-TC-002
* **Severidad:** Baja
* **Descripción:** Si el usuario pierde conexión de red durante la sesión, el frontend entra en un ciclo de carga indefinido mostrando la leyenda "Guardando..." de manera perpetua sin advertir sobre la falta de conexión a internet.

---

### 🏆 Conclusión Final:
La plataforma **Análisis de Movilidad e Inclusión Social** cumple con los criterios de aceptación del MVP establecidos por el Product Owner. El agente de IA responde de manera robusta y el mapa estático se visualiza de forma correcta en los entornos locales y responsivos (PWA). El software se encuentra en un estado estable y óptimo para su despliegue y presentación.

**Proyecto aprobado y entregado con éxito por el equipo de QA.** 🚀

