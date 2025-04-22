🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 04**](../Readme.md) ➡️ / 📝 `Ejemplo 02: Uso de CompletableFuture en operaciones asincrónicas`

## 🎯 Objetivo

🔍 Aprender a crear y ejecutar **tareas asincrónicas** con `CompletableFuture`, encadenar operaciones usando `thenApply`, `thenAccept`, y manejar errores con `exceptionally`, para lograr flujos de trabajo más robustos y flexibles.

---

## ⚙️ Requisitos

- JDK 17 o superior  
- Editor compatible con Java (IntelliJ IDEA, VS Code, etc.)  
- Conocimientos básicos de **asincronía** y **ExecutorService**

---

## 🧠 Contexto del ejemplo

Imagina un **sistema de pedidos en línea**, donde después de **procesar un pago**, se debe:

1. Confirmar el pago.
2. Generar una factura.
3. Enviar una notificación.

Cada paso puede tomar tiempo (simulando **latencia**), pero el sistema debe continuar **de forma no bloqueante**, utilizando **`CompletableFuture`** para encadenar estas operaciones.

---

## 🧱 Código de ejemplo

```java
import java.util.concurrent.*;

public class SistemaPedidos {

    public static void main(String[] args) {
        System.out.println("⚙️ Procesando pedido asincrónicamente...\n");

        CompletableFuture<Void> pedido = procesarPago()
            .thenApply(pago -> generarFactura(pago)) // 🔄 Encadena y transforma el resultado
            .thenAccept(factura -> enviarNotificacion(factura)) // 📤 Consume el resultado final
            .exceptionally(ex -> { // ❌ Maneja errores
                System.out.println("🚨 Error en el proceso: " + ex.getMessage());
                return null;
            });

        pedido.join(); // 🕒 Espera que termine todo el flujo
    }

    // 🏦 Simula el procesamiento de un pago
    public static CompletableFuture<String> procesarPago() {
        return CompletableFuture.supplyAsync(() -> {
            System.out.println("💳 Procesando pago...");
            dormir(2);
            System.out.println("✅ Pago confirmado");
            return "Pago#123";
        });
    }

    // 🧾 Simula la generación de una factura
    public static String generarFactura(String pago) {
        System.out.println("📝 Generando factura para " + pago + "...");
        dormir(1);
        String factura = "Factura#456";
        System.out.println("✅ Factura generada: " + factura);
        return factura;
    }

    // 📧 Simula el envío de una notificación
    public static void enviarNotificacion(String factura) {
        System.out.println("📧 Enviando notificación por " + factura + "...");
        dormir(1);
        System.out.println("✅ Notificación enviada");
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
⚙️ Procesando pedido asincrónicamente...

💳 Procesando pago...
✅ Pago confirmado
📝 Generando factura para Pago#123...
✅ Factura generada: Factura#456
📧 Enviando notificación por Factura#456...
✅ Notificación enviada
```

---

## 🔍 Conceptos clave utilizados

| Concepto             | Descripción |
|----------------------|-------------|
| `CompletableFuture`  | Permite crear tareas asincrónicas y encadenarlas |
| `thenApply()`        | Transforma el resultado de una tarea previa |
| `thenAccept()`       | Consume el resultado final sin devolver nada |
| `exceptionally()`    | Maneja errores en cualquier parte del flujo asincrónico |
| `supplyAsync()`      | Ejecuta una tarea de forma asincrónica y devuelve un valor |

---

## 📝 En resumen

- **`CompletableFuture`** permite **encadenar operaciones asincrónicas** de forma declarativa y flexible.
- **`thenApply`** transforma el resultado de una operación (ideal para pasar de un estado a otro, como de pago a factura).  
- **`thenAccept`** es útil para **acciones finales** (como enviar una notificación).
- **`exceptionally`** asegura que **cualquier error en el flujo sea manejado**, evitando que el sistema falle silenciosamente.
- Esta técnica permite **evitar bloqueos** en procesos como **pagos en línea**, **consultas a bases de datos remotas** o **llamadas a APIs externas**, donde es común que haya **latencia**.

---

📘 Recursos adicionales:

- 🔗 [CompletableFuture en Java – Baeldung](https://www.baeldung.com/java-completablefuture)
- 🔗 [Asynchronous Programming – Oracle Docs](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletableFuture.html)

---

⬅️ [**Anterior**](../Ejemplo-01/Readme.md) | [**Siguiente**](../Reto-01/Readme.md)➡️  