🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 07**](../Readme.md) ➡️ / 📝 `Ejemplo 03: Comunicación entre microservicios`

## 🎯 Objetivo

🔗 Comprender cómo se realiza la **comunicación entre microservicios** utilizando **REST** y **JSON** como mecanismos de intercambio de datos.  
Además, conocerás el concepto de **API Gateway** y utilizarás **Postman** o **Swagger** para probar las interacciones entre servicios.

---

## ⚙️ Requisitos

- JDK 17 o superior  
- IDE compatible con Java (IntelliJ IDEA, Eclipse, VSCode)  
- Maven o Gradle instalado  
- **Postman** o **Swagger** (opcional para pruebas)

---

## 🧠 Contexto del ejemplo

En un sistema basado en **microservicios**, los módulos no se comunican directamente a través de métodos internos, sino mediante **solicitudes HTTP REST** que intercambian datos en **formato JSON**.

En este ejemplo tendrás **dos microservicios independientes**:

1. **Servicio de Empleados**: expone información de empleados (nombre, ID, idDepartamento).  
2. **Servicio de Departamentos**: devuelve el nombre del departamento dado un **idDepartamento**.

El **Servicio de Empleados** se comunica vía **HTTP REST** con el **Servicio de Departamentos** para enriquecer su información y devolver a los clientes un **JSON combinado**.

---

## 📂 Estructura del proyecto

```
Ejemplo-03/
│
├── departamento_service/   <-- Proyecto Maven independiente
│   └── src/main/java/com/bedu/departamento_service/controller/
│       └── DepartamentoController.java
│
└── empleado_service/       <-- Proyecto Maven independiente
    └── src/main/java/com/bedu/empleado_service/controller/
        └── EmpleadoController.java
```

🔔 **Importante:**  
Cada microservicio es un **proyecto Maven independiente** con su propio `pom.xml` y estructura de carpetas.  
No se deben crear como paquetes dentro del mismo proyecto. **Cada uno se ejecuta por separado** y se comunica mediante HTTP.

---

## ⚙️ ¿Cómo crear cada microservicio?

### Opción 1: Usando [https://start.spring.io](https://start.spring.io) (Recomendado)

1. Abre [https://start.spring.io](https://start.spring.io).
2. Configura:
   - **Group:** `com.bedu`
   - **Artifact:** `departamento_service` (o `empleado_service`)
   - **Dependencies:** `Spring Web`
3. Descarga el proyecto y descomprímelo en la carpeta correspondiente (`departamento_service/` o `empleado_service/`).
4. Abre cada proyecto en tu IDE.

### Opción 2: Crear proyecto Maven desde tu IDE

1. En IntelliJ IDEA:  
   - File → New → Project → Maven  
   - Configura el **GroupId** y **ArtifactId** como corresponde.
2. Agrega el siguiente bloque en el `pom.xml`:

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>3.4.5</version>
    <relativePath/> <!-- lookup parent from repository -->
</parent>
```

Y las dependencias necesarias:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

---

## 💻 Código

### 🧩 Microservicio: **departamento_service**

```java
// DepartamentoController.java
package com.bedu.departamento_service.controller;

import org.springframework.web.bind.annotation.*;

import java.util.Map;

@RestController
@RequestMapping("/api/departamentos/") // Nota: Incluye slash final para evitar confusión
public class DepartamentoController {

    // Simula una base de datos con un Map inmutable de departamentos (ID -> Nombre).
    private static final Map<Long, String> DEPARTAMENTOS = Map.of(
        1L, "Marketing",
        2L, "IT",
        3L, "Finanzas"
    );

    // Endpoint que devuelve el nombre del departamento según el ID proporcionado.
    @GetMapping("/{id}")
    public String obtenerDepartamento(@PathVariable Long id) {
        return DEPARTAMENTOS.getOrDefault(id, "Desconocido");
    }

    // Endpoint que devuelve todos los departamentos en formato JSON.
    @GetMapping
    public Map<Long, String> obtenerTodosLosDepartamentos() {
        return DEPARTAMENTOS;
    }
}
```

---

### 🧩 Microservicio: **empleado_service**

```java
// EmpleadoController.java
package com.bedu.empleado_service.controller;

import org.springframework.web.bind.annotation.*;
import org.springframework.web.client.RestTemplate;

import java.util.List;
import java.util.Map;

@RestController
@RequestMapping("/api/empleados")
public class EmpleadoController {

    // Simula una base de datos de empleados como una lista inmutable de mapas (cada mapa representa un empleado).
    private static final List<Map<String, Object>> EMPLEADOS = List.of(
        Map.of("id", 1, "nombre", "Ana Gómez", "idDepartamento", 1L),
        Map.of("id", 2, "nombre", "Carlos Pérez", "idDepartamento", 2L)
    );

    // RestTemplate es un cliente HTTP que permite consumir otros servicios REST.
    private final RestTemplate restTemplate = new RestTemplate();

    // Endpoint que devuelve la lista de empleados, agregando cada empleado con el nombre del departamento.
    @GetMapping
    public List<Map<String, Object>> obtenerEmpleados() {
        // Recorre cada empleado de la lista original
        return EMPLEADOS.stream().map(empleado -> {
            // Obtiene el ID del departamento del empleado actual
            Long idDepto = (Long) empleado.get("idDepartamento");

            // Realiza una llamada HTTP GET al microservicio departamento_service para obtener el nombre del departamento
            String departamento = restTemplate.getForObject(
                "http://localhost:8081/api/departamentos/" + idDepto, // URL construida dinámicamente con el idDepartamento
                String.class // Se espera una respuesta en formato String (nombre del departamento)
            );

            // Crea una copia mutable del mapa de empleado original (porque List.of() y Map.of() generan colecciones inmutables)
            Map<String, Object> empleadoModificado = new java.util.HashMap<>(empleado);

            // Agrega el nombre del departamento al mapa del empleado
            empleadoModificado.put("departamento", departamento);

            // Devuelve el empleado enriquecido con la información del departamento
            return empleadoModificado;
        }).toList(); // Recolecta todos los empleados modificados en una nueva lista
    }
}
```

---

### ⚙️ Configuración de puertos

Cada microservicio debe correr en **puertos distintos**. Agrega en el `application.properties` de cada uno:

#### departamento_service (puerto 8081):

```properties
server.port=8081
```

#### empleado_service (puerto 8080):

```properties
server.port=8080
```

---

## 🧪 Cómo probar la comunicación

1. Arranca **departamento_service** (escuchando en `localhost:8081`).  
2. Arranca **empleado_service** (escuchando en `localhost:8080`).  
3. Abre **Postman** o tu navegador en:

```
http://localhost:8080/api/empleados
```

4. Deberías ver un **JSON combinado**:

```json
[
  { "id": 1, "nombre": "Ana Gómez", "idDepartamento": 1, "departamento": "Marketing" },
  { "id": 2, "nombre": "Carlos Pérez", "idDepartamento": 2, "departamento": "IT" }
]
```

---

## 📝 Conceptos clave utilizados

- **REST**: Patrón para comunicación entre servicios usando HTTP.  
- **JSON**: Formato estándar para intercambiar datos entre microservicios.  
- **RestTemplate**: Cliente HTTP en Spring para consumir otros servicios REST.  
- **API Gateway**: Punto central de entrada que coordina las llamadas a múltiples microservicios (no implementado, solo explicado).

---

## 🚀 Resumen

Este ejemplo mostró cómo dos **microservicios independientes** se comunican mediante **HTTP REST** y **JSON**. Aprendiste a usar **RestTemplate** para realizar solicitudes entre servicios y comprendiste el rol que juega un **API Gateway** como punto central para coordinar las comunicaciones en arquitecturas basadas en microservicios.

> **Tip final:** Aunque en este ejemplo se usa **RestTemplate**, en proyectos más robustos puedes utilizar **Feign Client** o **Spring Cloud Gateway** para facilitar la comunicación entre microservicios.

---

⬅️ [**Anterior**](../Ejemplo-02/Readme.md) | [**Siguiente**](../Reto-01/Readme.md)➡️  