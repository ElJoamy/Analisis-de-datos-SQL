# Modelo Conceptual y Lógico de un Documento de Compra

## Tarea: 
Crear un modelo conceptual y lógico de un documento de compra.

## Enunciado:
Hola chicos, realicemos un modelo conceptual y lógico de un documento de compra de cualquier supermercado.

La idea es identificar **entidades**, **propiedades** y **relaciones**.

Esta tarea tiene puntaje de **10**, ayudará en su promedio final.

Los casos que deseen exponerlos tendrán un punto adicional sobre el trabajo.

**Buen fin de semana.**

**Saludos**

## Modelo Conceptual

El modelo conceptual identifica las entidades, atributos y relaciones necesarias para gestionar un documento de compra en un supermercado.

### **Entidades y Propiedades**

1. **Cliente**: 
   - **Propiedades**: 
     - ID_Cliente (PK): Identificador único del cliente.
     - Nombre: Nombre completo del cliente.
     - Teléfono: Número de contacto.
     - Correo Electrónico: Dirección de correo electrónico.

2. **Producto**: 
   - **Propiedades**: 
     - ID_Producto (PK): Identificador único del producto.
     - ID_Sucursal (FK): Identificador de la sucursal a la que pertenece.
     - Nombre: Nombre del producto.
     - Categoría: Tipo o categoría del producto.
     - Precio: Precio unitario.
     - Stock: Cantidad disponible en inventario.

3. **Documento de Compra**: 
   - **Propiedades**: 
     - ID_Compra (PK): Identificador único del documento de compra.
     - ID_Cliente (FK): Cliente que realizó la compra.
     - ID_Empleado (FK): Empleado que gestionó la compra.
     - Fecha: Fecha y hora de la compra.
     - Total: Monto total de la compra.
     - Forma de Pago: Método de pago utilizado (efectivo, tarjeta, etc.).

4. **Factura**:
   - **Propiedades**: 
     - ID_Factura (PK): Identificador único de la factura.
     - ID_Compra (FK, UNIQUE): Documento de compra relacionado.
     - Número de Factura: Código de la factura.
     - Fecha de Emisión: Fecha en que se emitió la factura.
     - Total Facturado: Monto total facturado.
     - Moneda: Moneda en que se emitió la factura (USD, BOB, etc.).

5. **Detalle de Factura**:
   - **Propiedades**: 
     - ID_Factura (FK): Factura a la que pertenece el detalle.
     - ID_Producto (FK): Producto incluido en la factura.
     - Cantidad: Número de unidades facturadas.
     - Precio Unitario: Precio de cada producto en el momento de la factura.
     - Subtotal: Cantidad × Precio Unitario.
     - Descuento: Descuento aplicado al producto (opcional).
   - **Relaciones**:
     - Una factura puede tener múltiples detalles.
     - Cada detalle está relacionado con un producto específico.

6. **Supermercado**: 
   - **Propiedades**: 
     - ID_Sucursal (PK): Identificador único de la sucursal.
     - Nombre: Nombre de la sucursal.
     - Dirección: Ubicación de la sucursal.

7. **Empleado/Cajero**: 
   - **Propiedades**: 
     - ID_Empleado (PK): Identificador único del empleado.
     - ID_Sucursal (FK): Sucursal a la que pertenece el empleado.
     - Nombre: Nombre completo del empleado.
     - Puesto: Cargo o rol del empleado (cajero, gerente, etc.).

## Modelo Lógico

El modelo lógico convierte las entidades y relaciones en tablas para su implementación en **SQL**. Las siguientes estructuras incluyen las restricciones necesarias.

### 1. Tabla: Clientes
```sql
CREATE TABLE Clientes (
    ID_Cliente INT PRIMARY KEY,
    Nombre NVARCHAR(50),
    Telefono NVARCHAR(15),
    Correo NVARCHAR(50)
);
```

### 2. Tabla: Productos
```sql
CREATE TABLE Productos (
    ID_Producto INT PRIMARY KEY,
    ID_Sucursal INT,
    Nombre NVARCHAR(50),
    Categoria NVARCHAR(30),
    Precio DECIMAL(10, 2),
    Stock INT,
    CONSTRAINT FK_Sucursal FOREIGN KEY (ID_Sucursal) REFERENCES Supermercado(ID_Sucursal)
);
```

### 3. Tabla: DocumentosCompra
```sql
CREATE TABLE DocumentosCompra (
    ID_Compra INT PRIMARY KEY,
    ID_Cliente INT,
    ID_Empleado INT,
    Fecha DATETIME,
    Total DECIMAL(10, 2),
    FormaPago NVARCHAR(20),
    CONSTRAINT FK_Cliente FOREIGN KEY (ID_Cliente) REFERENCES Clientes(ID_Cliente),
    CONSTRAINT FK_Empleado FOREIGN KEY (ID_Empleado) REFERENCES Empleados(ID_Empleado)
);
```

### 4. Tabla: Compra_Producto
```sql
CREATE TABLE Compra_Producto (
    ID_Compra INT,
    ID_Producto INT,
    Cantidad INT,
    CONSTRAINT FK_Compra FOREIGN KEY (ID_Compra) REFERENCES DocumentosCompra(ID_Compra),
    CONSTRAINT FK_Producto FOREIGN KEY (ID_Producto) REFERENCES Productos(ID_Producto)
);
```

### 5. Tabla: Supermercado
```sql
CREATE TABLE Supermercado (
    ID_Sucursal INT PRIMARY KEY,
    Nombre NVARCHAR(50),
    Direccion NVARCHAR(100)
);
```

### 6. Tabla: Empleados
```sql
CREATE TABLE Empleados (
    ID_Empleado INT PRIMARY KEY,
    ID_Sucursal INT,
    Nombre NVARCHAR(50),
    Puesto NVARCHAR(30),
    CONSTRAINT FK_Sucursal FOREIGN KEY (ID_Sucursal) REFERENCES Supermercado(ID_Sucursal)
);
```

### 7. Tabla: Factura
```sql
CREATE TABLE Factura (
    ID_Factura INT PRIMARY KEY,
    ID_Compra INT UNIQUE,
    NumeroFactura NVARCHAR(20),
    FechaEmision DATETIME,
    TotalFacturado DECIMAL(10, 2),
    Moneda NVARCHAR(10),
    CONSTRAINT FK_Compra FOREIGN KEY (ID_Compra) REFERENCES DocumentosCompra(ID_Compra)
);
```

### 8. Tabla: DetalleFactura
```sql
CREATE TABLE DetalleFactura (
    ID_Factura INT,
    ID_Producto INT,
    Cantidad INT,
    PrecioUnitario DECIMAL(10, 2),
    Subtotal DECIMAL(10, 2),
    Descuento DECIMAL(10, 2) DEFAULT 0,
    CONSTRAINT FK_Factura FOREIGN KEY (ID_Factura) REFERENCES Factura(ID_Factura),
    CONSTRAINT FK_Producto FOREIGN KEY (ID_Producto) REFERENCES Productos(ID_Producto)
);
```

### Diagrama ER
<div class="mermaid">
erDiagram
    Supermercado {
        INT ID_Sucursal PK
        NVARCHAR Nombre
        NVARCHAR Direccion
    }

    Empleados {
        INT ID_Empleado PK
        INT ID_Sucursal FK
        NVARCHAR Nombre
        NVARCHAR Puesto
    }

    Clientes {
        INT ID_Cliente PK
        NVARCHAR Nombre
        NVARCHAR Telefono
        NVARCHAR Correo
    }

    Productos {
        INT ID_Producto PK
        INT ID_Sucursal FK
        NVARCHAR Nombre
        NVARCHAR Categoria
        DECIMAL Precio
        INT Stock
    }

    DocumentosCompra {
        INT ID_Compra PK
        INT ID_Cliente FK
        INT ID_Empleado FK
        DATETIME Fecha
        DECIMAL Total
        NVARCHAR FormaPago
    }

    Factura {
        INT ID_Factura PK
        INT ID_Compra FK
        NVARCHAR NumeroFactura
        DATETIME FechaEmision
        DECIMAL TotalFacturado
        NVARCHAR Moneda
    }

    DetalleFactura {
        INT ID_Factura FK
        INT ID_Producto FK
        INT Cantidad
        DECIMAL PrecioUnitario
        DECIMAL Subtotal
        DECIMAL Descuento
    }

    Compra_Producto {
        INT ID_Compra FK
        INT ID_Producto FK
        INT Cantidad
    }

    Supermercado ||--o{ Empleados : emplea
    Supermercado ||--o{ Productos : contiene
    Clientes ||--o{ DocumentosCompra : realiza
    DocumentosCompra ||--o{ Compra_Producto : incluye
    Productos }o--o{ Compra_Producto : es_parte
    Empleados ||--o{ DocumentosCompra : atiende
    DocumentosCompra ||--|| Factura : genera
    Factura ||--o{ DetalleFactura : contiene
    Productos ||--o{ DetalleFactura : relacionado
</div>
<script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>
<script>
    mermaid.initialize({ startOnLoad: true });
</script>

### **Relaciones**

1. **Clientes realiza DocumentosCompra**
   - Relación de `1:N`.
   - Un cliente puede realizar múltiples compras, pero cada compra pertenece a un único cliente.

2. **DocumentosCompra incluye Productos**
   - Relación de `N:M`.
   - Un documento de compra puede incluir múltiples productos, y un producto puede formar parte de múltiples documentos de compra.

3. **DocumentosCompra genera Factura**
   - Relación de `1:1`.
   - Cada documento de compra genera una única factura, y cada factura está asociada a un único documento de compra.

4. **Factura detalla Productos (Detalle de Factura)**
   - Relación de `1:N`.
   - Cada factura tiene múltiples detalles, y cada detalle corresponde a un producto específico.

5. **Supermercado emplea Empleados**
   - Relación de `1:N`.
   - Un supermercado puede tener múltiples empleados, pero cada empleado pertenece a una única sucursal.

6. **Supermercado contiene Productos**
   - Relación de `1:N`.
   - Un supermercado puede tener múltiples productos, pero cada producto pertenece a una única sucursal.

7. **Empleados atienden DocumentosCompra**
   - Relación de `1:N`.
   - Un empleado puede gestionar múltiples documentos de compra, pero cada compra es atendida por un único empleado.

### **Conexiones Visuales**
- **Llave Primaria (PK)**: Se define con el atributo `PK` en las entidades para identificar de manera única cada registro.
- **Llave Foránea (FK)**: Representa una conexión entre tablas relacionadas y asegura integridad referencial.
- **Relaciones**: Indicadas con notaciones como:
  - `||--o{` para relaciones 1:N (uno a muchos).
  - `}o--o{` para relaciones N:M (muchos a muchos).

## Link:
- Puedes acceder a la tarea en el classroom en el siguiente [enlace](https://classroom.google.com/c/NzM5NDcxNTYyMTMw/a/NzM5NjI1ODA5MjUx/details?pli=1).

## ✍️ Autor
<div style="background-image: url('../../imgs/background.jpg'); background-size: cover; padding: 20px; text-align: center; border-radius: 10px;">
    <a href="https://github.com/ElJoamy" style="text-decoration: none; color: black; display: inline-block; text-align: center;">
        <img src="https://avatars.githubusercontent.com/u/68487005?v=4" width="100" alt="ElJoamy" style="border-radius: 50%; border: 2px solid #000;"/>
        <h1 style="margin: 10px 0 0; font-size: 1.5em; color: black; font-weight: bold;">Joseph Anthony Meneses Salguero</h1>
    </a>
    <br />
    <a href="https://linkedin.com/in/joamy5902" title="LinkedIn"><img src="https://img.shields.io/badge/-LinkedIn-blue?style=flat&logo=linkedin"></a>
    <a href="mailto:joamysalguero1@gmail.com" title="Email"><img src="https://img.shields.io/badge/-Email-red?style=flat&logo=gmail"></a>
    <a href="https://medium.com/@joamysalguero1" title="Medium"><img src="https://img.shields.io/badge/-Medium-black?style=flat&logo=medium"></a>
</div>
