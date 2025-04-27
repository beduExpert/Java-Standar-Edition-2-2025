🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 05**](../Readme.md) ➡️ / ⚡ `Reto 02: Monitoreo reactivo de signos vitales en una UCI`

## 🎯 Objetivo

⚒️ Simular un sistema **reactivo** que **monitorea signos vitales** de **pacientes críticos** en tiempo real en una **Unidad de Cuidados Intensivos (UCI)**, aplicando **backpressure** para controlar el flujo de datos y **encadenar operaciones reactivas** que filtren eventos anómalos.

---

## 🧠 Contexto del reto

En una UCI moderna, los **sensores** de pacientes generan constantemente datos como:

- **Frecuencia cardíaca (FC)**  
- **Presión arterial (PA)**  
- **Nivel de oxígeno (SpO2)**

Estos datos **se generan rápidamente**, pero **el sistema médico no puede procesar todo al mismo ritmo**. Debes construir un **flujo reactivo** que:

1. **Filtre valores críticos** (ej. FC muy alta/baja, PA fuera de rango, SpO2 bajo).  
2. Aplique **backpressure** para **controlar la velocidad de procesamiento**, evitando saturar al personal médico.  
3. Muestre **alertas en consola** sólo para **eventos críticos**.

---

## 📝 Instrucciones

1. **Simula generación continua de datos** usando `Flux.interval()` para **3 pacientes**.  
   - Cada paciente debe emitir eventos **cada 300 ms** con **valores aleatorios** para **FC**, **PA** y **SpO2**.

2. **Filtra los eventos críticos** con estas condiciones:

| Parámetro            | Rango crítico                  |
|----------------------|---------------------------------|
| Frecuencia cardíaca  | < 50 o > 120 bpm               |
| Presión arterial     | < 90/60 mmHg o > 140/90 mmHg   |
| Oxígeno en sangre    | < 90%                          |

3. Implementa **backpressure** con `delayElements()` para **procesar eventos críticos** a un ritmo **más lento (1 seg)**.  
4. Muestra **alertas** en consola, por ejemplo:

```
⚠️ Paciente 2 - FC crítica: 130 bpm
⚠️ Paciente 1 - SpO2 baja: 85%
```

---

## 💪 Desafío adicional (opcional)

- **Fusiona los flujos de los 3 pacientes** usando `Flux.merge()` o `Flux.concat()` para **gestionar todos los eventos en un solo flujo**.  
- Prioriza los eventos de **FC** sobre **PA** o **SpO2** si hay múltiples eventos simultáneos.

---

## 💡 Ejemplo de salida esperada

```
⚠️ Paciente 1 - FC crítica: 130 bpm
⚠️ Paciente 2 - SpO2 baja: 85%
⚠️ Paciente 3 - PA crítica: 150/95 mmHg
```

> ⚠️ **El orden puede variar** debido al procesamiento reactivo y la fusión de flujos.

---

🏆 Si logras **filtrar, fusionar flujos** y aplicar **backpressure** en el monitoreo de signos vitales, ¡reto completado con éxito! 🎉

---

⬅️ [**Anterior**](../Ejemplo-03/Readme.md) | [**Siguiente**](../../Sesion-06/Readme.md)➡️  