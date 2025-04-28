🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 08**](../Readme.md) ➡️ / ⚡ `Reto 01: Refactorizar un procesador de pagos aplicando SOLID`

---

## 🎯 Objetivo

⚒️ **Identificar malas prácticas** en un procesador de pagos y **refactorizarlo aplicando principios SOLID** (especialmente **SRP**, **OCP** y **DIP**), mejorando la **mantenibilidad** y **extensibilidad** del código.

---

## 🧠 Contexto del reto

Tienes un sistema de **procesamiento de pagos** que permite realizar transacciones usando **tarjeta**, **PayPal** o **criptomonedas**.  
Sin embargo, **toda la lógica está mezclada** dentro de una sola clase, lo que **viola varios principios SOLID**.

Este diseño **dificulta agregar nuevos métodos de pago** (por ejemplo, Apple Pay o transferencias), ya que tendrías que **modificar la clase existente**, afectando otras partes del sistema.

---

## 📋 Instrucciones

1. Analiza el siguiente código mal diseñado (**violando SRP, OCP y DIP**).

2. Refactorízalo aplicando **principios SOLID**:

   - **SRP**: Cada clase debe tener una **única responsabilidad**.
   - **OCP**: El código debe estar **abierto a extensión**, pero **cerrado a modificación**.
   - **DIP**: El servicio debe depender de **abstracciones** (interfaces), no de implementaciones concretas.

3. Crea al menos **tres métodos de pago** (**tarjeta**, **PayPal** y **cripto**), y asegúrate de que **puedan agregarse más en el futuro sin modificar las clases existentes**.

4. Implementa una **clase principal (`Main`)** para probar tu solución.

---

## 💻 Código inicial (mal diseño)

```java
public class PaymentProcessor {

    public void processPayment(String method, double amount) {
        if ("card".equals(method)) {
            System.out.println("Procesando pago con tarjeta por $" + amount);
            // Lógica específica de tarjeta
        } else if ("paypal".equals(method)) {
            System.out.println("Procesando pago con PayPal por $" + amount);
            // Lógica específica de PayPal
        } else if ("crypto".equals(method)) {
            System.out.println("Procesando pago con criptomonedas por $" + amount);
            // Lógica específica de cripto
        } else {
            System.out.println("Método de pago no soportado");
        }
    }
}
```

---

## 🧪 Prueba esperada

Desde tu `Main`:

```java
public class Main {
    public static void main(String[] args) {
        // Ejemplo para tarjeta
        // Ejemplo para PayPal
        // Ejemplo para cripto
    }
}
```

### Salida esperada:

```plaintext
💳 Procesando pago con tarjeta por $1,500.00
💻 Procesando pago con PayPal por $8,500.00
🪙 Procesando pago con criptomonedas por $10,557.00
🏦 Procesando pago con transferencia bancaria por $150,897.27
```

---

## 🚀 Desafío adicional

- Implementa una **nueva opción de pago** (por ejemplo, **Apple Pay** o **transferencia bancaria**) **sin modificar las clases existentes** (solo creando nuevas clases).

---

⬅️ [**Anterior**](../Ejemplo-01/Readme.md) | [**Siguiente**](../Ejemplo-02/Readme.md)➡️  