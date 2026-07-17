# 📄 README - Plan de Pruebas y Reporte de Ejecución - S03-26-Equipo 13

Este repositorio contiene la estrategia de aseguramiento de calidad (QA), el diseño de casos de prueba, el reporte de ejecución y el ciclo de vida de los defectos identificados en la plataforma **Startup CRM**. El proyecto ha sido desarrollado en el marco de la simulación de trabajo real de **No Country**.

---

## 🚀 1. Resumen del Proyecto y Participantes

**Startup CRM** es una plataforma inteligente con integración nativa a WhatsApp y correo electrónico, diseñada para startups que gestionan relaciones con leads y clientes en tiempo real. La herramienta centraliza conversaciones, automatiza seguimientos y segmenta usuarios de forma colaborativa y asincrónica.

### 👥 Equipo de Trabajo:
* **Product Owner:** Mariana Conte 🇦🇷
* **QA Tester:** Maria Grillo 🇦🇷
* **Frontend Developers:** Joaquín Romero 🇦🇷 | Yerlin Rojas 🇦🇷
* **Backend Developers:** Max Jherzon Rodas Palacios 🇧🇴 | Sara Villegas Gusmán 🇨🇴

### 🎯 Objetivos de QA:
1. Validar el cumplimiento de los requerimientos funcionales críticos (Autenticación, Contactos, Tareas y Mensajería).
2. Garantizar que la API REST responda según los códigos de estado HTTP estándar (200, 201, 400, 401, 403, 500).
3. Reportar, documentar e iniciar el ciclo de resolución de los defectos (bugs) detectados en el Frontend (Web App) y el Backend (API).

---

## 🧪 2. Estrategia y Plan de Pruebas

El plan de pruebas abarcó pruebas funcionales, pruebas de integración de API (caja negra) utilizando herramientas como **Insomnia** y **Thunder Client**, y pruebas de interfaz de usuario (UI) de manera manual en el navegador Google Chrome.

### 💻 Entornos de Pruebas Utilizados:
* **Entorno de API:** `http://localhost:3001`


---

## 📋 3. Matriz de Casos de Prueba y Resultados (Resumen)

Se ejecutó una matriz unificada de pruebas funcionales sobre el sistema. A continuación, se detallan algunos de los casos de prueba clave:

| ID | Módulo / Funcionalidad | Descripción del Caso de Prueba | Inputs / Datos | Resultado Esperado | Estado |
| :---: | :--- | :--- | :--- | :--- | :---: |
| **TC-AUTH-01** | Registro de Usuario (API) | Registrar un usuario nuevo de forma exitosa | maria_test@ejemplo.com, Password123!, Maria Lombardi | 201 Created | **EXITOSA** |
| **TC-AUTH-02** | Registro de Usuario (API) | Impedir el registro de un email duplicado | maria_test@ejemplo.com (duplicado) | 400 Bad Request / 409 Conflict | **EXITOSA** |
| **TC-AUTH-05** | Inicio de Sesión (API) | Verificar la autenticación con credenciales válidas | maria_test_01@correo.com, Password123! | 200 OK | **EXITOSA** |
| **TC-CONT-01** | Creación de Contacto (API) | Crear un nuevo contacto básico en el CRM | Name: Pablo Lombardi, Email: pablo@test.com | 201 Created | **EXITOSA** |
| **TC-CONT-04** | Eliminar Contacto (API) | Verificar restricción de permisos para no-admins | Token de Portador (No Admin) | 403 Forbidden | **EXITOSA** |
| **REG-02** | Formulario Contacto (Web) | Bloquear duplicación de emails en el listado | test@mail.com (ya existente) | Mensaje "Ya existe un usuario con ese email" | **FALLIDA** |
| **REG-09** | Gestión de Tareas (Web) | Validar obligatoriedad de título de tarea | Título: (Vacío) | Mensaje "El título es obligatorio" | **EXITOSA** |

---

## 🐛 4. Gestión de Defectos (Bug Log)

Durante los ciclos de prueba funcionales e integrados, se registraron los siguientes defectos críticos:

### 🚨 BUG-REG-001: Falta de validación de correos duplicados en Frontend
* **Severidad:** Alta
* **Descripción:** Al intentar registrar un contacto desde el formulario web utilizando un correo electrónico que ya existe en la base de datos, el sistema completa el flujo con éxito en lugar de validar la duplicidad e informar al usuario.
* **Pasos para reproducir:**
**Pasos para reproducir:**
1. Ir a `https://vigu.blog/dashboard/contactos`.
2. Registrar un contacto con el email `test@mail.com`.
3. Intentar registrar un segundo contacto con el mismo email `test@mail.com`.
   
* **Resultado Esperado:** Alerta indicando: *"Ya existe un usuario con ese email"*.
* **Resultado Obtenido:** Se registra duplicado en el listado visual sin restricción.

### 🚨 BUG-CONT-001: Error 500 en actualización de Status
* **Severidad:** Alta
* **Descripción:** El campo `status` de los contactos falla con un Error 500 al ser editado mediante peticiones PATCH de API, mientras otros datos de contacto se procesan de manera correcta.
* **Estado:** Pendiente de revisión técnica en el Backend.

### 🚨 BUG-AUTH-001: Error de Autenticación 401 en Logout y Perfil (Solucionado)
* **Severidad:** Crítica
* **Descripción:** El botón de Logout del Frontend no respondía y los endpoints protegidos (como `/me` o `/setup-channels`) devolvían un Error 401 Unauthorized debido a que el Token Bearer no era reconocido.
* **Causa Raíz:** Falta de la variable `JWT_SECRET` en el archivo `.env`.
* **Estado:** **RESUELTO** (Verificado tras la corrección en variables de entorno).

---

## 🎯 5. Conclusiones y Recomendaciones

* **Recomendación:** En lugar de mostrarle al usuario el mensaje del sistema en inglés ("email must be an email"), muestra un aviso amigable en español como: "Por favor, escribe un correo electrónico válido".
* **Próximo Paso:** Desarrollar y desplegar la corrección en el Frontend para validar la unicidad del email de contactos (BUG-REG-001) para resguardar la integridad del listado.
