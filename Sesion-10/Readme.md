🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 10**](../Readme.md) ➡️ / 🧠 `Sesión 10: Repaso integral y Mentorship Final`

---

## 🎯 Objetivo general
Reflexionar, preguntar y reforzar conocimientos clave adquiridos en el módulo **Java Standard Edition**, a través de preguntas detonadoras, ejecución de ejemplos prácticos y acompañamiento grupal.

---

## 🧩 Sesión 01: Gestión de bases de datos

✅ **Recordatorio rápido**  
Conectamos Java con bases de datos usando JPA y Hibernate, automatizando la persistencia de datos mediante entidades, repositorios, servicios y controladores en Spring Boot.

💬 **Preguntas detonadoras**
- ¿Qué ventaja ofrece usar JPA frente a escribir SQL manualmente?
- ¿Por qué es importante separar la lógica en capas (controlador, servicio, repositorio)?
- ¿Qué datos básicos necesitas configurar en `application.properties` para conectar tu aplicación a una base de datos?

⚙️ **Ejercicio**

Define una entidad Java llamada `Producto` que represente una tabla con los campos `id`, `nombre` y `precio`. Asegúrate de usar las anotaciones de JPA correctamente para que esta clase pueda mapearse a una base de datos.

```java
package com.miempresa.model;

import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;

@Entity  // Marca esta clase como una entidad de base de datos
public class Producto {

    @Id  // Define el campo como clave primaria
    @GeneratedValue(strategy = GenerationType.IDENTITY)  // Auto-incrementable
    private Long id;

    private String nombre;
    private double precio;

    // Constructor vacío necesario para JPA
    public Producto() {}

    // Constructor con atributos
    public Producto(String nombre, double precio) {
        this.nombre = nombre;
        this.precio = precio;
    }

    // Getters y setters
    public Long getId() {
        return id;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public double getPrecio() {
        return precio;
    }

    public void setPrecio(double precio) {
        this.precio = precio;
    }
}

```

---

## 🔄  Sesión 02: Multihilos y procesos concurrentes

🧵 **Recordatorio rápido**  
Utilizamos hilos para ejecutar múltiples tareas en paralelo y aprendimos a gestionar la concurrencia de forma controlada usando `ExecutorService` y `Callable`.

💬 **Preguntas detonadoras**
- ¿Cuál es la diferencia entre crear un hilo con `Thread` y gestionar múltiples tareas con `ExecutorService`?
- ¿Por qué es importante manejar correctamente el acceso a recursos compartidos en programas concurrentes?
- ¿Qué método puedes usar para pausar un hilo por un periodo de tiempo?

⚙️ **Ejercicio**

Crea un hilo que imprima el mensaje `"Hola desde otro hilo"` y luego detén el hilo principal (`main`) durante 2 segundos usando `sleep()`.

```java
package com.miempresa.concurrencia;

// Implementamos la interfaz Runnable para definir la tarea del hilo
public class HiloSaludo implements Runnable {

    @Override
    public void run() {
        // Código que ejecutará el hilo al iniciarse
        System.out.println("Hola desde otro hilo");
    }

    public static void main(String[] args) {
        // Creamos una instancia del Runnable
        HiloSaludo tarea = new HiloSaludo();

        // Asociamos la tarea a un nuevo hilo
        Thread hilo = new Thread(tarea);

        // Iniciamos el hilo (se ejecuta el método run())
        hilo.start();

        try {
            // Pausamos el hilo principal por 2 segundos (2000 milisegundos)
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            // Capturamos la posible interrupción del hilo durante el sueño
            e.printStackTrace();
        }

        // Mensaje desde el hilo principal (se ejecuta después de dormir)
        System.out.println("Fin del hilo principal");
    }
}
```

---

## 🧱 Sesión 03: Programación funcional

🧵 **Recordatorio rápido**  
Aplicaste funciones puras, lambdas, Optional y Streams para escribir código más claro, seguro y expresivo, procesando datos de manera fluida sin ciclos tradicionales.

💬 **Preguntas detonadoras**
- ¿Qué características tiene una función pura?
- ¿Para qué situaciones es útil el uso de `Optional`?
- ¿Qué operaciones puedes encadenar utilizando la API de Streams en Java?

⚙️ **Ejercicio**

Usa un Stream para recorrer una lista de nombres, filtrar los nombres que tengan más de 4 letras y mostrarlos en consola en mayúsculas.

```java
package com.miempresa.programacionfuncional;

import java.util.Arrays;
import java.util.List;

public class StreamEjemplo {

    public static void main(String[] args) {
        // Creamos una lista de nombres
        List<String> nombres = Arrays.asList("Ana", "Roberto", "Luis", "Gabriela");

        // Procesamos la lista usando Stream
        nombres.stream()
            .filter(nombre -> nombre.length() > 4) // Filtra nombres con más de 4 caracteres
            .map(String::toUpperCase)              // Convierte los nombres filtrados a mayúsculas
            .forEach(System.out::println);         // Imprime cada nombre resultante en consola
    }
}
```
---

## 📦 Sesión 04: Procesos asíncronos

🧵 **Recordatorio rápido**  
Implementaste procesos asíncronos en Java usando `CompletableFuture`, permitiendo ejecutar tareas en segundo plano sin bloquear el flujo principal de la aplicación.

💬 **Preguntas detonadoras**
- ¿Qué ventaja tiene usar `CompletableFuture` frente a ejecutar métodos de forma tradicional?
- ¿Qué método puedes utilizar para ejecutar una acción después de que una tarea asíncrona se complete?
- ¿Cómo manejarías una excepción dentro de un flujo de `CompletableFuture`?

⚙️ **Ejercicio**

Lanza una tarea asíncrona que devuelva el número 42, y al terminar, imprime en consola el mensaje `"Resultado obtenido: 42"`.

```java
package com.miempresa.procesosasincronos;

import java.util.concurrent.CompletableFuture;

public class CompletableFutureEjemplo {

    public static void main(String[] args) {
        // Creamos una tarea asíncrona que devuelve el número 42
        CompletableFuture<Integer> tarea = CompletableFuture.supplyAsync(() -> {
            // Simulamos una tarea que calcula un valor
            return 42;
        });

        // Cuando la tarea termina, imprimimos el resultado
        tarea.thenAccept(resultado -> {
            System.out.println("Resultado obtenido: " + resultado);
        });

        // Pausa breve para que la tarea asíncrona alcance a completarse antes de que finalice el programa
        try {
            Thread.sleep(1000); // 1 segundo
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```
---

## 🧬 Sesión 05: Stream Reactivos

✅ **Recordatorio rápido**  
Exploraste cómo manejar flujos de datos asíncronos usando Mono y Flux en programación reactiva, controlando la emisión, transformación y consumo de eventos.

💬 **Preguntas detonadoras**
- ¿Cuál es la diferencia entre Mono y Flux en programación reactiva?
- ¿Qué operador puedes usar para transformar los elementos de un flujo?
- ¿Qué sucede si los datos llegan más rápido de lo que el sistema puede procesarlos?

⚙️ **Ejercicio**
Crea un Mono que contenga el mensaje `"¡Hola reactivo!"` y suscríbete a él para imprimirlo en consola.

```java
package com.miempresa.streamreactivos;

import reactor.core.publisher.Mono;

public class MonoEjemplo {

    public static void main(String[] args) {
        // Creamos un Mono que contiene un solo elemento: un mensaje
        Mono<String> saludo = Mono.just("¡Hola reactivo!");

        // Nos suscribimos al Mono para recibir el valor y mostrarlo en consola
        saludo.subscribe(mensaje -> System.out.println(mensaje));
    }
}
```

---

## 🧰 Sesión 06: Clases genéricas

✅ **Recordatorio rápido**  
Aprendiste a crear clases y métodos genéricos que pueden trabajar con diferentes tipos de datos, manteniendo la seguridad en tiempo de compilación y evitando conversiones innecesarias.

💬 **Preguntas detonadoras**
- ¿Qué ventaja ofrece una clase genérica frente a una clase específica de un tipo?
- ¿Qué representa el símbolo `<T>` en una definición genérica?
- ¿Cuándo es útil usar restricciones como `<T extends Number>` en genéricos?

⚙️ **Ejercicio**

Crea una clase genérica llamada `Caja` que pueda almacenar un objeto de cualquier tipo y permita obtenerlo.

```java
package com.miempresa.clasesgenericas;

// Definimos una clase genérica llamada Caja
public class Caja<T> {

    // Variable para almacenar un objeto de tipo T
    private T contenido;

    // Método para guardar un objeto en la caja
    public void guardar(T contenido) {
        this.contenido = contenido;
    }

    // Método para obtener el contenido de la caja
    public T obtener() {
        return contenido;
    }

    public static void main(String[] args) {
        // Creamos una caja que guarda un String
        Caja<String> cajaDeTexto = new Caja<>();
        cajaDeTexto.guardar("¡Hola, mundo!");
        System.out.println(cajaDeTexto.obtener());

        // Creamos una caja que guarda un número
        Caja<Integer> cajaDeNumero = new Caja<>();
        cajaDeNumero.guardar(123);
        System.out.println(cajaDeNumero.obtener());
    }
}
```

---

## 📂 Sesión 07: Microservicios

✅ **Recordatorio rápido**  
Exploraste cómo modularizar aplicaciones dividiéndolas en servicios pequeños e independientes usando Spring Boot para construir APIs REST de manera sencilla y organizada.

💬 **Preguntas detonadoras**
- ¿Qué ventaja principal tiene una arquitectura de microservicios comparada con un monolito?
- ¿Qué anotación en Spring Boot permite exponer un endpoint como servicio web REST?
- ¿Cuál es el comportamiento de `@SpringBootApplication`?

⚙️ **Ejercicio**

Crea un controlador REST que responda al endpoint `/saludo` con el mensaje `"¡Bienvenido al mundo de los microservicios!"`.

```java
package com.miempresa.microservicios;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

// Anotación que marca la clase principal de una aplicación Spring Boot
@SpringBootApplication
public class MicroservicioAplicacion {

    public static void main(String[] args) {
        // Inicia la aplicación Spring Boot
        SpringApplication.run(MicroservicioAplicacion.class, args);
    }
}

// Anotación que indica que esta clase manejará solicitudes HTTP REST
@RestController
class SaludoControlador {

    // Anotación que mapea el endpoint GET /saludo
    @GetMapping("/saludo")
    public String enviarSaludo() {
        // Retorna un mensaje de bienvenida
        return "¡Bienvenido al mundo de los microservicios!";
    }
}
```

---

## 🛠️ Sesión 08: Buenas prácticas

✅ **Recordatorio rápido**  
Aplicaste convenciones de código, pruebas unitarias, manejo de logs y control de versiones, asegurando que los proyectos Java sean claros, mantenibles y listos para trabajar en equipo.

💬 **Preguntas detonadoras**
- ¿Por qué es importante seguir convenciones de código en un proyecto?
- ¿Qué valida una prueba unitaria en JUnit?
- ¿Cuál es la función de los logs en una aplicación?

⚙️ **Ejercicio**

Crea una prueba unitaria usando JUnit 5 que verifique que un método `sumar(int a, int b)` retorna la suma correcta de dos números.

```java
package com.miempresa.buenaspracticas;

// Clase con un método de suma sencillo
public class Calculadora {

    // Método que suma dos números enteros
    public int sumar(int a, int b) {
        return a + b;
    }
}
```
```java
package com.miempresa.buenaspracticas;

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

// Clase de prueba para la Calculadora
public class CalculadoraTest {

    @Test  // Indica que este método es una prueba unitaria
    void pruebaSuma() {
        // Creamos una instancia de la clase a probar
        Calculadora calc = new Calculadora();

        // Verificamos que la suma de 2 + 3 sea igual a 5
        assertEquals(5, calc.sumar(2, 3));
    }
}
```

---

### 🎤 Espacio abierto 

- Resolver dudas específicas de código o conceptos.
- Compartir aprendizajes, experiencias, errores comunes.
- Tips de práctica y siguientes pasos: ¿qué seguir estudiando?

---

⬅️ [**Anterior**](../Sesion-09/Readme.md)