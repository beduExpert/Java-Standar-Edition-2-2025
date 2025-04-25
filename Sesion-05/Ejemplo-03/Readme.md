🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 05**](../Readme.md) ➡️ / 📝 `Ejemplo 03: Manejo avanzado de flujos y backpressure`

## 🎯 Objetivo

🔍 Comprender cómo manejar **backpressure** (control de velocidad de emisión de datos) y cómo **encadenar operaciones reactivas** usando **Flux** y **Project Reactor**, explorando diferentes **escenarios del mundo real**.

---

## ⚙️ Requisitos

- JDK 17 o superior  
- IntelliJ IDEA o cualquier editor compatible con Java  
- Dependencias de **Project Reactor** (`reactor-core`)  
- Conocimientos previos de `Flux`, `map`, `flatMap`, `filter`

---

## 🧠 Contexto del ejemplo

En esta sesión verás **tres escenarios distintos** donde **backpressure** y **Flux** son útiles:

1️⃣ **Sistema de pedidos en línea** (prioritarios vs normales).  
2️⃣ **Alertas de sensores** (sólo altas temperaturas deben procesarse lentamente).  
3️⃣ **Mensajes en redes sociales** (alta demanda, procesar solo mensajes importantes).

Estos ejemplos muestran cómo:

- **Controlar la velocidad** del flujo (backpressure).  
- **Filtrar**, **transformar** y **procesar flujos reactivos** de forma flexible.

---

## 📦 Configuración de dependencias (Maven)

Agrega esta dependencia en tu archivo `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>io.projectreactor</groupId>
        <artifactId>reactor-core</artifactId>
        <version>3.6.11</version>
    </dependency>
</dependencies>
```

---

## 📄 Código base: `ManejoAvanzadoReactor.java`

```java
import reactor.core.publisher.Flux;
import java.time.Duration;

public class ManejoAvanzadoReactor {

    public static void main(String[] args) throws InterruptedException {

        // Ejemplo 1️⃣: Sistema de pedidos con backpressure
        Flux.interval(Duration.ofMillis(500))
                .onBackpressureBuffer() // 👈 Añadido para evitar overflow
                .map(i -> new Pedido(i + 1, i % 3 == 0 ? "Prioritario" : "Normal"))
                .take(9)
                .filter(p -> p.getTipo().equals("Prioritario"))
                .doOnNext(p -> System.out.println("📥 Pedido recibido: " + p))
                .delayElements(Duration.ofSeconds(1))
                .subscribe(p -> System.out.println("✅ Pedido procesado: " + p));

        // Ejemplo 2️⃣: Alertas de sensores
        Flux.interval(Duration.ofMillis(400))
                .onBackpressureBuffer() // 👈 Añadido para evitar overflow
                .map(i -> (int) (Math.random() * 50))
                .take(7)
                .filter(temp -> temp > 30)
                .delayElements(Duration.ofMillis(800))
                .subscribe(temp -> System.out.println("⚠️ Alerta: Temperatura alta - " + temp + "°C"));

        // Ejemplo 3️⃣: Mensajes en redes sociales
        Flux.interval(Duration.ofMillis(300))
                .onBackpressureBuffer() // 👈 Añadido para evitar overflow
                .map(i -> "Mensaje #" + (i + 1))
                .take(5)
                .doOnNext(m -> System.out.println("💬 Mensaje recibido: " + m))
                .delayElements(Duration.ofMillis(1000))
                .subscribe(m -> System.out.println("📢 Procesado: " + m));

        Thread.sleep(10000); // Esperar todos los flujos
    }

    // Clase auxiliar Pedido
    static class Pedido {
        private final long id;
        private final String tipo;

        public Pedido(long id, String tipo) {
            this.id = id;
            this.tipo = tipo;
        }

        public String getTipo() { return tipo; }

        @Override
        public String toString() {
            return "Pedido#" + id + " [" + tipo + "]";
        }
    }
}
```

---

## 🧪 Resultado esperado (fragmento)

```
📥 Pedido recibido: Pedido#3 [Prioritario]
✅ Pedido procesado: Pedido#3 [Prioritario]
⚠️ Alerta: Temperatura alta - 42°C
💬 Mensaje recibido: Mensaje #1
📢 Procesado: Mensaje #1
📥 Pedido recibido: Pedido#6 [Prioritario]
✅ Pedido procesado: Pedido#6 [Prioritario]
⚠️ Alerta: Temperatura alta - 39°C
💬 Mensaje recibido: Mensaje #2
📢 Procesado: Mensaje #2
...
```

> ⚠️ El **orden puede variar** debido a la **naturaleza asíncrona** de cada **Flux**.

---

## 🔍 Conceptos clave utilizados

| Concepto             | Descripción |
|----------------------|-------------|
| `Flux.interval()`    | Genera un flujo de datos a intervalos regulares (pedidos, temperaturas, mensajes). |
| `onBackpressureBuffer()` | Controla el **backpressure** almacenando temporalmente los elementos si el consumidor procesa más lento que el productor. |
| `filter()`           | Filtra elementos relevantes (ej. solo prioritarios o temperaturas altas). |
| `map()`              | Transforma elementos del flujo (ej. índice → objeto o temperatura). |
| `flatMap()`          | (No usado aquí, pero útil para expandir un flujo en múltiples subflujos). |
| `doOnNext()`         | Ejecuta acciones secundarias (logs, monitoreo) sin modificar el flujo. |
| `delayElements()`    | Introduce latencia entre cada elemento emitido, controlando la velocidad (**simula backpressure**). |
| `subscribe()`        | Activa el flujo reactivo (sin suscripción no sucede nada). |

---

## 📝 En resumen

- **Backpressure** es una técnica fundamental para **evitar que el consumidor se vea saturado** cuando el productor emite datos más rápido de lo que pueden procesarse.  
  - Herramientas como **`onBackpressureBuffer()`** permiten **almacenar temporalmente los elementos excedentes** para mantener un flujo estable.
  
- **Combinar varios Flux** permite modelar sistemas **concurrentes y reactivos**, adaptados a diferentes ritmos de producción y consumo (pedidos, sensores, mensajes en tiempo real).

- Los operadores **`filter`**, **`map`**, **`delayElements`**, **`doOnNext`** y **`onBackpressureBuffer()`** son esenciales para construir **flujos robustos, adaptables y seguros** en entornos de alta demanda.

- **El control del ritmo del flujo** garantiza que el sistema **no colapse ante cargas variables**, ofreciendo **resiliencia y flexibilidad**.


> 💡 **Tip:** En casos más complejos, puedes combinar **Flux.merge()** o **Flux.concat()** para fusionar varios flujos.

---

📘 **Recursos adicionales**:

- 🔗 [Backpressure en Reactor – Project Reactor Docs](https://projectreactor.io/docs/core/release/reference/#backpressure)  
- 🔗 [Programación reactiva avanzada en Java – DZone](https://dzone.com/articles/reactive-programming-with-java-9-flow-api)  
- 🔗 [Project Reactor – Official Documentation](https://projectreactor.io/docs/core/release/reference/)

---

⬅️ [**Anterior**](../Reto-01/Readme.md) | [**Siguiente**](../Reto-02/Readme.md)➡️