🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 01**](../Readme.md) ➡️ / 📝 `Ejemplo 03: Aplicación web con CRUD y JPA`

## 🎯 Objetivo

🔍 Construir una aplicación Java web utilizando Spring Boot y JPA que permita exponer operaciones CRUD mediante un API REST, integrando base de datos, servicios y controladores.

---

## ⚙️ Requisitos

- Proyecto Spring Boot con la entidad `Producto`  
- IntelliJ IDEA o editor compatible con Spring Boot  
- [Postman](https://www.postman.com/downloads/) o cualquier cliente REST  
- Dependencias: Spring Web, Spring Data JPA, H2 Database  
- Archivo `application.properties` correctamente configurado  

---

## 🧱 Arquitectura y organización del proyecto

¿Has notado que cada vez hay más archivos en nuestro proyecto?  
Para mantener todo ordenado y escalable, este ejemplo sigue una arquitectura en capas, separando controladores, servicios, repositorios y modelos, con el fin de facilitar la escalabilidad y mantenibilidad del proyecto.

| Capa         | Ubicación en el proyecto            | Rol |
|--------------|-------------------------------------|-----|
| **Modelo**   | `models/`                           | Representa la estructura de datos (`Producto`) |
| **Controlador** | `controllers/`                   | Expone endpoints que reciben peticiones HTTP |
| **Servicio** | `services/`                          | Contiene la lógica de negocio entre el controlador y la base de datos |
| **Repositorio** | `repositories/`                  | Interactúa con la base de datos usando JPA |

> Esta separación **mejora la mantenibilidad, pruebas y escalabilidad** del proyecto.

---

## 📁 Estructura general

```
src/main/java/com/bedu/inventario/
├── controllers/
│   └── ProductoController.java
├── services/
│   └── ProductoService.java
├── repositories/
│   └── ProductoRepository.java
├── models/
│   └── Producto.java
└── InventarioApplication.java
```

---

## 🧱 Paso 1: Crear el servicio `ProductoService`

```java
import com.bedu.inventario.models.Producto;
import com.bedu.inventario.repositories.ProductoRepository;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class ProductoService {

    private final ProductoRepository repository;

    public ProductoService(ProductoRepository repository) {
        this.repository = repository;
    }

    public List<Producto> obtenerTodos() {
        return repository.findAll();
    }

    public Producto guardar(Producto producto) {
        return repository.save(producto);
    }
}
```

---

## 🌐 Paso 2: Crear el controlador `ProductoController`

```java
import com.bedu.inventario.models.Producto;
import com.bedu.inventario.services.ProductoService;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/api/productos")
public class ProductoController {

    private final ProductoService servicio;

    public ProductoController(ProductoService servicio) {
        this.servicio = servicio;
    }

    @GetMapping
    public List<Producto> obtenerProductos() {
        return servicio.obtenerTodos();
    }

    @PostMapping
    public Producto crearProducto(@RequestBody Producto producto) {
        return servicio.guardar(producto);
    }
}
```

---

## ✅ Paso 3: implementación para `InventarioApplication.java`

```java
import com.bedu.inventario.models.Producto;
import com.bedu.inventario.repositories.ProductoRepository;
import org.springframework.boot.*;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;

@SpringBootApplication
public class InventarioApplication {

	public static void main(String[] args) {
		SpringApplication.run(InventarioApplication.class, args);
	}

	@Bean
	public CommandLineRunner initData(ProductoRepository productoRepo) {
		return args -> {
			productoRepo.save(new Producto("Laptop Lenovo", "AMD Ryzen 7, 16GB RAM", 18500.0));
			productoRepo.save(new Producto("Mouse inalámbrico", "Marca Logitech, sensor óptico", 350.0));
			productoRepo.save(new Producto("Monitor LG", "27 pulgadas, Full HD", 4300.0));

			System.out.println("📦 Productos cargados:");
			productoRepo.findAll().forEach(System.out::println);
		};
	}
}
```

---

## 🧪 Pruebas con Postman (paso a paso)

### 🔹 1. Iniciar la aplicación

Asegúrate de que la app esté corriendo en `http://localhost:8080`.

---

### 🔹 2. Obtener productos (GET)

- **Método:** `GET`  
- **URL:** `http://localhost:8080/api/productos`  
- **Resultado esperado:** Lista de productos

---

### 🔹 3. Crear un producto (POST)

- **Método:** `POST`  
- **URL:** `http://localhost:8080/api/productos`  
- **Headers:**  
  - `Content-Type`: `application/json`  
- **Body (raw, JSON):**

```json
{
  "nombre": "Smartwatch Xiaomi",
  "descripcion": "Pantalla AMOLED, resistente al agua",
  "precio": 1800.0
}
```

---

## 🧠 Notas

- Este ejemplo marca el inicio del desarrollo de una **API REST completa** con Spring Boot.
- El uso de `@RestController` permite exponer endpoints sin configuración adicional.
- Esta versión está intencionadamente simplificada para enfocarse en CRUD sin relaciones.
- Para versiones más complejas (con relaciones o lógica adicional), puedes usar DTOs, validaciones y controladores separados por recurso.

---

## 📝 En resumen

- Implementamos una **API REST básica** en Java usando **Spring Boot** y **JPA**, siguiendo una **arquitectura en capas** (controladores, servicios, repositorios, modelos).
- **`ProductoController`** expone los **endpoints HTTP** (`GET`, `POST`) para interactuar con los datos.
- **`ProductoService`** encapsula la **lógica de negocio**, mientras que **`ProductoRepository`** maneja la **persistencia** mediante **Spring Data JPA**.
- Probamos la API con **Postman**, simulando la creación y consulta de productos en la base de datos **H2 embebida**.
- Esta estructura permite **extender fácilmente la aplicación**, añadiendo nuevas funcionalidades, relaciones entre entidades o integraciones externas.

---

📘 Recursos útiles:  
🔗 [Spring Boot REST API – Baeldung](https://www.baeldung.com/spring-boot-building-a-restful-web-service)  
🔗 [Postman – Guía oficial](https://learning.postman.com/docs/getting-started/introduction/)

---

⬅️ [**Anterior**](../Reto-02/Readme.md) | [**Siguiente**](../../Sesion-02/Readme.md)➡️  