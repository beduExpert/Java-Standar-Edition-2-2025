🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 03**](../Readme.md) ➡️ / 📝 `Ejemplo 03: Composición funcional con flatMap y Function`

## 🎯 Objetivo

🔍 Comprender cómo **componer funciones** en Java, aplicando `flatMap` y encadenando transformaciones funcionales para procesar estructuras más complejas (como listas anidadas) de forma fluida y segura.

---

## ⚙️ Requisitos

- JDK 17 o superior  
- Editor compatible con Java (IntelliJ IDEA, VS Code, etc.)  
- Conocimientos previos de programación funcional básica (`Stream`, `Optional`, `map`, `filter`)

---

## 🧠 Contexto del ejemplo

En una **pizzería** con varias sucursales, cada sucursal tiene su propia lista de **pedidos**.  
El objetivo es:

- Acceder a **todas las listas de pedidos** (listas anidadas).  
- Filtrar los **pedidos para entrega a domicilio**.  
- Recuperar los **teléfonos disponibles** (sin `null`) para confirmar los pedidos.  
- Transformar los teléfonos en **mensajes personalizados**.

Usaremos `flatMap` para **desanidar listas** y procesar todos los pedidos de todas las sucursales como un solo flujo.

---

## 🧱 Paso 1: Crear las clases `Pedido` y `Sucursal`

### 📄 `Pedido.java`

```java
public class Pedido {
    private final String cliente;
    private final String tipoEntrega; // "domicilio" o "local"
    private final String telefono; // Puede ser null

    public Pedido(String cliente, String tipoEntrega, String telefono) {
        this.cliente = cliente;
        this.tipoEntrega = tipoEntrega;
        this.telefono = telefono;
    }

    public String getCliente(){ return cliente; }
    public String getTipoEntrega() { return tipoEntrega; }
    public Optional<String> getTelefono() { return Optional.ofNullable(telefono); }
}
```

### 📄 `Sucursal.java`

```java
import java.util.List;

public class Sucursal {
    private final String nombre;
    private final List<Pedido> pedidos;

    public Sucursal(String nombre, List<Pedido> pedidos) {
        this.nombre = nombre;
        this.pedidos = pedidos;
    }

    public List<Pedido> getPedidos() { return pedidos; }
    public String getNombre() { return nombre; }
}
```

---

## 🧱 Paso 2: Procesar todas las sucursales con `flatMap` y `Function`

```java
package com.bedu.pizzeria;

import java.util.*;
import java.util.stream.*;

public class ConfirmacionPedidosGlobal {

    public static void main(String[] args) {
        // 📦 Lista de sucursales con sus pedidos
        List<Sucursal> sucursales = List.of(
            new Sucursal("Centro", List.of(
                new Pedido("Juan", "domicilio", "555-1234"),
                new Pedido("María", "local", null)
            )),
            new Sucursal("Norte", List.of(
                new Pedido("Carlos", "domicilio", null),
                new Pedido("Luisa", "domicilio", "555-5678")
            )),
            new Sucursal("Sur", List.of(
                new Pedido("Esteban", "domicilio", "555-9012"),
                new Pedido("Diana", "domicilio", null)
            )),
            new Sucursal("Este", List.of(
                new Pedido("Andrés", "local", null),
                new Pedido("Sofía", "domicilio", "555-3456")
            ))
        );

        System.out.println("📋 Confirmaciones de pedidos globales:");

        // 🏁 Procesamos todos los pedidos de todas las sucursales
        sucursales.stream()
            .flatMap(sucursal -> 
                sucursal.getPedidos().stream()
                    .filter(p -> p.getTipoEntrega().equalsIgnoreCase("domicilio")) // 🔍 Filtrar entregas a domicilio
                    .map(pedido -> new Confirmacion(pedido, sucursal.getNombre())) // 📝 Combinar pedido + sucursal
            )
            .filter(conf -> conf.getPedido().getTelefono().isPresent()) // 🔍 Filtrar Optional con valor
            .map(conf -> {
                String telefono = conf.getPedido().getTelefono().get();
                return "📞 Pedido de " + conf.getPedido().getCliente() + 
                       " en la sucursal " + conf.getSucursal() + 
                       " confirmado al número: " + telefono;
            })
            .forEach(System.out::println); // 📤 Imprimir mensajes
    }

    // Clase auxiliar para transportar Pedido + Sucursal juntos
    static class Confirmacion {
        private final Pedido pedido;
        private final String sucursal;

        public Confirmacion(Pedido pedido, String sucursal) {
            this.pedido = pedido;
            this.sucursal = sucursal;
        }

        public Pedido getPedido() { return pedido; }
        public String getSucursal() { return sucursal; }
    }
}

```

---

## 🧪 Resultado esperado

```
📋 Confirmaciones de pedidos globales:
📞 Pedido de Juan en la sucursal Centro confirmado al número: 555-1234
📞 Pedido de Luisa en la sucursal Norte confirmado al número: 555-5678
📞 Pedido de Esteban en la sucursal Sur confirmado al número: 555-9012
📞 Pedido de Sofía en la sucursal Este confirmado al número: 555-3456
```

---

## 🔍 Elementos funcionales utilizados

| Elemento         | Descripción |
|------------------|-------------|
| `flatMap()`      | **Desanida listas** (lista de listas → flujo plano) |
| `Optional`       | Maneja valores nulos de forma segura |
| `map()`          | Transforma elementos (ej. Pedido → Optional → String) |
| `filter()`       | Filtra elementos según una condición |
| `collect()`      | Recolecta los elementos del stream en una colección (ej. `List`) |

---

## 📝 En resumen

- Usamos **`flatMap()`** para **desanidar estructuras** complejas (listas dentro de listas), procesando todos los pedidos de varias sucursales como un **flujo continuo**.
- Combinamos **`filter()`**, **`map()`** y **`Optional`** para **filtrar entregas a domicilio**, **eliminar pedidos sin teléfono** y **crear mensajes personalizados**.
- Esta composición funcional permite **trabajar con colecciones anidadas de forma limpia y fluida**, evitando ciclos anidados y estructuras imperativas.
- **`flatMap()`** es especialmente útil en contextos como **pedidos globales**, **consultas a múltiples fuentes de datos** o **procesos con estructuras jerárquicas**.


---

### 💡 ¿Sabías que...?

- `flatMap` es esencial para **trabajar con listas anidadas** o estructuras complejas, permitiendo procesarlas como un solo flujo continuo.
- Puedes **componer funciones** encadenando `map`, `filter`, `flatMap`, generando pipelines declarativos y expresivos.

---

📘 Recursos adicionales:

- 🔗 [flatMap en Java – Baeldung](https://www.baeldung.com/java-flat-map)  
- 🔗 [Stream API – Oracle Docs](https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html)

---

⬅️ [**Anterior**](../Reto-01/Readme.md) | [**Siguiente**](../Reto-02/Readme.md)➡️  