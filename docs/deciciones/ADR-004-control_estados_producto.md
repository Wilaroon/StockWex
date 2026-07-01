ADR-004

Titulo:
Control de estados y disponibilidad en la tabla de productos.

Motivo:

Permite gestionar el ciclo de vida del producto de forma independiente a sus existencias fisicas (ej. un producto puede tener stock 0 pero seguir estando activo/disponible para recibir mercancia).

Evita que productos descontinuados o pausados por administracion sean vendidos, incluso si aun queda stock remanente en bodega.

Mantiene la integridad del catalogo comercial separada de la logica logistica del inventario en StockWex.

Consecuencias:

Pros: Mayor precision en las reglas de negocio. Permite implementar estados avanzados como "Borrador", "Activo", "Pausado" o "Descontinuado" sin alterar los calculos de stock real.

Contras: Las consultas para el proceso de venta o visualizacion en catalogo ahora deben validar ambas condiciones obligatoriamente (ej. status = 'activo' AND stock > 0) para garantizar una transaccion valida.