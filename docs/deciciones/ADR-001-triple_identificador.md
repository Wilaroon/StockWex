ADR-001

Título:
Las imágenes de los productos se almacenarán en una tabla independiente.

Motivo:

Un producto puede tener múltiples imágenes.
Se evita repetir columnas.
Permite escalar.
Facilita almacenamiento en S3.

Consecuencias:

Se requiere un JOIN para obtener las imágenes.

Titulo: Estrategia de Triple Identificador en la Tabla de Productos

Contexto
Para balancear rendimiento, seguridad y logica de negocio, la tabla productos usara tres identificadores distintos:

id (BigInt): Clave primaria interna. Solo para JOINs y relaciones.

uuid (UUIDv4): Identificador publico. Solo para URLs, APIs y uso externo.

code (String): Identificador de negocio (SKU/Codigo de barras). Editable por el usuario.

Consecuencias

Beneficios

Seguridad: El uuid evita el rastreo (scraping) de datos por ID secuencial.


Velocidad: Los JOINs internos siguen siendo numericos y super rapidos.


Flexibilidad: El cliente puede cambiar su SKU (code) sin romper la base de datos.

Costos y Mitigaciones

Almacenamiento: El uuid y el code consumen mas espacio en disco. (Mitigacion: Costo marginal aceptable por el beneficio ).


Carga mental: El equipo debe recordar la regla: id para backend/DB, uuid para APIs/rutas, code para busquedas del usuario.


indices extra: Requiere indices unicos para uuid y code, lo que ralentiza un poco los INSERT.