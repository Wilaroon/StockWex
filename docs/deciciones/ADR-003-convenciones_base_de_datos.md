ADR-003

Título:
Estandarizacion y convenciones para el diseno de la base de datos.

Motivo:

Evita inconsistencias críticas en el nombrado de tablas (ej. prevenir duplicados o variantes como ProductType, product_type y productTypes simultaneamente).

Agiliza el desarrollo al eliminar debates sobre cómo nombrar columnas en nuevas características.

Facilita la automatización y mapeo de modelos en el ORM del backend.

Convenciones Adoptadas:

Tablas: Siempre en plural y usando snake_case (ej. productos, producto_imagenes).

Claves Primarias (PK): Siempre se llamaran exactamente id.

Claves Foraneas (FK): Siempre terminaran con el sufijo _id (ej. producto_id).

Campos de Auditoria: Todas las tablas incluiran de forma obligatoria created_at y updated_at.

Campos de Identificacion Unica Global: Todos los campos destinados a UUID se llamaran estrictamente uuid.

Consecuencias:

Pros: Legibilidad inmediata del esquema de datos para cualquier desarrollador nuevo. Cero friccion al crear migraciones.

Contras: Obliga a realizar revisiones de codigo (Code Reviews) mas estrictas al inicio para asegurar que nadie rompa la regla por descuido.