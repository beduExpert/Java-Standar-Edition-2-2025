🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 08**](../Readme.md) ➡️ / 📝 `Ejemplo 03: Organización de proyecto y control de versiones`

---

## 🎯 Objetivo

⚒️ Aplicar buenas prácticas de **organización del código en Java** usando **estructura por capas** y configurar un **repositorio Git** con una **documentación mínima**, facilitando el trabajo en equipo y la mantenibilidad del proyecto.

---

## ⚙️ Requisitos

- JDK 17 o superior  
- IDE compatible con Java (IntelliJ IDEA, Eclipse, VSCode)  
- Git instalado  
- GitHub (opcional para repositorio remoto)  

---

## 🧠 Contexto del ejemplo

En proyectos reales, mantener el código **ordenado y bien documentado** es esencial para:

- Evitar duplicidad y caos.
- Facilitar la colaboración entre desarrolladores.
- Asegurar que cualquier persona pueda entender y contribuir al proyecto.

Este ejemplo muestra cómo **organizar un proyecto Java por capas** (controladores, servicios y modelos), implementar un **control de versiones básico con Git**, y mantener una **documentación mínima pero efectiva**.

---

## 📂 Estructura del proyecto

```
Ejemplo-03/
├── controller/
│   └── ProductoController.java
├── service/
│   └── ProductoService.java
├── model/
│   └── Producto.java
├── Main.java
├── .gitignore
└── README.md
```

---

## 💻 Código completo

### 🧩 Modelo: Producto

```java
// model/Producto.java
package model;

public class Producto {
    private String nombre;
    private double precio;

    public Producto(String nombre, double precio) {
        this.nombre = nombre;
        this.precio = precio;
    }

    public String getNombre() { return nombre; }
    public double getPrecio() { return precio; }
}
```

---

### 🧩 Servicio: ProductoService

```java
// service/ProductoService.java
package service;

import com.bedu.organizacion.model.Producto;
import java.util.List;

public class ProductoService {

    public List<Producto> obtenerProductos() {
        return List.of(
            new Producto("Laptop", 1500.0),
            new Producto("Mouse", 25.0)
        );
    }
}
```

---

### 🧩 Controlador: ProductoController

```java
// controller/ProductoController.java
package controller;

import com.bedu.organizacion.model.Producto;
import com.bedu.organizacion.service.ProductoService;
import java.util.List;

public class ProductoController {

    private final ProductoService productoService = new ProductoService();

    public void listarProductos() {
        List<Producto> productos = productoService.obtenerProductos();
        productos.forEach(producto -> 
            System.out.println("📦 Producto: " + producto.getNombre() + " | Precio: $" + String.format("%,.2f", producto.getPrecio()))
        );
    }
}
```

---

### 🧩 Clase principal (Main.java)

```java
// Main.java
import controller.ProductoController;

public class Main {
    public static void main(String[] args) {
        ProductoController controller = new ProductoController();
        controller.listarProductos();
    }
}
```

---

## 📝 Documentación mínima (`README.md` del proyecto)

```markdown
# 🎯 Proyecto de Organización por Capas

Este proyecto implementa una **estructura por capas** en Java:

- `controller/` → Maneja la interacción principal (simula controladores HTTP).
- `service/` → Contiene la lógica de negocio.
- `model/` → Define las entidades o modelos de datos.

## 🚀 ¿Cómo ejecutar?

1. Asegúrate de tener **JDK 17** instalado.
2. Compila el proyecto:

```bash
javac model/*.java service/*.java controller/*.java Main.java
```

3. Ejecuta la clase principal:

```bash
java Main
```
```

---

## 🛠️ Configuración básica de Git

1. Inicializa un repositorio Git en el proyecto:

```bash
git init
```

2. Crea un archivo **`.gitignore`** para excluir archivos no deseados (ejemplo básico):

```
/target/
*.class
.idea/
*.iml
```

3. Realiza tu primer commit:

```bash
git add .
git commit -m "Inicializa proyecto con estructura por capas"
```

4. (Opcional) Conecta con un repositorio remoto en **GitHub**:

```bash
git remote add origin https://github.com/usuario/organizacion-proyecto.git
git push -u origin main
```

---

## 📝 Conceptos clave utilizados

- **Estructura por capas** (controlador, servicio, modelo).
- **Convenciones de paquetes** (`com.bedu.organizacion`).
- **Control de versiones con Git**.
- **Documentación mínima (`README.md`)**.

---

## 🚀 Resumen

Este ejemplo mostró cómo **organizar un proyecto Java** por capas y configurar un **repositorio Git básico**, asegurando un proyecto limpio, mantenible y colaborativo.

> **Tip final:** Mantén siempre una estructura coherente y un flujo de trabajo Git disciplinado para proyectos de cualquier tamaño.

---

⬅️ [**Anterior**](../Ejemplo-02/Readme.md) | [**Siguiente**](../Reto-02/Readme.md)➡️  