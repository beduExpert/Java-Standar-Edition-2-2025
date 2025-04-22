🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 01**](../Readme.md) ➡️ / 📝 `Ejemplo 01: JPA - Creación de entidades y repositorios`

## 🎯 Objetivo

🔍 Aprender a crear una entidad Java utilizando JPA y definir un repositorio para gestionar operaciones básicas con una base de datos, simulando un sistema de inventario.

---

## ⚙️ Requisitos

- IntelliJ IDEA Community Edition
- Apache Maven 3.8.4 o superior
- JDK 17 o superior (se recomienda Java 17+)
- Spring Boot 3.x
- Navegador web para Spring Initializr

---

## 📦 Creación del proyecto con Spring Initializr

1. Ingresa a [https://start.spring.io](https://start.spring.io/)
2. Configura lo siguiente:
   - **Project**: Maven
   - **Language**: Java
   - **Spring Boot**: 3.2.x (última versión estable)
   - **Group**: `com.bedu`
   - **Artifact**: `inventario`
   - **Java**: 17
3. Agrega estas dependencias:
   - Spring Web
   - Spring Data JPA
   - H2 Database (para pruebas rápidas sin instalar nada)

4. Haz clic en "Generate" y abre el proyecto en IntelliJ IDEA.

---

## 🧱 Creación de la entidad `Producto`

Creamos una clase `Producto` con anotaciones JPA:

```java
package com.bedu.inventario;

import jakarta.persistence.*;

@Entity
public class Producto {

    @Id // Campo que funcionará como clave primaria de la tabla
    @GeneratedValue(strategy = GenerationType.IDENTITY) // El ID se generará automáticamente (autoincremental)
    private Long id;

    // Campos que serán columnas en la tabla 'producto'
    private String nombre;
    private String descripcion;
    private double precio;

    protected Producto() {} // Constructor por defecto requerido por JPA

    // Constructor público para crear objetos de tipo Producto con los campos necesarios
    public Producto(String nombre, String descripcion, double precio) {
        this.nombre = nombre;
        this.descripcion = descripcion;
        this.precio = precio;
    }

    // Getters para acceder a los atributos (necesarios para el funcionamiento de JPA y buenas prácticas)
    public Long getId() { return id; }
    public String getNombre() { return nombre; }
    public String getDescripcion() { return descripcion; }
    public double getPrecio() { return precio; }

    // Método que permite imprimir el objeto de forma legible (útil para logs o consola)
    @Override
    public String toString() {
        return String.format("Producto[id=%d, nombre='%s', precio=%.2f]",
                id, nombre, precio);
    }
}
```

---

## 📁 Creación del repositorio `ProductoRepository`

```java
package com.bedu.inventario;

import org.springframework.data.jpa.repository.JpaRepository;

import java.util.List;

// Esta interfaz extiende JpaRepository para gestionar operaciones CRUD sobre la entidad Producto
public interface ProductoRepository extends JpaRepository<Producto, Long> {

    // Método personalizado que busca productos cuyo nombre contenga un texto específico (no sensible a mayúsculas)
    List<Producto> findByNombreContaining(String nombre);
}
```

---

## 🚀 Probar el repositorio desde la clase principal

Edita tu clase `InventarioApplication.java` para incluir un `CommandLineRunner` que pruebe operaciones básicas:

```java
package com.bedu.inventario;

import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;

@SpringBootApplication
public class InventarioApplication {

    public static void main(String[] args) {
        SpringApplication.run(InventarioApplication.class, args);
    }

    @Bean
    public CommandLineRunner demo(ProductoRepository repository) {
        return (args) -> {
            // Guardar algunos productos
            repository.save(new Producto("Laptop", "Portátil de 16 pulgadas", 1200.00));
            repository.save(new Producto("Teclado mecánico", "Switch azul", 800.00));
            repository.save(new Producto("Mouse gamer", "Alta precisión", 600.00));

            // Mostrar todos los productos
			System.out.println("📂 Productos disponibles:");
			repository.findAll().forEach(System.out::println);

			// Buscar por nombre parcial
			System.out.println("\n🔍 Productos que contienen 'Lap':");
			repository.findByNombreContaining("Lap").forEach(System.out::println);
        };
    }
}
```

---

## 🧪 Resultado esperado en consola

Al ejecutar el programa verás una salida similar a:

```
📂 Productos disponibles:
Producto[id=1, nombre='Laptop', precio=1200.00]
Producto[id=2, nombre='Teclado mecánico', precio=800.00]
Producto[id=3, nombre='Mouse gamer', precio=600.00]

🔍 Productos que contienen 'Lap':
Producto[id=1, nombre='Laptop', precio=1200.00]
```

---

## 🔍 Conceptos clave utilizados

| Anotación / Clase | Propósito |
|-------------------|-----------|
| `@Entity`         | Marca una clase como entidad persistente |
| `@Id`             | Indica el atributo que será la clave primaria |
| `@GeneratedValue` | Especifica cómo se genera automáticamente el ID |
| `JpaRepository`   | Permite usar métodos como `save()`, `findAll()`, `deleteById()` sin código adicional |
| `CommandLineRunner` | Ejecuta código al iniciar la app (útil para pruebas sin frontend) |

---

### 💡 ¿Sabías que...?

- **JPA** no es una implementación en sí, sino una **especificación**. Las implementaciones más conocidas son **Hibernate**, **EclipseLink** y **TopLink**.
- Spring Boot **detecta automáticamente** las entidades y configura el datasource si encuentra dependencias como `spring-boot-starter-data-jpa` y una base de datos embebida como H2.
- Puedes **cambiar la base de datos** de desarrollo (por ejemplo, de H2 a MySQL) simplemente modificando tu archivo `application.properties` sin tocar el código de tus entidades.
- Gracias a la convención de nombres, Spring Data JPA puede **generar automáticamente consultas** como `findByNombreContaining` o `findByPrecioGreaterThan`.
- **JPA con Spring Boot** permite crear operaciones CRUD completas sin escribir SQL manualmente, gracias al uso de repositorios.
- `@Bean CommandLineRunner` ejecuta código automáticamente al iniciar la app, útil para probar sin interfaz gráfica.

---

### 📘 Recursos adicionales

- 🔗 [Spring Data JPA – Query Methods](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repositories.query-methods)
- 🔗 [POO en Java – W3Schools](https://www.w3schools.com/java/java_oop.asp)
- 🔗 [Spring Boot: Guía oficial](https://spring.io/projects/spring-boot)

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Reto-01/Readme.md)➡️  