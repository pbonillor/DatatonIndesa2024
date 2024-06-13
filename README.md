# Introducción

Este documento tiene como objetivo proporcionar información relevante para comprender el reto de automatización de la planificación de la producción de la empresa Graphy Cems en el marco de la Dataton 2024 de IndesIA. La documentación incluye una descripción general de IndesIA Dataton, una descripción de Graphy Cems y el reto específico que se plantea en la competición. Además del codigo generado.

# IndesIA Dataton

IndesIA Dataton es una iniciativa anual organizada por la Asociación Industrial para el Impulso de la Economía del Dato y de la Inteligencia Artificial (IndesIA). El objetivo de la Dataton es fomentar el uso de la inteligencia artificial (IA) y el análisis de datos en la industria Española, especialmente en pequeñas y medianas empresas (pymes).

La Dataton reúne a equipos de profesionales, estudiantes e investigadores para competir en el desarrollo de soluciones de IA para retos específicos planteados por empresas reales. Los equipos participantes tienen un tiempo limitado para trabajar en sus soluciones, utilizando los datos proporcionados por las empresas y las herramientas y recursos disponibles en el evento.

# Graphy Cems

Graphy Cems es una empresa Española especializada en la impresión y encuadernación de libros, catálogos, revistas e impresos en general. La empresa cuenta con más de 30 años de experiencia en el sector y está certificada con los estándares de calidad ISO 9001, 14001, PEFC y FSC. Graphy Cems exporta sus productos a toda Europa y se ha posicionado como líder en el mercado español.

#  Reto de Automatización de la Planificación de la Producción

El reto de Graphy Cems en la Dataton 2024 de IndesIA se centra en la automatización de la planificación de la producción. Actualmente, la planificación de la producción en Graphy Cems se realiza de forma manual, lo que resulta un proceso lento y propenso a errores. La empresa busca desarrollar una solución de IA que pueda optimizar la planificación de la producción, reduciendo el tiempo y los costes asociados al proceso actual.

# Especificaciones del Reto

El reto de automatización de la planificación de la producción de Graphy Cems tiene como objetivo desarrollar una solución de IA que pueda:

Analizar los datos históricos de producción y demanda para identificar patrones y tendencias.
Predecir la demanda futura de productos específicos.
Optimizar la planificación de la producción teniendo en cuenta la demanda prevista, la capacidad de producción y los recursos disponibles.
Generar un plan de producción detallado que incluya la programación de las tareas de producción, la asignación de recursos y los tiempos de entrega.
La solución de IA debe ser capaz de integrarse con los sistemas existentes de Graphy Cems y debe ser fácil de usar para el personal de la empresa.

# Datos Disponibles

Graphy Cems proporcionará a los equipos participantes los siguientes datos para trabajar en el reto:

Datos históricos de producción: Estos datos incluyen información sobre los productos fabricados, las cantidades producidas, las fechas de producción y los recursos utilizados.
Datos de demanda: Estos datos incluyen información sobre los pedidos recibidos, las cantidades pedidas, las fechas de entrega y los clientes.
Datos de recursos: Estos datos incluyen información sobre la capacidad de producción de las máquinas y los equipos, la disponibilidad de materiales y la mano de obra disponible.

# Recursos Adicionales

Además de los datos proporcionados por Graphy Cems, los equipos participantes tendrán acceso a los siguientes recursos:

Mentoría de expertos en IA y planificación de la producción.
Talleres y sesiones de formación sobre IA y herramientas de análisis de datos.
Un espacio de trabajo colaborativo con acceso a ordenadores y software.

Finalmente Graphy Cems nos proporciono un resplado de su base de datos del ERM en MYSQL, nos explico las tablas de orden_fabricacion, materiales, impresion, encuadernacion y la tabla prod_plan donde las maquinas de las que dispone para fabricar los libres colocan como se procesaron historicamente las ordenes.

Con esto se resolvio el reto segun la siguiente arquitectura:

1.- Se recibe el pdf con el pedido y el mismo se transforma a texto utilizando langchain 
2.- se valida que en este texto esten los datos necesarios crear una orden de fabricación con campo principal el ISBN de los contrario se devuelve un email al cliente solicitandole que revise la solicitud del pedido
3.- utilizando gpt-4 turbo y el agente sql de langchain se realiza un RAG, es decir se dota a gtp4-turbo de los datos propios de la base de datos de Grapy Cems de tal manera de poder realizar consultas sobre esos datos particulares
4.- con los datos del pdf y la base de datos (consultada a través de un agente RAG SQL de langchain) se le solicita a gpt-4 turbo que valide el pedido y cree los registros en las tablas de orden_fabricion, materiales, impresion y cuadernacion. se hace un pronostico general sobre la planificación para poder imprimir este libro consultando con el mismo metodo pero sobre la tabla de prod_plans
5.- tambien se utiliza todo lo descrito en el punto anterior para realizar preguntas sobre la planificacion y gestión de la producción a un chatbot llamado #helena, todo esto como apoyo a la alta gerencia y a los operadores
6.- utilizando tecnicas de machine learning se entreno un algoritmo por cada maquina y se realizan predicciones las cuales se envian a un reporte en Microsoft Power BI para poder visualizar las predicciones en un formato de storytelling.
7- utilizando modelos avanzados de matematica aplicada se construyo un modelo para la gestión de la planificación

El codigo del proyecto fue desarrollado utilizando notebooks en Databricks y dejando los archivos en el raw del Catalogo de Databricks
![image](https://github.com/pbonillor/DatatonIndesa2024/assets/42980042/fe9e4dd3-8306-449e-9473-7e04de7211ed)

Se estructura de la siguiente manera:



