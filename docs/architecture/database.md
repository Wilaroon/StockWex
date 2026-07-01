StockWex - Arquitectura de Base de Datos
Objetivo

Definir la estructura de la base de datos de StockWex, asegurando escalabilidad, normalización y consistencia en el manejo de productos, inventario y pedidos.

Esta arquitectura está diseñada para soportar crecimiento hacia módulos avanzados como ventas, compras, clientes y múltiples sucursales.

Motor de base de datos
PostgreSQL

Se selecciona por su robustez, soporte para relaciones complejas, integridad transaccional y compatibilidad con herramientas modernas como SQLAlchemy y Alembic.

Principios de diseño
Normalización de datos para evitar redundancia.
Separación de responsabilidades por tablas.
Uso de claves primarias numéricas (id) para relaciones internas.
Uso de identificador público (uuid) en entidades principales.
Uso de migraciones para cualquier cambio estructural.
Uso de timestamps estándar (created_at, updated_at).
Relaciones explícitas mediante claves foráneas.
Modelo general del sistema

El sistema se basa en los siguientes bloques principales:

Productos
Catálogos (marcas, departamentos, tipos, unidades)
Inventario
Pedidos
Imágenes de productos
Entidad principal: products

Tabla central del sistema.

Campos principales:

id (PK interna)
uuid (identificador público)
code (SKU o código de barras)
name
description
brand_id (FK)
department_id (FK)
product_type_id (FK)
unit_measure_id (FK)
buy_price
sell_price
stock
stock_min
status_id (estado del producto)
created_at
updated_at
created_by
updated_by
Catálogos del sistema

Estas tablas sirven para normalizar información repetitiva.

brands
id
name
description
created_at
updated_at
departments
id
name
description
created_at
updated_at
product_types
id
name
description
created_at
updated_at
unit_measures
id
name
abbreviation
created_at
updated_at
product_statuses
id
code
name
description

Estados posibles:

ACTIVE
INACTIVE
DISCONTINUED
Imágenes de productos

Se manejan de forma independiente.

product_images
id
product_id (FK)
file_name
path
is_main
order
alt_text
created_at

Reglas:

Un producto puede tener múltiples imágenes.
Solo una imagen puede ser principal.
Las imágenes no se almacenan en la base de datos, solo sus rutas.
Inventario

El inventario se maneja directamente en la tabla products mediante el campo stock.

Reglas:

stock representa la cantidad actual disponible.
stock_min se usa para alertas.
El stock cambia únicamente a través de movimientos del sistema (ventas, compras, ajustes).
Pedidos (estructura futura base)

Aunque se implementará en fases posteriores, la base está definida.

Se contemplan:

orders
order_items

Reglas:

Un pedido puede tener múltiples productos.
Cada item del pedido afecta el inventario.
Los pedidos tienen estados (pendiente, completado, cancelado).
Relaciones principales

products se relaciona con:

brands
departments
product_types
unit_measures
product_statuses
product_images
Diagrama conceptual
Un producto pertenece a una marca.
Un producto pertenece a un departamento.
Un producto pertenece a un tipo.
Un producto tiene una unidad de medida.
Un producto tiene un estado.
Un producto puede tener muchas imágenes.
Un producto tiene un control de stock directo.
Reglas de integridad
No se permiten productos sin relaciones básicas (brand, department, type, unit).
El stock nunca puede ser negativo.
El código (code) debe ser único.
El UUID es único e inmutable.
Solo una imagen principal por producto.
Escalabilidad futura

Esta arquitectura permite extender el sistema hacia:

Múltiples sucursales
Inventario distribuido
Historial de movimientos de stock
Compras a proveedores
Ventas a clientes
API pública
Aplicación móvil