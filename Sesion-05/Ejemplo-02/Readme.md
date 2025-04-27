🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 05**](../Readme.md) ➡️ / 📝 `Ejemplo 02: Uso de operadores en Flux`


## 🎯 Objetivo

🔍 Aplicar **operadores clave** de **Flux** (`map`, `flatMap`, `filter`) para transformar y procesar flujos reactivos, con varios ejemplos del mundo real. Entender cómo funciona la **subscripción** y cómo manejar flujos **concurrentes y asíncronos**.

---

## ⚙️ Requisitos

- JDK 17 o superior  
- IntelliJ IDEA o cualquier editor compatible con Java  
- Dependencias de **Project Reactor** (`reactor-core`)  
- Conocimientos previos de **Stream API** y **Flux**

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

## 🧠 Contexto del ejemplo

Imagina diferentes **plataformas** que requieren enviar **notificaciones o tareas concurrentes**:

1. **Universidad**: Enviar **correos a estudiantes**.  
2. **Empresa de logística**: Confirmar **entregas a clientes**.  
3. **Sistema de monitoreo**: Notificar **alertas de sensores**.

Con estos **tres flujos (Flux)** verás cómo aplicar **operadores reactivos** en situaciones distintas, explorando:

- Cómo **transformar** elementos (`map`).  
- Cómo **filtrar** elementos (`filter`).  
- Cómo **expandir** un flujo (`flatMap`).  

> 🧪 **¿Por qué usar varios Flux?**  
> - **Mejora la comprensión** del modelo reactivo.  
> - Simula **escenarios reales complejos**.  
> - Permite **comparar comportamientos** entre flujos.

---

## 📄 Código base: `OperadoresReactorDemo.java`

```java
import reactor.core.publisher.Flux;
import java.time.Duration;
import java.util.List;

public class OperadoresReactorDemo {

    public static void main(String[] args) throws InterruptedException {
        
        // Ejemplo 1️⃣: Notificaciones en Universidad
        List<Usuario> usuarios = List.of(
            new Usuario("Ana", "Estudiante", "ana@uni.edu"),
            new Usuario("Carlos", "Profesor", "carlos@uni.edu"),
            new Usuario("Luisa", "Estudiante", "luisa@uni.edu"),
            new Usuario("Sofía", "Administrativo", "sofia@uni.edu")
        );

        Flux.fromIterable(usuarios)
            .filter(u -> u.getRol().equalsIgnoreCase("Estudiante")) // 🔍 Filtra estudiantes
            .map(u -> "📢 Notificación para: " + u.getNombre())     // 🔄 Transforma en mensaje
            .delayElements(Duration.ofMillis(500))
            .subscribe(m -> System.out.println("✅ Universidad: " + m));

        // Ejemplo 2️⃣: Confirmación de entregas (logística)
        Flux.just("Pedido 1", "Pedido 2", "Pedido 3")
            .flatMap(pedido -> simularEntrega(pedido)) // 🔁 Cada pedido genera otro flujo (simula proceso asíncrono)
            .subscribe(m -> System.out.println("🚚 Logística: " + m));

        // Ejemplo 3️⃣: Alertas de sensores
        Flux.just(18, 22, 35, 45) // 🔢 Temperaturas de sensores
            .filter(temp -> temp > 30) // 🔍 Filtra temperaturas altas
            .map(temp -> "⚠️ Alerta: Temperatura alta: " + temp + "°C")
            .subscribe(System.out::println);

        Thread.sleep(4000); // Esperar finalización
    }

    // 🔧 Simula proceso asíncrono para confirmación de entrega
    private static Flux<String> simularEntrega(String pedido) {
        return Flux.just(pedido + " confirmado")
                   .delayElements(Duration.ofMillis(700));
    }

    // Clase auxiliar
    static class Usuario {
        private final String nombre;
        private final String rol;
        private final String correo;

        public Usuario(String nombre, String rol, String correo) {
            this.nombre = nombre;
            this.rol = rol;
            this.correo = correo;
        }

        public String getNombre() { return nombre; }
        public String getRol() { return rol; }
    }
}
```

---

## 🧪 Resultado esperado

```
⚠️ Alerta: Temperatura alta: 35°C
⚠️ Alerta: Temperatura alta: 45°C
✅ Universidad: 📢 Notificación para: Ana
🚚 Logística: Pedido 2 confirmado
🚚 Logística: Pedido 1 confirmado
🚚 Logística: Pedido 3 confirmado
✅ Universidad: 📢 Notificación para: Luisa
```

> ⚠️ El **orden de ejecución puede variar** entre los flujos por la **naturaleza asíncrona de Flux**.

---

## 🔍 Operadores utilizados en Flux

| Operador        | Propósito |
|-----------------|-----------|
| `fromIterable()`| Crea un **Flux** a partir de una colección. |
| `just()`        | Crea un **Flux** con uno o más elementos. |
| `filter()`      | Filtra los elementos que cumplen una condición. |
| `map()`         | Transforma cada elemento. |
| `flatMap()`     | Expande cada elemento en otro **Flux** (flujo dentro de flujo). |
| `delayElements()`| Introduce una latencia entre cada elemento emitido. |
| `subscribe()`   | Inicia el flujo reactivo. |

---

## 📝 En resumen

- Usar **varios Flux** ayuda a **comparar casos de uso reales**:  
  - **Notificaciones de universidad** (map + filter).  
  - **Procesos logísticos** (flatMap + asincronía).  
  - **Alertas de sensores** (filter + map).

- **`flatMap`** permite lanzar **subprocesos reactivos** dentro de un flujo.  
- La **latencia simulada** (`delayElements`) muestra **procesos asíncronos sin bloquear hilos**.

---

⬅️ [**Anterior**](../Ejemplo-01/Readme.md) | [**Siguiente**](../Reto-01/Readme.md)➡️