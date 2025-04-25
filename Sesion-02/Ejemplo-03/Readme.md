🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 02**](../Readme.md) ➡️ / 📝 `Ejemplo 03: Sincronización con synchronized y Locks`

## 🎯 Objetivo

🔍 Entender cómo evitar errores de concurrencia (como condiciones de carrera) en programas multihilo usando `synchronized` y estructuras modernas de bloqueo como `ReentrantLock`.

---

## ⚙️ Requisitos

- JDK 17 o superior  
- IntelliJ IDEA o cualquier editor compatible con Java  
- Conocimientos previos de programación concurrente (`Runnable`, `ExecutorService`)

---

## 🧠 Contexto del ejemplo

En entornos multihilo, varios hilos pueden intentar **modificar al mismo tiempo una misma variable o recurso**, lo que genera inconsistencias. En este ejemplo simulamos una cuenta bancaria compartida, donde múltiples hilos intentan retirar dinero a la vez.

Veremos cómo proteger ese acceso usando dos enfoques:

1. `synchronized` (bloqueo implícito de objetos)
2. `ReentrantLock` (bloqueo explícito más flexible)

---

## 🧱 Paso 1: Simulación con `synchronized`

### 📄 `CuentaBancaria.java`

```java
public class CuentaBancaria {
    private int saldo = 1000;

    public synchronized void retirar(String nombre, int cantidad) {
        if (saldo >= cantidad) {
            System.out.println(nombre + " está retirando $" + cantidad);
            saldo -= cantidad;
            System.out.println(nombre + " completó el retiro. Saldo restante: $" + saldo);
        } else {
            System.out.println(nombre + " no pudo retirar: fondos insuficientes.");
        }
    }

    public int getSaldo() {
        return saldo;
    }
}
```

---

## 🚀 Paso 2: Clase principal con múltiples hilos

### 📄 `Main.java`

```java
public class Main {
    public static void main(String[] args) {
        CuentaBancaria cuenta = new CuentaBancaria();

        Runnable tarea = () -> {
            String nombreHilo = Thread.currentThread().getName();
            cuenta.retirar(nombreHilo, 300);
        };

        Thread t1 = new Thread(tarea, "Astronauta-1");
        Thread t2 = new Thread(tarea, "Astronauta-2");
        Thread t3 = new Thread(tarea, "Astronauta-3");

        t1.start();
        t2.start();
        t3.start();
    }
}
```

---

## 🧪 Resultado esperado (usando `synchronized`)

```
Astronauta-1 está retirando $300
Astronauta-1 completó el retiro. Saldo restante: $700
Astronauta-2 está retirando $300
Astronauta-2 completó el retiro. Saldo restante: $400
Astronauta-3 está retirando $300
Astronauta-3 completó el retiro. Saldo restante: $100
```

> ⚠️ Sin `synchronized`, los hilos podrían modificar el saldo al mismo tiempo y crear un saldo incorrecto.

---

## 🔁 Alternativa: `ReentrantLock`

Puedes modificar `CuentaBancaria` para usar esta estructura de bloqueo más avanzada:

```java
import java.util.concurrent.locks.ReentrantLock;

public class CuentaBancaria {
    private int saldo = 1000;
    private final ReentrantLock lock = new ReentrantLock();

    public void retirar(String nombre, int cantidad) {
        lock.lock();
        try {
            if (saldo >= cantidad) {
                System.out.println(nombre + " está retirando $" + cantidad);
                saldo -= cantidad;
                System.out.println(nombre + " completó el retiro. Saldo restante: $" + saldo);
            } else {
                System.out.println(nombre + " no pudo retirar: fondos insuficientes.");
            }
        } finally {
            lock.unlock(); // ⚠️ ¡Siempre liberar el lock!
        }
    }

    public int getSaldo() {
        return saldo;
    }
}
```

---


### 🧪 Resultado esperado (usando `ReentrantLock`)

La salida será muy similar a la de `synchronized`, pero ahora con control explícito del bloqueo:

```
Astronauta-1 está retirando $300
Astronauta-1 completó el retiro. Saldo restante: $700
Astronauta-3 está retirando $300
Astronauta-3 completó el retiro. Saldo restante: $400
Astronauta-2 está retirando $300
Astronauta-2 completó el retiro. Saldo restante: $100
```

> ✅ El orden puede variar, pero el **control de acceso al recurso compartido está garantizado**, sin condiciones de carrera.

---

## 🔍 Conceptos clave utilizados

| Concepto        | Descripción |
|-----------------|-------------|
| `synchronized`  | Bloquea automáticamente el objeto al entrar al método |
| `ReentrantLock` | Permite controlar manualmente el bloqueo/desbloqueo, y usar condiciones |
| `Thread.currentThread().getName()` | Permite identificar el hilo activo |

---

## 📝 En resumen

- Las **condiciones de carrera** ocurren cuando varios **hilos acceden y modifican recursos compartidos sin control**, lo que puede provocar inconsistencias en los datos.
- Para prevenirlas, usamos **mecanismos de sincronización** como:
  - **`synchronized`** → Bloqueo implícito más simple.
  - **`ReentrantLock`** → Bloqueo explícito que permite **mayor control** (como tiempo de espera, desbloqueo manual).
- Ambos enfoques garantizan que **solo un hilo a la vez acceda a la sección crítica**, pero **ReentrantLock** es más flexible en sistemas complejos.
- Este ejemplo muestra cómo proteger operaciones sensibles (como **retiros de una cuenta bancaria**) para asegurar **consistencia y seguridad** en entornos multihilo.


---

## 💡 ¿Sabías que...?

- Usar `synchronized` es más simple, pero `ReentrantLock` da mayor control (por ejemplo, tiempo de espera, interrupción).
- Las condiciones de carrera son uno de los errores más difíciles de depurar en sistemas concurrentes.
- Java también ofrece estructuras seguras como `AtomicInteger`, `ConcurrentHashMap` y `Semaphore`.

---

📘 Recursos adicionales:  
🔗 [Bloqueo con synchronized – Oracle](https://docs.oracle.com/javase/tutorial/essential/concurrency/sync.html)  
🔗 [ReentrantLock – Java Docs](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/ReentrantLock.html)

---

⬅️ [**Anterior**](../Reto-01/Readme.md) | [**Siguiente**](../Reto-02/Readme.md)➡️  