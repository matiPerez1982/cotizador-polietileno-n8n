# Ecosistema de Automatización IA: Cotizador Polietileno B2B

## 📄 Descripción del Proyecto
Este repositorio contiene la solución completa de automatización para la gestión, procesamiento, aprobación y envío de cotizaciones industriales en el sector de plásticos/polietileno B2B.

El sistema integra inteligencia artificial para análisis dinámico de requerimientos, procesamiento con Human-in-the-Loop (HITL), persistencia en base de datos relational/Airtable, comunicación multicanal y arquitectura resiliente con manejo de errores global.

---

## 🗂️ Estructura del Repositorio y Entregables

De acuerdo con las especificaciones y normativas de la entrega final:

* 📄 **[Diagrama de Flujo (PDF)](./diagrama_de_flujo.pdf)**: Visualización técnica interactiva de la arquitectura del flujo n8n.
* 📷 **[Documentación de Screenshots / Evidencias (PDF)](./screenshots.pdf)**: Capturas de pantalla verificadas de cada etapa y ejecuciones exitosas.
* ⚙️ **`Cotizador_Polietileno_B2B.json`**: Archivo de exportación oficial del flujo ejecutable en n8n.
* 📝 **`README.md`**: Especificaciones integrales del sistema (este documento).

---

## 📋 Ficha Técnica por Caso de Uso (Los 7 Puntos de la Rúbrica)

### Caso de Uso 1: Cotización Automática y Proceso Multicanal B2B

1. **Objetivo / Problema del Negocio (1-2 frases):**  
   Optimizar y automatizar el tiempo de respuesta a clientes B2B para solicitudes de cotización de polietileno industrial, eliminando la carga manual y reduciendo el tiempo de procesamiento de días a segundos.

2. **Trigger / Disparador:**  
   `Webhook` (HTTP POST) que recibe el payload JSON con la solicitud del cliente (Nombre, Email, Especificaciones técnicas del polietileno).

3. **Agente(s) / Pasos (en orden):**  
   * **Paso 1 (Trigger):** Webhook captura la petición.
   * **Paso 2 (IA Agent - Google Gemini): El nodo de Google Gemini (modelo `models/gemini-pro-latest`) evalúa el texto, especificaciones de micrones y volumen, y genera la cotización personalizada en formato estructurado.
   * **Paso 3 (Estructuración):** `Code in JavaScript` normaliza las variables del resultado.
   * **Paso 4 (Human in the Loop):** `Wait` pausa la ejecución solicitando la validación o revisión previa antes de impactar sistemas centrales.
   * **Paso 5 (Base de Datos):** `Create a record` escribe el resultado en Airtable.
   * **Paso 6 (Multicanalidad):** `Send a message (Gmail)` envía la cotización final confirmada al correo del cliente.

4. Mecanismo Human-in-the-Loop (HITL):
* El flujo ejecuta un nodo de pausa Wait antes de la salida crítica.
* Validación: El supervisor revisa el borrador de la cotización (Cliente, Producto, Volumen, Micrones, Precio Estimado).
* Rama Aprobado: Se actualiza el estado en Airtable a "Aprobado" y se despacha automáticamente el correo al cliente vía Gmail.
* Rama Rechazado: Se registra en Airtable con estado "Requiere revisión" y se envía una notificación interna para ajuste manual. (Evidencia visual documentada en el archivo screenshots.pdf).

5. Outputs (Ejemplo de Ejecución Real):
* Registro creado en Airtable (ID de Registro: recPCRLJmrx6gZpRT, Estado: "Aprobado").
* Correo electrónico de confirmación despachado por Gmail (Message ID: 19fb118a65ab8a35).
*(Verificado en screenshots.pdf - pantallas de Airtable y Gmail).*

6. Límites y Manejo de Errores (Error Handling & Rules):
* Si falta un dato obligatorio o falla la llamada a la API de Gemini/Airtable, el flujo secundario Error Trigger atrapa la excepción globalmente y ejecuta Gmail Error Alert, notificando inmediatamente al responsable de operaciones con el ID de ejecución. (Evidencia del flujo de fallos detallada en diagrama_de_flujo.pdf y verificado en screenshots.pdf).
  
7. **Resultado Esperado / Impacto:**  
   * Reducción del 95% en el tiempo de procesamiento de cotizaciones.
   * Eliminación de errores de tipeo manuales.
   * Respuesta inmediata multicanal (Airtable + Correo al Cliente).

---

## 🛠️ Tecnologías Utilizadas

* Orquestador: n8n Cloud
* IA: Google Gemini API (`models/gemini-pro-latest` - Free Tier)
* Base de Datos: Airtable
* Comunicaciones: Gmail API
* Control de Errores: Error Trigger + Alertas Automatizadas

---

## 📊 8. Enlaces de Acceso Público

- **Dashboard de Control y Base de Datos (Shared View):** [Ver en Airtable](https://airtable.com/appqUAYkJzmn8N1Nr/shrjSUZI9ekxbMN7b)
- **Repositorio Oficial:** [Ver en GitHub](https://github.com/matiPerez1982/cotizador-polietileno-n8n)

---
*Desarrollado para el Proyecto Final del Curso de Automatización e IA.*
