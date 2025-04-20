🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 01**](../Readme.md) ➡️ / ⚡ `Reto 02: Modelo de relaciones para una tienda en línea`

## 🎯 Objetivo

⚒️ Aplicar relaciones entre entidades utilizando anotaciones de JPA (`@OneToMany`, `@ManyToOne`) para modelar una estructura básica de una tienda en línea, como categorías y productos. Se utilizará el mismo proyecto del Ejemplo 02.

---

## 📝 Instrucciones

📌 **Importante:**  
No es necesario crear un nuevo proyecto. Este reto debe resolverse usando el mismo proyecto del **Ejemplo 02**, reutilizando las clases `Producto` y `Categoria`.

---

### 🛠️ Tareas a realizar:

1. ✍️ Asegúrate de tener la clase `Producto` con la relación `@ManyToOne` hacia `Categoria`.

2. ➕ Agrega en la clase `Categoria` la relación inversa `@OneToMany`:

```java
@OneToMany(mappedBy = "categoria")
private List<Producto> productos;
```

3. 🔄 Carga datos desde `CommandLineRunner`:
   - Crea al menos **2 categorías**
   - Asocia al menos **2 productos a cada categoría**

4. 🧪 Recorre e imprime los productos asociados a cada categoría:

```java
System.out.println("📚 Productos por categoría:");
categoriaRepo.findAll().forEach(categoria -> {
    System.out.println("🗂️ " + categoria.getNombre() + ":");
    categoria.getProductos().forEach(producto -> System.out.println("   - " + producto.getNombre()));
});
```

5. ⚙️ Asegúrate de tener los métodos `getProductos()` en `Categoria` y `getCategoria()` en `Producto`.

---

📘 Recursos útiles:  
🔗 [JPA OneToMany – Baeldung](https://www.baeldung.com/jpa-one-to-many)  
🔗 [JPA Relaciones bidireccionales – Baeldung](https://www.baeldung.com/jpa-joincolumn-vs-mappedby)

---

🧠 **Nota:**  
Este reto refuerza el entendimiento de relaciones bidireccionales. Recuerda que `mappedBy` indica que el lado "fuerte" de la relación ya está definido en la entidad `Producto`.

---

🏆 Si logras ver productos agrupados correctamente por categoría en la consola, ¡vas por muy buen camino!

---

⬅️ [**Anterior**](../Ejemplo-02/Readme.md) | [**Siguiente**](../Sesion-02/Readme.md)➡️  