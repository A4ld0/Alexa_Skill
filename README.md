Cumple Gestor – Alexa Skill

Cumple Gestor es una skill de Alexa diseñada para organizar fiestas de cumpleaños.
Permite registrar personas con sus gustos, consultar su información y generar listas de compras personalizadas basadas en sus preferencias.

Funcionalidad principal
Registro de personas

La skill guía al usuario paso a paso para capturar:

Nombre

Fecha de nacimiento

Temática favorita

Colores favoritos

Snacks favoritos

Tipo de música

Estilo de decoración

La información queda almacenada para usarse posteriormente.

Consulta de personas

Funciones disponibles:

Listar todas las personas registradas

Ver los detalles completos de una persona específica

Generación de listas de compras

Con base en la temática y gustos capturados, la skill genera una lista personalizada usando:

Plantillas base por tema

Reglas que ajustan la lista según colores, snacks, música y decoración

Cada lista queda asociada a la persona seleccionada.

Gestión de las listas de compras

El usuario puede:

Marcar artículos como comprados

Revisar qué falta por comprar

Cerrar una lista cuando todos los artículos están marcados

Persistencia en S3

Los datos se guardan en un archivo JSON dentro de un bucket S3.
Esto permite que las personas y sus listas persistan entre sesiones.

Estructura del proyecto
lambda_function.py

Punto de entrada de la función Lambda

Configura y registra todos los handlers

Maneja launch, help, stop y fallback

Módulos de intents (intents_*.py)

Cada archivo maneja un intent específico:

Registro de persona

Continuación del registro

Confirmación del registro

Listar personas

Consultar persona

Generar lista de compras

Marcar artículos

Cerrar listas

La conversación del registro se controla mediante estado de sesión.

storage.py

Capa de persistencia sobre S3:

Guarda y obtiene personas

Guarda y obtiene listas de compras

Normaliza nombres

Administra un JSON central dentro del bucket

templates.py

Plantillas de artículos por temática

Diccionario de sinónimos para normalizar los temas ingresados por voz

rules_engine.py

Ajusta plantillas base utilizando preferencias individuales

Agrega colores, snacks, música y decoración a la lista final

models.py

Define las clases Person y Birthday

Incluye métodos to_dict y from_dict

utils.py

Generación de URLs prefirmadas para acceder a archivos en S3 cuando se requiera

Flujo básico de uso

Abrir la skill
"Alexa, abre cumple gestor"

Registrar persona
"Registra una persona"
Alexa realiza preguntas paso por paso.

Consultar personas
"Lista mis personas"
"Muestra información de Sofia"

Generar lista
"Genera la lista de compras para Sofia"

Marcar artículos
"Marca globos verdes como comprado"

Cerrar lista
"Cierra la lista"

Requisitos

Cuenta de AWS

Función Lambda con permisos de lectura y escritura en S3

Bucket S3 configurado para el archivo JSON

Configuración del modelo de interacción en Alexa Developer Console
