🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 04**](../Readme.md) ➡️ / 📝 `Ejemplo 03: Caso práctico de asincronía con operaciones I/O`

## 🎯 Objetivo

🔍 Aplicar **asincronía con `CompletableFuture`** en un **caso práctico de operaciones I/O**, como la **consulta a servicios externos simulados**, para visualizar cómo se pueden realizar varias tareas simultáneamente sin bloquear el hilo principal.

---

## ⚙️ Requisitos

- JDK 17 o superior  
- Editor compatible con Java (IntelliJ IDEA, VS Code, etc.)  
- Conocimientos previos de asincronía y `CompletableFuture`

---

## 🧠 Contexto del ejemplo

Simularemos un **sistema de consulta de clima** que obtiene datos de **dos servicios externos distintos** (por ejemplo, **API de clima** y **API de tráfico**).  
Ambas consultas pueden tener **latencia variable** (representando tiempos de respuesta diferentes).  
Queremos:

1. **Realizar ambas consultas de manera asincrónica**.  
2. **Combinar los resultados** para generar un **reporte final** sin bloquear el flujo principal.

---

## 🧱 Código de ejemplo

```java
import java.util.concurrent.*;

public class ConsultaServiciosExternos {

    public static void main(String[] args) {
        System.out.println("🌐 Iniciando consultas a servicios externos...\n");

        CompletableFuture<String> climaFuture = obtenerClima();
        CompletableFuture<String> traficoFuture = obtenerTrafico();

        // 🔗 Combina ambas consultas en un solo reporte
        CompletableFuture<Void> reporteFinal = climaFuture.thenCombine(traficoFuture, 
            (clima, trafico) -> {
                return "📊 Reporte del día:\n- Clima: " + clima + "\n- Tráfico: " + trafico;
            })
            .thenAccept(System.out::println) // 📤 Imprimir reporte
            .exceptionally(ex -> { // ❌ Manejo de errores
                System.out.println("🚨 Error al generar el reporte: " + ex.getMessage());
                return null;
            });

        // Esperar que todo termine
        reporteFinal.join();
    }

    // 🌦️ Simula consulta a un servicio de clima
    public static CompletableFuture<String> obtenerClima() {
        return CompletableFuture.supplyAsync(() -> {
            System.out.println("🌦️ Consultando clima...");
            dormir(3); // Latencia simulada
            return "Soleado, 25°C";
        });
    }

    // 🚗 Simula consulta a un servicio de tráfico
    public static CompletableFuture<String> obtenerTrafico() {
        return CompletableFuture.supplyAsync(() -> {
            System.out.println("🚗 Consultando tráfico...");
            dormir(2); // Latencia simulada
            return "Moderado en el centro";
        });
    }

    // 💤 Método auxiliar para simular latencia
    public static void dormir(int segundos) {
        try {
            TimeUnit.SECONDS.sleep(segundos);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }
}
```

---

## 🧪 Resultado esperado

```
🌐 Iniciando consultas a servicios externos...

🌦️ Consultando clima...
🚗 Consultando tráfico...
📊 Reporte del día:
- Clima: Soleado, 25°C
- Tráfico: Moderado en el centro
```

> ⚠️ **Nota:** El orden de las **consultas puede variar** debido a la **naturaleza asincrónica** de las operaciones.

---

## 🔍 Conceptos clave utilizados

| Concepto               | Descripción |
|------------------------|-------------|
| `CompletableFuture`    | Permite consultas asincrónicas y composición de resultados. |
| `thenCombine()`        | Combina resultados de **dos tareas independientes**. |
| `thenAccept()`         | Ejecuta una acción final sobre el resultado combinado. |
| `exceptionally()`      | Maneja errores en el flujo asincrónico. |
| `supplyAsync()`        | Ejecuta una tarea que devuelve un valor de forma asincrónica. |

---

## 🚀 Conexión con APIs reales (opcional)

Si quisieras **llevar este ejemplo a un entorno real**, conectándote a **APIs externas** en lugar de simular servicios, podrías utilizar herramientas como:

### 🔧 Librerías útiles en Java:

| Librería         | Uso principal |
|------------------|---------------|
| **Spring WebClient** | Cliente reactivo para consumir APIs REST (no bloqueante). |
| **OkHttp**       | Cliente HTTP moderno y eficiente para Java/Kotlin. |
| **Apache HttpClient** | Cliente HTTP tradicional, ampliamente usado en Java. |

---

### 🌐 Ejemplos de APIs públicas:

| API                         | Descripción                                  | URL |
|-----------------------------|----------------------------------------------|-----|
| **OpenWeatherMap**          | Datos de clima en tiempo real y pronósticos. | [https://openweathermap.org/api](https://openweathermap.org/api) |
| **HERE Traffic API**        | Datos de tráfico en tiempo real.             | [https://developer.here.com](https://developer.here.com) |
| **API-Ninjas**              | Diversas APIs (clima, tráfico, noticias, etc.). | [https://api-ninjas.com](https://api-ninjas.com) |

---

### 💡 ¿Cómo integrarlas?

- Usar **WebClient** de Spring para realizar solicitudes **no bloqueantes**:
  ```java
  WebClient webClient = WebClient.create("https://api.openweathermap.org");
  Mono<String> response = webClient.get()
      .uri("/data/2.5/weather?q=Monterrey&appid=YOUR_API_KEY")
      .retrieve()
      .bodyToMono(String.class);
  ```

- O con **OkHttp** (más simple):
  ```java
  OkHttpClient client = new OkHttpClient();
  Request request = new Request.Builder()
      .url("https://api.openweathermap.org/data/2.5/weather?q=Monterrey&appid=YOUR_API_KEY")
      .build();
  ```

> 📌 **Nota:** Usar APIs reales requiere manejar **claves API** y puede tener **limitaciones de uso gratuito**.

---

## 📝 En resumen

- **`CompletableFuture`** permite **consultar múltiples servicios externos en paralelo**, optimizando tiempos de espera.
- **`thenCombine`** es ideal para **unir resultados de dos consultas independientes** (ej. clima y tráfico).
- **Asincronía** en operaciones I/O ayuda a **mejorar la eficiencia** en aplicaciones que dependen de **servicios externos o bases de datos**.

> 🔍 Ejemplos de uso:
> - Aplicaciones móviles consultando **API de clima y tráfico**.
> - Sistemas de monitoreo que integran **múltiples fuentes de datos**.

---

📘 Recursos adicionales:

- 🔗 [CompletableFuture en Java – Baeldung](https://www.baeldung.com/java-completablefuture)
- 🔗 [Asynchronous I/O – Oracle Docs](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletableFuture.html)

---

⬅️ [**Anterior**](../Reto-01/Readme.md) | [**Siguiente**](../Reto-02/Readme.md)➡️  