🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 01**](../Readme.md) ➡️ / 📝 `Ejemplo 02: Configuración de conexión y creación de tablas`

## 🎯 Objetivo

🔍 Aprender a configurar correctamente la conexión a base de datos en un proyecto Spring Boot con JPA, y modelar una relación simple entre entidades para representar un caso de uso real como una tienda en línea.

---

## ⚙️ Requisitos

- Proyecto base generado en [Spring Initializr](https://start.spring.io) (puedes reutilizar el proyecto del Ejemplo 01)
- IntelliJ IDEA Community Edition
- Apache Maven 3.8.4 o superior
- JDK 17 o superior
- Base de datos H2 (embebida)
- Archivo `application.properties` correctamente configurado

---

## 🧰 ¿Qué veremos en este ejemplo?

- Cómo configurar la conexión a la base de datos en `application.properties`
- Cómo crear una entidad nueva (`Categoria`)
- Cómo relacionarla con `Producto` usando anotaciones JPA (`@ManyToOne`, `@JoinColumn`)
- Cómo verificar que las tablas se crean correctamente

---

## 📁 Estructura de entidades

### 🧱 `Categoria.java`

```java
package com.bedu.inventario;

import jakarta.persistence.*;

@Entity
public class Categoria {

    @Id // Esta anotación indica que el campo 'id' será la clave primaria de la tabla
    @GeneratedValue(strategy = GenerationType.IDENTITY) // El valor del ID se generará automáticamente (autoincremental) por la base de datos
    private Long id;

    private String nombre;

    protected Categoria() {}

    public Categoria(String nombre) {
        this.nombre = nombre;
    }

    public Long getId() { return id; }
    public String getNombre() { return nombre; }
}
```

---

### 🧱 Ajustes en `Producto.java`

Además de agregar el campo `categoria` como una relación, es importante complementar la clase con los siguientes elementos:

```java
// Justo después de los demás atributos
@ManyToOne
@JoinColumn(name = "categoria_id") // nombre de la columna FK en la tabla productos
private Categoria categoria;
```

```java
// Dentro del constructor público (debajo de los otros parámetros)
public Producto(String nombre, String descripcion, double precio, Categoria categoria) {
    this.nombre = nombre;
    this.descripcion = descripcion;
    this.precio = precio;
    this.categoria = categoria;
}
```

```java
// Agregar un getter al final de los métodos de acceso
public Categoria getCategoria() {
    return categoria;
}
```

```java
// Dentro del método toString(), agrega la categoría de forma opcional
@Override
public String toString() {
    return String.format(
        "Producto[id=%d, nombre='%s', precio=%.2f, categoria='%s']",
        id, nombre, precio, categoria != null ? categoria.getNombre() : "Sin categoría"
    );
}
```

> 📌 Recuerda que estas modificaciones deben integrarse dentro de la clase `Producto`, en su ubicación correspondiente (atributos arriba, métodos abajo). No deben duplicarse fuera de la clase.

---

## ⚙️ Configuración de `application.properties`

Asegúrate de tener este archivo dentro de `src/main/resources`:

```properties
spring.datasource.url=jdbc:h2:mem:inventariodb
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

spring.jpa.hibernate.ddl-auto=update
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
```

---

## 🚀 Prueba rápida en `CommandLineRunner`

Agrega este código en `InventarioApplication.java` para cargar una categoría y asociarla a productos:

```java
@Bean
public CommandLineRunner demo(ProductoRepository productoRepo, CategoriaRepository categoriaRepo) {
    return (args) -> {
        Categoria tecnologia = new Categoria("Tecnología");
        categoriaRepo.save(tecnologia);

        productoRepo.save(new Producto("Laptop ASUS ROG Strix SCAR 18", "Intel Core i9, RTX 5090", 90000.00, tecnologia));
        productoRepo.save(new Producto("Laptop MSI Titan 18 HX", "Intel Core i9, RTX 4090", 140000.00, tecnologia));
        productoRepo.save(new Producto("Tablet Lenovo", "Pantalla 10 pulgadas", 7800.00, tecnologia));

        System.out.println("📂 Productos registrados:");
        productoRepo.findAll().forEach(p -> System.out.println(p.getNombre() + " - " + p.getCategoria().getNombre()));
    };
}
```

---

## 🧪 Resultado esperado en consola

Al ejecutar el proyecto, deberías ver una salida similar a esta:

```
📂 Productos registrados:
Laptop ASUS ROG Strix SCAR 18 - Tecnología
Laptop MSI Titan 18 HX - Tecnología
Tablet Lenovo - Tecnología
```

Esto confirma que:
- Las entidades fueron creadas correctamente
- La relación `@ManyToOne` entre `Producto` y `Categoria` funciona
- Los datos se están consultando correctamente desde la base de datos embebida

> 💡 Si no ves el nombre de la categoría o aparece como `null`, asegúrate de haber guardado la categoría antes de asociarla a los productos y de haber actualizado el método `toString()` y el getter.


---

## 🧪 Verificación en consola H2

1. Ejecuta la aplicación
2. Abre el navegador: [http://localhost:8080/h2-console](http://localhost:8080/h2-console)
3. Usa la URL: `jdbc:h2:mem:inventariodb`  
4. Tabla `producto` debe tener una columna `categoria_id`
5. Puedes hacer consultas como:

```sql
SELECT * FROM producto;
SELECT * FROM categoria;
```

---

## 🧠 Notas

- `@ManyToOne` se usa cuando varios productos pertenecen a una misma categoría.
- `@JoinColumn` permite personalizar el nombre de la columna de la clave foránea.
- Spring Boot se encarga de crear automáticamente las tablas si `ddl-auto=update`.

---


## 💡 **¿Y si quiero usar MySQL o MariaDB?**  
> Aunque este ejemplo usa H2 por simplicidad, puedes cambiar fácilmente a MySQL o MariaDB modificando el archivo `application.properties` y agregando el conector correspondiente al `pom.xml`. Esto se recomienda como actividad adicional fuera de clase.


Podríamos incluir un fragmento de configuración para MySQL como referencia:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/inventario_db
spring.datasource.username=root
spring.datasource.password=123456
spring.jpa.hibernate.ddl-auto=update
```

Y el conector en el `pom.xml`:

```xml
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <scope>runtime</scope>
</dependency>
```

---

## 📝 En resumen

- Configuramos la **conexión a una base de datos** embebida (H2) en un proyecto **Spring Boot** usando **`application.properties`**.
- Creamos una relación **`@ManyToOne`** entre **`Producto`** y **`Categoria`**, modelando un escenario típico de **tienda en línea** donde varios productos comparten la misma categoría.
- Probamos la conexión y las entidades usando **`CommandLineRunner`**, cargando datos y verificando la **persistencia**.
- También validamos el esquema en la **consola H2**, asegurándonos que las tablas y las relaciones se crearon correctamente.
- Esta estructura facilita la **escalabilidad** del sistema, permitiendo agregar nuevas entidades o cambiar la base de datos (por ejemplo, de H2 a **MySQL** o **MariaDB**) sin modificar el código fuente de las entidades.

---

📘 Recursos útiles:  
🔗 [Relaciones en JPA – Baeldung](https://www.baeldung.com/jpa-joincolumn-vs-mappedby)  
🔗 [JPA Relationships – Official Guide](https://jakarta.ee/specifications/persistence/)

---

⬅️ [**Anterior**](../Reto-01/Readme.md) | [**Siguiente**](../Reto-02/Readme.md)➡️  