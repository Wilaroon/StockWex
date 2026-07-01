ADR-002

Titulo:
Las imagenes de los productos se almacenaran en una tabla independiente.

Motivo:

Un producto puede tener multiples imagenes.
Se evita repetir columnas.
Permite escalar.
Facilita almacenamiento en S3.

Consecuencias:

Se requiere un JOIN para obtener las imagenes.