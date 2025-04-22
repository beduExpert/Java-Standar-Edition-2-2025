🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 04**](../Readme.md) ➡️ / 📝 `Ejemplo 01: Diferencias entre concurrencia y asincronía`

## 🎯 Objetivo

🔍 Entender las diferencias entre **concurrencia** y **asincronía** en Java mediante un ejemplo práctico, visualizando cómo se comportan los hilos en cada caso y cuáles son los beneficios de cada enfoque.

---

## ⚙️ Requisitos

- JDK 17 o superior  
- Editor compatible con Java (IntelliJ IDEA, VS Code, etc.)  
- Conocimientos previos de hilos (`Thread`, `ExecutorService`)  

---

## 🧠 Contexto del ejemplo

Imagina un **restaurante** donde se reciben **órdenes de comida**.  
Queremos comparar dos enfoques para procesar esas órdenes:

- **Concurrencia**: múltiples **hilos** procesan las órdenes al mismo tiempo (bloqueante).  
- **Asincronía**: las órdenes se procesan de forma **no bloqueante**, liberando recursos mientras esperan, usando `CompletableFuture`.

Este ejemplo mostrará cómo **ambos enfoques se comportan de manera distinta** frente a **latencia** (ej. tiempos de cocción).

---

## 🧱 Código de ejemplo

```java
import java.util.concurrent.*;

public class ProcesadorOrdenes {

    public static void main(String[] args) throws InterruptedException {
        System.out.println("🍽️ Ejecución concurrente con ExecutorService:");
        ExecutorService executor = Executors.newFixedThreadPool(3); // Concurrencia: 3 hilos

        // 🔹 Concurrencia: más órdenes
        executor.submit(() -> procesarOrden("Orden 1 (Pizza)", 3));
        executor.submit(() -> procesarOrden("Orden 2 (Pasta)", 2));
        executor.submit(() -> procesarOrden("Orden 3 (Hamburguesa)", 4));
        executor.submit(() -> procesarOrden("Orden 4 (Ensalada)", 1));

        executor.shutdown();
        executor.awaitTermination(10, TimeUnit.SECONDS); // Espera que terminen las órdenes concurrentes

        System.out.println("\n⚡ Ejecución asincrónica con CompletableFuture:");

        // 🔹 Asincronía: más órdenes
        CompletableFuture<Void> ordenAsync1 = CompletableFuture.runAsync(() -> procesarOrden("Orden 5 (Sopa)", 2));
        CompletableFuture<Void> ordenAsync2 = CompletableFuture.runAsync(() -> procesarOrden("Orden 6 (Tacos)", 3));
        CompletableFuture<Void> ordenAsync3 = CompletableFuture.runAsync(() -> procesarOrden("Orden 7 (Sandwich)", 2));

        CompletableFuture.allOf(ordenAsync1, ordenAsync2, ordenAsync3).join(); // Espera que todas las órdenes asincrónicas terminen
    }

    // Simula procesamiento de una orden con tiempo de espera (latencia)
    public static void procesarOrden(String orden, int segundos) {
        System.out.println("⏳ Procesando " + orden);
        try {
            TimeUnit.SECONDS.sleep(segundos);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
        System.out.println("✅ " + orden + " completada");
    }
}
```

---

## 🧪 Resultado esperado

```
🍽️ Ejecución concurrente con ExecutorService:
⏳ Procesando Orden 1 (Pizza)
⏳ Procesando Orden 2 (Pasta)
⏳ Procesando Orden 3 (Hamburguesa)
✅ Orden 2 (Pasta) completada
⏳ Procesando Orden 4 (Ensalada)
✅ Orden 1 (Pizza) completada
✅ Orden 4 (Ensalada) completada
✅ Orden 3 (Hamburguesa) completada

⚡ Ejecución asincrónica con CompletableFuture:
⏳ Procesando Orden 5 (Sopa)
⏳ Procesando Orden 6 (Tacos)
⏳ Procesando Orden 7 (Sandwich)
✅ Orden 5 (Sopa) completada
✅ Orden 7 (Sandwich) completada
✅ Orden 6 (Tacos) completada
```
> ⚠️ El orden de finalización de las órdenes puede variar en cada ejecución debido a la naturaleza concurrente y asincrónica de los hilos.

> 💡 Ambos enfoques procesan en paralelo, pero **CompletableFuture** permite mayor **flexibilidad para componer tareas** y liberar hilos mientras esperan resultados.

---

## 🔍 Conceptos clave utilizados

| Concepto            | Descripción |
|---------------------|-------------|
| **Concurrencia**    | Ejecución simultánea de tareas usando **hilos** (pueden ser bloqueantes). |
| **Asincronía**      | Ejecución **no bloqueante**, liberando recursos mientras se espera el resultado (con `CompletableFuture`). |
| **ExecutorService** | Manejador de hilos que permite controlar la concurrencia. |
| **CompletableFuture** | Herramienta para manejar asincronía, permitiendo componer, encadenar y manejar tareas no bloqueantes. |

---

## 📝 En resumen

- **Concurrencia** y **asincronía** son técnicas complementarias, pero **resuelven problemas distintos**:
  - **Concurrencia** te permite ejecutar **varias tareas al mismo tiempo** usando múltiples hilos, pero puede implicar **bloqueos** (si las tareas esperan resultados).
  - **Asincronía** permite que las tareas **no bloqueen** el hilo mientras esperan (ej. tiempos de cocción, operaciones I/O), usando herramientas como **`CompletableFuture`**.

- **¿Y cual elegir?**
  - Usa **concurrencia** cuando necesitas **multiprocesamiento** (ej. cálculos intensivos en varios núcleos).
  - Usa **asincronía** cuando quieres **liberar recursos mientras esperas** (ej. llamadas a servicios externos, operaciones de red o I/O).

> 🔍 **Clave:**  
> **`ExecutorService`** controla **cuántos hilos se usan** (concurrencia).  
> **`CompletableFuture`** permite **componer tareas** sin bloquear hilos (asincronía).

---

📘 Recursos adicionales:

- 🔗 [Concurrencia vs asincronía – Baeldung](https://www.baeldung.com/java-asynchronous-synchronous)
- 🔗 [CompletableFuture – Java Docs](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletableFuture.html)

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Ejemplo-02/Readme.md)➡️  