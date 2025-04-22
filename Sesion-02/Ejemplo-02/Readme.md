🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 02**](../Readme.md) ➡️ / 📝 `Ejemplo 02: ExecutorService y tareas concurrentes`

## 🎯 Objetivo

⚒️ Simular un sistema de procesamiento de pedidos en una tienda en línea, donde múltiples pedidos se procesan en paralelo utilizando `ExecutorService`, `Callable` y `Future`.

---

## ⚙️ Requisitos

- JDK 17 o superior  
- IntelliJ IDEA o cualquier editor con soporte para Java  
- Conocimientos básicos de hilos y concurrencia  

---

## 🧱 Contexto del ejemplo

Imagina una tienda en línea que recibe múltiples pedidos simultáneamente. En lugar de procesar uno por uno, podemos usar **hilos concurrentes** para manejar cada pedido en paralelo, reduciendo el tiempo total de atención.

Este ejemplo simula 3 pedidos que se procesan de manera concurrente con tiempos de espera variables.

---

## 📄 Código base: `ProcesadorDePedidos.java`

```java
import java.util.concurrent.*;

public class ProcesadorDePedidos {

    public static void main(String[] args) throws InterruptedException, ExecutionException {
        ExecutorService executor = Executors.newFixedThreadPool(3);

        Callable<String> pedido1 = () -> {
            Thread.sleep(1200); // Simula procesamiento
            return "📦 Pedido #1 entregado en 1.2 segundos";
        };

        Callable<String> pedido2 = () -> {
            Thread.sleep(800);
            return "📦 Pedido #2 entregado en 0.8 segundos";
        };

        Callable<String> pedido3 = () -> {
            Thread.sleep(1500);
            return "📦 Pedido #3 entregado en 1.5 segundos";
        };

        System.out.println("🛒 Procesando pedidos...");
        Future<String> r1 = executor.submit(pedido1);
        Future<String> r2 = executor.submit(pedido2);
        Future<String> r3 = executor.submit(pedido3);

        System.out.println(r1.get());
        System.out.println(r2.get());
        System.out.println(r3.get());

        executor.shutdown();
        System.out.println("✅ Todos los pedidos fueron procesados.");
    }
}
```

---

## 🧪 Resultado esperado

```
🛒 Procesando pedidos...
📦 Pedido #1 entregado en 1.2 segundos
📦 Pedido #2 entregado en 0.8 segundos
📦 Pedido #3 entregado en 1.5 segundos
✅ Todos los pedidos fueron procesados.
```

> ⚠️ El orden puede variar dependiendo de los tiempos de ejecución de cada tarea.

---

## 🔍 Conceptos clave utilizados

| Concepto           | Descripción |
|--------------------|-------------|
| `ExecutorService`  | Gestiona un conjunto de hilos reutilizables |
| `Callable`         | Tarea que puede devolver un resultado y lanzar excepciones |
| `Future`           | Objeto que representa el resultado futuro de una tarea |
| `submit()`         | Envía la tarea al pool de hilos |
| `get()`            | Espera y obtiene el resultado de una tarea |
| `shutdown()`       | Detiene el pool de hilos tras finalizar las tareas |

---

## 💡 ¿Sabías que...?

- Usar `ExecutorService` es más eficiente que crear hilos manualmente, especialmente en aplicaciones con muchas tareas pequeñas.
- Puedes cambiar `newFixedThreadPool(3)` por `newCachedThreadPool()` para una gestión dinámica del número de hilos.
- `Callable` y `Future` te permiten recibir datos de las tareas, a diferencia de `Runnable`.

---

📘 Recursos útiles:  
🔗 [Java Executors – Oracle Docs](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ExecutorService.html)  
🔗 [Concurrencia moderna en Java – Baeldung](https://www.baeldung.com/java-executor-service-tutorial)  

---

⬅️ [**Anterior**](../Ejemplo-01/Readme.md) | [**Siguiente**](../Reto-01/Readme.md)➡️  