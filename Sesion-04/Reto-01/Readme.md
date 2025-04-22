🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 04**](../Readme.md) ➡️ / ⚡ `Reto 01: Simulación asincrónica en una app de movilidad`

## 🎯 Objetivo

⚒️ Aplicar `CompletableFuture` para simular **procesos asincrónicos** en una **app de movilidad** (tipo Uber o DiDi), realizando tareas en paralelo como **calcular la ruta** y **estimar la tarifa**, y enviando una **notificación** al usuario una vez finalizadas.

---

## 🧠 Contexto del reto

En una app de movilidad, al solicitar un viaje:

1. Se calcula la **ruta óptima** entre origen y destino.  
2. Se estima la **tarifa** considerando distancia y demanda.  
3. Una vez ambas operaciones terminan, se envía una **confirmación al usuario** con la información.

Todo este flujo debe ser **asincrónico y no bloqueante**, permitiendo procesar otras solicitudes mientras estas tareas se completan.

---

## 📝 Instrucciones

1. Crea una clase **`MovilidadApp`** con los siguientes métodos:

   - `CompletableFuture<String> calcularRuta()`:  
     - Simula calcular la **ruta óptima** (latencia de 2-3 segundos).
     - Retorna un mensaje como `"Ruta: Centro -> Norte"`.

   - `CompletableFuture<Double> estimarTarifa()`:  
     - Simula la **estimación de la tarifa** (latencia de 1-2 segundos).
     - Retorna un valor numérico como `75.50`.

   - Un método para **combinar ambas operaciones**:
     - Muestra un mensaje final como:

     ```
     🚗 Ruta calculada: Centro -> Norte | Tarifa estimada: $75.50
     ```

2. Encadena las operaciones usando **`thenCombine`** y maneja **errores** con `exceptionally` para casos donde alguna operación pueda fallar (simula con una excepción si quieres).

3. Muestra los resultados en consola.

---

## 💡 Ejemplo de salida esperada

```
🚦 Calculando ruta...
💰 Estimando tarifa...
✅ 🚗 Ruta calculada: Centro -> Norte | Tarifa estimada: $75.50
```

---

📘 Recursos útiles:

- 🔗 [CompletableFuture – Oracle Docs](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletableFuture.html)  
- 🔗 [Asynchronous Programming in Java – Baeldung](https://www.baeldung.com/java-completablefuture)

---

🏆 Si logras **combinar correctamente los resultados asincrónicos** y mostrar el mensaje final, ¡reto completado con éxito!

---

⬅️ [**Anterior**](../Ejemplo-02/Readme.md) | [**Siguiente**](../Ejemplo-03/Readme.md)➡️  