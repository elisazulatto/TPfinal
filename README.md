# Asistente de consultas por email con IA

## Descripción

Proyecto final de automatización desarrollado con n8n para gestionar consultas recibidas por correo electrónico utilizando inteligencia artificial.

El sistema recibe correos mediante Gmail, registra las consultas en Airtable y utiliza OpenAI para clasificar el mensaje, determinar su prioridad, generar un resumen y proponer una respuesta.

Antes de enviar cualquier respuesta al cliente, el workflow incorpora una instancia de aprobación humana.

## Tecnologías utilizadas

- n8n
- Gmail
- Airtable
- OpenAI GPT-4o mini

## Flujo general

1. Gmail detecta un nuevo correo.
2. La consulta se registra en Airtable.
3. Se valida que el correo contenga un mensaje.
4. OpenAI analiza la consulta.
5. La IA devuelve:
 - Categoría
 - Prioridad
 - Resumen
 - Respuesta sugerida
6. Los resultados se almacenan en Airtable.
7. El workflow espera la aprobación humana.
8. Si la respuesta es aprobada, Gmail envía el correo.
9. Si no es aprobada, la consulta queda con estado Rechazado.
10. Los errores detectados durante el procesamiento quedan registrados en Airtable.

## Human in the Loop

Las respuestas generadas por inteligencia artificial no se envían automáticamente.

Antes del envío, una persona debe revisar la respuesta en Airtable y aprobarla mediante el campo "Aprobación humana".

Si la respuesta es aprobada, el workflow continúa con el envío. En caso contrario, el correo no se envía.

## Manejo de errores

El workflow contempla distintos escenarios de error.

Si el correo no contiene un mensaje, no se realiza una llamada a OpenAI y la consulta queda registrada con estado "Error".

También se configuró una salida específica de error para OpenAI, permitiendo registrar en Airtable los problemas que puedan producirse durante el procesamiento.

## Optimización de costos

Se seleccionó GPT-4o mini por su relación entre costo, velocidad y capacidad para tareas de clasificación y generación de respuestas breves.

Además, la salida del modelo se encuentra limitada a un máximo de 400 tokens para controlar el consumo por ejecución.

## Base de datos

La información se almacena en Airtable utilizando dos tablas relacionadas:

- Clientes
- Consultas

La relación es de tipo 1:N: un cliente puede tener múltiples consultas y cada consulta puede estar asociada a un único cliente.

## Dashboard

Se desarrolló un dashboard de control en Airtable para visualizar indicadores del funcionamiento del sistema, incluyendo:

- Total de consultas
- Consultas enviadas
- Consultas con error
- Tasa de error
- Consultas agrupadas por estado

### Link al dashboard / base de datos
https://airtable.com/appnqNoRAWAFyk4Eu/pag4fWRVO4noPCwg0/edit

## Documentación

La documentación completa del proyecto se encuentra incluida en este repositorio e incluye:

- Arquitectura de la solución
- Estructura de datos
- Matriz de selección del modelo
- Optimización de costos
- Seguridad y resiliencia
- Pruebas realizadas
- Evidencias mediante capturas de pantalla
- Dashboard de control

## Evidencias de prueba

Se validaron diferentes escenarios:

- Happy path completo con envío exitoso del correo.
- Correo sin contenido.
- Rechazo durante la aprobación humana.
- Procesamiento con límite máximo de 400 tokens.
- Registro de estados y errores en Airtable.

## Archivos principales

- Documentación completa del proyecto.
- Workflow de n8n exportado en formato JSON.
- Evidencias de ejecución.
- Diagrama de arquitectura.

## Autor

María Elisa Zulatto
