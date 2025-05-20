🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 `Prework sesión 04`

<div align="center">
    <img src="../Imagenes/S04.jpg" alt="Bedu | Haz + con tu talento | JAVA STANDARD EDITION II">
</div>

##### **PREWORK**
#### **🟧 Sesión 04**
#### **Procesos asincronos**


##### 🔶 **Introducción**

👋 Bienvenido/a

¿Te imaginas si cada vez que pides comida a domicilio, tu día se detuviera hasta que llegara el repartidor?  
¡Qué pérdida de tiempo! 🕒  

Eso mismo pasa en las aplicaciones cuando hacen tareas que tardan demasiado y bloquean todo el flujo. Pero no te preocupes, aquí aprenderás cómo liberar a tus programas de esas esperas innecesarias usando **procesos asíncronos**.

Esta sesión te mostrará cómo trabajar con `CompletableFuture`, una herramienta de Java moderna para manejar tareas que pueden tardar, sin que tu aplicación se congele.

---

#### 🎯 Objetivo

- Entender las diferencias entre concurrencia y asincronía.
- Crear y manejar tareas asíncronas con CompletableFuture.
- Encadenar acciones asíncronas y controlar el flujo de trabajo.
- Manejar errores de forma elegante en procesos asíncronos.
- Aplicar la asincronía en casos reales como operaciones de red o archivos.

---

#### 📋 Instrucciones

Este Prework está diseñado para conocer el contenido que se practicará durante la sesión en vivo. **Por favor no lo omitas.**

Toma notas de lo que consideres relevante y guarda tus preguntas o dudas para resolverlas en la sesión.

Antes de arrancar, verifica que tu entorno de desarrollo esté listo. Es fundamental que tengas instalado IntelliJ IDEA Community Edition y el JDK (Java Development Kit) para trabajar sin interrupciones.

Si te surge alguna dificultad con la instalación o cualquier duda, no dudes en pedir ayuda a tu experto/a. ¡Estamos aquí para asegurarnos de que todo fluya sin problemas! 🚀

---

**Bienvenido/a**

Bienvenid@ al cuarto Prework del módulo. A continuación, te presentamos el tiempo estimado de lectura por tema, para que puedas revisar todos los recursos al máximo: 

| **📖 Temario**                          | **🕰️ Tiempo sugerido** |
|-----------------------------------------|------------------------|
| Tema 01. Asincronía vs concurrencia     | 10 min                 |
| Tema 02. Uso de `CompletableFuture`     | 10 min                 |
| Tema 03. Aplicaciones prácticas         | 10 min                 |


**¡Comencemos! 🏁**

---
 
#### 📚 Tema 01. Asincronía vs concurrencia
##### ⏳ 10 minutos de lectura

Aunque suenan parecido, asincronía y concurrencia NO son lo mismo.
Ambas ayudan a que las aplicaciones hagan varias cosas a la vez, pero lo logran de formas distintas.

**🧠 Diferencias clave**

| Concepto     | ¿Qué hace?                                                                               | Ejemplo de la vida real                            |
|--------------|------------------------------------------------------------------------------------------|----------------------------------------------------|
| Concurrencia | Ejecutar varias tareas a la vez (turnándose el procesador o en hilos separados).         | Un chef que cocina varios platos al mismo tiempo.  |
| Asincronía   | No esperar a que una tarea termine: lanzas algo, sigues, y recoges el resultado después. | Pides la comida y sigues trabajando mientras llega.|

Para poder entender mejor esto, hableremos de Latencia y tareas no bloqueantes 

**🟡 ¿Qué es la latencia?**  
La latencia es el tiempo que tarda una tarea en completarse desde que se inicia hasta que se obtiene una respuesta.  

Piensa en:
- Hacer una consulta a una API externa
- Leer un archivo pesado
- Esperar una respuesta de una base de datos remota

Todo eso toma tiempo. A veces es milisegundos, a veces varios segundos o más. Ese tiempo de espera es latencia.

**🔴 Tarea bloqueante: cuando el sistema se detiene**

Cuando una tarea es bloqueante, el flujo del programa se detiene hasta que esa tarea termina.

💬 Ejemplo realista:

- En una app que consulta un API del clima, si la llamada es bloqueante, el usuario no puede hacer nada más hasta que reciba la respuesta.

| Situación                       | ¿Qué pasa?                            |
|---------------------------------|---------------------------------------|
| API bloqueante (espera activa)  | La aplicación se queda congelada.     |
| Operación de archivo bloqueante | No puedes hacer otra cosa en ese hilo.|

🔍 Problema: El usuario siente que la app es lenta, incluso si solo espera unos segundos.  

**🟢 Tarea no bloqueante: cuando el sistema sigue funcionando**  

Una tarea no bloqueante lanza la operación (como la consulta al API), pero no espera a que termine para seguir haciendo otras cosas.

💬 Ejemplo realista:

- La app consulta el clima, pero el usuario sigue navegando por otras secciones mientras llega la respuesta.

| Situación                          | ¿Qué pasa?                                |
|------------------------------------|-------------------------------------------|
| API no bloqueante                  | El usuario sigue interactuando con la app.|
| Operación de archivo no bloqueante | El sistema puede atender otras tareas.    |

🔑 **Clave de la asincronía**  

Liberar el flujo principal mientras las tareas lentas trabajan en segundo plano.

> **⚡ Asincronía = tareas no bloqueantes + buen uso del tiempo**

**🎯 ¿Por qué importa esto?**  

- Mejora la experiencia del usuario: El sistema no se congela aunque algo tarde en completarse.
- Aprovechas mejor los recursos: En lugar de tener hilos esperando sin hacer nada, liberas esos recursos para otras tareas.

**💡 Tip mental**  
Si ves que tu app “espera” mucho, piensa en hacer la tarea no bloqueante usando asincronía.

**🔁 Uso combinado con hilos**

📌 ¿Qué son los hilos?  
Un hilo es una unidad de ejecución dentro de un proceso. Cuando tienes varios hilos, puedes realizar varias tareas al mismo tiempo (o casi, dependiendo del procesador).

**🔄 Concurrencia = varios hilos trabajando a la vez**  

La concurrencia suele involucrar múltiples hilos que trabajan de forma paralela o intercalada.

💬 Ejemplo realista:
- Un servidor web maneja varias solicitudes de clientes al mismo tiempo usando un hilo por solicitud.

⚠️ Importante: Cada hilo consume recursos (memoria, CPU). Si creas demasiados hilos, puedes saturar el sistema.

**🚀 Asincronía + hilos: cómo trabajan juntos**  

La asincronía puede usar hilos, pero no depende solo de ellos. Su objetivo es que una tarea no detenga el flujo, independientemente de cuántos hilos uses.

| Tipo                 | ¿Qué hace?                                                     |
|----------------------|----------------------------------------------------------------|
| Hilos (concurrencia) | Ejecutan varias tareas al mismo tiempo.                        |
| Asincronía           | Lanza una tarea y sigue con otra sin esperar, con o sin hilos. |

**🎯 ¿Cuándo usar hilos y cuándo asincronía?**

| Situación                             | ¿Qué usar?               |
|---------------------------------------|--------------------------|
| Varias tareas independientes a la vez | Concurrencia (hilos)     |
| Una tarea tarda pero no debe bloquear | Asincronía               |
| Mezcla de ambos casos                 | Concurrencia + asincronía |

**Resumen...**  

Ahora comprendes por qué la latencia es un desafío y cómo las tareas no bloqueantes permiten que el sistema siga funcionando sin congelarse.
También viste cómo la concurrencia (con hilos) y la asincronía pueden combinarse para lograr eficiencia y fluidez en tus aplicaciones.

**💡 Tip práctico:**
- Si algo tarda mucho, hazlo asíncrono.
- Si necesitas hacer muchas cosas a la vez, usa concurrencia.
- Si puedes hacer ambas, combínalas con cuidado. 😉

---

#### 📚 Tema 02. Uso de `CompletableFuture`
##### ⏳ 10 minutos de lectura

JEn las aplicaciones modernas, a menudo tienes tareas que tardan:
consultar una API, leer archivos pesados, o procesar grandes cantidades de datos.
Pero no quieres que tu app se quede esperando. Aquí es donde entra CompletableFuture, una herramienta poderosa de Java para lanzar, controlar y combinar tareas asíncronas de forma fluida y elegante.

Piensa en `CompletableFuture` como una promesa:  
*"Voy a hacer esto... y cuando esté listo, te aviso."*  

**🧩 ¿Qué es `CompletableFuture`?**  

Es una clase de Java que te permite:  
- Ejecutar tareas en segundo plano sin bloquear el hilo principal.
- Encadenar acciones que se ejecutan cuando la tarea esté lista.
- Combinar múltiples tareas y coordinar sus resultados.
- Manejar errores de forma limpia y sin romper tu código.

🔧 Es como tener un planificador inteligente que decide cuándo lanzar cada tarea y qué hacer con los resultados.

**🛠️ Creación y ejecución de tareas asíncronas**

🧪 Ejemplo básico

```java
CompletableFuture<String> tarea = CompletableFuture.supplyAsync(() -> {
    try {
        Thread.sleep(2000); // Simulando tarea tardada (2 segundos)
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    return "Resultado listo";
});
```

🔍 ¿Qué hace esto?
- Lanza una tarea asíncrona (en otro hilo) que devuelve un resultado después de 2 segundos.
- Devuelve un futuro (un objeto `CompletableFuture<String>`) que contendrá ese resultado cuando esté listo.

**🚨 Importante**  
La tarea **no bloquea el hilo principal**. Puedes seguir haciendo otras cosas mientras el resultado se procesa.  

**🔗 Encadenamiento con `thenApply`, `thenAccept`, `thenCompose`**

🧩 Encadenar acciones

```java
tarea
    .thenApply(resultado -> resultado.toUpperCase())  // Transforma el resultado
    .thenAccept(System.out::println);                // Lo imprime cuando esté listo
```

| Método         | ¿Qué hace?                                                     |
|----------------|----------------------------------------------------------------|
| `thenApply()`  | Transforma el resultado (y devuelve otro valor).               |
| `thenAccept()` | Consume el resultado (ejecuta una acción, no devuelve).        |
| `thenCompose()`| Encadena otra tarea asíncrona basada en el resultado anterior. |


🔧 Ejemplo con `thenCompose`:
```java
CompletableFuture<String> saludo = CompletableFuture.supplyAsync(() -> "Hola");

saludo
    .thenCompose(s -> CompletableFuture.supplyAsync(() -> s + " Mundo")) // Crea otra tarea asíncrona
    .thenAccept(System.out::println); // Resultado final: "Hola Mundo"
```
🤔 ¿Por qué `thenCompose`?  
Cuando el siguiente paso también lanza una tarea asíncrona, `thenCompose` evita tener futuros anidados.

⚠️ Manejo de errores con `exceptionally`  
Las cosas pueden fallar (una API no responde, un archivo no existe…). `CompletableFuture` te permite manejar esos errores sin romper tu app.

🧪 Ejemplo con error controlado
```java
CompletableFuture<String> tarea = CompletableFuture.supplyAsync(() -> {
    throw new RuntimeException("Algo salió mal");
});

tarea
    .exceptionally(e -> "Error controlado: " + e.getMessage()) // Maneja el error y devuelve valor alternativo
    .thenAccept(System.out::println); // Imprime: Error controlado: Algo salió mal
```
🎯 Con `exceptionally` puedes:  

- Capturar el error
- Devolver un valor alternativo para mantener el flujo funcionando

**🧠 ¿Cuándo usar `CompletableFuture`?**

| Situación                         | ¿Por qué usarlo?                                       |
|-----------------------------------|--------------------------------------------------------|
| Consulta a APIs que pueden tardar | Para no bloquear la interfaz o el flujo principal.     |
| Procesamiento de archivos grandes | Para permitir que otras tareas sigan mientras termina. |
| Coordinar múltiples tareas        | Puedes combinar resultados o manejar dependencias.     |

🔄 Flujo visual de `CompletableFuture`  

```plaintext
Lanza tarea asíncrona → Encadena pasos → Maneja errores → Resultado final
```

Como si lanzaras un boomerang:
- Sale volando (la tarea se ejecuta).
- Pasa por obstáculos (transformaciones, errores).
- Vuelve a ti con el resultado final.

🏆 Buenas prácticas con `CompletableFuture`

- Evita tareas muy pesadas en `supplyAsync` (delegalas a servicios o microservicios).
- Siempre maneja errores con `exceptionally` o `handle` (¡nunca confíes que todo saldrá bien!).
- Usa `thenCompose` si encadenas tareas asíncronas, y `thenApply` si solo transformas resultados.

**Resumen...**

Con `CompletableFuture`, tu código no espera: avanza.
Puedes lanzar tareas en segundo plano, transformar los resultados, encadenar procesos y manejar errores sin bloquear tu aplicación. Esto permite que tu sistema siga respondiendo mientras tareas lentas se ejecutan por detrás.

**💡 Tip final:**  
Cuando pienses:

>*"¿Qué hago mientras espero este resultado?"*

… la respuesta es: `CompletableFuture` lo hace por ti.

---

#### 📚 Tema 03. Aplicaciones prácticas
##### ⏳ 10 minutos de lectura

Ya sabes cómo funciona la asincronía y cómo lanzar tareas con `CompletableFuture`, pero... ¿dónde lo usarías realmente?

Aquí veremos casos concretos y comunes en el desarrollo de software donde la asincronía marca la diferencia:

- Operaciones de entrada/salida (I/O)
- Llamadas a servicios externos
- Consideraciones de diseño para que tu aplicación fluya sin bloqueos

**🔌 Operaciones I/O asíncronas**

**🧠 ¿Qué es I/O?**

I/O (Input/Output) son operaciones de entrada y salida de datos, como:

- Leer o escribir en archivos
- Consultar bases de datos
- Realizar solicitudes HTTP a APIs externas

Estas operaciones pueden tardar y, si no las manejas bien, bloquean tu aplicación.

🧪 Ejemplo: Simular escritura de archivo sin bloquear

```java
CompletableFuture<Void> escrituraArchivo = CompletableFuture.runAsync(() -> {
    System.out.println("Empezando a escribir en el archivo...");
    try {
        Thread.sleep(3000); // Simula una operación tardada (3 segundos)
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    System.out.println("¡Archivo escrito!");
});
```

🔍 ¿Qué pasa aquí?

- Lanza la tarea que simula escribir un archivo (tarda 3 segundos).
- La aplicación no se detiene mientras esto sucede.

🎯 ¿Dónde usarlo?

- Cuando guardas reportes o procesas grandes volúmenes de datos en segundo plano.

**💡 Tip:** Usa esto en sistemas donde guardar datos puede tardar, pero no quieres frenar al usuario.

🌐 Simulación de llamadas a servicios externos  
Imagina que tu aplicación consulta un servicio externo (como el clima o un sistema de pagos).  
Estas llamadas pueden tardar segundos y bloquear si no las haces bien.  

🧪 Ejemplo: Simular una consulta a un servicio externo

```java
CompletableFuture<String> consultaServicio = CompletableFuture.supplyAsync(() -> {
    System.out.println("Consultando servicio externo...");
    try {
        Thread.sleep(5000); // Simula una llamada tardada (5 segundos)
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    return "Respuesta del servicio externo";
});

consultaServicio.thenAccept(respuesta -> System.out.println("Respuesta recibida: " + respuesta));
```

🔍 ¿Qué sucede aquí?

- Lanzas la consulta al servicio (simulada con un retardo).
- Mientras el servicio responde, tu aplicación sigue viva (no bloqueada).
- Cuando el servicio responde, procesas el resultado.

🎯 ¿Dónde usarlo?

- Consultas a APIs (clima, geolocalización, pagos, etc.).
- Validaciones externas (verificar datos en otro sistema).

**💡 Tip:** Siempre maneja timeouts cuando llames servicios externos (no querrás esperar eternamente).

**🏗️ Consideraciones de diseño**

Usar asincronía es sumamente útil, pero como toda herramienta, hay que saber cuándo y cómo usarla. Aquí algunos principios clave:

| Buenas prácticas                    | ¿Por qué importa?                                                       |
|-------------------------------------|-------------------------------------------------------------------------|
| Usa asincronía donde aporte valor   | No todo necesita ser asíncrono. Úsalo en tareas lentas.                 |
| Controla el número de tareas        | Demasiadas tareas pueden saturar los recursos (hilos, memoria).         |
| Maneja errores y timeouts           | No asumas que todo saldrá bien. Siempre prevé fallos.                   |
| Coordina resultados si es necesario | Usa thenCombine, allOf, anyOf si varias tareas deben completarse juntas.|


**🔄 Ejemplo avanzado: Combinar tareas**
```java
CompletableFuture<String> servicioA = CompletableFuture.supplyAsync(() -> "Resultado A");
CompletableFuture<String> servicioB = CompletableFuture.supplyAsync(() -> "Resultado B");

CompletableFuture<Void> combinacion = servicioA
    .thenCombine(servicioB, (a, b) -> a + " y " + b)
    .thenAccept(System.out::println); // Resultado: Resultado A y Resultado B
```

🔍 ¿Qué hicimos aquí?
- Lanzamos dos tareas asíncronas en paralelo.
- Cuando ambas terminan, combinamos los resultados.

**💡 Tip:** Esto es útil cuando varios servicios deben responder antes de continuar.

**Resumen...**

Aquí viste cómo aplicar la asincronía en problemas reales:

- Leer archivos o consultar servicios sin bloquear tu app.
- Combinar múltiples tareas y coordinar sus resultados.
- Diseñar tu aplicación para responder siempre, incluso si algo tarda.

**💡 Tip final:** La asincronía es como tener múltiples asistentes:

>Cada uno trabaja en su tarea mientras tú sigues adelante.
Solo recoges los resultados cuando están listos.
Eso mantiene tu aplicación fluida, rápida y profesional.
---

#### 🧠 Actividad de reforzamiento

**Actividad: Elige la mejor estrategia – Asincronía vs Concurrencia vs Bloqueante**  

**🎯 Objetivo**  
Aplicar lo aprendido sobre procesos asíncronos y concurrencia para decidir cuál estrategia usar en situaciones reales.

**🧩 Instrucciones**
1. Lee cada caso hipotético que se presenta a continuación.
2. Reflexiona sobre las necesidades de la situación:
- ¿Es una tarea que puede tardar?
- ¿Debo atender muchas cosas a la vez?
- ¿Puedo permitir que se bloquee el flujo?
3. Elige la opción más adecuada entre las alternativas propuestas (Asincronía, Concurrencia o Bloqueante).
4. Justifica brevemente tu elección (2-3 líneas) explicando por qué elegiste esa estrategia.

**📝 Situaciones**

**1. Procesamiento de imágenes para perfiles de usuarios**

Tienes una aplicación donde los usuarios suben su foto de perfil. Cada vez que alguien sube una imagen, el sistema debe redimensionarla, optimizarla y guardarla.
Mientras esto ocurre, el usuario debería seguir navegando por la app sin bloqueos.

¿Qué usarías?
- **🔴 Bloqueante**: Detienes el flujo de la app hasta que termine el procesamiento de la imagen.
- **🟢 Asincronía**: Lanzas el procesamiento de la imagen y permites que el usuario siga navegando mientras se completa la tarea.
- **🟠 Concurrencia**: Procesas varias imágenes al mismo tiempo en distintos hilos, pero cada hilo sigue siendo bloqueante mientras termina.

**2. Servidor web que atiende a múltiples clientes**

Tienes un servidor que recibe solicitudes de cientos de usuarios conectados al mismo tiempo. Cada usuario puede pedir cosas diferentes: ver estadísticas, descargar archivos, etc.

¿Qué usarías?
- **🔴 Bloqueante**: Atiendes una solicitud a la vez, y los demás usuarios deben esperar.
- **🟢 Concurrencia**: Atiendes varias solicitudes al mismo tiempo, cada una en su propio hilo o proceso.
- **🟠 Asincronía**: Atiendes una solicitud y si hay alguna operación lenta (como consultar una base de datos), no bloqueas el hilo mientras esperas.

**3. Consulta a un servicio de clima**

Tu app consulta una API externa del clima que puede tardar 3-4 segundos en responder. Mientras tanto, el usuario debería seguir usando la app.

¿Qué usarías?

- **🔴 Bloqueante**: Detienes todo hasta que llegue la respuesta de la API.
- **🟠 Concurrencia**: Creas un hilo dedicado para esa consulta, pero el hilo sigue bloqueado hasta recibir la respuesta.
- **🟢 Asincronía**: Lanzas la consulta al API y sigues permitiendo que el usuario interactúe con la app, sin bloquear el flujo.

**4. Procesamiento masivo de facturas**

Tu sistema recibe 500 facturas que deben ser validadas, procesadas y reportadas. Quieres que el proceso sea rápido y eficiente.

¿Qué usarías?

- **🔴 Bloqueante**: Procesas una factura a la vez, sin hacer nada más hasta que termines todas.
- **🟢 Concurrencia**: Procesas varias facturas al mismo tiempo en distintos hilos (distribuyes la carga).
- **🟠 Asincronía**: Procesas las facturas sin bloquear otras operaciones del sistema (puedes seguir atendiendo usuarios mientras procesas).

**5. Sistema de monitoreo de sensores**

Diseñas una app que monitorea sensores en tiempo real (temperatura, presión, etc.). Cada sensor envía datos cada segundo, y necesitas procesarlos y mostrarlos continuamente.

¿Qué usarías?

- **🔴 Bloqueante**: Procesas los datos de un sensor a la vez, deteniendo el resto mientras terminas.
- **🟢 Concurrencia**: Cada sensor tiene su propio hilo independiente, procesando los datos al mismo tiempo.
- **🟠 Asincronía**: Recibes los datos y los procesas sin bloquear el flujo general, permitiendo que otros sensores sigan enviando información.

---

#### **📝 Cierre**

¡Felicidades! 🎉  
Ahora sabes cómo hacer que tus programas sean más ágiles y eficientes usando asincronía.

No todo tiene que esperar. Puedes lanzar tareas, seguir trabajando, y recoger los resultados cuando estén listos.

Lo mejor de todo es que puedes manejar errores sin romper tu flujo, encadenar acciones y crear aplicaciones resistentes y rápidas.

💡 Por último:  
Cuando tu app tenga que hacer algo lento o externo, déjala fluir. Usa asincronía para que el usuario nunca sienta que espera… aunque tu sistema siga trabajando por detrás.

---

⬅️ [**Anterior**](../../Sesion-03/Prework/Readme.md) | [**Siguiente**](../../Sesion-05/Prework/Readme.md)➡️  