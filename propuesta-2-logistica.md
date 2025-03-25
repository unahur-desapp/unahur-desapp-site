---
layout: default
---

# Propuesta 2: Sistema de Gestión de Remitos

## Contexto y Objetivos

Esta propuesta se enfoca en el desarrollo de un sistema integral para el registro y monitoreo de los remitos que documentan la mercadería cuyo transporte es solicitado a Logística Acme SRL. Los remitos constituyen la documentación fundamental que formaliza cada solicitud de traslado de mercadería, detallando las características de la carga, su origen, destino y condiciones particulares.

Logística Acme organiza el retiro de la mercadería desde una ubicación relacionada con el cliente, y su translado hasta un punto fijo que pertenece a una red de destinos que están prefijados, cuando se confecciona un remito se elige uno de estos destinos.

## Descripción Funcional

### Proceso de Gestión de Remitos

En el flujo operativo de Logística Acme, los remitos son documentos preimpresos que se distribuyen mediante talonarios a empleados propios y de empresas asociadas. Estos documentos se completan manualmente al momento de registrar una solicitud de transporte, y posteriormente son ingresados al sistema informático. Por lo tanto, cada remito ya cuenta con un número asignado al momento de su registro digital.

### Registro de Entidades

El sistema deberá permitir el mantenimiento de las siguientes entidades principales:

#### Clientes

- Información básica: razón social, CUIT/RUT, tipo de cliente (empresa privada, organismo estatal, particular).
- Dirección única asociada (considerada como origen predeterminado para todos sus remitos).
- Datos de contacto: teléfonos, correos electrónicos, personas autorizadas.

#### Destino

- Información que indica los destinos dentro de la red que maneja Logística Acme. Para cada destino se debe indicar país, provincia, localidad y dirección previamente cargados.

#### Estados

Los remitos poseen estados que permiten a la empresa dar seguimiento. Los mismos pueden ser:

- Autorizado: Disponible para rutear
- En preparación: Se está armando el envoltorio del remito.
- En carga: Cuando el remito se asigna a un viaje.
- En camino: El viaje que transporta el remito ya comenzó el recorrido.
- No entregado: Fallo de la entrega.
- Entregado: Entrega finalizada.

### Registro de Remitos

El sistema permitirá el ingreso y seguimiento de remitos con la siguiente información:

#### Datos Básicos del Remito

- Número de remito (proveniente del talonario físico, ingresado manualmente).
- Cliente solicitante (seleccionado del registro de clientes).
- Destino (seleccionado de los destinos previamente cargados).
- Fecha de emisión del remito.

#### Información de la Mercadería

- **Datos obligatorios**:
  - Peso total en kilogramos.
  - Volumen en metros cúbicos.
  - Valor declarado de la mercadería (en la moneda correspondiente)
  - Tipo de mercadería (categorización general, se selecciona entre una lista de opciones precargadas).
- **Datos optativos**:
  - Cantidad de pallets.
  - Cantidad de bultos.
  - Cantidad de racks.
  - Cantidad de bobinas.
  - Cantidad de tambores.
  - Requisitos especiales de manipulación o transporte.

#### Información Adicional

- Campo de observaciones (texto libre para especificaciones particulares)
- Documentación adjunta (posibilidad de vincular imágenes o archivos PDF)
- Usuario que registró el remito en el sistema (trazabilidad)

### Flujo de Trabajo y Validaciones

#### Registro Inicial:

- De acuerdo a lo recién indicado como "registro de remitos". Validación de número de remito (formato y unicidad). Verificación de campos obligatorios.

### Consultas y Reportes

El sistema ofrecerá un motor de búsqueda y filtrado:

#### Listado General de Remitos con capacidad de filtrado por:

- Número de remito (exacto o rango).
- Cliente solicitante.
- Rango de valor declarado (desde/hasta).
- Contenido específico (con/sin pallets, bultos, racks, bobinas o tambores).
- Provincia de origen.
- Provincia de destino.
- Estado actual (en preparación, autorizado, retenido).
- Rango de fechas de emisión.

#### Reportes Específicos:

- Volumen total de mercadería por cliente/período.
- Distribución geográfica de orígenes y destinos.
- Análisis de valor declarado por tipo de mercadería.

## Aspectos Técnicos y de Implementación

### Arquitectura Propuesta

- Aplicación web con interfaces intuitivas para carga rápida de datos.
- Base de datos optimizada para consultas frecuentes y reportes complejos.
- Mecanismos de auditoría para seguimiento de modificaciones.
- API documentada para integración con otros módulos del sistema.

### Integraciones

- Vinculación futura con el módulo de Viajes (Propuesta 1), permitiendo asignar remitos a viajes específicos.
- Posibilidad de generar documentación digital a partir de los remitos registrados.
- Interfaces para notificación automática a clientes sobre el estado de sus remitos.

### Alcance del Desarrollo para el Cuatrimestre

Durante el presente cuatrimestre, el desarrollo se enfocará en:

1. Diseño completo del modelo de datos para clientes, destinos y remitos.
2. Interfaces de usuario para registro y consulta de remitos, incluyendo las validaciones básicas.
3. Motor de búsqueda con todos los filtros especificados.
4. Reportes específicos.

## Funcionalidades Extras

### Workflow del Workflow

#### Gestión de Prioridad

- Asignar prioridad (normal, alta, urgente)
- Modificar nivel de prioridad

#### Estado del Remito

Asignar un estado a cada remito, dentro de las alternativas que se listan a continuación.

- Retenido: No se puede despachar.
- Autorizado: Disponible para incluir en un viaje.
- En preparación: Se está armando el envoltorio del remito.
- En carga: Cuando el remito se asigna a un viaje.
- En camino: El viaje que transporta el remito ya comenzó el recorrido.
- No entregado: Fallo de la entrega.
- Entregado: Remito entregado en destino.

Cuando se crea un remito se le asigna el estado "Autorizado".

#### Control de Retención

- Retener remito (con motivo obligatorio)
- Liberar remito retenido (con registro de resolución)

#### Ciclo de Preparación

- Iniciar preparación de mercadería
- Registrar avances parciales
- Finalizar preparación

#### Eventos de Traslado

- Iniciar preparación de mercadería
- Iniciar traslado
- Finalizar traslado

#### Entrega y Cierre

- Registrar entrega en destino
- Documentar conformidad del receptor
- Completar documentación de cierre (imagen de remito firmado)

### Sistema de Estadísticas y Business Intelligence

#### Reportes Generales

- Remitos pendientes de autorización.
- Remitos retenidos y motivos.
- Remitos próximos a incluir en planificación de viajes.

#### Estadísticas por Cliente

- Volumen total de operaciones (peso, volumen, valor)
- Ranking de clientes por diferentes métricas (valor total, cantidad de remitos, volumen)
- Distribución geográfica de destinos solicitados

#### Estadísticas de Unidades de Carga

- Cantidad total de pallets movilizados por período
- Análisis de uso de racks por cliente y destino
- Estadísticas de transporte de bobinas por industria
- Proyecciones de demanda futura por tipo de unidad

#### Análisis Geográfico

- Mapa de calor de orígenes y destinos
- Valor declarado total por provincia/región
- Flujos predominantes de mercadería entre regiones
- Análisis comparativo entre zonas geográficas
- Identificación de corredores logísticos principales

#### Análisis Temporal

- Evolución histórica de volúmenes manejados
- Comparativas interanuales
- Identificación de patrones estacionales
- Análisis de picos de demanda

#### Dashboards Configurables

- Pantallas de resumen ejecutivo
- Indicadores clave de desempeño (KPIs)
- Exportación a múltiples formatos
- Programación de reportes automáticos

#### Métricas de Eficiencia Operativa

- Tiempos promedio en cada etapa del workflow
- Análisis de causas de retención
- Efectividad de la priorización
