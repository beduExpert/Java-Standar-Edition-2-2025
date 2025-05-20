🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 01**](../Readme.md) ➡️ / 📝 `Ejemplo 01: Introducción a clases y métodos genéricos`

## 🎯 Objetivo

🔍 Comprender qué son las **clases genéricas** en Java, cómo se declaran y cuál es su importancia para crear **código reutilizable y seguro en tiempo de compilación**, evitando duplicación de lógica.

---

## ⚙️ Requisitos

- JDK 17 o superior  
- IntelliJ IDEA o cualquier editor compatible con Java  
- Conocimientos básicos de clases y métodos en Java  

---

## 🧠 Contexto del ejemplo

Imagina que gestionas **almacenes** para distintos tipos de productos: **electrónicos**, **ropa**, **alimentos**. Aunque el tipo de producto es diferente, **la lógica para almacenar, recuperar y consultar el stock es la misma**.

Si creas una clase específica para cada tipo, duplicarías código. Aquí es donde **los genéricos** entran en acción:  
Permiten definir **una sola clase que funcione para cualquier tipo de dato**, manteniendo la **seguridad de tipos**.

---

## 🧱 Paso 1: Crear la clase genérica `Almacen<T>`

```java
public class Almacen<T> {

    private T producto;

    // Guarda un producto de cualquier tipo
    public void guardarProducto(T producto) {
        this.producto = producto;
        System.out.println("📦 Producto guardado: " + producto);
    }

    // Devuelve el producto almacenado
    public T obtenerProducto() {
        return producto;
    }

    // Verifica si el almacén está vacío
    public boolean estaVacio() {
        return producto == null;
    }

    // Muestra el tipo de producto almacenado
    public void mostrarTipoProducto() {
        if (producto != null) {
            System.out.println("🔍 Tipo de producto almacenado: " + producto.getClass().getSimpleName());
        } else {
            System.out.println("🚫 El almacén está vacío.");
        }
    }
}
```

> 🔍 **`T`** es un **parámetro de tipo genérico** que se reemplaza por el tipo real (ej. `String`, `Integer`, `Producto`) cuando se usa la clase.

---

## 🚀 Paso 2: Uso de `Almacen<T>` con distintos tipos

```java
public class Main {
    public static void main(String[] args) {
        // 🧺 Almacén de ropa
        Almacen<String> almacenRopa = new Almacen<>();
        System.out.println("¿Almacén de ropa vacío? " + almacenRopa.estaVacio());
        almacenRopa.guardarProducto("Camisa");
        almacenRopa.mostrarTipoProducto();

        // 🔢 Almacén de números
        Almacen<Integer> almacenNumeros = new Almacen<>();
        almacenNumeros.guardarProducto(42);
        almacenNumeros.mostrarTipoProducto();

        // 🍏 Almacén de alimentos
        Almacen<String> almacenAlimentos = new Almacen<>();
        almacenAlimentos.guardarProducto("Manzana");
        almacenAlimentos.mostrarTipoProducto();

        // 🎯 Mostrar productos recuperados
        System.out.println("\n🎯 Productos recuperados:");
        System.out.println("🧺 Ropa: " + almacenRopa.obtenerProducto());
        System.out.println("🔢 Número: " + almacenNumeros.obtenerProducto());
        System.out.println("🍏 Alimento: " + almacenAlimentos.obtenerProducto());
    }
}
```

---

## 🧪 Resultado esperado

```
¿Almacén de ropa vacío? true
📦 Producto guardado: Camisa
🔍 Tipo de producto almacenado: String
📦 Producto guardado: 42
🔍 Tipo de producto almacenado: Integer
📦 Producto guardado: Manzana
🔍 Tipo de producto almacenado: String

🎯 Productos recuperados:
🧺 Ropa: Camisa
🔢 Número: 42
🍏 Alimento: Manzana
```

---

## 🔍 Conceptos clave utilizados

| Concepto              | Descripción |
|-----------------------|-------------|
| `T`                   | Parámetro de tipo genérico (puede ser cualquier identificador como `T`, `E`, `K`, `V`). |
| `Almacen<T>`          | Clase genérica que adapta su comportamiento al tipo especificado en tiempo de compilación. |
| `guardarProducto(T)`  | Método que recibe un parámetro del tipo genérico. |
| `obtenerProducto()`   | Devuelve el objeto almacenado del tipo genérico `T`. |
| `mostrarTipoProducto()` | Muestra el tipo real del producto almacenado usando **reflection** (`getClass().getSimpleName()`). |
| `estaVacio()`         | Método que verifica si el almacén está vacío (sin producto almacenado). |

---

## 📝 En resumen

- Los **genéricos** permiten crear **clases y métodos reutilizables** para diferentes tipos sin duplicar código.
- Son **seguros en tiempo de compilación**, evitando errores por tipo incorrecto.
- Se usan ampliamente en **estructuras de datos** como **List<T>**, **Map<K,V>**, **Set<T>** y en **APIs modernas**.

> 💡 **Tip:** En el siguiente ejemplo, aprenderemos a aplicar **restricciones** a los genéricos y a utilizar **wildcards** (`?`, `extends`, `super`) para mayor control.

---

📘 **Recursos adicionales:**

- 🔗 [Guía de genéricos en Java – Oracle](https://docs.oracle.com/javase/tutorial/java/generics/index.html)  
- 🔗 [Generics – GeeksForGeeks](https://www.geeksforgeeks.org/generics-in-java/)  

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Reto-01/Readme.md)➡️  