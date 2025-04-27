🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 02**](../Readme.md) ➡️ / ⚡ `Reto 02: Acceso controlado a un recurso médico crítico con ReentrantLock`

## 🎯 Objetivo

⚒️ Simular una situación hospitalaria donde múltiples profesionales médicos necesitan acceder a un recurso crítico (como una sala de cirugía), aplicando sincronización con `ReentrantLock` para evitar condiciones de carrera y garantizar la integridad del sistema.

---

## 🧠 Contexto del reto

En hospitales, algunos recursos como quirófanos, equipos de resonancia magnética o camas de cuidados intensivos, solo pueden ser usados por **un profesional a la vez**. Este reto representa esa situación utilizando múltiples hilos que intentan acceder a un mismo recurso compartido.

---

## 📝 Instrucciones

### 1️⃣ Crear una clase `RecursoMedico`

- Debe tener un atributo `String nombre` que represente el recurso (ej. "Sala de cirugía").
- Implementa un método `usar(String profesional)` que simule:
  - La entrada de un profesional al recurso
  - El tiempo de uso (puede usar `Thread.sleep()`)
  - La salida del recurso
- Usa un `ReentrantLock` para asegurar que solo un hilo acceda al recurso a la vez.

---

### 2️⃣ Crear tareas que representen a profesionales médicos

- Implementa varias clases o lambdas que usen `Runnable`.
- Cada una representa a un médico o enfermero intentando usar el recurso médico.
- El nombre del hilo debe indicar quién accede (ej. `"Dra. Sánchez"`).

---

### 3️⃣ Ejecutar la simulación

- Usa un `ExecutorService` con al menos 4 hilos para simular concurrencia.
- Ejecuta todas las tareas e imprime en consola el flujo de uso del recurso.

---

## 🧪 Resultado esperado

```
🏥 Iniciando acceso a la Sala de cirugía...
👩‍⚕️ Dra. Sánchez ha ingresado a Sala de cirugía
✅ Dra. Sánchez ha salido de Sala de cirugía
👨‍⚕️ Dr. Gómez ha ingresado a Sala de cirugía
✅ Dr. Gómez ha salido de Sala de cirugía
...
```

> 🔒 El acceso debe estar completamente sincronizado para evitar que dos profesionales usen el recurso al mismo tiempo.

---

📘 Recursos útiles:

- 🔗 [ReentrantLock – Oracle Docs](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/ReentrantLock.html)  
- 🔗 [Java Threads & Concurrency – Baeldung](https://www.baeldung.com/java-concurrent-locks)

---

🏆 Si logras simular correctamente el acceso exclusivo al recurso médico por parte de múltiples profesionales, ¡reto completado con éxito!

---

⬅️ [**Anterior**](../Ejemplo-03/Readme.md) | [**Siguiente**](../../Sesion-03/Readme.md)➡️  