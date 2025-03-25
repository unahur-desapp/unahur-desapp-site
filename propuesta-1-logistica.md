---
layout: default
---

# Propuesta 1: Sistema de Gestión de Viajes

## Contexto y Objetivos

El propósito principal de esta propuesta es desarrollar un sistema eficiente para el registro y gestión de los viajes organizados por Logística Acme SRL. Este módulo constituye una pieza fundamental en la operatoria de la empresa, permitiendo mantener un control detallado sobre todos los traslados de mercadería que coordina entre los diversos depósitos de su red logística.

La gestión requerida incluye información sobre vehículos que pertenecen, y choferes que trabajan para, las empresas transportistas que tienen convenio con Logística Acme.

## Descripción Funcional

### Gestión de Entidades

El sistema deberá permitir el registro y mantenimiento de las siguientes entidades:

#### Empresas Transportistas

- Información básica: razón social, CUIT/RUT, domicilio fiscal, datos de contacto.

#### Flota de Vehículos

- Datos del vehículo: patente, marca, modelo, año.
- Características técnicas: capacidad de carga (volumen y peso), tipo de vehículo (selección de una lista configurable).
- A cuál de las empresas transportistas pertenece.

#### Choferes

- Datos personales: nombre completo, DNI/identificación, fecha de nacimiento.
- Para cuál de las empresas transportistas trabaja.
- Vehículo asignado por defecto.

#### Red de Depósitos

- Localización: dirección completa, coordenadas geográficas, provincia/estado, país.
- Tipo: propio o de terceros.
- Horarios de operación y restricciones de acceso.
- Personal de contacto.

### Registro de Viajes

El sistema permitirá la creación, modificación y seguimiento de viajes con la siguiente información:

#### Datos Básicos del Viaje

- Número único de viaje (generado automáticamente por el sistema)
- Depósito de origen (seleccionado de la red de depósitos)
- Depósito de destino (seleccionado de la red de depósitos)
- Fecha y hora programadas para el inicio del viaje
- Fecha y hora estimadas de llegada a destino

#### Asignación de Recursos

- Empresa transportista seleccionada
- Chofer asignado (con validación de pertenencia a la empresa transportista)
- Vehículo a utilizar (por defecto el asignado al chofer, con posibilidad de cambio)

### Consultas y Reportes

El sistema ofrecerá herramientas avanzadas de filtrado y visualización.

#### Listado General de Viajes con capacidad de filtrado por:

- Rango de fechas de inicio
- Número de viaje
- Empresa transportista
- Chofer específico
- Vehículo particular
- Tipo de viaje: nacional (origen y destino en Argentina) o internacional
- Provincia/estado de origen
- Provincia/estado de destino

## Aspectos Técnicos y de Implementación

### Arquitectura Propuesta

- Aplicación web responsive con backend.
- Base de datos no relacional para el almacenamiento de entidades.
- API documentada para integración con otros módulos del sistema.

### Integraciones

- Servicios de geocodificación para cálculo de rutas y distancias.
- Posibilidad de integración con sistemas GPS para seguimiento en tiempo real.
- Preparación para futura integración con el módulo de remitos (Propuesta 2).

## Beneficios Esperados

- Mejora en la trazabilidad de los servicios de transporte
- Optimización en la asignación de recursos (vehículos y choferes)
- Mayor control sobre el estado de las flotas y el cumplimiento de tiempos
- Información consolidada para la toma de decisiones estratégicas

## Alcance del Desarrollo para el Cuatrimestre

Durante el presente cuatrimestre, el desarrollo se enfocará en:

- Diseño e implementación del modelo de datos completo.
- Interfaces CRUD para todas las entidades mencionadas.
- Proceso principal de registro de viajes con validaciones.
- Sistema básico de consultas y filtros.

## Funcionalidades Extras

### Estados del Viaje

Asociar un estado a cada viaje, que puede ser:

- Planificado: viaje programado pero aún no iniciado.
- En tránsito: viaje iniciado pero no finalizado.
- Completado: viaje finalizado correctamente.
- Demorado: viaje con retraso respecto a la estimación.
- Incidente: viaje con problemas en ruta.
- Cancelado: viaje que no se realizará.

Cuando se crea un viaje, se le asigna el estado "Planificado".

Agregar la funcionalidad de cambio de estado a un viaje, y la capacidad de filtrar los viajes de acuerdo a su estado.

#### Reportes Específicos:

- Viajes programados para los próximos días; agenda para un vehículo o para un chofer.
- Vehículos en tránsito actualmente.
- Historial de viajes por empresa transportista.
- Historial de viajes por chofer.
- Tiempo promedio de viaje entre pares de depósitos.
- Incidencias por ruta o por transportista.

#### Documentación de los choferes

- Datos del registro de conducir para validar que tenga vigencia. (Deber poder subir una imagen)
- Si el chofer puede realizar transporte de mercadería peligrosa debe tener en vigencia el curso.

#### Alertas y Notificaciones

- Viajes próximos a iniciar.
- Demoras respecto a los tiempos estimados.
- Vencimientos próximos de documentación (licencias, seguros, etc.).
