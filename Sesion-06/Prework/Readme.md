🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 `Prework sesión 06`

<div align="center">
    <img src="../Imagenes/S06.jpg" alt="Bedu | Haz + con tu talento | JAVA STANDARD EDITION II">
</div>

##### **PREWORK**
#### **🟧 Sesión 06**
#### **Clases genéricas**


##### 🔶 **Introducción**

¡Hola! 👋 

En esta sesión vamos a descubrir el secreto para escribir código flexible, reutilizable y seguro en Java: los genéricos.

¿Te imaginas tener una misma clase o método que funcione para cualquier tipo de dato, sin repetir código?
Eso es precisamente lo que logras con los genéricos. Son como moldes que puedes adaptar según el material que necesites:
puedes tener listas de enteros, listas de cadenas, listas de objetos personalizados, todo usando la misma estructura base.

Los genéricos son fundamentales en Java y los encontrarás en casi todas las librerías estándar (por ejemplo, `List<T>`,`Map<K, V>`, etc.).
Hoy aprenderás cómo funcionan y por qué son tan usados.

---

#### 🎯 Objetivo

- Comprender qué son los genéricos y por qué son útiles.
- Aprender a declarar clases y métodos genéricos.
- Conocer los wildcards (`?`, `extends`, `super`) y sus restricciones.
- Aplicar genéricos en estructuras comunes como `List<T>` y `Map<K, V>`.
- Seguir buenas prácticas para aprovechar al máximo los genéricos.

---

#### 📋 Instrucciones

Este Prework está diseñado para conocer el contenido que se practicará durante la sesión en vivo. **Por favor no lo omitas.**

Toma notas de lo que consideres relevante y guarda tus preguntas o dudas para resolverlas en la sesión.

Antes de arrancar, verifica que tu entorno de desarrollo esté listo. Es fundamental que tengas instalado IntelliJ IDEA Community Edition y el JDK (Java Development Kit) para trabajar sin interrupciones.

Si te surge alguna dificultad con la instalación o cualquier duda, no dudes en pedir ayuda a tu experto/a. ¡Estamos aquí para asegurarnos de que todo fluya sin problemas! 🚀

---

**Bienvenido/a**

Bienvenid@ al sexto Prework del módulo. A continuación, te presentamos el tiempo estimado de lectura por tema, para que puedas revisar todos los recursos al máximo: 

| **📖 Temario**                                   | **🕰️ Tiempo sugerido** |
|--------------------------------------------------|------------------------|
| Tema 01. Introducción a los genéricos en Java    | 10 min                 |
| Tema 02. Wildcards y restricciones               | 10 min                 |
| Tema 03. Aplicaciones comunes                    | 10 min                 |


**¡Comencemos! 🏁**

---
 
#### 📚 Tema 01. Introducción a los genéricos en Java
##### ⏳ 10 minutos de lectura

**📌 ¿Qué son los genéricos?**
Los genéricos en Java permiten definir clases, interfaces y métodos que se adaptan a diferentes tipos de datos, sin sacrificar la seguridad en tiempo de compilación.

En lugar de crear clases o métodos distintos para cada tipo de dato (por ejemplo, una clase para enteros, otra para cadenas, otra para objetos personalizados), los genéricos te permiten crear una sola estructura que puede funcionar con cualquiera de esos tipos.

Visualízalo así:
<table style="border-collapse: collapse;">
  <tr>
    <td style="border: 1px solid white; padding: 10px; vertical-align: top;">
      <img src="../Imagenes/S06_Fig01.jpg" alt="caja de herramientas" width="60">
    </td>
    <td style="border: 1px solid white; padding: 10px;">
      Imagina una caja multiusos. Puedes usarla para guardar tornillos, libros o herramientas, pero sigue siendo la misma caja. Solo decides qué tipo de objeto vas a colocar cuando la uses.
    </td>
  </tr>
</table>

**🧩 ¿Cómo se representan?**
Los genéricos utilizan letras mayúsculas entre corchetes angulares `< >` para representar parámetros de tipo.
El más común es `T` (de Type), pero puedes usar otros como:

| Letra | Significado común
|-------|---------------------------------------|
| T     | Type (tipo genérico)                  |
| E     | Element (elemento, para colecciones)  |
| K     | Key (clave, en mapas)                 |
| V     | Value (valor, en mapas)               |
| N     | Number (número)                       |

Estos nombres son convenciones, pero puedes usar cualquier identificador.


**🤔 ¿Por qué usar genéricos?**

Sin genéricos, tendrías que trabajar con Object, el tipo base de Java, lo cual implica castings manuales (conversiones de tipo) y riesgo de errores en tiempo de ejecución.

Con genéricos:

✅ El compilador revisa los tipos por ti, previniendo errores.
✅ Evitas castings innecesarios.
✅ Haces tu código más mantenible y adaptable.

| 👎 Sin genéricos	                                   | 👍Con genéricos                                            |
|-------------------------------------------------------|------------------------------------------------------------|
| `List lista = new ArrayList();`                       | `List<String> lista = new ArrayList<>();`                  |
| Necesitas hacer casting manual al extraer elementos.  | No necesitas casting; el tipo está definido.               |
| `String nombre = (String) lista.get(0);`              | `String nombre = lista.get(0);`                            |
| Posible error si el tipo es incorrecto (en ejecución).| Error detectado en compilación si el tipo no es compatible.|


🌟 Los genéricos permiten escribir una sola vez estructuras que sirven para varios tipos de datos, mejorando la seguridad y adaptabilidad del código.

**🛠️ Declaración de clases y métodos genéricos**

🧪 Ejemplo: Clase genérica simple

```java
public class Caja<T> {
    private T contenido;

    public void guardar(T contenido) {
        this.contenido = contenido;
    }

    public T obtener() {
        return contenido;
    }
}
```

👀 ¿Qué sucede aquí?

- `T` es un parámetro de tipo (puede ser cualquier tipo que elijas).
- Al usar la clase, decides el tipo específico:

```java
Caja<String> cajaDeTexto = new Caja<>();
cajaDeTexto.guardar("Hola");
System.out.println(cajaDeTexto.obtener()); // Imprime: Hola
```

🛠️ Ejemplo: Método genérico

```java

public static <T> void imprimirArray(T[] array) {
    for (T elemento : array) {
        System.out.println(elemento);
    }
}
```
👀 Este método funciona con cualquier tipo de array:

```java
String[] nombres = {"Ana", "Luis"};
Integer[] numeros = {1, 2, 3};

imprimirArray(nombres); // Funciona
imprimirArray(numeros); // También funciona
```
**🧠 Ventajas concretas en un entorno de trabajo**

1. Mantenimiento más sencillo:
    - Si cambias el tipo de datos, no necesitas reescribir tu lógica.

2. Reutilización de componentes:
    - Puedes tener utilerías, colecciones o estructuras de datos que funcionen para distintos tipos sin crear nuevas clases.

3. Seguridad en compilación:
    - El compilador valida los tipos, lo que reduce errores al integrar módulos o consumir APIs internas.

En el desarrollo diario, es común encontrarte con situaciones donde trabajas con colecciones de distintos tipos (listas de clientes, productos, números, etc.).

Los genéricos son una de las principales herramientas para evitar duplicar código cuando manejas esas estructuras, y te permiten mantener la consistencia en el manejo de tipos.

**🔥 Tip final** 

Cuando diseñes una API o librería interna en tu empresa, considera usar genéricos si:

- Vas a crear métodos o clases de utilidad que podrían aplicarse a diferentes tipos de datos.

- Quieres evitar castings manuales y asegurar que los tipos se verifiquen en compilación.

- Necesitas garantizar que quienes consuman tu código lo hagan de forma segura y flexible.

Adoptar genéricos desde el diseño inicial evita refactorizaciones a futuro cuando el sistema crece y nuevos tipos de datos entran en juego. 💫



---

#### 📚 Tema 02. Wildcards y restricciones
##### ⏳ 10 minutos de lectura

**📌 ¿Qué son los wildcards en Java?**
Los wildcards (`?`) permiten que los genéricos sean aún más flexibles, aceptando múltiples tipos de datos relacionados entre sí sin especificar uno exacto.
Son especialmente útiles cuando quieres leer datos de una colección, pero no necesitas modificarla o cuando diferentes tipos comparten una misma jerarquía.

Visualizalo asi:
<table style="border-collapse: collapse;">
  <tr>
    <td style="border: 1px solid white; padding: 10px; vertical-align: top;">
      <img src="../Imagenes/S06_Fig02.jpg" alt="caja de papeles" width="60">
    </td>
    <td style="border: 1px solid white; padding: 10px;">
      Imagina un cajón donde puedes guardar diferentes documentos, pero todos deben ser papeles (pueden ser facturas, contratos, recibos). 
      El wildcard te permite no especificar exactamente qué tipo de papel es, pero sabes que comparten algo en común.
    </td>
  </tr>
</table>

**🛠️ Tipos de wildcards**

| Símbolo          | ¿Qué permite?                | Ejemplo práctico |
|------------------|------------------------------|------------------|
| `?`              | Acepta cualquier tipo        | `List<?>` – Lista de cualquier tipo|
| `? extends Tipo` | Acepta Tipo o sus subtipos   | `List<? extends Number>` – Lista de números (Integer, Double, etc.)|
| `? super Tipo`   | Acepta Tipo o sus supertipos | `List<? super Integer>` – Lista de Integer o cualquier supertipo (ej. Number, Object)|

**🤔 ¿Cómo saber cuándo usar cada wildcard?**

Imagina que estás diseñando un módulo de recursos humanos. En este módulo tienes distintas clases:

- `Empleado` (la clase base)
- `Gerente` y `Director` (que extienden de `Empleado`)

Ahora quieres crear métodos que interactúan con colecciones de empleados, gerentes o directores. Pero cada situación requiere una lógica distinta según qué tan específico necesitas ser con los tipos.

**🧩 Situación 1: Solo necesitas leer los elementos**

Vas a crear un reporte general de nombres de empleados. No importa si son empleados, gerentes o directores, solo necesitas leer sus datos, no modificar la lista.

Aquí usarías:
```java

List<? extends Empleado>
```

Este wildcard indica:

> *"Pásame una lista de cualquier cosa que sea Empleado o un subtipo, pero no voy a cambiarla, solo voy a leer."*

⁉️ ¿Por qué no puedes modificar?

Porque no sabes el tipo exacto de los objetos en esa lista (pueden ser `Gerente`, `Director`...), y agregar algo incorrecto podría causar problemas.

**🧩 Situación 2: Necesitas agregar elementos**

Ahora quieres crear un método que agregue nuevos empleados a una lista.
Aquí no te importa si la lista es de `Empleado` o algo más genérico (como `Object`), pero debes poder insertar empleados.

Usarías:

```java
List<? super Empleado>
```

Este wildcard indica:

> *"Pásame una lista que acepte objetos tipo Empleado o cualquier supertipo (como Object), para que yo pueda agregar Empleados."*

⁉️ ¿Por qué es seguro agregar?

Porque Empleado es compatible con todos sus supertipos. Pero al leer, solo puedes obtener Object, ya que no sabes el tipo exacto de la lista.

**🧩 Situación 3: No te importa el tipo, solo interactúas sin preocuparte del detalle**

Si tienes un método que solo itera por una lista y hace algo genérico, sin depender del tipo específico (por ejemplo, solo contar elementos o imprimir sin procesar):

```java
List<?>
```

Esto es como decir:

> *"Pásame cualquier lista de cualquier tipo. No me importa qué contiene, solo voy a hacer operaciones básicas."*

**🧠 Comparación mental**

- `? extends Tipo` → Lees datos (ej. hacer reportes).
- `? super Tipo` → Agregas datos (ej. registrar empleados).
- `?` → No te interesa el tipo, solo usas la colección de forma básica.

**🚀 Tip para recordar**

📖 Si quieres leer, piensa en `extends` (leer hacia arriba en la jerarquía).
✍️ Si quieres escribir, piensa en `super` (agregar hacia abajo en la jerarquía).

**🏗️ Restricciones en los genéricos**

Puedes limitar los tipos que acepta un genérico usando extends:

```java

public class CajaNumeros<T extends Number> {
    private T contenido;

    public void guardar(T contenido) {
        this.contenido = contenido;
    }
}
```

🧐 ¿Qué hace esto?

- Solo puedes usar tipos que sean subtipos de `Number` (como Integer, Double).
- No puedes usar String, por ejemplo.

🧪 Ejemplo de restricción
```java
CajaNumeros<Integer> cajaEnteros = new CajaNumeros<>();
cajaEnteros.guardar(10); // ✅

CajaNumeros<String> cajaTexto = new CajaNumeros<>(); // ❌ Error en compilación
```

**🏆 Buenas prácticas al usar wildcards**

- Usa `? extends` cuando solo necesites leer de una colección.
- Usa `? super` cuando necesites agregar elementos.
- Evita usar wildcards si no es necesario:
    - Si conoces el tipo exacto, decláralo explícitamente para mejorar la legibilidad.

**Resumen...**

Los wildcards te ofrecen una forma adaptable de trabajar con colecciones de diferentes tipos relacionados, permitiéndote leer o escribir según la necesidad.

Además, aprendiste a restringir los tipos genéricos para asegurar que solo ciertos tipos puedan ser utilizados.

**🔥 Tip final** 
Cuando diseñes interfaces o servicios genéricos que deban interactuar con varias entidades relacionadas, considera usar wildcards para flexibilizar la lectura o escritura, pero sin perder el control sobre los tipos.

Esto es útil, por ejemplo, cuando trabajas con jerarquías de clases (como Empleado, Gerente, Director).




---

#### 📚 Tema 03.  Aplicaciones comunes
##### ⏳ 10 minutos de lectura

Hasta aquí ya conoces qué son los genéricos, cómo declararlos, y cómo usar wildcards para flexibilizar el manejo de tipos.
Pero... ¿cómo se aplican realmente en el día a día de un programador?
Aquí te muestro buenas prácticas y situaciones comunes donde los genéricos son más que útiles, son necesarios para mantener tu código organizado y seguro.

**🏗️ Buena práctica 1: Evitar castings manuales**

Uno de los mayores beneficios de los genéricos es que te ahorran hacer castings (conversiones) manualmente.

Antes (sin genéricos):

``` java
List lista = new ArrayList();
lista.add("Hola");

String texto = (String) lista.get(0); // Necesitas casting
```

Ahora (con genéricos):

```java
List<String> lista = new ArrayList<>();
lista.add("Hola");

String texto = lista.get(0); // No necesitas casting
```

💫 Ventaja:
El compilador verifica los tipos por ti, reduciendo errores en tiempo de ejecución.

**🏗️ Buena práctica 2: Diseñar clases reutilizables**

Si tienes clases o métodos de utilidad (como controladores, repositorios o servicios), decláralos genéricos para que sirvan para varios tipos de objetos.

Ejemplo: Repositorio genérico

```java
public class Repositorio<T> {
    private List<T> datos = new ArrayList<>();

    public void agregar(T elemento) {
        datos.add(elemento);
    }

    public T obtener(int indice) {
        return datos.get(indice);
    }
}
```

Uso del repositorio:

```java
Repositorio<String> repoTexto = new Repositorio<>();
repoTexto.agregar("Hola");

Repositorio<Integer> repoNumeros = new Repositorio<>();
repoNumeros.agregar(100);
```

💯 Beneficio:
Una sola estructura sirve para cualquier tipo de entidad (productos, clientes, números).

**🏗️ Buena práctica 3: Limitar el tipo aceptado (restricciones)**
Si una clase o método solo debe aceptar ciertos tipos (por ejemplo, solo números), usa restricciones para evitar usos indebidos.

```java
public class Calculadora<T extends Number> {
    public double sumar(T a, T b) {
        return a.doubleValue() + b.doubleValue();
    }
}
```

Esto evita que alguien intente usar String u otro tipo incompatible:

```java
Calculadora<Integer> calcInt = new Calculadora<>(); // ✅
Calculadora<String> calcStr = new Calculadora<>();  // ❌ Error en compilación
```

💯 Beneficio:
Previenes errores en etapas tempranas (antes de que el programa corra).

**🏗️ Buena práctica 4: Combinar wildcards para flexibilidad**

Cuando diseñas interfaces o métodos genéricos, usa wildcards si necesitas adaptarte a jerarquías de clases.

Ejemplo:

```java
public void imprimirLista(List<? extends Number> lista) {
    for (Number n : lista) {
        System.out.println(n);
    }
}
```

- Puedes pasarle `List<Integer>`, `List<Double>`, etc.
- No puedes modificar la lista, pero puedes leer sin problemas.

🧐 Situación común
Este patrón es frecuente en reportes o validaciones, donde solo necesitas consultar los datos.

**🧩 Casos de uso comunes en el mundo real**

1. Colecciones en APIs:
- Cuando defines servicios REST que retornan listas de objetos (productos, usuarios, etc.).
- Ejemplo: `List<Producto>`.

2. Servicios genéricos en microservicios:
- Para manejar diferentes entidades (clientes, órdenes, facturas) usando repositorios o controladores genéricos.

3. Validadores de datos:
- Puedes crear un validador genérico para cualquier tipo de entrada.

4. Integración con bases de datos:
- Repositorios o DAOs que manejan diferentes tablas usando una estructura base genérica.

5. Procesamiento de colecciones con wildcards:
- Para trabajar con jerarquías de objetos (ej. `Empleado`, `Gerente`, `Director`), especialmente en reportes o filtros.

**Resumen...**

Los genéricos son parte fundamental de Java moderno, y su uso adecuado:

- ✅ Facilita el mantenimiento del código (evitas duplicar estructuras).
- ✅ Mejora la seguridad en compilación (menos errores en tiempo de ejecución).
- ✅ Permite crear componentes reutilizables para cualquier tipo de datos.

**🔥 Tip final** 
Si te encuentras repetiendo clases o métodos para diferentes tipos de datos,
o forzando castings, detente y piensa:

> *¿Podría simplificar esto usando genéricos?*

Adoptar genéricos en tus interfaces, repositorios y utilerías es una decisión técnica que ahorra tiempo a largo plazo.

---

#### 🧠 Actividad de reforzamiento


**🧩 Instrucciones**
1. Lee con atención cada caso hipotético que se presenta en las preguntas.
2. En cada situación, analiza qué opción es la más adecuada según el uso de genéricos en Java.
3. Selecciona la respuesta correcta entre las opciones propuestas.
4. Reflexiona por qué elegiste esa respuesta y cómo podrías aplicar esa lógica en un proyecto real.

**💡 Tip**
Si dudas entre dos opciones, piensa qué objetivo quieres lograr:
- ¿Necesitas leer o escribir datos en una colección?
- ¿Quieres controlar el tipo de dato o permitir mayor flexibilidad?

**🔹 Pregunta 1: Uso de genéricos en repositorios**

Estás creando una clase de repositorio que almacenará diferentes tipos de objetos (Clientes, Productos, Órdenes). Quieres evitar duplicar código y permitir que el mismo repositorio se adapte a cualquier tipo de entidad.

¿Qué enfoque deberías tomar?

a) Crear una clase base `Repositorio` que use `Object` y hacer castings cuando necesites recuperar elementos.
b) Crear una clase genérica `Repositorio<T>` y definir el tipo en cada uso.
c) Crear una clase `Repositorio` para cada entidad específica (RepositorioClientes, RepositorioProductos).


**🔹 Pregunta 2: Uso de wildcards para listas jerárquicas**

Tienes una jerarquía de clases donde `Empleado` es la clase base, y `Gerente` y `Director` son subclases. Debes diseñar un método que reciba una lista de empleados o cualquier subtipo para leer datos y generar un reporte.

¿Qué tipo de wildcard usarías?

a) `List<Empleado>`
b) `List<? extends Empleado>`
c) `List<? super Empleado>`

**🔹 Pregunta 3: Insertar elementos en una colección usando wildcards**

Estás desarrollando un módulo donde necesitas agregar objetos `Integer` a una lista, pero no sabes si la lista será de Integer, Number o incluso Object.
Tu único requisito es poder insertar números enteros.

¿Qué wildcard es el adecuado?

a) `List<? super Integer>`
b) `List<? extends Integer>`
c) `List<?>`

**🔹 Pregunta 4: Método genérico para validar diferentes tipos**
Vas a crear un método genérico que tome cualquier lista de elementos y valide su longitud. No necesitas saber qué tipo de elementos contiene, solo contar cuántos hay.

¿Cuál sería la mejor firma para el método?

a) `public <T> void validarLista(List<T> lista)`
b) `public void validarLista(List<?> lista)`
c) `public void validarLista(List<Object> lista)`


**🔹 Pregunta 5: Restricción de tipos en genéricos**
Debes crear una calculadora genérica que solo acepte números (Integer, Double, Float, etc.). El objetivo es prevenir que se usen tipos no numéricos como String.

¿Cómo aplicarías la restricción de tipos?

a) `<T> class Calculadora { ... }`
b) `<T extends Object> class Calculadora { ... }`
c) `<T extends Number> class Calculadora { ... }`

---

#### **📝 Cierre**

Hoy has aprendido a crear estructuras adaptables y seguras usando genéricos en Java. Ahora sabes que no necesitas escribir código diferente para cada tipo de dato, sino que puedes diseñar componentes que se ajusten a lo que el proyecto demande.

Además, exploraste cómo ampliar o limitar esa flexibilidad con los wildcards (`?`, `extends`, `super`), lo cual te permite:

- Leer o escribir colecciones de objetos relacionados,
- Definir límites en las clases o métodos para asegurar el tipo correcto.

**🔥 Tip final**
La próxima vez que diseñes una API, repositorio, o servicio compartido, considera si tu código puede beneficiar a otros módulos o equipos con una estructura genérica bien pensada.

Esto ademas de mejorar la reutilización del código, también reducira errores y acelerara el desarrollo cuando surgen nuevas necesidades.

Usar genéricos es una decisión que se nota cuando el proyecto crece. 🌱🚀

