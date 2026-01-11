
# 🚚 LogiTrack: Sistema de Gestión Logística de Última Milla

![Java](https://img.shields.io/badge/Java-17-orange) ![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.0-green) ![MySQL](https://img.shields.io/badge/Database-MySQL-blue) ![Status](https://img.shields.io/badge/Status-En_Desarrollo-yellow)

> **Backend Solution** enfocada en la optimización de rutas, control de flota y trazabilidad de envíos mediante la aplicación de Patrones de Diseño (GoF) y Arquitectura Limpia.

## 📋 Descripción del Proyecto

**LogiTrack** es una solución de software diseñada para resolver la problemática de la logística de "última milla". El sistema gestiona el ciclo de vida completo de un paquete, desde su recepción en el centro de distribución hasta la entrega final al cliente, manejando reglas de negocio complejas como validación de capacidad de carga, zonas de reparto y cálculo dinámico de costos.

Este proyecto destaca por **no ser un simple CRUD**, sino un sistema transaccional con lógica de estados y algoritmos de asignación.

---

## ⚙️ Arquitectura y Diseño (Ingeniería de Software)

Este proyecto fue concebido primero desde el **Análisis y Diseño de Sistemas** antes de pasar a la implementación.

### 1. Modelado de Dominio (UML)
El núcleo del sistema se basa en un modelo orientado a objetos que resuelve la relación histórica entre `Paquetes` y `Hojas de Ruta`.
* **Desafío:** Permitir que un paquete "rebotado" (intento fallido) pueda ser reasignado a una nueva ruta sin perder el historial.
* **Solución:** Implementación de una clase intermedia `DetalleHojaRuta` para manejar la relación N:M temporal.

*(Aquí puedes subir la imagen de tu Diagrama de Clases a la carpeta /docs de tu repo y enlazarla así:)*
![Diagrama de Clases](./docs/diagrama_clases.png)

### 2. Máquina de Estados (State Pattern)
El ciclo de vida del paquete (`Recibido` -> `En Depósito` -> `En Camino` -> `Entregado`) no se maneja con strings simples.
* Se implementó un flujo de control estricto para evitar inconsistencias (ej: no se puede "Entregar" algo que no ha "Salido a Reparto").
* Se diseñó un **Ciclo de Vida Resiliente**: manejo de excepciones y retornos a depósito.

*(Aquí iría tu imagen del DTE)*
![Diagrama de Transición de Estados](./docs/dte_paquete.png)

---

## 🛠️ Patrones de Diseño Aplicados (GoF)

Para garantizar la mantenibilidad y escalabilidad, se aplicaron los siguientes patrones:

* **Strategy Pattern:** Para el cálculo de costos de envío. Permite cambiar el algoritmo (Standard, Flash, Internacional) sin modificar la clase `Paquete`.
* **State Pattern:** Para delegar el comportamiento del paquete según su estado actual, eliminando sentencias `if-else` complejas y anidadas.
* **Factory Method:** Para la instanciación polimórfica de los distintos tipos de `Vehículos` (Motos, Camionetas, Drones).
* **DTO (Data Transfer Object):** Para desacoplar la capa de persistencia (Entidades JPA) de la capa de presentación (API REST), protegiendo la estructura interna de la base de datos.

---

## 🚀 Stack Tecnológico

* **Lenguaje:** Java 17 (LTS)
* **Framework:** Spring Boot 3 (Spring Web, Spring Data JPA)
* **Base de Datos:** MySQL (Diseño normalizado a 3FN)
* **Herramientas:** Maven, Git, Postman.
* **Documentación:** Swagger / OpenAPI (Próximamente).

---

## 📂 Estructura del Proyecto

El código sigue una arquitectura en capas para separar responsabilidades:

```bash
com.valentinaluna.logitrack
├── config          # Configuraciones (Swagger, Security, Beans)
├── controller      # Capa REST (Endpoints de entrada)
├── dto             # Objetos de transferencia de datos
├── model           # Entidades JPA (Reflejo de la BD)
│   ├── enums       # Estados y Tipos
│   └── strategy    # Implementación de patrones
├── repository      # Interfaces de acceso a datos (Hibernate)
└── service         # Lógica de negocio pura (Casos de Uso)

```

---

## ⚡ Instalación y Ejecución

1. **Clonar el repositorio:**
```bash
git clone [https://github.com/valentinaluna14/LogiTrack-Backend.git](https://github.com/valentinaluna14/LogiTrack-Backend.git)

```


2. **Configurar Base de Datos:**
Crea una base de datos en MySQL llamada `logitrack_db` y actualiza el archivo `src/main/resources/application.properties` con tus credenciales.
3. **Ejecutar la aplicación:**
```bash
./mvnw spring-boot:run

```


4. **Probar Endpoints:**
La API estará disponible en `http://localhost:8080/api/v1`

---

## 👤 Autor

**Valentina Luna**
*Analista de Sistemas & Desarrolladora Java en formación*

[LinkedIn](https://www.linkedin.com/in/valentina-luna-39a76b281/) | [GitHub](https://www.google.com/search?q=https://github.com/valentinaluna14)

---

*Este proyecto fue desarrollado como parte de un desafío técnico de verano para aplicar conocimientos avanzados de Diseño de Sistemas y Arquitectura de Software.*

```

***

```