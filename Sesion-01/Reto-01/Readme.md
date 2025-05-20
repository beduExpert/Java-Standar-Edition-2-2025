🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 01**](../Readme.md) ➡️ / ⚡ `Reto 01: Gestión de órdenes de producción en planta industrial`

## 🎯 Objetivo

⚒️ Implementar **genéricos** y **wildcards** para gestionar diferentes tipos de **órdenes de producción** en una **planta industrial**, clasificando entre **producción en masa**, **personalizada** y **prototipos**.  
Además, deberás procesar las órdenes utilizando métodos flexibles con **restricciones de tipo**.

---

## 🧠 Contexto del reto

Imagina que trabajas en una **planta industrial** que produce:

- 🔧 **Órdenes de producción en masa** (productos estándar).  
- 🛠️ **Órdenes personalizadas** (adaptadas a cliente).  
- 🧪 **Prototipos** (productos en prueba).

Debes implementar un sistema que:

1. **Gestione listas de órdenes de diferentes tipos** (usando genéricos).  
2. **Muestre información de las órdenes** sin importar el tipo.  
3. **Procese las órdenes personalizadas**, agregando un **costo adicional** por ajuste.

---

## 📝 Instrucciones

1. Crea una **clase abstracta** llamada `OrdenProduccion` con los siguientes atributos:

   - `codigo` (String)  
   - `cantidad` (int)

   Incluye un método `mostrarResumen()` para imprimir información básica.

2. Crea tres subclases:

   - `OrdenMasa` (producción en masa)  
   - `OrdenPersonalizada` (agrega `cliente` como atributo)  
   - `OrdenPrototipo` (agrega `faseDesarrollo` como atributo)

3. Implementa un método genérico:

   - `mostrarOrdenes(List<? extends OrdenProduccion> lista)`  
   (Debe **leer** cualquier tipo de orden y mostrar sus datos).

4. Implementa otro método:

   - `procesarPersonalizadas(List<? super OrdenPersonalizada> lista, int costoAdicional)`  
   (Debe **modificar** solo las órdenes personalizadas, mostrando un mensaje con el costo agregado).

5. En el método `main`, crea listas con varios tipos de órdenes (mínimo **2 por tipo**) y prueba los métodos anteriores.

---

## 💪 Desafío adicional (opcional)

- Implementa una función que **cuente** el total de órdenes de **cada tipo** en la planta.

---

## 💡 Ejemplo de salida esperada

```
📋 Órdenes registradas:
🔧 OrdenMasa - Código: A123 - Cantidad: 500
🔧 OrdenMasa - Código: A124 - Cantidad: 750

📋 Órdenes registradas:
🛠️ OrdenPersonalizada - Código: P456 - Cantidad: 100 - Cliente: ClienteX
🛠️ OrdenPersonalizada - Código: P789 - Cantidad: 150 - Cliente: ClienteY

📋 Órdenes registradas:
🧪 OrdenPrototipo - Código: T789 - Cantidad: 10 - Fase: Diseño
🧪 OrdenPrototipo - Código: T790 - Cantidad: 5 - Fase: Pruebas

💰 Procesando órdenes personalizadas...
✅ Orden P456 ajustada con costo adicional de $200
✅ Orden P789 ajustada con costo adicional de $200

📊 Resumen total de órdenes:
🔧 Producción en masa: 2
🛠️ Personalizadas: 2
🧪 Prototipos: 2
```

---

📘 **Recursos útiles**:

- 🔗 [Genéricos y wildcards – Java Tutorial](https://docs.oracle.com/javase/tutorial/java/generics/wildcards.html)  
- 🔗 [Casos de uso de genéricos – Baeldung](https://www.baeldung.com/java-generics)

---

🏆 Si logras **leer y procesar diferentes tipos de órdenes** utilizando **genéricos** y **wildcards**, ¡reto completado!

---

⬅️ [**Anterior**](../Ejemplo-01/Readme.md) | [**Siguiente**](../Ejemplo-02/Readme.md)➡️