🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 10**](../Readme.md) ➡️ / 📝 `Ejemplo 01: Introducción a hilos con Runnable`

## 🎯 Objetivo

🔍 Comprender cómo se crean y ejecutan hilos en Java utilizando la interfaz `Runnable`, y visualizar el comportamiento concurrente mediante impresiones en consola.

---

## ⚙️ Requisitos

- IntelliJ IDEA Community Edition  
- JDK 17 o superior  
- Conocimientos previos de programación orientada a objetos  
- Proyecto Java (sin necesidad de Spring Boot)

---

## 🧱 Creación del ejemplo

1. Crea una clase llamada `Tarea` que implemente `Runnable`.  
2. En el método `run()`, imprime un mensaje junto con el nombre del hilo actual.  
3. Crea varios hilos en la clase principal y observa su ejecución simultánea.

---

## 📄 Clase `Tarea.java`

```java
public class Tarea implements Runnable {

    private String nombre;

    public Tarea(String nombre) {
        this.nombre = nombre;
    }

    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Ejecutando " + nombre + " - Iteración " + i +
                               " - Hilo: " + Thread.currentThread().getName());
            try {
                Thread.sleep(500); // Simula una operación que toma tiempo
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
                System.out.println(nombre + " fue interrumpido");
            }
        }
    }
}
```

---

## 🚀 Clase principal `Main.java`

```java
public class Main {
    public static void main(String[] args) {
        Thread hilo1 = new Thread(new Tarea("Tarea 1"));
        Thread hilo2 = new Thread(new Tarea("Tarea 2"));

        hilo1.start(); // Inicia la ejecución del hilo 1
        hilo2.start(); // Inicia la ejecución del hilo 2

        System.out.println("Hilos iniciados desde el hilo principal: " +
                           Thread.currentThread().getName());
    }
}
```

---

## 🧪 Resultado esperado

Al ejecutar el programa, verás las tareas ejecutándose de manera intercalada:

```
Hilos iniciados desde el hilo principal: main
Ejecutando Tarea 1 - Iteración 1 - Hilo: Thread-0
Ejecutando Tarea 2 - Iteración 1 - Hilo: Thread-1
Ejecutando Tarea 1 - Iteración 2 - Hilo: Thread-0
Ejecutando Tarea 2 - Iteración 2 - Hilo: Thread-1
...
```

> ⚠️ El orden puede variar cada vez que ejecutes el programa, debido a la naturaleza concurrente de los hilos.

---

## 🔍 Conceptos clave utilizados

| Concepto     | Descripción |
|--------------|-------------|
| `Runnable`   | Interfaz funcional para definir tareas que pueden ser ejecutadas por un hilo |
| `Thread`     | Clase que representa un hilo de ejecución en Java |
| `start()`    | Inicia la ejecución del hilo llamando internamente al método `run()` |
| `sleep(ms)`  | Suspende temporalmente el hilo actual (útil para simular procesos) |
| `currentThread()` | Permite obtener el nombre del hilo en ejecución |

---

## 💡 ¿Sabías que...?

- Java trata cada hilo como una unidad de ejecución independiente, lo que permite realizar múltiples tareas al mismo tiempo (concurrencia).
- Usar `Thread.sleep()` puede simular operaciones largas, como accesos a bases de datos o servicios web.
- Si llamas a `run()` directamente en lugar de `start()`, **el hilo no se ejecuta concurrentemente**, sino de forma secuencial dentro del hilo actual.
- El método `Thread.currentThread().getName()` ayuda a identificar qué hilo está ejecutando una parte del código, muy útil para depuración.

---

📘 Recursos adicionales:  
🔗 [Documentación oficial de `Thread`](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html)  
🔗 [Programación concurrente en Java – Baeldung](https://www.baeldung.com/java-thread)  

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Ejemplo-02/Readme.md)➡️  