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
├── controller/     📂 Controladores (gestión de interacción)
│   └── ProductoController.java
├── service/        🔧 Servicios (lógica de negocio)
│   └── ProductoService.java
├── model/          📦 Modelos (entidades de datos)
│   └── Producto.java
├── Main.java       ▶️ Punto de entrada del programa
├── .gitignore      🚫 Configuración para excluir archivos no deseados
└── Readme.md       📝 Documentación mínima del proyecto
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

import model.Producto;
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

import model.Producto;
import service.ProductoService;
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

## 🛠️ Instrucciones para compilar y ejecutar

1. **Compilar el proyecto:**

```bash
javac model/*.java service/*.java controller/*.java Main.java
```

2. **Ejecutar la clase principal:**

```bash
java Main
```

### 📝 Salida esperada:

```
📦 Producto: Laptop | Precio: $1,500.00
📦 Producto: Mouse  | Precio: $25.00
```

---

## 📝 Documentación mínima recomendada

Incluye estos elementos en el **README.md** del proyecto:

- 🎯 **Nombre del proyecto:** Proyecto de Organización por Capas.
- 📝 **Descripción:** Implementa una estructura por capas en Java para facilitar la organización del código.
- 🛠️ **Instrucciones para compilar y ejecutar** (como las mostradas anteriormente).
- 🗂️ **Estructura del proyecto** (como se mostró al inicio).

---

## 🚫 `.gitignore` básico sugerido

```
*.class          🚫 Archivos compilados
/target/         🚫 Carpeta de compilación (si existiera)
/.idea/          🚫 Configuración de IntelliJ IDEA
*.iml            🚫 Archivos de proyecto de IntelliJ
```

---

## 🛠️ Configuración básica de Git

### 🔃 Inicializa el repositorio local:

```bash
git init
```

### 💾 Realiza tu primer commit:

```bash
git add .
git commit -m "🚀 Inicializa proyecto con estructura por capas"
```

### 🌐 Conecta tu repositorio a **GitHub** (opcional):

```bash
git remote add origin https://github.com/usuario/organizacion-proyecto.git
git push -u origin main
```

### 🔥 Tip final:

- Usa **commits pequeños y descriptivos**:
  
  - ❌ `Cambios varios`  
  - ✅ `🎨 Refactoriza ProductoService para mejorar legibilidad`

- Sincroniza frecuentemente con el repositorio remoto (`git pull`, `git push`). 🔄

---

## 📝 Conceptos clave utilizados

- **Estructura por capas** (controlador, servicio, modelo).
- **Control de versiones con Git**.
- **Documentación mínima del proyecto**.

---

## 🚀 Resumen

Este ejemplo mostró cómo **organizar un proyecto Java** por capas y configurar un **repositorio Git básico**, asegurando un proyecto limpio, mantenible y colaborativo.

> **Tip final:** Mantén siempre una estructura coherente y un flujo de trabajo Git disciplinado para proyectos de cualquier tamaño.

---

⬅️ [**Anterior**](../Reto-02/Readme.md) | [**Siguiente**](../../Readme.md)➡️  