# Perfil2_Willidinho
Base de datos


DROP database IF exists bs_rapidmart;

CREATE DATABASE bs_rapidmart;

USE bs_rapidmart;
--
-- Base de datos: `bs_rapidmart`
--

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `movimientos_inventarios`
--

CREATE TABLE `tb_Movimientos_Inventarios` (
  `id_Movimiento_inventario` int(11) NOT NULL,
  `id_Inventario` int(11) NOT NULL,
  `Tipo_movimiento` enum('Entrada','Salida') NOT NULL,
  `Cantidad` int(11) NOT NULL,
  `Fecha_movimiento` date NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `tb_categorias`
--

CREATE TABLE `tb_Categorias` (
  `id_Categoria` int(11) NOT NULL,
  `Nombre_categoria` varchar(50) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `tb_inventarios`
--

CREATE TABLE `tb_Inventarios` (
  `id_Inventario` int(11) NOT NULL,
  `id_Producto` int(11) NOT NULL,
  `Cantidad_disponible` int(11) NOT NULL,
  `Fecha_ingreso` date NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `tb_productos`
--

CREATE TABLE `tb_Productos` (
  `id_Producto` int(11) NOT NULL,
  `Nombre_producto` varchar(50) NOT NULL,
  `Descripcion_producto` varchar(250) NOT NULL,
  `Precio_unitario` decimal(10,2) NOT NULL,
  `id_Categoria` int(11) NOT NULL,
  `id_Proveedor` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `tb_proveedores`
--

CREATE TABLE `tb_Proveedores` (
  `id_Proveedor` int(11) NOT NULL,
  `Nombre_proveedor` varchar(50) NOT NULL,
  `Direccion_proveedor` varchar(50) NOT NULL,
  `Telefono_proveedor` varchar(10) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Índices para tablas volcadas
--

--
-- Indices de la tabla `movimientos_inventarios`
--
ALTER TABLE `tb_Movimientos_Inventarios`
  ADD PRIMARY KEY (`id_Movimiento_inventario`);

--
-- Indices de la tabla `tb_categorias`
--
ALTER TABLE `tb_Categorias`
  ADD PRIMARY KEY (`id_Categoria`);

--
-- Indices de la tabla `tb_inventarios`
--
ALTER TABLE `tb_Inventarios`
  ADD PRIMARY KEY (`id_Inventario`);

--
-- Indices de la tabla `tb_productos`
--
ALTER TABLE `tb_Productos`
  ADD PRIMARY KEY (`id_Producto`);

--
-- Indices de la tabla `tb_proveedores`
--
ALTER TABLE `tb_Proveedores`
  ADD PRIMARY KEY (`id_Proveedor`);

--
-- AUTO_INCREMENT de las tablas volcadas
--

--

--
-- Restricciones para tablas volcadas
--

--
-- Filtros para la tabla `movimientos_inventarios`
--
ALTER TABLE `tb_Movimientos_Inventarios`
  ADD CONSTRAINT `tb_Movimientos_Inventarios` FOREIGN KEY (`id_Movimiento_inventario`) REFERENCES `tb_Inventarios` (`id_Inventario`) ON DELETE CASCADE ON UPDATE CASCADE;

--
-- Filtros para la tabla `tb_categorias`
--
ALTER TABLE `tb_Categorias`
  ADD CONSTRAINT `tb_Categorias` FOREIGN KEY (`id_Categoria`) REFERENCES `tb_Productos` (`id_Producto`) ON DELETE CASCADE ON UPDATE CASCADE;

--
-- Filtros para la tabla `tb_productos`
--
ALTER TABLE `tb_Productos`
  ADD CONSTRAINT `tb_Productos` FOREIGN KEY (`id_Producto`) REFERENCES `tb_Inventarios` (`id_Inventario`) ON DELETE CASCADE ON UPDATE CASCADE;

--
-- Filtros para la tabla `tb_proveedores`
--
ALTER TABLE `tb_Proveedores`
  ADD CONSTRAINT `tb_Proveedores` FOREIGN KEY (`id_Proveedor`) REFERENCES `tb_Productos` (`id_Producto`) ON DELETE CASCADE ON UPDATE CASCADE;
COMMIT;
