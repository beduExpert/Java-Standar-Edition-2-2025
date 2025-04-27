🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 06**](../Readme.md) ➡️ / ⚡ `Reto 02: Gestión de materiales de curso en una plataforma educativa`

## 🎯 Objetivo

⚒️ Utilizar **genéricos**, **wildcards** (`?`, `extends`, `super`) y **restricciones de tipo** para gestionar diferentes **materiales de un curso** (videos, artículos, ejercicios) en una **plataforma educativa**, aplicando **filtros** y **acciones específicas** por tipo de material.

---

## 🧠 Contexto del reto

En una **plataforma educativa online**, los cursos están compuestos por diferentes tipos de **materiales**:

- 🎥 **Videos**  
- 📄 **Artículos**  
- 📝 **Ejercicios**

El sistema debe:

1. **Mostrar todos los materiales disponibles** de un curso.  
2. **Filtrar solo los videos** para contar su duración total.  
3. **Actualizar** los materiales de tipo **ejercicio**, marcándolos como **revisados**.

---

## 📝 Instrucciones

1. Define una **clase abstracta** `MaterialCurso` con:

   - `titulo` (String)  
   - `autor` (String)  
   - Método abstracto `mostrarDetalle()`.

2. Crea las subclases:

   - `Video` (agrega `duracion` en minutos).  
   - `Articulo` (agrega `palabras` como conteo).  
   - `Ejercicio` (agrega `revisado` como booleano).

3. Implementa los siguientes métodos genéricos:

   - `mostrarMateriales(List<? extends MaterialCurso> lista)`  
   (Muestra el detalle de todos los materiales).

   - `contarDuracionVideos(List<? extends Video> lista)`  
   (Suma y muestra la duración total de los videos).

   - `marcarEjerciciosRevisados(List<? super Ejercicio> lista)`  
   (Actualiza el estado de los ejercicios a `revisado = true` y muestra un mensaje por cada uno).

4. En el `main`, crea una lista con al menos **2 videos**, **2 artículos** y **2 ejercicios**, y prueba los métodos anteriores.

---

## 💪 Desafío adicional (opcional)

- Implementa un método genérico que **filtre materiales** por **autor** usando `Predicate<MaterialCurso>`.

---

## 💡 Ejemplo de salida esperada

```
📚 Materiales del curso:
🎥 Video: Introducción a Java - Autor: Mario - Duración: 15 min
🎥 Video: POO en Java - Autor: Carlos - Duración: 20 min
📄 Artículo: Historia de Java - Autor: Ana - Palabras: 1200
📄 Artículo: Tipos de datos - Autor: Luis - Palabras: 800
📝 Ejercicio: Variables y tipos - Autor: Luis - Revisado: false
📝 Ejercicio: Condicionales - Autor: Mario - Revisado: false

🎥 Duración total de videos: 35 minutos

✅ Ejercicio 'Variables y tipos' marcado como revisado.
✅ Ejercicio 'Condicionales' marcado como revisado.

🔍 Filtrando materiales por autor:
🎥 Video: Introducción a Java - Autor: Mario - Duración: 15 min
📝 Ejercicio: Condicionales - Autor: Mario - Revisado: true
```

---

📘 **Recursos útiles**:

- 🔗 [Wildcards en Java – Oracle](https://docs.oracle.com/javase/tutorial/java/generics/wildcards.html)  
- 🔗 [Java Predicate – Baeldung](https://www.baeldung.com/java-predicate-chain)

---

🏆 Si logras **mostrar**, **filtrar** y **actualizar** los materiales correctamente usando **genéricos** y **wildcards**, ¡reto completado con éxito!

---

⬅️ [**Anterior**](../Reto-02/Readme.md) | [**Siguiente**](../Ejemplo-03/Readme.md)➡️