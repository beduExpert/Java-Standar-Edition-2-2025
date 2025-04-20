🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 01**](../Readme.md) ➡️ / ⚡ `Reto 01: Registro de productos para inventario`

## 🎯 Objetivo

⚒️ Reforzar la creación de entidades con **JPA**, usando el mismo proyecto del ejemplo anterior para agregar validaciones y consultas específicas en la clase `Producto`, simulando un sistema de inventario más realista.

---

## 📝 Instrucciones

📌 **Importante:**  
**No es necesario crear un nuevo proyecto**. Este reto debe resolverse **utilizando el mismo proyecto creado durante el _Ejemplo 01_** (`inventario`), extendiendo la lógica de la clase `Producto` y del `ProductoRepository`.

---

### 🛠️ Tareas a realizar:

1. ✍️ Asegúrate de tener tu clase `Producto` creada con los siguientes atributos:
   - `id` (tipo `Long`, llave primaria generada automáticamente)
   - `nombre` (tipo `String`)
   - `descripcion` (tipo `String`)
   - `precio` (tipo `double`)

2. 🔒 Implementa las siguientes **validaciones en la entidad**:
   - `@NotBlank` en `nombre` y `descripcion`
   - `@Min(1)` en `precio`
   > Puedes usar `jakarta.validation.constraints` y asegurarte de tener la dependencia `spring-boot-starter-validation`.

3. 🔍 En `ProductoRepository`, agrega los siguientes métodos personalizados:
   ```java
   List<Producto> findByPrecioGreaterThan(double precio);
   List<Producto> findByNombreContainingIgnoreCase(String nombre);
   List<Producto> findByPrecioBetween(double min, double max);
   List<Producto> findByNombreStartingWithIgnoreCase(String prefijo);
   ```

4. 🧪 Prueba estas consultas y validaciones desde `CommandLineRunner`:
   - Guarda al menos **4 productos**
   - Imprime todos los productos con precio mayor a `500`
   - Imprime todos los productos que contengan `"lap"` en su nombre
   - Imprime productos con precio entre `400` y `1000`
   - Imprime productos cuyo nombre comience con `"m"` o `"M"`

5. 🧾 Muestra la salida en consola con `System.out.println()` o usando `Logger`

---

📘 Recursos útiles:  
🔗 [Spring Data JPA: Derived Query Methods](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repositories.query-methods.details)  
🔗 [Jakarta Bean Validation (JSR 380)](https://jakarta.ee/specifications/bean-validation/)

---

🧠 **Nota:**  
Este reto busca que apliques prácticas reales de validación y consultas personalizadas. Piensa cómo esto puede escalar a un backend completo, y cómo estas consultas permiten construir endpoints en una API REST.

---

🏆 Si logras ver en consola los resultados filtrados correctamente según los criterios establecidos, ¡vas por muy buen camino!

---

⬅️ [**Anterior**](../Ejemplo-01/Readme.md) | [**Siguiente**](../Ejemplo-02/Readme.md)➡️  