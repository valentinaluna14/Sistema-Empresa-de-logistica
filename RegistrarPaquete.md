# CU: Registrar paquete

**Actor:** Operador logístico
**Actor:** Sistema

1. Iniciar CU
2. Mostrar mensaje “Registrar paquete ingresado”
3. Mostrar mensaje “Ingrese la siguiente información: nombreDestinatario, correoDestinatario, telefonoDestinatario, peso, volumen, direccionEntrega, zonaPreferente, tipoEnvio”
4. Ingresar datos (nombreDestinatario, correoDestinatario, telefonoDestinatario, peso, volumen, direccionEntrega, zonaPreferente, tipoEnvio)
5. Buscar instancia de clase PaqueteEstado
    a. Con nombreEstadoPaquete igual a “Recibido”
6. Buscar instancia de clase ZonaPreferente
    a. Con nombreZonaPreferente igual a zonaPreferente ingresada (Norte/Sur/Centro)
7. Buscar instancia de clase TipoEnvio
    a. Con nombreTipoEnvio igual a tipoEnvio ingresado (Standard/Flash/Fragile)
8. Calcular Costo de Envío
    a. Delegar cálculo a la estrategia correspondiente del TipoEnvio seleccionado (EstrategiaCalculoCosto) usando el peso y volumen.
9. Crear instancia de clase Paquete
    a. Con codigoSeguimiento generado
    b. Con correoDestinatario igual a correoDestinatario ingresado
    c. Con direccionEntrega igual a direccionEntrega ingresada
    d. Con fechaHoraLLegada igual a la actual
    e. Con nombreDestinatario igual a nombreDestinatario ingresado
    f. Con numeroPaquete definido
    g. Con peso igual a peso ingresado
    h. Con volumen igual volumen ingresado
    i. Con telefonoDestinatario igual a telefonoDestinatario ingresado
    j. Con costo igual al costo calculado (Paso 8)
    k. Con relacion a la instancia de clase PaqueteEstado (Paso 5)
    l. Con relacion a la instancia de clase ZonaPreferente (Paso 6)
    m. Con relacion a la instancia de clase TipoEnvio (Paso 7)
10. Mostrar mensaje “Paquete ingresado al sistema. Costo calculado: [monto]”
11. Mostrar mensaje “¿Desea ingresar otro paquete?”
12. Ingresar respuesta (SI/NO)
13. Comprobar que respuesta igual a “NO”
14. Guardar Cambios
15. FIN CU

## Camino Alterno N°1: Respuesta ingresada “SI”
**Actor:** Operador Logistico
**Actor:** Sistema

1. Ir a paso 2 (Camino Normal).
