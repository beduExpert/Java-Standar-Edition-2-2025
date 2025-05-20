🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 07**](../Readme.md) ➡️ / 📝 `Ejemplo 02: API REST básica con Spring Boot`

## 🎯 Objetivo

🚀 Conocer la **estructura básica de un proyecto Spring Boot** y aprender a crear una **API REST simple**, utilizando **controladores** y **servicios** para manejar solicitudes HTTP.

---

## 📦 Creación del proyecto con Spring Initializr

1. Ingresa a [https://start.spring.io](https://start.spring.io/)
2. Configura lo siguiente:
   - **Project**: Maven
   - **Language**: Java
   - **Spring Boot**: 3.2.x (última versión estable)
   - **Group**: `com.bedu`
   - **Artifact**: `rrhhapi`
   - **Java**: 17
3. Agrega estas dependencias:
   - **Spring Web** (para crear la API REST)
   
4. Haz clic en **Generate** y abre el proyecto en **IntelliJ IDEA** o tu IDE favorito.

---

### 📄 Dependencias principales (`pom.xml`)

Si solo vas a crear la **API REST**, el `pom.xml` básico incluiría:

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>3.4.5</version>
    <relativePath/> <!-- lookup parent from repository -->
</parent>

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

## 🧠 Contexto del ejemplo

Imagina que trabajas en el área de **Recursos Humanos (RRHH)** de una empresa y necesitas una **API REST** para **gestionar empleados**. Esta API permitirá:

- **Listar los empleados registrados**  
- **Agregar nuevos empleados** (con nombre, puesto y salario)

A través de este ejemplo aprenderás:

- La **estructura básica** de un proyecto con **Spring Boot**.  
- Cómo implementar **controladores** y **servicios** para manejar solicitudes HTTP.

---

## 📂 Estructura del proyecto

```
Ejemplo-02/
│
├── src/main/java/com/bedu/rrhhapi/
│   ├── controller/
│   │   └── EmpleadoController.java
│   ├── model/
│   │   └── Empleado.java
│   ├── service/
│   │   └── EmpleadoService.java
│   └── RrhhApiApplication.java
│
└── pom.xml
```

---

## 💻 Código

### 🧩 Modelo: Empleado

```java
// model/Empleado.java
package com.bedu.rrhhapi.model;

public class Empleado {
    private Long id;
    private String nombre;
    private String puesto;
    private double salario;

    public Empleado(Long id, String nombre, String puesto, double salario) {
        this.id = id;
        this.nombre = nombre;
        this.puesto = puesto;
        this.salario = salario;
    }

    // Getters y setters
    public Long getId() { return id; }
    public String getNombre() { return nombre; }
    public String getPuesto() { return puesto; }
    public double getSalario() { return salario; }

    public void setId(Long id) { this.id = id; }
    public void setNombre(String nombre) { this.nombre = nombre; }
    public void setPuesto(String puesto) { this.puesto = puesto; }
    public void setSalario(double salario) { this.salario = salario; }
}
```

---

### 🧩 Servicio: EmpleadoService

```java
// service/EmpleadoService.java
package com.bedu.rrhhapi.service;

import com.bedu.rrhhapi.model.Empleado;
import org.springframework.stereotype.Service;

import java.util.ArrayList;
import java.util.List;

@Service
public class EmpleadoService {
    private final List<Empleado> empleados = new ArrayList<>();

    public EmpleadoService() {
        // Lista de empleados iniciales 👥
        empleados.add(new Empleado(1L, "Ana Gómez", "Gerente de Marketing", 55000));
        empleados.add(new Empleado(2L, "Carlos Pérez", "Desarrollador Backend", 45000));
    }

    public List<Empleado> obtenerTodos() {
        return empleados;
    }

    public void agregarEmpleado(Empleado empleado) {
        empleados.add(empleado);
    }
}
```

---

### 🧩 Controlador: EmpleadoController

```java
// controller/EmpleadoController.java
package com.bedu.rrhhapi.controller;

import com.bedu.rrhhapi.model.Empleado;
import com.bedu.rrhhapi.service.EmpleadoService;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/api/empleados")
public class EmpleadoController {
    private final EmpleadoService empleadoService;

    public EmpleadoController(EmpleadoService empleadoService) {
        this.empleadoService = empleadoService;
    }

    // Obtener todos los empleados 👥
    @GetMapping
    public List<Empleado> obtenerEmpleados() {
        return empleadoService.obtenerTodos();
    }

    // Agregar un nuevo empleado 🆕
    @PostMapping
    public void agregarEmpleado(@RequestBody Empleado empleado) {
        empleadoService.agregarEmpleado(empleado);
    }
}
```

---

### 🧩 Clase principal

```java
// RrhhApiApplication.java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class RrhhapiApplication {

    public static void main(String[] args) {
        SpringApplication.run(RrhhapiApplication.class, args);
    }
}
```

---

## 🧪 Cómo probar la API

1. **Ejecuta el proyecto** corriendo `RrhhApiApplication.java`.  
   - Verás en la consola: `Tomcat started on port(s): 8080 (http)...`.

2. **Probar el endpoint GET (listar empleados):**

   - **Navegador o Postman**:  
     - URL: `http://localhost:8080/api/empleados`  
     - Resultado esperado:

     ```json
     [
       { "id": 1, "nombre": "Ana Gómez", "puesto": "Gerente de Marketing", "salario": 55000 },
       { "id": 2, "nombre": "Carlos Pérez", "puesto": "Desarrollador Backend", "salario": 45000 }
     ]
     ```

3. **Probar el endpoint POST (agregar empleado):**

   - **Postman**:  
     - Método: `POST`  
     - URL: `http://localhost:8080/api/empleados`  
     - Body (JSON):

     ```json
     {
       "id": 3,
       "nombre": "Laura Sánchez",
       "puesto": "Analista de Datos",
       "salario": 48000
     }
     ```

   - **Verifica** con un nuevo `GET` que el empleado se agregó correctamente.

4. **Opción rápida (línea de comandos):**

   ```bash
   curl http://localhost:8080/api/empleados
   ```

   ```bash
   curl -X POST -H "Content-Type: application/json" -d '{"id":4,"nombre":"Mario Gonzalez","puesto":"Ingeniero Backend","salario":110000}' http://localhost:8080/api/empleados
   ```

---

## 📝 Conceptos clave utilizados

- **Spring Boot**: Framework que simplifica la creación de aplicaciones Java, especialmente APIs REST.
- **Controlador (`@RestController`)**: Define los endpoints que responden a las solicitudes HTTP.
- **Servicio (`@Service`)**: Contiene la lógica de negocio.
- **Modelo (POJO)**: Representa los datos de los empleados (nombre, puesto, salario).

---

## 📚 Recursos adicionales

- [Documentación oficial de Spring Boot](https://spring.io/projects/spring-boot)  
- [Guía RESTful API con Spring Boot (Baeldung)](https://www.baeldung.com/building-a-restful-web-service-with-spring-and-java-based-configuration)  
- [Postman – Herramienta para probar APIs](https://www.postman.com/)  

---

## 🚀 Resumen

Este ejemplo mostró cómo crear una **API REST básica con Spring Boot** para **gestionar empleados** dentro de un sistema de **Recursos Humanos (RRHH)**. Aprendiste:

- La **estructura de un proyecto** Spring Boot.  
- Cómo implementar **controladores** para manejar solicitudes HTTP.  
- Cómo encapsular la **lógica de negocio** en **servicios**.

Además, conociste el ecosistema que hace posible esta arquitectura:

---

### 🎯 **Comparativa del ecosistema Spring**

| Concepto                 | ¿Qué es?                                   | ¿Para qué sirve?                                  |
|--------------------------|---------------------------------------------|---------------------------------------------------|
| **Spring Framework**     | Framework base (modular)                   | Desarrollar cualquier tipo de aplicación Java     |
| **Spring Boot**          | Herramienta que simplifica Spring Framework | Crear apps rápidas con mínima configuración       |
| **Spring Web (Starter)** | Módulo de Spring Boot (incluye Spring MVC)  | Construir aplicaciones web y APIs REST (Tomcat embebido) |

---

> **Tip final:** Esta estructura es ideal para **escalar en el futuro**, integrando funcionalidades como **bases de datos**, **autenticación**, o extendiendo hacia módulos de **vacaciones**, **nómina** o **evaluaciones** de desempeño.

---

⬅️ [**Anterior**](../Ejemplo-01/Readme.md) | [**Siguiente**](../Reto-01/Readme.md) ➡️  