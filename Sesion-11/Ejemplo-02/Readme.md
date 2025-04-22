🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 11**](../Readme.md) ➡️ / 📝 `Ejemplo 02: Uso de Optional y transformaciones con Stream`

## 🎯 Objetivo

🔍 Comprender el funcionamiento de `Stream API` en Java, utilizando operaciones como `map`, `filter`, `forEach` y el manejo seguro de valores nulos con `Optional`. Aplicaremos estas técnicas para transformar y procesar listas de objetos de forma funcional y segura.

---

## ⚙️ Requisitos

- JDK 17 o superior  
- Editor compatible con Java (IntelliJ IDEA, VS Code, etc.)  
- Conocimientos previos de programación funcional básica (`Predicate`, `Function`, lambdas)

---

## 🧠 Introducción a `Stream API` y `Optional`

### 🔹 ¿Qué es `Stream API`?

`Stream API` permite procesar **colecciones de datos (listas, sets, etc.)** de manera **declarativa y funcional**, mediante una secuencia de operaciones:

- **Operaciones intermedias**: transforman o filtran los elementos del stream (`map`, `filter`, etc.)
- **Operaciones terminales**: consumen el stream y producen un resultado (`forEach`, `collect`, etc.)

> 📘 *Un stream **no almacena datos**, sino que procesa los elementos de la colección en forma de flujo.*

---

### 🔹 ¿Qué es `Optional`?

`Optional<T>` es un **contenedor de valor opcional**, diseñado para **evitar el uso de `null`** y manejar posibles valores ausentes de manera segura.

- Permite **encadenar operaciones** como `.map()`, `.filter()`, `.orElse()`.
- Evita excepciones como `NullPointerException`.

---

## 🧱 Paso 1: Ampliar la clase `Paciente` para uso con `Optional`

```java
public class Paciente {
    private final String nombre;
    private final int edad;
    private final boolean enObservacion;
    private final String correo; // Puede ser nulo

    public Paciente(String nombre, int edad, boolean enObservacion, String correo) {
        this.nombre = nombre;
        this.edad = edad;
        this.enObservacion = enObservacion;
        this.correo = correo;
    }

    public String getNombre() { return nombre; }
    public int getEdad() { return edad; }
    public boolean isEnObservacion() { return enObservacion; }

    // 📧 Método que devuelve Optional para evitar NullPointerException
    public Optional<String> getCorreo() {
        return Optional.ofNullable(correo);
    }

    @Override
    public String toString() {
        return nombre + " (Edad: " + edad + ")";
    }
}
```

---

## 🧱 Paso 2: Uso de `Stream API` y `Optional`

```java
import java.util.*;
import java.util.stream.*;

public class EvaluadorPacientesOptional {

    public static void main(String[] args) {
        List<Paciente> pacientes = List.of(
            new Paciente("Ana", 34, false, "ana@example.com"),
            new Paciente("Luis", 70, true, null),
            new Paciente("Marta", 45, true, "marta@example.com"),
            new Paciente("Pedro", 28, false, null)
        );

        System.out.println("📧 Correos electrónicos disponibles:");

        // 🏁 Iniciamos el stream sobre la lista de pacientes
        pacientes.stream() 
            .map(Paciente::getCorreo) // 🔄 map transforma Paciente → Optional<String> (correo)
            .filter(Optional::isPresent) // 🔍 filter permite solo los Optionals que tienen valor (no vacíos)
            .map(Optional::get) // 📥 map extrae el valor del Optional
            .forEach(System.out::println); // 📤 forEach imprime los valores finales

        System.out.println("\n📝 Pacientes en observación (mayores de 40 años):");

        pacientes.stream()
            .filter(p -> p.isEnObservacion() && p.getEdad() > 40) // 🔍 filter aplica condición booleana
            .forEach(System.out::println); // 📤 forEach imprime los pacientes filtrados
    }
}
```

---

## 🧪 Resultado esperado

```
📧 Correos electrónicos disponibles:
ana@example.com
marta@example.com

📝 Pacientes en observación (mayores de 40 años):
Luis (Edad: 70)
Marta (Edad: 45)
```

---

## 🔍 Operaciones explicadas en `Stream API`

| Operación       | Tipo         | Descripción |
|-----------------|--------------|-------------|
| `stream()`      | Inicialización | Inicia el flujo de datos desde la colección |
| `map()`         | Intermedia   | Transforma cada elemento en otro tipo (ej. de `Paciente` a `Optional<String>`) |
| `filter()`      | Intermedia   | Filtra elementos según una condición booleana |
| `forEach()`     | Terminal     | Ejecuta una acción sobre cada elemento (ej. imprimir) |

---

### 💡 ¿Sabías que...?

- Puedes encadenar operaciones intermedias (`map`, `filter`) para transformar y filtrar colecciones sin modificar la colección original.
- Las operaciones en un `Stream` son **perezosas**: solo se ejecutan cuando se llega a una **operación terminal** como `forEach` o `collect`.
- `Optional` es una **herramienta poderosa** para eliminar el riesgo de `null`, permitiendo encadenar operaciones sin preocuparte por excepciones inesperadas.

---

📘 Recursos adicionales:

- 🔗 [Optional – Java Docs](https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html)  
- 🔗 [Stream API – Baeldung](https://www.baeldung.com/java-8-streams)

---

⬅️ [**Anterior**](../Ejemplo-01/Readme.md) | [**Siguiente**](../Reto-01/Readme.md)➡️  