DROP database IF exists dbrapid_mart;

CREATE DATABASE dbrapid_mart;

USE dbrapid_mart;
--
-- Base de datos: `bs_rapidmart`
--

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `movimientos_inventarios`
--

CREATE TABLE `tb_Movimientos_Inventarios` (
  `id_Movimiento_inventario` varchar(36) default UUID(),
  `id_Inventario` int(11) NOT NULL,
  `Tipo_movimiento` enum('Entrada','Salida') NOT NULL,
  `Cantidad` int(11) NOT NULL,
  `Fecha_movimiento` date NOT NULL,
  CONSTRAINT ch_Cantidad CHECK (Cantidad >= 0),
  CONSTRAINT ch_Fecha_movimiento CHECK (Fecha_movimiento >= 'YYYY-MM-DD')
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=UTF8MB4_GENERAL_CI;

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `tb_categorias`
--

CREATE TABLE `tb_Categorias` (
  `id_Categoria` varchar(36) default UUID(),
  `Nombre_categoria` varchar(50) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `tb_inventarios`
--

CREATE TABLE `tb_Inventarios` (
  `id_Inventario` varchar(36) default UUID(),
  `id_Producto` int(11) NOT NULL,
  `Cantidad_disponible` int(11) NOT NULL,
  `Fecha_ingreso` date NOT NULL,
  CONSTRAINT ch_Cantidad_disponible CHECK (Cantidad_disponible >= 0),
  CONSTRAINT ch_Fecha_ingreso CHECK (Fecha_ingreso >='YYYY-MM-DD')
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;


-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `tb_productos`
--

CREATE TABLE `tb_Productos` (
  `id_Producto` varchar(36) default UUID(),
  `Nombre_producto` varchar(50) NOT NULL,
  `Descripcion_producto` varchar(250) NOT NULL,
  `Precio_unitario` decimal(10,2) NOT NULL,
  `id_Categoria` int(11) NOT NULL,
  `id_Proveedor` int(11) NOT NULL,
  CONSTRAINT ch_Precio_unitario CHECK (Precio_unitario >= 0)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `tb_proveedores`
--

CREATE TABLE `tb_Proveedores` (
  `id_Proveedor` varchar(36) default UUID(),
  `Nombre_proveedor` varchar(50) NOT NULL,
  `Direccion_proveedor` varchar(50) NOT NULL,
  `Telefono_proveedor` varchar(10) NOT NULL,
  CONSTRAINT Si_Telefono_proveedor UNIQUE (Telefono_proveedor)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

  
  
-- Modificar la tabla tb_Movimientos_Inventarios
ALTER TABLE tb_Movimientos_Inventarios MODIFY COLUMN id_Movimiento_inventario VARCHAR(36) DEFAULT UUID();

-- Modificar la tabla tb_Categorias
ALTER TABLE tb_Categorias MODIFY COLUMN id_Categoria VARCHAR(36) DEFAULT UUID();

-- Modificar la tabla tb_Inventarios
ALTER TABLE tb_Inventarios MODIFY COLUMN id_Inventario VARCHAR(36) DEFAULT UUID();

-- Modificar la tabla tb_Productos
ALTER TABLE tb_Productos MODIFY COLUMN id_Producto VARCHAR(36) DEFAULT UUID();

-- Modificar la tabla tb_Proveedores
ALTER TABLE tb_Proveedores MODIFY COLUMN id_Proveedor VARCHAR(36) DEFAULT UUID();

-- Insertar datos en la tabla tb_Movimientos_Inventarios
INSERT INTO tb_Movimientos_Inventarios (id_Movimiento_inventario, id_Inventario, Tipo_movimiento, Cantidad, Fecha_movimiento) VALUES
(UUID(), '1', 'Entrada', '10', '2024-01-01'),
(UUID(), '2', 'Salida', '5', '2024-01-02'),
(UUID(), '3', 'Entrada', '8', '2024-01-03'),
(UUID(), '4', 'Salida', '3', '2024-01-04'),
(UUID(), '5', 'Entrada', '12', '2024-01-05'),
(UUID(), '6', 'Salida', '7', '2024-01-06'),
(UUID(), '7', 'Entrada', '15', '2024-01-07'),
(UUID(), '8', 'Salida', '4', '2024-01-08'),
(UUID(), '9', 'Entrada', '20', '2024-01-09'),
(UUID(), '10', 'Salida', '6', '2024-01-10');

SELECT * FROM tb_Movimientos_Inventarios;

-- Insertar datos en la tabla tb_Categorias
INSERT INTO tb_Categorias (id_Categoria, Nombre_categoria) VALUES
(UUID(), 'Electrónica'),
(UUID(), 'Ropa'),
(UUID(), 'Alimentos'),
(UUID(), 'Hogar y jardín'),
(UUID(), 'Salud y belleza'),
(UUID(), 'Automóviles'),
(UUID(), 'Juguetes'),
(UUID(), 'Deportes y aire libre'),
(UUID(), 'Libros y música'),
(UUID(), 'Electrodomésticos');

SELECT * FROM tb_Categorias;

-- Insertar datos en la tabla tb_Inventarios
INSERT INTO tb_Inventarios (id_Inventario, id_Producto, Cantidad_disponible, Fecha_ingreso) VALUES
(UUID(), '1', '100', '2024-01-01'),
(UUID(), '2', '200', '2024-01-02'),
(UUID(), '3', '150', '2024-01-03'),
(UUID(), '4', '50', '2024-01-04'),
(UUID(), '5', '80', '2024-01-05'),
(UUID(), '6', '30', '2024-01-06'),
(UUID(), '7', '120', '2024-01-07'),
(UUID(), '8', '60', '2024-01-08'),
(UUID(), '9', '90', '2024-01-09'),
(UUID(), '10', '40', '2024-01-10');

SELECT * FROM tb_Inventarios;

-- Insertar datos en la tabla tb_Productos
INSERT INTO tb_Productos (id_Producto, Nombre_producto, Descripcion_producto, Precio_unitario, id_Categoria, id_Proveedor) VALUES
(UUID(), 'Producto 1', 'Descripción 1', '10.00', '1', '1'),
(UUID(), 'Producto 2', 'Descripción 2', '20.00', '2', '2'),
(UUID(), 'Producto 3', 'Descripción 3', '30.00', '3', '3'),
(UUID(), 'Producto 4', 'Descripción 4', '40.00', '4', '4'),
(UUID(), 'Producto 5', 'Descripción 5', '50.00', '5', '5'),
(UUID(), 'Producto 6', 'Descripción 6', '60.00', '6', '6'),
(UUID(), 'Producto 7', 'Descripción 7', '70.00', '7', '7'),
(UUID(), 'Producto 8', 'Descripción 8', '80.00', '8', '8'),
(UUID(), 'Producto 9', 'Descripción 9', '90.00', '9', '9'),
(UUID(), 'Producto 10', 'Descripción 10', '100.00', '10', '10');

SELECT * FROM tb_Productos;

-- Insertar datos en la tabla tb_Proveedores
INSERT INTO tb_Proveedores (id_Proveedor, Nombre_proveedor, Direccion_proveedor, Telefono_proveedor) VALUES
(UUID(), 'Proveedor 1', 'Direccion 1', '1234567890'),
(UUID(), 'Proveedor 2', 'Direccion 2', '1234567891'),
(UUID(), 'Proveedor 3', 'Direccion 3', '1234567892'),
(UUID(), 'Proveedor 4', 'Direccion 4', '1234567893'),
(UUID(), 'Proveedor 5', 'Direccion 5', '1234567894'),
(UUID(), 'Proveedor 6', 'Direccion 6', '1234567895'),
(UUID(), 'Proveedor 7', 'Direccion 7', '1234567896'),
(UUID(), 'Proveedor 8', 'Direccion 8', '1234567897'),
(UUID(), 'Proveedor 9', 'Direccion 9', '1234567898'),
(UUID(), 'Proveedor 10', 'Direccion 10', '1234567899');

SELECT * FROM tb_proveedores;



  
DELIMITER //

CREATE TRIGGER actualizar_inventario AFTER INSERT ON tb_Movimientos_Inventarios
FOR EACH ROW
BEGIN
    DECLARE cantidad_actual INT;
    
    -- Obtener la cantidad actual en inventario del producto
    SELECT Cantidad_disponible INTO cantidad_actual
    FROM tb_Inventarios
    WHERE id_Inventario = NEW.id_Inventario;
    
    -- Actualizar la cantidad disponible en el inventario
    IF NEW.Tipo_movimiento = 'Entrada' THEN
        UPDATE tb_Inventarios
        SET Cantidad_disponible = cantidad_actual + NEW.Cantidad
        WHERE id_Inventario = NEW.id_Inventario;
    ELSE
        UPDATE tb_Inventarios
        SET Cantidad_disponible = cantidad_actual - NEW.Cantidad
        WHERE id_Inventario = NEW.id_Inventario;
    END IF;
END//

DELIMITER ;

  
  
COMMIT;
