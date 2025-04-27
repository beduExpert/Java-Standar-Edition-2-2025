🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 03**](../Readme.md) ➡️ / ⚡ `Reto 02: Cadena funcional para procesamiento de encuestas en una clínica`

## 🎯 Objetivo

⚒️ Aplicar composición funcional en Java utilizando `Stream API` y `flatMap` para procesar listas anidadas (encuestas de distintas sucursales de una clínica), filtrar respuestas específicas y transformar los datos en mensajes útiles para el área de calidad.

---

## 🧠 Contexto del reto

Una **clínica** recopila **encuestas de satisfacción de pacientes** en distintas sucursales.  
Cada encuesta incluye:

- El **nombre del paciente**.  
- El **comentario** (puede ser `null` si no dejó uno).  
- La **calificación** (escala del 1 al 5).

El **área de calidad** desea:

- Filtrar **solo las encuestas con calificación menor o igual a 3** (pacientes insatisfechos).  
- Recuperar los **comentarios disponibles** (sin `null`) de esas encuestas.  
- Transformar cada comentario en un **mensaje de seguimiento** para la sucursal correspondiente.

---

## 📝 Instrucciones

### 1️⃣ Crear las clases `Encuesta` y `Sucursal`

- **`Encuesta`**:
  - `paciente` (`String`)
  - `comentario` (`String`, puede ser `null`)
  - `calificacion` (`int`)

  Implementa un método `getComentario()` que devuelva un `Optional<String>`.

- **`Sucursal`**:
  - `nombre` (`String`)
  - Lista de **encuestas** (`List<Encuesta>`)

---

### 2️⃣ Procesar las encuestas con `Stream API` y `flatMap`

1. Desanidar todas las encuestas de las sucursales usando `flatMap`.  
2. Filtrar **solo las encuestas con calificación menor o igual a 3**.  
3. Recuperar los **comentarios disponibles** usando `Optional`.  
4. Transformar cada comentario en un mensaje:

```
Sucursal [Nombre]: Seguimiento a paciente con comentario: "<comentario>"
```

5. Mostrar todos los mensajes en consola.

---

## 💡 Ejemplo de salida esperada

```
Sucursal Centro: Seguimiento a paciente con comentario: "El tiempo de espera fue largo"
Sucursal Norte: Seguimiento a paciente con comentario: "La atención fue buena, pero la limpieza puede mejorar"
```

---

📘 Recursos útiles:

- 🔗 [Stream API – Oracle Docs](https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html)  
- 🔗 [Optional – Baeldung](https://www.baeldung.com/java-optional)

---

🏆 Si logras filtrar correctamente las encuestas insatisfechas y generar los mensajes de seguimiento, ¡reto completado con éxito!

---

⬅️ [**Anterior**](../Ejemplo-03/Readme.md) | [**Siguiente**](../../Sesion-04/Readme.md)➡️  