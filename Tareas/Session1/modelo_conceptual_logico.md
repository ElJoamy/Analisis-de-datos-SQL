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

### **Entidades y Propiedades**:
- **Cliente**: 
  - ID_Cliente, Nombre, Teléfono, Correo Electrónico.
- **Producto**: 
  - ID_Producto, Nombre, Categoría, Precio, Stock.
- **Documento de Compra**: 
  - ID_Compra, Fecha, Total, Forma de Pago.
- **Supermercado**: 
  - ID_Sucursal, Nombre, Dirección.
- **Empleado/Cajero**: 
  - ID_Empleado, Nombre, Puesto.

### **Relaciones**:
- Un cliente **realiza** una compra (1:N).
- Un documento de compra **incluye** productos (N:M).
- Un empleado **gestiona** la compra (1:N).

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
    Nombre NVARCHAR(50),
    Categoria NVARCHAR(30),
    Precio DECIMAL(10, 2),
    Stock INT
);
```

### 3. Tabla: DocumentosCompra
```sql
CREATE TABLE DocumentosCompra (
    ID_Compra INT PRIMARY KEY,
    ID_Cliente INT,
    Fecha DATETIME,
    Total DECIMAL(10, 2),
    FormaPago NVARCHAR(20),
    CONSTRAINT FK_Cliente FOREIGN KEY (ID_Cliente) REFERENCES Clientes(ID_Cliente)
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
    Nombre NVARCHAR(50),
    Puesto NVARCHAR(30)
);
```

### Diagrama ER
```mermaid
erDiagram
    Clientes {
        INT ID_Cliente PK
        NVARCHAR Nombre
        NVARCHAR Telefono
        NVARCHAR Correo
    }

    Productos {
        INT ID_Producto PK
        NVARCHAR Nombre
        NVARCHAR Categoria
        DECIMAL Precio
        INT Stock
    }

    DocumentosCompra {
        INT ID_Compra PK
        INT ID_Cliente FK
        DATETIME Fecha
        DECIMAL Total
        NVARCHAR FormaPago
    }

    Compra_Producto {
        INT ID_Compra FK
        INT ID_Producto FK
        INT Cantidad
    }

    Supermercado {
        INT ID_Sucursal PK
        NVARCHAR Nombre
        NVARCHAR Direccion
    }

    Empleados {
        INT ID_Empleado PK
        NVARCHAR Nombre
        NVARCHAR Puesto
    }

    Clientes ||--o{ DocumentosCompra : realiza
    DocumentosCompra ||--o{ Compra_Producto : incluye
    Productos }o--o{ Compra_Producto : es_parte
    Supermercado ||--o{ Empleados : pertenece
```

## Link:
- Puedes acceder a la tarea en el siguiente [enlace](https://classroom.google.com/c/NzM5NDcxNTYyMTMw/a/NzM5NjI1ODA5MjUx/details?pli=1).

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