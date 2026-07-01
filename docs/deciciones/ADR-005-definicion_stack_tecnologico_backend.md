ADR-005

Titulo:
Definicion del stack tecnologico para el backend y entorno de base de datos local.

Motivo:

PostgreSQL: Proporciona una base de datos relacional robusta, con soporte nativo estricto para transacciones ACID, alto rendimiento e integracion optima con ORMs (como SQLAlchemy) y manejo de tipos de datos complejos como JSON.

Docker: Garantiza la homogeneidad del entorno de desarrollo local para la base de datos, asegurando que todos los desarrolladores utilicen la misma version exacta de PostgreSQL sin conflictos de dependencias del sistema operativo.

FastAPI: Ofrece alto rendimiento, tipado estatico nativo mediante Python Type Hints, validacion de esquemas automatica con Pydantic y generacion de documentacion interactiva (Swagger/ReDoc) sin configuracion adicional.

Python: Permite un desarrollo agil y mantenible. Aunque es un lenguaje interpretado, el perfil de carga de StockWex estara limitado principalmente por operaciones de Entrada/Salida (I/O Bound) como consultas a la base de datos y peticiones de red, donde el impacto de ejecucion del lenguaje es marginal.

Consecuencias:

Pros: Ciclo de desarrollo acelerado y documentacion automatizada de los endpoints del inventario. Entorno local facilmente replicable mediante contenedores. Estabilidad de datos garantizada por el motor relacional.

Contras: Introduce una ligera sobrecarga en la gestion y configuracion inicial de la orquestacion de contenedores Docker en el entorno local de desarrollo.