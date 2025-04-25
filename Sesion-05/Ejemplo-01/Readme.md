🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 05**](../Readme.md) ➡️ / 📝 `Ejemplo 01: Comparativa entre Stream API y programación reactiva`

## 🎯 Objetivo

🔍 Comparar el comportamiento de **Stream API tradicional** y **programación reactiva** con **Flux** en Java, mostrando cómo cada enfoque gestiona **notificaciones** a usuarios en una **plataforma de mensajería** y cómo manejan la **latencia** de entrega.

---

## 🧠 Contexto del ejemplo

Supongamos que administras un sistema de **notificaciones de usuarios**. Queremos enviar **mensajes personalizados** a cada usuario:

- Con **Stream API tradicional**, los mensajes se procesan **en bloque** (uno por uno hasta completar todos).
- Con **Flux** (reactivo), los mensajes se **emiten a medida que están disponibles**, permitiendo una entrega **más fluida y no bloqueante**.

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

## 🧱 Paso 1: Notificaciones con **Stream API**

```java
import java.util.List;
import java.util.concurrent.TimeUnit;

public class NotificacionesStreamTradicional {
    public static void main(String[] args) throws InterruptedException {
        List<String> usuarios = List.of("Ana", "Luis", "Marta", "Carlos");

        System.out.println("📢 Enviando notificaciones con Stream API:");

        usuarios.forEach(NotificacionesStreamTradicional::enviarNotificacion);
    }

    private static void enviarNotificacion(String usuario) {
        try {
            TimeUnit.SECONDS.sleep(1); // Simula retraso en enviar la notificación
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
        System.out.println("✅ Notificación enviada a: " + usuario);
    }
}
```

---

## 🧱 Paso 2: Notificaciones con **Flux** (Programación reactiva)

```java
import reactor.core.publisher.Flux;
import java.time.Duration;

public class NotificacionesFluxReactivo {
    public static void main(String[] args) throws InterruptedException {
        System.out.println("\n⚡ Enviando notificaciones con Flux:");

        Flux<String> usuariosFlux = Flux.just("Ana", "Luis", "Marta", "Carlos")
                                        .delayElements(Duration.ofSeconds(1)); // Simula llegada gradual

        usuariosFlux.subscribe(usuario -> 
            System.out.println("✅ Notificación enviada a: " + usuario)
        );

        // Esperar que terminen las notificaciones reactivas
        Thread.sleep(5000);
    }
}
```

---

## 🧪 Resultado esperado

```
📢 Enviando notificaciones con Stream API:
✅ Notificación enviada a: Ana
✅ Notificación enviada a: Luis
✅ Notificación enviada a: Marta
✅ Notificación enviada a: Carlos

⚡ Enviando notificaciones con Flux:
✅ Notificación enviada a: Ana
✅ Notificación enviada a: Luis
✅ Notificación enviada a: Marta
✅ Notificación enviada a: Carlos
```

> 🔍 **Diferencia clave**:  
> - En **Stream API**, el proceso es **secuencial** y **bloquea** el hilo principal (`main`) hasta enviar todas las notificaciones.  
> - Con **Flux**, cada notificación **fluye de forma independiente**, **sin bloquear** el hilo, ideal para **sistemas en tiempo real**.

---

## 🔍 Conceptos clave utilizados

| Concepto     | Descripción |
|--------------|-------------|
| `Stream API` | Procesa colecciones de datos en **bloque**, de forma secuencial y **bloqueante**. |
| `Flux`       | Publicador reactivo que emite **múltiples elementos** en un flujo **no bloqueante**. |
| `delayElements()` | Introduce latencia entre elementos emitidos por Flux, simulando llegada gradual. |
| `subscribe()` | Activa el flujo y define cómo se procesan los elementos emitidos. |

---

## 📝 En resumen

- **Stream API tradicional** es **bloqueante** y procesa **colecciones completas** de datos.  
- **Flux (reactivo)** permite **procesar elementos conforme llegan**, sin bloquear hilos, ideal para **flujos continuos o en tiempo real**.

> 🚀 **¿Cuándo usar cada uno?**  
> - Usa **Stream API** para procesar listas ya completas (ej. colecciones en memoria).  
> - Usa **Flux** para **eventos en tiempo real**, **mensajería**, **sensores**, o cuando los datos **se generan gradualmente**.

---

📘 Recursos útiles:

- 🔗 [Project Reactor – Guía oficial](https://projectreactor.io/docs/core/release/reference/)  
- 🔗 [Programación reactiva vs tradicional – Reflectoring](https://reflectoring.io/reactive-vs-traditional/)

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Ejemplo-02/Readme.md)➡️  