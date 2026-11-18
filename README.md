# Almacén Backend API

API diseñada para la gestión integral de un almacén logístico. Este repositorio contiene el diseño del contrato OpenAPI 3.0, el servidor simulado con WireMock y la colección de pruebas automatizadas en Postman.

## Estructura del Proyecto

* `openapi.yaml`: Especificación completa de la API bajo el estándar OpenAPI 3.0 (modelos, relaciones, validaciones y códigos de respuesta `200`, `201`, `204`, `400`, `404` y `500`).
* `wiremock/mappings/`: Stubs individuales en formato JSON para simular todos los endpoints CRUD, filtros y escenarios de error de las 5 entidades.
* `postman_collection.json`: Colección parametrizada (`{{baseUrl}}`) con 35 peticiones y sus respectivos scripts de validación (`pm.test`) para ejecución en el Collection Runner.

## Modelo de Datos (5 Entidades)

1. **Productos** (`/api/v1/productos`): Gestión del catálogo, SKU, precio, stock y relaciones con ubicación y proveedor.
2. **Ubicaciones** (`/api/v1/ubicaciones`): Control de pasillos, estanterías, capacidad máxima y disponibilidad.
3. **Proveedores** (`/api/v1/proveedores`): Directorio de empresas suministradoras, CIF, estado activo y valoración.
4. **Pedidos a Proveedor** (`/api/v1/pedidos`): Registro de albaranes, fechas previstas de entrega, costes y estado de recepción.
5. **Empleados** (`/api/v1/empleados`): Gestión del personal de almacén, DNI, salario y asignación de turno nocturno.

## Cómo levantar el entorno con WireMock

1. Asegúrate de tener Java instalado y sitúate en la raíz del proyecto (`Almacen-backend-api`).
2. Ejecuta el servidor de WireMock en el puerto `8080`:

```bash
java -jar wiremock-standalone.jar --root-dir ./wiremock --port 8080
```

La API simulada quedará escuchando en `http://localhost:8080/api/v1`.

## Cómo ejecutar las pruebas en Postman

1. Abre **Postman** y selecciona **Import** para cargar el archivo `postman_collection.json` situado en la raíz del proyecto.
2. Verifica que la variable de colección `baseUrl` apunta a `http://localhost:8080/api/v1`.
3. Haz clic en los tres puntos (`...`) de la colección **Almacen API - Coleccion Completa CRUD** > **Run**.
4. Se ejecutarán automáticamente las **35 pruebas** cubriendo operaciones `GET` (con hasta 3 filtros por entidad), `POST`, `PUT`, `DELETE` y respuestas de error `400`, `404` y `500`.