🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 11**](../Readme.md) ➡️ / 📝 `Ejemplo 01: Uso de lambdas y funciones puras`

## 🎯 Objetivo

🔍 Comprender los fundamentos de la programación funcional en Java mediante el uso de expresiones lambda, funciones puras y `Predicate`, con un enfoque práctico basado en un escenario de evaluación de pacientes en un entorno médico.

---

## ⚙️ Requisitos

- JDK 17 o superior  
- Editor compatible con Java (IntelliJ IDEA, VS Code, NetBeans, etc.)
- Conocimientos previos sobre clases, objetos y colecciones en Java

---

## 🧠 Contexto del ejemplo

Imagina que eres parte de un sistema médico que debe **filtrar y evaluar pacientes** con base en su edad o condición. En lugar de escribir múltiples `if/else`, puedes aplicar **lógica funcional** para filtrar listas, definir criterios reutilizables y mantener el código limpio y expresivo.

---

## 🧱 Paso 1: Crear la clase `Paciente`

```java
public class Paciente {

    // Variables globales
    private final String nombre;
    private final int edad;
    private final boolean enObservacion;

    // Constructor
    public Paciente(String nombre, int edad, boolean enObservacion) {
        this.nombre = nombre;
        this.edad = edad;
        this.enObservacion = enObservacion;
    }

    // Métodos get
    public String getNombre() { return nombre; }
    public int getEdad() { return edad; }
    public boolean isEnObservacion() { return enObservacion; }

    // Método toString
    @Override
    public String toString() {
        return nombre + " (Edad: " + edad + ", Observación: " + enObservacion + ")";
    }
}
```

---

## 🧱 Paso 2: Evaluar pacientes con funciones funcionales

```java
import java.util.*;
import java.util.function.*;
import java.util.stream.Collectors;

public class EvaluadorPacientes {

    public static void main(String[] args) {
        // Lista de pacientes simulada
        List<Paciente> pacientes = List.of(
            new Paciente("Ana", 34, false),
            new Paciente("Luis", 70, true),
            new Paciente("Marta", 45, true),
            new Paciente("Pedro", 28, false)
        );

        // ✅ Lambda: Predicate para pacientes mayores de 60
        Predicate<Paciente> mayoresDe60 = p -> p.getEdad() > 60;

        // ✅ Method reference: Predicate para pacientes en observación
        Predicate<Paciente> enObservacion = Paciente::isEnObservacion;

        // ✅ Composición funcional con Predicate.and()
        Predicate<Paciente> casoCritico = mayoresDe60.and(enObservacion);

        System.out.println("🩺 Pacientes en estado crítico:");

        // ✅ Uso de stream para recorrer la lista de pacientes
        pacientes.stream() // ← Stream inicia aquí
            .filter(casoCritico) // ← filter aplica Predicate<Paciente>
            .forEach(System.out::println); // ← forEach aplica método por referencia

        // ✅ Function: transforma un Paciente en un String resumen
        Function<Paciente, String> resumen = p ->
            "🧾 Paciente: " + p.getNombre() + " | Edad: " + p.getEdad();

        System.out.println("\n📋 Resumen general:");

        pacientes.stream() // ← Stream API
            .map(resumen) // ← map aplica Function<Paciente, String>
            .forEach(System.out::println); // ← Acción final (output en consola)
    }
}
```

---

¡Claro, Mario! Aquí tienes la sección que puedes agregar:

---

📘 **Nota:**  
En este ejemplo utilizamos `Stream API` como **vehículo** para aplicar lambdas e interfaces funcionales como `Predicate` y `Function`. Sin embargo, **profundizaremos formalmente en `Stream API`** (operaciones intermedias, terminales, composición) en el siguiente ejercicio.

---


## 🧪 Resultado esperado

```
🩺 Pacientes en estado crítico:
Luis (Edad: 70, Observación: true)

📋 Resumen general:
🧾 Paciente: Ana | Edad: 34
🧾 Paciente: Luis | Edad: 70
🧾 Paciente: Marta | Edad: 45
🧾 Paciente: Pedro | Edad: 28
```

---


### 🔍 Elementos funcionales utilizados

| Elemento         | Descripción |
|------------------|-------------|
| `Predicate<T>`   | Evalúa una condición booleana sobre un objeto (usado para filtrar pacientes) |
| `Function<T,R>`  | Transforma un objeto T en otro tipo R (para crear mensajes o resúmenes) |
| `Stream`         | Flujo de datos para aplicar operaciones funcionales sobre colecciones |
| `filter()`       | Operación intermedia que filtra elementos según una condición (`Predicate`) |
| `map()`          | Transforma cada elemento en otro usando una función (`Function`) |
| `forEach()`      | Operación terminal que ejecuta una acción sobre cada elemento del stream |
| `Lambda`         | Funciones anónimas usadas como argumentos para interfaces funcionales |
| `Method reference` | Notación `::` para pasar métodos existentes como lambdas (`Paciente::isEnObservacion`) |


---

### 💡 ¿Sabías que...?

- Las **funciones puras** no modifican variables externas ni dependen de estados mutables.
- Puedes combinar múltiples `Predicate` con `.and()`, `.or()` y `.negate()` para lógica más expresiva.
- Programación funcional reduce errores, mejora la legibilidad y facilita pruebas unitarias.

---

📘 Recursos adicionales:

- 🔗 [Interfaces funcionales – Java Docs](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html)  
- 🔗 [Programación funcional en Java – Baeldung](https://www.baeldung.com/java-functional-programming)

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Ejemplo-02/Readme.md)➡️  