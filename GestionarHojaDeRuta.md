# CU: Gestionar Hoja de Ruta

**Actor:** Operador Logístico
**Actor:** Sistema

1. Iniciar CU
2. Mostrar mensaje “¿Qué acción desea realizar?”
    A. Crear Hoja de Ruta
    B. Añadir Paquete a Hoja de Ruta Existente
    C. Cambiar Conductor
    D. Cambiar Vehículo
    E. Eliminar paquete”
3. Seleccionar opción (A/B/C/D/E)
4. Comprobar que Opción elegida igual a “A”
    A. Buscar instancias de Vehículo
        a. Condición: Que fechaBajaVehiculo sea nulo (activos).
    B. POR CADA instancia de Vehículo:
        a. Leer patente
        b. Leer marca
        c. Leer modelo
        d. Leer capacidadMaximaPeso
        e. Leer capacidadMaximaVolumen
        f. Leer tipoVehiculo (Moto/Camioneta/etc)
        g. Leer zonaPreferente
    C. Mostrar mensaje “Seleccione el Vehículo para la ruta”
    D. Mostrar lista de Vehículos con sus datos
    E. Seleccionar un Vehículo de la lista
    F. Buscar instancias de Conductor
        a. Condición: Que fechaBajaConductor sea nulo (activos).
    G. POR CADA instancia de Conductor:
        a. Leer nombreConductor
        b. Leer dniConductor
        c. Mostrar mensaje “Seleccione el Conductor responsable”
        d. Mostrar lista de Conductores
    H. Seleccionar un Conductor de la lista
    I. Buscar instancia de EstadoHojaDeRuta
        a. con nombreEstadoHoja igual a “Pendiente”
    J. Crear instancia de HojaDeRuta
        a. con numeroHojaDeRuta generado
        b. con fechaHojaDeRuta igual a la actual
        c. Relacionada a instancia de EstadoHojaDeRuta (paso I)
        d. Relacionada a la instancia de Vehículo (seleccionada en E)
        e. Relacionada a la instancia de Conductor (seleccionada en H)
5. Mostrar mensaje “Hoja de Ruta creada”
6. Mostrar mensaje “¿Desea crear otra Hoja De Ruta?”
7. Ingresar respuesta (SI/NO)
8. Comprobar que respuesta igual a “NO”
9. Mostrar mensaje “¿Desea realizar otra acción?”
10. Ingresar respuesta (SI/NO)
11. Comprobar que respuesta igual a “NO”
12. FIN CU

## Camino Alterno N°1: Añadir paquete a hoja de ruta existente
**Actor:** Operador Logístico
**Actor:** Sistema

1. Buscar instancia de HojaDeRuta
    a. Relacionada a instancia de EstadoHojaDeRuta
        i. Con nombreEstadoHoja igual a Pendiente
2. POR CADA instancia de HojaDeRuta
    a. Leer numeroHojaDeRuta
    b. Leer fechaHojaDeRuta
    c. Mostrar numeroHojaDeRuta
    d. Mostrar fechaHojaDeRuta
3. Mostrar mensaje “Seleccione Hoja de Ruta”
4. Selecciona HojaDeRuta
5. Seleccionar HojaDeRuta con numeroHojaDeRuta ingresado
6. Buscar instancias de Paquete
    a. Relacionada a EstadoPaquete
        i. Con nombreEstadoPaquete igual a Recibido
7. POR CADA instancia de Paquete
    a. Leer numeroPaquete
    b. Leer peso
    c. Leer volumen
    d. Leer direccionEntrega
    e. Leer zonaPreferente
    f. Leer tipoEnvio
8. Mostrar mensaje “Seleccione paquete que desea agregar”
9. Selecciona Paquete
10. Seleccionar Paquete con numeroPaquete ingresado
11. Leer pesoAcumulado de HojaDeRuta
    Leer volumenAcumulado de HojaDeRuta
12. Leer Vehículo de HojaDeRuta
13. Leer capacidadMaximaPeso de Vehiculo
14. Leer capacidadMaximaVolumen de Vehiculo
15. Leer tipoVehiculo de Vehiculo
16. Leer zonaPreferente de Vehiculo
17. Leer volumen de Paquete
18. Leer peso de Paquete
19. Leer tipoEnvio de Paquete
20. Leer zonaPreferente de Paquete
21. Buscar instancias de PaqueteHojaDeRuta
    a. Con relación a instancia de Paquete
22. **Validación de Transporte (Fragile):**
    SI Paquete.tipoEnvio es "Fragile" Y Vehiculo.tipoVehiculo es "Moto"
    a. Mostrar mensaje "Error: Paquetes Frágiles no pueden asignarse a Motos. Se requiere Camioneta."
    b. Cancelar asignación y volver a Paso 8 (Seleccionar Paquete).
23. **Validación de Capacidad:**
    SI peso + pesoAcumulado <= capacidadMaximaPeso Y volumen + volumenAcumulado <= capacidadMaximaVolumen
    a. **Validación de Zona:**
       SI Paquete.zonaPreferente NO ES IGUAL A Vehiculo.zonaPreferente
       i. Mostrar Advertencia "El paquete pertenece a una zona distinta a la del vehículo. ¿Desea continuar?"
       ii. Ingresar Confirmación (SI/NO)
       iii. SI respuesta es "NO", Cancelar asignación y volver a Paso 8.
    b. Crear instancia de PaqueteHojaDeRuta
        i. con fechaPaqueteHojaDeRuta igual a la actual
        ii. Relacionar a Paquete
    c. Comprobar que instancias de PaqueteHojaDeRuta (paso 21) relacionado a Paquete
        i. Definir variable temporal numeroIteraciones = 0
        ii. Por cada instancia de PaqueteHojaDeRuta
            1. Leer iteracionHojaDeRuta
            2. Modificar variable temporal numeroIteraciones += iteracionHojaDeRuta
        iii. Modificar instancia de PaqueteHojaDeRuta creada
            1. Con iteracionHojaDeRuta igual a numeroIteraciones
        iv. Modificar instancia HojaDeRuta
            1. Con relación a PaqueteHojaDeRuta creada
            2. Actualizar pesoAcumulado y volumenAcumulado
    d. Cambiar Estado de Paquete a "Asignado"
24. SI NO (Fallo Capacidad)
    a. Mostrar mensaje “No es posible asignar este paquete. Excede la capacidad del Vehiculo”
25. Mostrar mensaje “¿Desea agregar otro Paquete?”
26. Ingresar respuesta (SI/NO)
27. Comprobar que respuesta igual a “NO”
28. FIN CU

## Camino Alterno N°2: Cambiar conductor
**Actor:** Operador Logístico
**Actor:** Sistema

1. Iniciar CU
2. Buscar instancia de HojaDeRuta
    b. Relacionada a instancia de EstadoHojaDeRuta
        i. Con nombreEstadoHoja igual a Pendiente
    POR CADA instancia de HojaDeRuta
    e. Leer numeroHojaDeRuta
    f. Leer fechaHojaDeRuta
    g. Mostrar numeroHojaDeRuta
    h. Mostrar fechaHojaDeRuta
3. Mostrar mensaje “Seleccione Hoja de Ruta”
4. Selecciona HojaDeRuta
5. Seleccionar HojaDeRuta con numeroHojaDeRuta
6. Buscar instancias de Conductor
    Condición: Que fechaBajaConductor sea nulo (activos).
    POR CADA instancia de Conductor:
    Leer nombreConductor
    Leer dniConductor
    Leer numeroConductor
    Mostrar nombreConductor
    Mostrar dniConductor
    Mostrar numeroConductor
    Mostrar mensaje “Seleccione el Conductor responsable”
7. Seleccionar Conductor (numeroConductor)
8. Seleccionar Conductor con numeroConductor igual al ingresado
9. Modificar instancia de HojaDeRuta
    a. Eliminar relación actual con Conductor
    b. Crear relación con instancia de Conductor (paso 8)
10. Mostrar mensaje “¿Desea cambiar otro Conductor?”
11. Ingresar respuesta (SI/NO)
12. Comprobar que respuesta igual a “NO”
13. FIN CU
    IR a Paso 2

## Camino Alterno N°3: Cambiar vehículo
**Actor:** Operador Logístico
**Actor:** Sistema

1. Iniciar CU
2. Buscar instancia de HojaDeRuta
    c. Relacionada a instancia de EstadoHojaDeRuta
        i. Con nombreEstadoHoja igual a Pendiente
    d. POR CADA instancia de HojaDeRuta
        1. Leer numeroHojaDeRuta
        ii. Leer fechaHojaDeRuta
        iii. Mostrar numeroHojaDeRuta
        iv. Mostrar fechaHojaDeRuta
    Mostrar mensaje “Seleccione Hoja de Ruta”
3. Seleccionar HojaDeRuta
4. Buscar instancias de Vehículo
    a. Condición: Que fechaBajaVehiculo sea nulo (activos).
    POR CADA instancia de Vehículo:
    b. Leer patente
    c. Leer marca
    d. Leer modelo
    e. Leer capacidadMaximaPeso
    f. Leer capacidadMaximaVolumen
    Mostrar mensaje “Seleccione el Vehículo para la ruta”
    Mostrar lista de Vehículos con sus datos
5. Seleccionar Vehiculo
6. Modificar instancia de Hoja De Ruta
    g. Eliminar relación con vehiculo actual
    h. Relacionar con instancia de Vehiculo seleccionada
7. Mostrar mensaje “¿Desea modificar otro Vehiculo?”
8. Ingresar respuesta (SI/NO)
13. Comprobar que respuesta igual a “NO”
14. FIN CU
    Ir a paso 2

## Camino Alterno N°4: Eliminar paquete
**Actor:** Operador Logístico
**Actor:** Sistema

1. Iniciar CU
2. Buscar instancia de HojaDeRuta
    e. Relacionada a instancia de EstadoHojaDeRuta
        i. Con nombreEstadoHoja igual a Pendiente
    f. POR CADA instancia de HojaDeRuta
        1. Leer numeroHojaDeRuta
        v. Leer fechaHojaDeRuta
        vi. Mostrar numeroHojaDeRuta
        vii. Mostrar fechaHojaDeRuta
    Mostrar mensaje “Seleccione Hoja de Ruta”
3. Seleccionar HojaDeRuta
4. Leer instancias de PaqueteHojaDeRuta
5. Leer instancias de Paquete relacionadas a PaqueteHojaDeRuta
6. Leer numeroPaquete
7. Leer fechaHoraLlegada
8. Leer peso
9. Leer volumen
10. Leer nombreDestinatario
11. Leer numeroPaquete
12. Leer fechaHoraLlegada
13. Leer peso
14. Leer volumen
15. Leer nombreDestinatario
16. Mostrar mensaje “Seleccionar Paquete a Eliminar”
17. Seleccionar Paquete
18. Buscar instancia de PaqueteHojaDeRuta
    a. Con relacion a Paquete seleccionado
19. Modificar instancia de HojaDeRuta
    a. Eliminar relacion con instancia/s de PaqueteHojaDeRuta
20. Mostrar mensaje “¿Desea eliminar otro paquete de la Hoja de ruta?
21. Ingresar respuesta (SI/NO)
13. Comprobar que respuesta igual a “NO”
14. FIN CU
    Ir a paso 16
