# Ecosistema de Automatización IA: Cotizador Polietileno B2B

## 📄 Descripción del Proyecto

Este repositorio contiene la solución completa de automatización para la gestión, procesamiento, aprobación y envío de cotizaciones industriales en el sector de plásticos/polietileno B2B.

**✅ Correcciones aplicadas para la Entrega Final:**
* **Estrategia Multi-Modelo:** Se implementó un ruteo dinámico con un nodo IF. Las cotizaciones complejas o urgentes se procesan con **Gemini Pro**, mientras que las estándar se derivan a **Gemini Flash** para optimizar costos y velocidad.
* **Bifurcación Completa (HITL):** Se añadió lógica de ramificación tras el nodo Wait. Si se aprueba, los datos se persisten en Airtable y se notifica el éxito. Si se rechaza, se envía un correo de cancelación sin contaminar la base de datos.

## 🗂️ Estructura del Repositorio y Entregables

* **diagrama_de_flujo.pdf**: Visualización técnica interactiva de la arquitectura del flujo n8n actualizada.
* **DOCUMENTACION_TECNICA.pdf**: Documento completo con la arquitectura del flujo y detalle de nodos.
* **screenshots.pdf**: Capturas de pantalla verificadas de las rutas de éxito, rechazo y base de datos.
* **Cotizador_Polietileno_B2B_Final.json**: Archivo de exportación oficial del flujo ejecutable en n8n.
* **Matriz de Decisión y Cuadro Comparativo de Modelos de IA.pdf**: Justificación técnica de costos y modelos.
* **README.md**: Especificaciones integrales del sistema (este documento).

## 📋 Ficha Técnica por Caso de Uso

**Objetivo:** Optimizar y automatizar el tiempo de respuesta a clientes B2B, eliminando la carga manual y reduciendo el tiempo de procesamiento.

**Trigger:** Webhook (HTTP POST) que recibe el payload JSON.

**Pasos del Flujo:**
1. **Trigger:** Webhook captura la petición del cliente.
2. **Evaluación de Complejidad:** Nodo IF detecta si el pedido es urgente.
3. **IA Multi-Modelo:** Se deriva la consulta a Gemini Pro o Gemini Flash para generar la cotización estructurada.
4. **Estructuración:** Nodo de código extrae el JSON limpio.
5. **Human in the Loop (HITL):** Nodo Wait pausa la ejecución solicitando revisión humana mediante formulario web.
6. **Bifurcación (Aprobado o no):** Nodo IF evalúa la decisión humana.
7. **Rama Aprobado (True):** Se registra la cotización en Airtable y se envía correo de confirmación vía Gmail.
8. **Rama Rechazado (False):** Se envía correo de disculpas al cliente (sin crear registro en Airtable).
9. **Manejo de Errores (Error Handling):** Flujo paralelo captura excepciones globales y envía alerta inmediata por Gmail al administrador.

## 🛠️ Tecnologías Utilizadas

* **Orquestador:** n8n Cloud
* **IA:** Google Gemini API (Pro y Flash)
* **Base de Datos:** Airtable
* **Comunicaciones:** Gmail API
* **Control de Errores:** Error Trigger + Alertas Automatizadas

## 📊 Enlaces de Acceso Público

* **Dashboard de Control (Airtable):** [Ver Dashboard](https://airtable.com/appqUAYkJzmn8N1Nr/shrWVY9Fyl4qjpWa8)
* **Base de Datos (Airtable):** [Ver Base de Datos](https://airtable.com/appqUAYkJzmn8N1Nr/shrjSUZI9ekxbMN7b)

## 📹 Video Demostrativo

🎥 [Enlace al video de Loom/Drive - Pendiente de agregar]

## 📊 8. Enlaces de Acceso Público
  - **Dashboard de Control (Airtable Shared View): https://airtable.com/appqUAYkJzmn8N1Nr/shrWVY9Fyl4qjpWa8
  <img width="1915" height="1008" alt="image" src="https://github.com/user-attachments/assets/2909b323-142b-4651-aef4-d32c920c2c2c" />

  Base de Datos / Tabla (Airtable): https://airtable.com/appqUAYkJzmn8N1Nr/shrjSUZI9ekxbMN7b (si abre en incógnito sin login)
   <img width="1920" height="1043" alt="image" src="https://github.com/user-attachments/assets/61b9ed18-4ec0-4073-8021-10aad214c0f6" />

- **Repositorio Oficial:** [Ver en GitHub](https://github.com/matiPerez1982/cotizador-polietileno-n8n)

---

## 📹 Video Demostrativo

Puedes ver la demostración completa del funcionamiento del sistema (flujo en n8n, interacción con la IA, aprobación humana y envío de correos) en el siguiente enlace:

🎥 [**Ver Video del Proyecto en Google Drive**](https://drive.google.com/file/d/1FBo74pHhKuJ39We8rpdERrUIuRLpqzPv/view?usp=sharing)

---
*Desarrollado para el Proyecto Final del Curso de Automatización e IA.*
