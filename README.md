# AUTOMATIZACIÓN DE SEGUIMIENTO A MATERIALES PENDIENTES DE ENTREGA

1. Introducción

Presentación del Problema

En mi trabajo actual, gestionamos información de proveedores a través de una tabla que se envia por mail a traves de SAP, ellos la completan y luego se envía por correo electrónico a los analistas según corresponda. Posteriormente, esta información debe ser transcrita manualmente a una hoja de Excel. Este proceso es tedioso, propenso a errores y consume tiempo que podría aprovecharse mejor en la gestión de proveedores que no responden o en la solución de problemas.

Relevancia del Proyecto

Automatizar este proceso mediante IA permitirá reducir la carga de trabajo manual, minimizar errores y optimizar la gestión de la información. La solución propuesta extraerá automáticamente los datos de los correos, los organizará y los volcará en un archivo Excel, mejorando la eficiencia operativa.

2. Desarrollo de la Propuesta de Solución

Uso de IA en la Solución

La solución se basa en modelos de inteligencia artificial que permiten:

Extraer y estructurar datos desde correos electrónicos usando modelos de Texto-Texto.

Generar visualizaciones gráficas automáticas de los datos mediante modelos de Texto-Imagen.

Optimizar la efectividad de la IA utilizando Fast Prompting, reduciendo la cantidad de consultas a la API y mejorando la calidad de la extracción de datos.

Modelo Texto-Texto 
Se utilizará un prompt diseñado para interpretar los correos recibidos de los proveedores y extraer la información clave, devolviéndola en un formato estructurado (JSON o CSV) listo para ser cargado en Excel o en una base de datos.
Ejemplo de Prompt
A partir del siguiente correo, extrae los siguientes datos y devuélvelos en formato JSON:
- Documento de compras
- Posición
- Material
- Texto Breve
- Cantidad de Pedido
- Por entregar (cantidad)
- Unidad medida pedido
- Fe.entrega
- OC Atraso Fecha Estimada
-Observaciones

Si algún dato falta, indica "N/A". El JSON debe ser estructurado de la siguiente manera:

{
    "documento_compras": "[Número de documento]",
    "posición": "[Número de posición]",
    "material": "[Código del material]",
    "texto_breve": "[Descripción del material]",
    "cantidad_pedido": [Número],
    "cantidad_por_entregar": [Número],
    "unidad_medida_pedido": "[Unidad]",
    "fecha_entrega": "[AAAA-MM-DD]",
    "fecha_estimada_atraso": "[AAAA-MM-DD o N/A]",
    "observaciones": "[Texto descriptivo o N/A]"
}

Flujo del proceso:
*	El modelo recibe el correo como entrada.
*	Extrae la información relevante.
* Devuelve los datos en formato estructurado.
* Se automatiza la carga en Excel o base de datos.
  
Modelo Texto-Imagen 
Se utilizará un modelo de generación de imágenes para representar visualmente el estado de las respuestas de los proveedores, generando dashboards automáticos.
Ejemplo de Prompt
Genera una imagen estilo dashboard con los siguientes datos:
- Un gráfico de barras mostrando la cantidad de proveedores que han respondido vs. los que no.
- Un contador con el porcentaje de respuestas recibidas.
- Indicadores en verde para proveedores que respondieron y rojo para los pendientes.
  
Flujo del proceso:
*	Se ingresan los datos extraídos por el modelo texto-texto.
* Se genera la visualización de proveedores con respuesta y sin respuesta.
* La imagen puede ser incluida en reportes o enviados por correo a los responsables.


3. Justificación de la Viabilidad

Para garantizar que la solución es factible dentro del tiempo y recursos disponibles, se consideran los siguientes aspectos:

•	Viabilidad técnica:

o	La extracción de datos puede realizarse con prompts bien estructurados.

o	La generación de dashboards puede hacerse con DALL·E o herramientas similares.

o	Puede implementarse una solución en Python con OpenAI API para automatizar el flujo.

•	Viabilidad económica:

o	Se utilizará una API externa de OpenAI.

o	Se puede establecer un límite de costo por consulta (por ejemplo, no gastar más de X dólares por día/mes).

o	Alternativamente, se podría explorar una solución con modelos open-source gratuitos.

•	Viabilidad en tiempos:

o	El prototipo puede desarrollarse en una semana.
o	Se realizarán pruebas con correos reales para verificar la precisión del modelo.
o	La generación de imágenes se probará en paralelo para asegurar consistencia.


4. Objetivos

Automatizar la extracción de datos desde correos mediante modelos de IA.

Optimizar la interpretación de tablas en los correos utilizando Fast Prompting.

Reducir la cantidad de consultas innecesarias a la API, mejorando la eficiencia y los costos.

Generar dashboards visuales a partir de los datos extraídos, facilitando el análisis de información.

5. Metodología

Pasos del Proyecto

Preprocesamiento de Correos: Se aplicarán técnicas de limpieza de texto para extraer la información relevante.

Uso de Fast Prompting: Se definirán prompts optimizados para extraer datos con la menor cantidad de llamadas a la API.

Conversión de Datos a Formato Excel: Se estructurará la información extraída y se guardará en un archivo Excel.

Generación de Reportes Visuales: Se crearán dashboards automáticos con información clave extraída.

6. Herramientas y Tecnologías

Modelos de IA:

Texto-Texto: GPT-4 (o similar) para extracción de datos.

Texto-Imagen: DALL·E (o similar) para generación de dashboards visuales.

Entorno de Desarrollo:

Google Colab para programación y ejecución.

Almacenamiento de Datos:

Pandas para manejo y conversión a Excel.

Optimización:

Fast Prompting para mejorar la eficiencia en consultas a la API.

7. Implementación (en Google Colab)

Se desarrollará un código en Python que incluya:

Un prompt optimizado para extraer tablas de correos.

Conversión y almacenamiento en un archivo Excel.

Generación de visualizaciones mediante IA generativa.

Interactividad para que el usuario pueda ingresar diferentes correos y observar los resultados.

