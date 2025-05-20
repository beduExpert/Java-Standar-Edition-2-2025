🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 `Prework sesión 05`

<div align="center">
    <img src="../Imagenes/S05.jpg" alt="Bedu | Haz + con tu talento | JAVA STANDARD EDITION II">
</div>

##### **PREWORK**
#### **🟧 Sesión 05**
#### **Stream Reactivos**


##### 🔶 **Introducción**

¡Hola! 👋 

En sesiones anteriores aprendiste sobre Streams tradicionales en Java para procesar colecciones de forma fluida, y sobre procesos asíncronos con `CompletableFuture`.
Hoy daremos un paso más allá con la programación reactiva, una herramienta ideal para procesar flujos de datos continuos (como eventos, sensores, mensajes, servicios web) de manera eficiente y no bloqueante.

Imagina tener un sistema que recibe miles de datos por segundo y necesita procesarlos sin saturarse.
Ahí es donde la programación reactiva brissshaa ✨

---

#### 🎯 Objetivo

- Comprender qué es la programación reactiva y en qué se diferencia de los Streams tradicionales.
- Conocer los conceptos clave como Mono y Flux.
- Aprender a usar Project Reactor (o RxJava) para crear flujos reactivos.
- Aplicar operadores comunes (`map`, `flatMap`, `filter`) en flujos reactivos.
- Entender el control de backpressure para manejar grandes cantidades de datos sin saturar tu sistema

---

#### 📋 Instrucciones

Este Prework está diseñado para conocer el contenido que se practicará durante la sesión en vivo. **Por favor no lo omitas.**

Toma notas de lo que consideres relevante y guarda tus preguntas o dudas para resolverlas en la sesión.

Antes de arrancar, verifica que tu entorno de desarrollo esté listo. Es fundamental que tengas instalado IntelliJ IDEA Community Edition y el JDK (Java Development Kit) para trabajar sin interrupciones.

Si te surge alguna dificultad con la instalación o cualquier duda, no dudes en pedir ayuda a tu experto/a. ¡Estamos aquí para asegurarnos de que todo fluya sin problemas! 🚀

---

**Bienvenido/a**

Bienvenid@ al quinto Prework del módulo. A continuación, te presentamos el tiempo estimado de lectura por tema, para que puedas revisar todos los recursos al máximo: 

| **📖 Temario**                                   | **🕰️ Tiempo sugerido** |
|--------------------------------------------------|------------------------|
| Tema 01. Introducción a programación reactiva    | 10 min                 |
| Tema 02. Project Reactor / RxJava                | 10 min                 |
| Tema 03. Manejo avanzado de flujos               | 10 min                 |


**¡Comencemos! 🏁**

---
 
#### 📚 Tema 01. Introducción a programación reactiva
##### ⏳ 10 minutos de lectura

La programación reactiva es un paradigma de programación diseñado para manejar flujos de datos dinámicos y cambios en el tiempo, de manera asíncrona y no bloqueante.

🔄 **Analogía sencilla**:

- **Stream tradicional** → Es como leer un libro completo de principio a fin (los datos ya existen).

- **Programación reactiva** → Es como escuchar la radio: los datos (música, noticias) van llegando mientras escuchas, y no sabes cuándo terminarán.

🤓 Clave mental:  
En los Streams tradicionales esperas tener todos los datos para procesarlos.  
En la programación reactiva, procesas los datos conforme llegan, incluso si nunca se terminan.  


**🧠 ¿Por qué existe la programación reactiva?**  
Porque las aplicaciones modernas ya no solo procesan datos estáticos. Ahora:  
- Reciben eventos constantes (usuarios conectados, sensores, mensajes).  
- Se enfrentan a altas cargas de tráfico que pueden variar (usuarios en picos, horarios pico).  
- Necesitan responder rápido sin saturar los recursos.  

Ejemplo:

- 🚫 Sin programación reactiva: Si tienes mil usuarios conectados al mismo tiempo, el servidor puede saturarse si maneja cada uno de manera sincrónica.
- ✅ Con programación reactiva: El servidor regula el flujo, procesa sin bloquear y mantiene fluidez, incluso con picos de carga.

**🤜🤛 Stream API tradicional vs Programación reactiva**

| Característica         | Stream API tradicional                                | Programación reactiva                           |
|------------------------|-------------------------------------------------------|-------------------------------------------------|
| Tipo de datos          | Colecciones finitas (listas, sets)                    | Flujos infinitos o continuos (eventos, sensores)|
| Ejecución              | Sincrónica                                            | Asíncrona y no bloqueante                       |
| Control de velocidad   | No controla si llegan muchos datos (fluye sin límites)| Usa backpressure para regular el flujo          |
| Uso típico             | Procesar datos ya existentes (ej. lista de productos) | Procesar datos que siguen llegando (ej. usuarios conectados) |

**🧠 Patrones reactivamente dirigidos (Reactive Manifesto)**

1. **Responsivo**: El sistema responde rápido y mantiene la interactividad, sin importar la carga.
2. **Resiliente**: Si algo falla (ej. un servicio externo), el sistema se recupera sin caerse.
3. **Elástico**: Se adapta a cambios en la carga (ej. pasa de 100 a 1000 usuarios sin colapsar).
4. **Orientado a mensajes**: Todo se basa en eventos y mensajes, permitiendo una comunicación fluida.

**🧩 Ejemplo práctico**

🔹Stream tradicional

```java
List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5);
numeros.stream().map(n -> n * 2).forEach(System.out::println);
```

🔹Programación reactiva (pseudo-código)

```java
Flux<Integer> flujoNumeros = Flux.fromIterable(Arrays.asList(1, 2, 3, 4, 5));
flujoNumeros.map(n -> n * 2).subscribe(System.out::println);
```
👀 Diferencia:  
El Flux puede seguir emitiendo números indefinidamente, no está limitado a colecciones finitas.

**Resumen...**  

Ya viste que la programación reactiva es ideal para sistemas modernos que nunca paran de recibir datos:
usuarios conectados, sensores, flujos de eventos, etc.
A diferencia de los Streams tradicionales, reaccionas en tiempo real y controlas el flujo de datos para no saturarte.

**🔥 Tip final**  
Si tienes un sistema donde los datos nunca dejan de llegar (eventos, conexiones, mensajes), no los esperes todos.
Con programación reactiva, procesas al vuelo y mantienes la fluidez. 🚀


---

#### 📚 Tema 02. Project Reactor / RxJava
##### ⏳ 10 minutos de lectura

**📌 ¿Qué es Project Reactor y RxJava?**

🔹Project Reactor es la librería reactiva oficial de Spring.Diseñada para crear flujos de datos reactivos, es una herramienta moderna para manejar flujos asíncronos y continuos.

🔹RxJava es otra librería reactiva en Java, inspirada en el concepto de ReactiveX (Reactive Extensions), una familia de librerías que también existen en otros lenguajes (RxJS, RxSwift, etc.).

🎯 Ambas permiten:

- Lanzar y controlar flujos de datos que nunca se detienen (como mensajes, sensores, eventos).

- Trabajar de forma asíncrona y no bloqueante, manteniendo el sistema fluido.

🧐 ¿Cuál usar?

- Si trabajas con Spring Boot, Project Reactor es la opción natural (ya viene integrado).

- Si usas un stack sin Spring, RxJava es igual de potente y versátil.

**🧠 Conceptos clave: Mono y Flux**

**🧩 Mono**
- Mono es un flujo que emite 0 o 1 valor y luego se completa.
- Útil cuando esperas un solo resultado, como:
    - Respuesta de un API (ej. consultar el clima de una ciudad).
    - Lectura de un archivo pequeño (que solo lees una vez).

💭 Piensa en Mono como una promesa:
> *"Te doy un resultado... si lo tengo."*

**🧩 Flux**
- Flux es un flujo que emite 0, 1 o muchos valores, puede ser infinito.
- Útil cuando:
    - Recibes secuencias de eventos (usuarios conectados, mensajes de chat).
    - Procesas flujos de datos continuos (sensores, streams de video).

💭 Piensa en Flux como una cinta transportadora:
> *"Los datos siguen llegando... y tú los procesas al vuelo."*

**🤜🤛 Mono vs Flux (Aplicaciones reales)**


| Característica | Mono (0 o 1 valor)                       | Flux (0, 1 o muchos valores)                    |
|----------------|------------------------------------------|-------------------------------------------------|
| Uso común      | Respuesta de API, lectura de un archivo  | Mensajes de usuarios, datos de sensores         |
| Duración       | Corto (termina cuando emite el valor)    | Puede ser infinito                              |
| Ejemplo real   | Consultar el saldo bancario de un cliente| Leer constantemente la temperatura de sensores  |

**🔗 Operadores en acción: `map`, `flatMap`, `filter`**

En la programación reactiva, los operadores son como herramientas de una fábrica:  
Transforman, filtran y combinan los datos mientras fluyen.  

**🧪 Ejemplo 1: Filtrar y transformar datos con Flux**

```java
Flux<Integer> numeros = Flux.just(1, 2, 3, 4, 5);

numeros
    .filter(n -> n % 2 == 0)           // Filtra los pares (2, 4)
    .map(n -> n * 10)                  // Multiplica por 10 (20, 40)
    .subscribe(System.out::println);   // Imprime: 20, 40
```

🧐 ¿Qué sucede?
- Solo procesas números pares.
- Los transformas mientras fluyen.

**🔥 Tip**: Cada operador encadena operaciones sobre los datos sin detener el flujo.

**🧪 Ejemplo 2: Combinar flujos con flatMap**

```java
Flux<String> nombres = Flux.just("Ana", "Luis");

nombres
    .flatMap(nombre -> Flux.just(nombre.toUpperCase(), nombre.toLowerCase()))
    .subscribe(System.out::println);
```

🧐 ¿Qué pasa aquí?
- De cada nombre, generas dos resultados (mayúsculas y minúsculas).
- flatMap combina los flujos de cada nombre en un solo flujo continuo.

💡 `flatMap` es útil cuando una entrada genera varios resultados o otra secuencia asíncrona.

**🧩 Subscripción y ejecución**

En programación reactiva, nada se ejecuta hasta que te suscribes. Esto permite:

- Controlar el inicio del flujo.

- Conectar el productor y el consumidor cuando estés listo.

```java
Flux<Integer> flujo = Flux.just(1, 2, 3); // Configuras el flujo
flujo.subscribe(System.out::println);    // ¡Empieza el flujo!
```

Antes de la subscripción, el flujo es como una fábrica lista pero apagada. Cuando te suscribes, enciendes la máquina.

**🎨 Visualización del flujo reactivo**

```plaintext
[Producer] → (filter) → (map) → (flatMap) → [Consumer]
```
- **Productor**: Envía datos.
- **Operadores**: Transforman los datos mientras fluyen.
- **Consumidor:** Recibe y procesa los datos cuando llegan.

**🏆 Buenas prácticas en Reactor / RxJava**

✔️ Prefiere operadores reactivos (`map`, `flatMap`, `filter`) en lugar de lógica imperativa.  
✔️ No olvides manejar errores con `onErrorResume` o `doOnError`.  
✔️ Usa `take(n)` o `limitRate()` si quieres controlar cuántos elementos procesas.  

**Resumen...**

Ya conoces las bases de las librerías reactivas en Java:

➡️ Mono para un resultado único.

➡️ Flux para flujos continuos de datos.

➡️Operadores para transformar, filtrar o combinar esos flujos de forma asíncrona y elegante.

Sabes que el flujo solo arranca cuando te suscribes, dándote el control total.

**🔥 Tip final**  
Si necesitas combinar asincronía + flujos continuos + control preciso, Reactor (o RxJava) es la herramienta ideal 🫶

---

#### 📚 Tema 03. Manejo avanzado de flujos
##### ⏳ 10 minutos de lectura

Hasta ahora aprendiste a crear flujos reactivos y a procesarlos con operadores básicos como `map`, `flatMap` y `filter`. Pero en ambientes reales las cosas pueden complicarse:

- ¿Qué pasa si los datos llegan demasiado rápido?
- ¿Cómo combinas múltiples flujos?
- ¿Qué haces si necesitas controlar cuándo y cómo procesas esos datos?

Aquí es donde entran las técnicas avanzadas de manejo de flujos: backpressure, encadenamiento de operaciones, y casos de uso comunes que te preparan para proyectos de la vida real.

**🧐 ¿Qué es el backpressure?**

Es una técnica para decirle al productor:

> *"¡Ey! Estoy ocupado. Espera antes de mandarme más datos."*

En Project Reactor, puedes controlar esto con operadores como:

- `limitRate(n)` – Solo procesa n elementos a la vez.

- `onBackpressureBuffer()` – Almacena temporalmente los datos si hay sobrecarga.

- `onBackpressureDrop()` – Descarta los datos que no alcanzan a procesarse.

🧪 Ejemplo: Usar `limitRate()`

```java
Flux.range(1, 1000)
    .limitRate(10) // Solo procesa 10 elementos a la vez
    .doOnNext(n -> System.out.println("Procesando: " + n))
    .subscribe();
```

🛑 Esto evita que tu app se sature si hay picos de datos.

**🌟 Tip**: Usa backpressure cuando proceses grandes cantidades de datos o trabajes con fuentes externas veloces.

**🔗 Encadenamiento de operaciones**  

Una de las ventajas más poderosas del paradigma reactivo es la capacidad de encadenar operaciones, como si crearas una receta paso a paso.

```java
Flux.just("Ana", "Luis", "Mario")
    .map(String::toUpperCase)
    .filter(nombre -> nombre.startsWith("M"))
    .flatMap(nombre -> Flux.just(nombre, nombre.length()))
    .subscribe(System.out::println);
```

**🧐 ¿Qué hicimos?**

1. Transformamos a mayúsculas
2. Filtramos los que empiezan con "M"
3. Por cada uno, emitimos el nombre y su longitud

✅ Todo esto en una sola cadena fluida de operaciones.

**📦 Casos de uso comunes**

📌 1. Microservicios
- Flujo de solicitudes entrantes (ej. API Gateway)
- Cada microservicio reacciona a eventos y responde sin bloquear

📌 2. Sistemas de mensajería (Kafka, RabbitMQ)
- Mensajes entran continuamente
- El consumidor debe procesarlos de forma fluida
- Backpressure evita que se acumulen demasiados mensajes

📌 3. Interfaces reactivas (UI/UX)
- Cada clic o evento del usuario puede activar flujos
- Procesar eventos con Flux permite manejar muchos inputs sin saturar la UI

📌 4. Monitorización de sensores / IoT
- Sensores transmiten datos todo el tiempo
- Cada valor debe procesarse rápido y sin interrupciones

📌 5. Streams de video, chat o gaming en línea
- Transmisión en tiempo real
- Flujo constante de mensajes, posiciones, audio, etc.

**🔁 Cadena reactiva avanzada**

```plaintext
[Productor] → (map) → (filter) → (flatMap) → (limitRate) → [Consumidor]
```

Cada operador es un eslabón en la cadena.  
Puedes insertar control de flujo, transformaciones, o ramificar flujos si lo necesitas.  


**Resumen...**

Aquí aprendiste a dominar flujos grandes y complejos usando herramientas como:

- Backpressure para no saturarte
- Encadenamiento para mantener el código limpio
- Casos de uso reales para que sepas cuándo aplicar cada técnica

**🔥 Tip final**

> Cuando tu aplicación recibe muchos datos al mismo tiempo, no necesitas correr más rápido…
…necesitas un buen control del flujo. Y eso es justo lo que te da la programación reactiva. ⚡

---

#### 🧠 Actividad de reforzamiento

**Actividad: Mini reto de código**

Completa el siguiente flujo para que:
1. Filtre solo los números mayores a 5.
2. Los multiplique por 2.
3. Los imprima.

```java
Flux<Integer> numeros = Flux.range(1, 10);

numeros
    // Completa aquí
    .subscribe(System.out::println);
```
🌟 Por ultimo, explica brevemente qué ventaja ofrece el backpressure en un flujo reactivo y da un ejemplo real donde lo aplicarías.



---

#### **📝 Cierre**

¡Felicidades! 🎉 Hoy diste un paso más hacia el desarrollo de aplicaciones modernas, eficientes y resilientes.

Aprendiste que los datos ya no esperan. Llegan constantemente, en volúmenes masivos y a velocidades impredecibles.
Y en lugar de dejar que eso te abrume, ahora sabes cómo dominar ese flujo usando:

- Mono y Flux para modelar datos únicos o continuos.
- Operadores reactivos (`map`, `flatMap`, `filter`) para transformar los datos al vuelo.
- Backpressure para regular la velocidad y evitar saturaciones.
- Subscripciones controladas para decidir cuándo y cómo empieza el flujo.

La programación reactiva no es solo una herramienta técnica: es una forma de pensar.
Se trata de reaccionar a los cambios, adaptarse a las cargas y mantener tu aplicación fluida, viva y lista para responder en cualquier momento.

**🔥 Tip final**  
La próxima vez que pienses en colecciones finitas o en procesos bloqueantes, pregúntate:

> *¿Y si los datos nunca se detuvieran? ¿Estoy listo para procesarlos mientras fluyen?*

Si la respuesta es sí, entonces estás en el camino de la programación reactiva. 🚀  


---

⬅️ [**Anterior**](../../Sesion-04/Prework/Readme.md) | [**Siguiente**](../../Sesion-06/Prework/Readme.md)➡️  