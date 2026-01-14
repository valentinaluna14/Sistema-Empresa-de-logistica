# Cambios en Diagramas

Este documento detalla los cambios necesarios en los diagramas del sistema LogiTrack para soportar los nuevos requisitos.

## 1. Diagrama de Clases

### Clase `Paquete`
*   **Nuevo Atributo:** `costo: float` (Para persistir el valor calculado del envío).
*   **Nueva Relación:** Asociación con `ZonaPreferente` (Multiplicidad 1 a 1).
    *   Un Paquete tiene asignada una Zona Preferente.
*   **Nueva Relación:** Asociación con `TipoEnvio` (Multiplicidad 1 a 1).
    *   Ya existía indirectamente, pero debe ser explícita para la validación de reglas (Fragile).

### Clase `Vehiculo`
*   Asegurar que `tipoVehiculo` permita distinguir entre "Moto" y "Camioneta" (Enum o Clase TipoVehiculo).
*   Asegurar relación con `ZonaPreferente`.

### Clase `TipoEnvio`
*   Debe soportar los tipos: "Standard", "Flash", "Fragile".

## 2. Diagrama de Casos de Uso
*   Sin cambios estructurales a nivel de actores y casos de uso principales.
*   El caso de uso "Registrar Paquete" ahora incluye internamente la lógica de "Seleccionar Tipo de Envío" y "Calcular Costo".
*   El caso de uso "Gestionar Hoja de Ruta" ahora incluye validaciones de reglas de negocio (Zona y Transporte Fragile).

## 3. Interfaces de Usuario (Mockups/Pantallas)

### Pantalla Registrar Paquete
*   **Agregar Selector:** "Zona de Entrega" (Norte, Sur, Centro).
*   **Agregar Selector:** "Tipo de Envío" (Standard, Flash, Fragile).
*   **Agregar Visualización:** Campo para mostrar el "Costo Estimado" una vez seleccionados los datos.

### Pantalla Gestionar Hoja de Ruta (Asignación)
*   **Agregar Alerta:** Pop-up o mensaje de advertencia cuando se intenta asignar un paquete de una Zona diferente a la del Vehículo.
*   **Agregar Bloqueo:** Mensaje de error si se intenta asignar "Fragile" a "Moto".
