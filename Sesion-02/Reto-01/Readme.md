🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 02**](../Readme.md) ➡️ / ⚡ `Reto 01: Simulación concurrente de sistemas en una misión espacial`

## 🎯 Objetivo

⚒️ Simular el comportamiento paralelo de varios subsistemas críticos durante una misión espacial utilizando programación concurrente con `Runnable`, `Callable`, `ExecutorService` y `Future`.

---

## 🧠 Contexto del reto

Durante una misión aeroespacial, múltiples sistemas trabajan **simultáneamente** para garantizar el éxito y la seguridad de la operación. En este reto, representarás 4 subsistemas:

1. 🛰️ **Sistema de navegación** – Calcula trayectoria y correcciones orbitales.  
2. 🧪 **Sistema de soporte vital** – Monitorea presión, oxígeno y condiciones internas.  
3. 🔥 **Sistema de control térmico** – Supervisa temperaturas internas y externas.  
4. 📡 **Sistema de comunicaciones** – Establece contacto con la estación terrestre.  

Cada uno se ejecutará como una **tarea independiente en un hilo concurrente**.

---

## 📝 Instrucciones

### Parte 1️⃣: Crear clases que simulen subsistemas

- Crea una clase por cada sistema que implemente `Callable<String>`.
- Simula el procesamiento con `Thread.sleep()` y devuelve un mensaje representando el estado del sistema.

```java
public class SistemaNavegacion implements Callable<String> {
    public String call() throws Exception {
        Thread.sleep(1000);
        return "🛰️ Navegación: trayectoria corregida con éxito.";
    }
}
```

### Parte 2️⃣: Ejecutar tareas con `ExecutorService`

- Usa `Executors.newFixedThreadPool(4)`
- Envía las tareas con `submit()`
- Recupera los resultados con `Future.get()`

```java
ExecutorService executor = Executors.newFixedThreadPool(4);
Future<String> nav = executor.submit(new SistemaNavegacion());
// ...otros sistemas
System.out.println(nav.get());
```

### Parte 3️⃣: Mostrar los resultados al finalizar

Asegúrate de imprimir todos los resultados y cerrar el executor con `shutdown()`.

---

## 🧪 Resultado esperado

```
🚀 Simulación de misión espacial iniciada...
📡 Comunicaciones: enlace con estación terrestre establecido.
🧪 Soporte vital: presión y oxígeno dentro de parámetros normales.
🔥 Control térmico: temperatura estable (22°C).
🛰️ Navegación: trayectoria corregida con éxito.
✅ Todos los sistemas reportan estado operativo.
```

> 🧠 Recuerda que el orden de salida puede variar por los tiempos de procesamiento simulados.

---


## 📘 Recursos útiles

- 🔗 [ExecutorService – Oracle Docs](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ExecutorService.html)  
- 🔗 [Callable & Future en Java](https://www.geeksforgeeks.org/callable-future-java/)

---

🏆 Si logras simular correctamente los 4 sistemas trabajando de forma paralela y mostrar los resultados correctamente, ¡reto completado con éxito!

---

⬅️ [**Anterior**](../Ejemplo-02/Readme.md) | [**Siguiente**](../Ejemplo-03/Readme.md)➡️  