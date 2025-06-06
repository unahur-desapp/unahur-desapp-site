---
layout: default
---

# Propuesta 3: Sistema de Gestión de Tarifas de Costos para Logística

## Contexto

La empresa de logística Acme SRL, al subcontratar a otras empresas los camiones para realizar las entregas, necesita implementar un sistema eficiente para el control de costos. Actualmente, los costos del alquiler de vehículos varían según múltiples factores que necesitan ser gestionados sistemáticamente.

## Concepto de "Tarifa de Costo"

Para organizar la información relacionada con el costo de los viajes, se define el concepto de "Tarifa de Costo" como el registro que permite determinar cuánto le cuesta a Acme SRL organizar un viaje con características específicas. Cada tarifa de costo estará compuesta por un valor base más posibles adicionales aplicables.

## Factores que influyen en el costo

Las tarifas de costo varían según los siguientes factores:

- **Tipo de vehículo**: El costo varía dependiendo si se utiliza una camioneta, un camión u otro tipo de vehículo para realizar las entregas.
- **Tipo de carga/viaje**: Existen diferentes categorías, entre ellas mencionamos:
  - Transportes regulares (rutas habituales entre un origen y destino).
  - Transportes particulares o para cargas especiales.
- **Zona de viaje**: Las zonas pueden ser AMBA, BsAs-Rosario, entre otras, afectando el costo base del servicio.
- **Transportista**: Cuál de las empresas que tienen convenios con Logística ACME ofrece esta tarifa de costo.

#### Información de Carga

- Tipo de carga (general, refrigerada, peligrosa, frágil, sobredimensionada, etc.)
- Peso total estimado
- Volumen total estimado
- Requisitos especiales de manipulación

## Adicionales

Cada tarifa puede incluir adicionales que se contratan según las necesidades específicas de cada viaje, entre ellos mencionamos:

- **Cargas peligrosas**: Transportes que requieren condiciones especiales de seguridad.
- **Ayudantes**: Personal adicional para la carga/descarga de mercancías.
- **Estadía**: Costos de alojamiento para el chofer en viajes de larga distancia.
- **Otros**: El sistema debe permitir agregar otros adicionales según las necesidades.

Cabe destacar que un adicional puede integrarse en una tarifa y no en otra, dependiendo de las características del servicio.

## Ejemplo: Estructura de una Tarifa de Costo

### Tarifa Base: "Transporte AMBA - Camión Mediano"

#### Datos básicos:

- **ID Tarifa**: TC-001
- **Tipo de vehículo**: Camión mediano (5 toneladas)
- **Zona**: AMBA (Área Metropolitana de Buenos Aires)
- **Tipo de carga**: Regular (no especial)
- **Transportista**: Logística del Litoral SA
- **Valor base**: $45,000

#### Adicionales que se integran en esta tarifa:

![adicionesl tarifa compra](./images/adicionales-tc-2.png)

### Tarifa Base: "Buenos Aires - Rosario - Camión Grande"

#### Datos básicos:

- **ID Tarifa**: TC-052
- **Tipo de vehículo**: Camión grande (12 toneladas)
- **Zona**: Buenos Aires - Rosario
- **Tipo de carga**: Regular
- **Transportista**: Transportes Rápidos SRL
- **Valor base**: $95,000

#### Adicionales que se integran en esta tarifa:

![adicionesl tarifa compra](./images/adicionales-tc-1.png)

## Funcionalidades del Sistema

### Gestión de datos básicos

Alta, baja, modificación y consulta de: adicionales (cada uno con un costo default), tipos de vehículo, tipos de carga, zonas de viaje, transportistas.

### Registro de Tarifas de Costo

- El valor base (sin adicionales) se ingresará manualmente.
- Cada adicional tendrá un costo predeterminado que podrá ser modificado al momento de agregarlo a una tarifa específica.

### Gestión de Tarifas

- Creación, visualización, modificación y baja de tarifas.
- Asignación de adicionales a las tarifas existentes.
- Modificación del costo de los adicionales para cada tarifa específica.

### Visualización de Información

El sistema presentará un listado de tarifas con:

- Costo base
- Total de adicionales
- Costo total (base + adicionales)

### Filtros para el Listado de Tarifas

El sistema permitirá filtrar las tarifas según:

- Tipo de vehículo
- Tipo de carga/viaje
- Zona de viaje
- Rango de fechas de vigencia
- Ordenamiento personalizable por diferentes criterios

### Reportes Operativos

#### Detalle de Tarifas por Zona

- Comparativa de todas las tarifas disponibles por zona geográfica
- Identificación de zonas con mayores/menores costos
- Mapa de calor de costos por región

#### Reporte de Adicionales Disponibles

- Catálogo completo de adicionales con costos estándar
- Frecuencia de uso en diferentes tarifas
- Adicionales más/menos utilizados

#### Análisis de Tarifas por Transportista

- Comparativa de costos entre diferentes transportistas para servicios similares
- Identificación de transportistas más/menos económicos
- Evaluación de relación precio/calidad

## Aspectos Técnicos y de Implementación

### Arquitectura Propuesta

- Aplicación web responsiva con interfaces intuitivas para la gestión de tarifas y costos
- Base de datos con estructura optimizada para:
  - Manejo de históricos de modificaciones
  - Procesamiento eficiente de reportes estadísticos
  - Consultas complejas con múltiples criterios de filtrado
- Implementación de mecanismos de versionado para el seguimiento de cambios en tarifas
- Capa de servicios (API REST) documentada para facilitar integraciones con sistemas externos

### Integraciones

- Vinculación futura con el módulo de Viajes (Propuesta 1), para asociar tarifas específicas y calcular rentabilidad
- Interfaces para la exportación de datos a herramientas de análisis financiero
- API para alimentar dashboards ejecutivos con KPIs actualizados en tiempo real

### Seguridad y Auditoría

- Registro detallado de modificaciones en tarifas.
- Control de acceso basado en roles para gestión de información sensible de costos
- Mecanismos de protección para evitar modificaciones no autorizadas en tarifas históricas
- Validaciones para garantizar la integridad de los datos históricos y cálculos derivados

### Alcance del Desarrollo para el Cuatrimestre

Durante el presente cuatrimestre, el desarrollo se enfocará en:

- Diseño completo del modelo de datos para datos básicos.
- Interfaces de usuario para registro y consulta de tarifas de costos, excepto el período de vigencia.
- Motor de búsqueda con todos los filtros especificados salvo el período de vigencia.
- Reportes de adicionales disponibles.

## Funcionalidades Extras

### 1. Histórico de Tarifas

- Registro automático de cada modificación realizada a una tarifa de costo.
- Almacenamiento de versiones anteriores con fecha y detalle de modificaciones.
- Consulta de la evolución histórica de cada tarifa mediante visualización cronológica.

### 2. Análisis Comparativo de Tarifas

- Listado detallado que muestra el aumento de cada tarifa entre dos fechas seleccionadas.
- Cálculo automático de la variación en:
  - Importe absoluto ($)
  - Porcentaje relativo (%)
- Visualización gráfica de tendencias de aumento por tipo de tarifa.

### 3. Registro de viajes

Registro de cada viaje que organiza Logística Acme, sólo a efectos estadísticos. Se ingresan: fecha del viaje, cliente (de una lista configurable), tarifa de costos utilizada, precio facturado al cliente.

### 4. Estadísticas de Uso de Tarifas

Reportes que muestran:

- Frecuencia de uso de cada tarifa de costo
- Importe total por tarifa en un rango de fechas definido
- Filtrado por cliente específico
- Tendencias de uso por período

### 5. Gestión de Transportistas

Registro completo de transportistas con:

- Datos de contacto
- Tipos de vehículos disponibles
- Zonas en las que operan
- Historial de servicios realizados
- Evaluación de desempeño

### 6. Análisis de Rentabilidad por Cliente

Listado detallado por cliente que incluye:

- Costo total de los servicios.
- Margen de ganancia.

### 7. Estadísticas de Adicionales

Informes detallados sobre el uso de adicionales:

- Cantidad total de días de peón utilizados
- Número de cargas peligrosas transportadas
- Segmentación de estadísticas por zona de viaje
- Identificación de adicionales más frecuentes
- Costos totales por tipo de adicional
