🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 `Prework sesión 02`

<div align="center">
    <img src="../Imagenes/S02.jpg" alt="Bedu | Haz + con tu talento | JAVA STANDARD EDITION II">
</div>

##### **PREWORK**
#### **🟧 Sesión 10**
#### **Multihilos y procesos concurrentes**


##### 🔶 **Introducción**

¿Alguna vez has usado una app que puede hacer varias cosas al mismo tiempo sin "trabarse"? Por ejemplo, reproducir música mientras descarga canciones o responde a tus clics.

Eso se logra gracias a la **concurrencia** y el uso de **multihilos**, una habilidad muy necesaria que aprenderás en esta sesión.

Con Java puedes ejecutar múltiples tareas al mismo tiempo, y aunque suena complejo, aquí lo vas a entender paso a paso, desde lo más básico hasta aplicar técnicas modernas como `ExecutorService`, `Callable`, `Future` y mecanismos de sincronización.

Prepárate para mejorar la fluidez, la velocidad y la eficiencia de tus programas. 🚀

---

#### 🎯 Objetivo

- Comprender qué es la concurrencia y cómo funcionan los procesos e hilos en Java.
- Crear hilos de manera controlada usando `Thread`, `Runnable`, `ExecutorService` y `Callable`.
- Utilizar estructuras como `Future` para obtener resultados de tareas concurrentes.
- Identificar y manejar condiciones de carrera mediante sincronización.
- Aplicar mecanismos de comunicación y bloqueo entre hilos (`wait()`, `notify()`, `Locks`).

---

#### 📋 Instrucciones

Este Prework está diseñado para conocer el contenido que se practicará durante la sesión en vivo. **Por favor no lo omitas.**

Toma notas de lo que consideres relevante y guarda tus preguntas o dudas para resolverlas en la sesión.

Antes de arrancar, verifica que tu entorno de desarrollo esté listo. Es fundamental que tengas instalado IntelliJ IDEA Community Edition y el JDK (Java Development Kit) para trabajar sin interrupciones.

Si te surge alguna dificultad con la instalación o cualquier duda, no dudes en pedir ayuda a tu experto/a. ¡Estamos aquí para asegurarnos de que todo fluya sin problemas! 🚀

---

**Bienvenido/a**

Bienvenid@ al segundo Prework del módulo. A continuación, te presentamos el tiempo estimado de lectura por tema, para que puedas revisar todos los recursos al máximo: 

| **📖 Temario**                                | **🕰️ Tiempo sugerido** |
|-----------------------------------------------|------------------------|
| Tema 01. Introducción a la concurrencia       | 10 min                 |
| Tema 02. Creación de hilos en Java            | 10 min                 |
| Tema 03. Sincronización de hilos              | 10 min                 |


**¡Comencemos! 🏁**

---
 
#### 📚 Tema 01. Introducción a la concurrencia
##### ⏳ 10 minutos de lectura

Concurrencia significa que varias tareas se ejecutan al mismo tiempo, o al menos *parecen* hacerlo. En Java, esto se logra con **procesos e hilos**.

Aprenderás cómo funciona el ciclo de vida de un hilo, qué ventajas tiene y cuándo puede volverse un problema si no lo controlas bien.

**🧠 Conceptos básicos**

| Término        | Definición rápida                                                       |
|----------------|-------------------------------------------------------------------------|
| Proceso        | Programa en ejecución, con su propio espacio de memoria.                |
| Hilo (Thread)  | Subunidad de un proceso; permite ejecutar tareas simultáneamente.       |
| Concurrencia   | Capacidad para manejar múltiples tareas a la vez o de forma intercalada.|

**🔄 Ciclo de vida de un hilo**

```plaintext
[New] → [Runnable] → [Running] → [Blocked] → [Dead]
```
**📘 Métodos clave en el ciclo de vida de un hilo**

Cuando trabajas con hilos, estos son los métodos más importantes que vas a usar y ver constantemente. Te explico cada uno con detalle:

**🔹 `start()`**
Este método **inicia oficialmente el hilo**.
Al llamarlo, el hilo pasa del estado New a Runnable, y el sistema lo programa para ejecutarse.

```java
MiHilo hilo = new MiHilo();
hilo.start(); // Aquí comienza la ejecución real
```
**⚠️ ¡Ojo!** Si llamas directamente a `run()` en lugar de `start()`, el código se ejecutará en el mismo hilo principal (¡no será concurrente!)

**🔹 `run()`**
Este método contiene el **código que quieres que el hilo ejecute**.
Es como el "corazón" de la tarea. Cuando se ejecuta el hilo, automáticamente se llama este método.

```java
public class MiHilo extends Thread {
    public void run() {
        System.out.println("Estoy corriendo en un hilo");
    }
}
```

**🧠 Tip**: Nunca llames a `run()` directamente si quieres ejecutar en paralelo. Usa `start()`.

**🔹 `sleep(milliseconds)`**
Este método **pausa temporalmente** la ejecución del hilo actual durante los milisegundos que especifiques.
Es útil si necesitas simular una espera, controlar la frecuencia de ejecución o reducir carga.

```java
try {
    Thread.sleep(2000); // pausa por 2 segundos
} catch (InterruptedException e) {
    e.printStackTrace();
}
```

**💡 Uso común:** Esperar entre ciclos en juegos, animaciones o procesos repetitivos.

**🔹 `join()`**

Este método hace que **un hilo espere a que otro termine antes de continuar**.
Es ideal cuando un hilo depende del resultado de otro para seguir.

```java

Thread hiloA = new MiHilo();
hiloA.start();
hiloA.join(); // Espera hasta que hiloA termine

System.out.println("Ahora sí, hiloA ha terminado");
```

**🎯 Tip realista**: Si lanzas varios hilos pero necesitas que todos terminen antes de pasar a la siguiente etapa (como imprimir un reporte), `join()` es la clave.

**Ventajas vs desventajas**

| Ventajas                    | Riesgos potenciales            |
|-----------------------------|--------------------------------|
| Mejora el rendimiento       | Condiciones de carrera         |
| Mejor respuesta del sistema | Problemas de sincronización    |
| Uso más eficiente del CPU   | Deadlocks (bloqueos circulares)|


**🔎 Resumen**

¡Bien! Ya diste el primer paso hacia el mundo de la programación paralela.
Ahora sabes qué son los hilos, cómo viven (y mueren) dentro de una app y por qué usarlos puede hacer tu sistema mucho más fluido. Verás que entender el ciclo de vida de un hilo te será útil cuando empieces a depurar procesos que “se quedan pensando”.

💡 **Tip**: Si tu aplicación se congela sin razón, revisa si un hilo está bloqueado o nunca termina su ciclo.


---

#### 📚 Tema 02. Creación de hilos en Java
##### ⏳ 10 minutos de lectura

Java ofrece muchas formas de crear hilos, desde lo más básico (`Thread`) hasta formas más organizadas como `ExecutorService`. 

**Métodos para crear hilos**

**A) Usando la clase `Thread`**
`Thread` es una clase de Java que representa un hilo de ejecución. Puedes extenderla (heredarla) para crear tu propia lógica dentro del método run().

```java
class MiHilo extends Thread {
    public void run() {
        System.out.println("Hilo corriendo...");
    }
}
```
**✅ Ventaja**: Sencillo para ejemplos pequeños
**⚠️ Desventaja**: Si ya estás heredando de otra clase, no puedes heredar también de Thread (Java no permite herencia múltiple)

**B) Usando `Runnable`**
`Runnable` es una interfaz funcional, lo que significa que puedes usarla para definir tu lógica con una expresión lambda. Luego, puedes pasarla como argumento a un objeto `Thread`.

```java
Runnable tarea = () -> System.out.println("Desde Runnable");
new Thread(tarea).start();
```
**✅ Ventaja**:
- Más flexible: puedes implementar múltiples interfaces
- Compatible con programación funcional (lambdas)
- Ideal cuando usas `ExecutorService` más adelante

**💬 ¿Cuál debería usar?**

Usa `Thread` solo si estás aprendiendo o el caso es muy simple.
**Para proyectos reales, siempre se recomienda usar `Runnable`**, porque es más flexible, limpio y escalable. Además, se integra fácilmente con otras herramientas modernas como `ExecutorService`.

**⚙️ `ExecutorService` y `Callable`**

- `ExecutorService`: permite manejar un "pool" de hilos sin crearlos manualmente.

- `Callable`: similar a `Runnable` pero permite devolver resultados.

- `Future`: permite capturar el resultado de una tarea en el futuro.

```java
ExecutorService executor = Executors.newFixedThreadPool(2);
Callable<Integer> tarea = () -> 42;
Future<Integer> resultado = executor.submit(tarea);
System.out.println(resultado.get()); // Devuelve 42
```

✅ **Ventaja**: No te preocupas por iniciar o detener hilos manualmente.


**🔎 Resumen**

Ya dominaste lo esencial para crear y controlar hilos, tanto a la antigua como a la moderna.

`Thread` y `Runnable` son geniales para comenzar, pero cuando tu app crece, herramientas como `ExecutorService` y `Callable` te salvan la vida.
Poder lanzar tareas y recoger sus resultados sin romper tu código es una de las claves para construir sistemas escalables.

**💡 Tip**: Usa `Executors.newFixedThreadPool()` cuando sepas cuántas tareas quieres controlar al mismo tiempo.

---

#### 📚 Tema 03. Sincronización de hilos
##### ⏳ 10 minutos de lectura

Cuando dos hilos acceden a los mismos datos al mismo tiempo, pueden ocurrir **errores aleatorios**. A eso se le llama **condición de carrera**. Para evitarlo, necesitas sincronización.

**🔐 ¿Qué hace exactamente `synchronized`?**
Cuando usas varios hilos que acceden o modifican los mismos datos al mismo tiempo, puedes tener resultados inesperados. Esto se conoce como una condición de carrera (race condition).

El modificador `synchronized` garantiza que solo un hilo a la vez pueda acceder a un bloque de código o método, evitando que los datos compartidos se corrompan.

**🧪 Ejemplo simple sin sincronización (puede fallar)**

```java
public class Contador {
    private int valor = 0;

    public void incrementar() {
        valor++;
    }
}
```
Si dos hilos llaman a `incrementar()` al mismo tiempo, podrían leer el mismo valor y sumarlo dos veces incorrectamente.

**✅ Ejemplo con `synchronized` (protegido)**
```java
public class Contador {
    private int valor = 0;

    public synchronized void incrementar() {
        valor++;
    }
}
```
**🔒 ¿Qué cambió?**
Solo un **hilo a la vez** puede entrar a `incrementar()`. Si otro hilo quiere ejecutarlo, **espera** a que el primero termine.

**📦 También puedes sincronizar bloques (más control)**
Si solo una parte del método necesita protección, puedes sincronizar solo ese fragmento:

```java
public void incrementar() {
    synchronized(this) {
        valor++;
    }
}
```
🧠 Esto es útil si solo una línea es crítica y no quieres bloquear todo el método.

**🎯 ¿Cuándo usar `synchronized`?**
- Cuando **múltiples hilos acceden al mismo recurso** (una variable, lista, mapa, archivo, etc.).

- Cuando necesitas garantizar que un bloque de código se ejecute **de forma exclusiva**.

- Cuando los resultados dependen del **orden de ejecución**.

**🚧 ¿Qué pasa si no sincronizas?**
- Resultados incorrectos o aleatorios.

- Datos corruptos (valores que "desaparecen" o se duplican).

- Problemas difíciles de detectar (¡funciona a veces y otras no!).

**💡 Tip práctico**
Usa `synchronized` con cuidado: si sincronizas demasiado código, puedes hacer que los hilos se bloqueen entre sí y tu app se vuelva lenta.

Si necesitas aún más control (como intentar obtener un bloqueo solo si está libre), considera usar `Lock` y `ReentrantLock`.

**🔁 Comunicación entre hilos: `wait()` y `notify()`**

Se usan para que un hilo espere y otro lo despierte cuando sea necesario.

```java
synchronized(obj) {
    obj.wait();    // espera
    obj.notify();  // despierta a otro hilo
}
```
🧠 Ideal en patrones como productor-consumidor.


**🔐 Alternativas modernas**

| Herramienta     | ¿Para qué sirve?                                    |
|-----------------|-----------------------------------------------------|
| `Lock`          | Alternativa a `synchronized` con más control        |
| `ReentrantLock` | Permite bloquear y desbloquear de forma explícita   |


**🔎 Resumen**
Aquí aprendiste lo que realmente separa a un programa funcional de uno que "explota por dentro": **la sincronización**.
Cuando varios hilos comparten recursos, debes organizar sus accesos para evitar errores locos y difíciles de reproducir.
Ahora sabes cómo usar `synchronized`, `wait()`, `notify()` y `Lock` para que todo fluya sin pisarse los pies.

**💡 Tip**: Si algo "funciona a veces", sospecha de una condición de carrera. ¡Y sincroniza ese código!

---

#### 🧠 Actividad de reforzamiento
**Actividad 1.** Relaciona columnas

| Concepto              | Función principal                                       |
|-----------------------|---------------------------------------------------------|
| A) `wait()`           | (___) Retorna el resultado de una tarea asíncrona       |
| B) `ExecutorService`   | (___) Hace que un hilo espere hasta ser notificado      |
| C) `Callable`         | (___) Clase que representa un hilo estándar             |
| D) `Thread`           | (___) Similar a Runnable, pero puede devolver un valor  |
| E) `Future`           | (___) Administra un conjunto de hilos y tareas          |

**Actividad 2.** Mini reto: magina que estás construyendo un programa que guarda pedidos mientras se procesan en paralelo.


**Preguntas:**

¿Qué estructuras y mecanismos usarías para:

- Ejecutar múltiples tareas que procesan los pedidos?

- Garantizar que no se procesen dos veces los mismos datos?

- Recoger los resultados una vez que cada tarea termine?

---

#### **📝 Cierre**

Ahora ya sabes cómo hacer que tus programas respiren multitarea sin explotar 💥
Con los hilos y la concurrencia, puedes lograr que tu app haga varias cosas a la vez de forma más eficiente y profesional.
Has conocido tanto la forma clásica (`Thread`, `Runnable`) como las modernas (`ExecutorService`, `Future`, `Locks`) para construir soluciones robustas.

¡Prepárate para ponerlo en práctica y descubrir el verdadero poder del paralelismo! ⚙️🔥  

---

⬅️ [**Anterior**](../../Readme.md) | [**Siguiente**](../../Sesion-03/Prework/Readme.md)➡️