🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 05**](../Readme.md) ➡️ / ⚡ `Reto 01: Gestión reactiva de sistemas críticos en Meridian Prime`

## 🎯 Objetivo

⚒️ Simular el **flujo reactivo y no bloqueante** para la **gestión en tiempo real de los sistemas críticos** de **Meridian Prime** (una ciudad inteligente inspirada en *Horizon Zero Dawn*), usando **Project Reactor** y **Flux** para procesar **múltiples flujos concurrentes**.

---

## 🧠 Contexto del reto

Como **chief engineer de Meridian Prime**, debes gestionar **cinco sistemas críticos** en **tiempo real**:

1. 🚗 **Sensores de tráfico** → Detectan congestión en las principales avenidas.
2. 🌫️ **Contaminación del aire** → Generan alertas si superan los límites saludables.
3. 🚑 **Accidentes viales** → Prioriza emergencias según la gravedad del accidente.
4. 🚝 **Trenes maglev** → Controla la frecuencia y detecta retrasos.
5. 🚦 **Semáforos inteligentes** → Ajusta tiempos según la repetición de señales rojas.

El sistema debe **procesar estos flujos en paralelo**, **filtrar eventos críticos** y **responder de forma fluida** sin bloquear el sistema.

---

## 📝 Instrucciones

1. **Crea cinco flujos `Flux` independientes**, cada uno simulando **un sistema crítico**:

   | Sistema                  | Dato simulado                        | Frecuencia sugerida  |
   |--------------------------|---------------------------------------|----------------------|
   | Sensores de tráfico      | Nivel de congestión (0-100%)          | Cada 500 ms          |
   | Contaminación del aire   | Nivel de partículas PM2.5 (ug/m3)     | Cada 600 ms          |
   | Accidentes viales        | Evento con prioridad (Baja, Media, Alta) | Cada 800 ms      |
   | Trenes maglev            | Retraso en minutos (0-10 min)         | Cada 700 ms          |
   | Semáforos inteligentes   | Estado (Verde, Amarillo, Rojo) por cruce | Cada 400 ms       |

2. **Filtra eventos críticos** en cada flujo:

   - 🚗 **Congestión mayor al 70%**.
   - 🌫️ **Contaminación superior a 50 ug/m3**.
   - 🚑 **Accidentes con prioridad Alta**.
   - 🚝 **Retrasos mayores a 5 minutos**.
   - 🚦 **Semáforo en rojo más de 3 veces seguidas**.

3. **Emite en consola los eventos críticos detectados** con mensajes descriptivos.

4. **Simula backpressure** en al menos un flujo (ej. sensores de tráfico o trenes maglev) usando **`delayElements`** o **`onBackpressureBuffer`**.

5. Implementa **subscripciones separadas** para cada flujo (puedes usar `merge()` si quieres combinarlos).

---

## 💪 Desafío adicional (opcional)

- Simula **eventos aleatorios críticos simultáneos** (ej. accidente múltiple + congestión severa + contaminación alta) para poner a prueba la **capacidad reactiva** de tu sistema.
- Muestra en consola una **alerta global** si **tres o más eventos críticos** ocurren al mismo tiempo.

---

## 💡 Ejemplo de salida esperada

```
🚗 Alerta: Congestión del 85% en Avenida Solar
🌫️ Alerta: Contaminación alta (PM2.5: 67 ug/m3)
🚑 Emergencia vial: Accidente con prioridad Alta
🚝 Tren maglev con retraso crítico: 8 minutos
🚦 Semáforo en Rojo detectado 3 veces seguidas en cruce Norte

🚨 Alerta global: Múltiples eventos críticos detectados en Meridian Prime
```

---

🏆 **Reto completado con éxito** si logras:

- **Controlar los cinco sistemas en paralelo**.
- **Filtrar y procesar eventos críticos de forma reactiva**.
- Simular **backpressure** y **alertas globales** correctamente.

---

⬅️ [**Anterior**](../Ejemplo-02/Readme.md) | [**Siguiente**](../Ejemplo-03/Readme.md)➡️  