🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 `Prework sesión 08`

<div align="center">
    <img src="../Imagenes/S08.jpg" alt="Bedu | Haz + con tu talento | JAVA STANDARD EDITION II">
</div>

##### **PREWORK**
#### **🟧 Sesión 08**
#### **Buenas prácticas**


##### 🔶 **Introducción**

👋 Bienvenido/a

El código que funciona es solo el primer paso 🧑‍💻.  
El verdadero reto comienza cuando el proyecto crece, más personas se suman al equipo, y necesitas leer, modificar o escalar ese código semanas o meses después.

Ahí es donde entran las buenas prácticas. Son esas pequeñas decisiones diarias (cómo nombras una variable, cómo estructuras tus paquetes, cómo pruebas tu lógica) que marcan la diferencia entre un proyecto que fluye y uno que se convierte en un dolor de cabeza 🤯.

Hoy, en esta sesión, vamos a revisar esas buenas costumbres del desarrollo en Java que no solo te ayudarán a evitar errores comunes, sino también a facilitar el trabajo en equipo, mejorar la calidad de tu código y reducir el tiempo de depuración. Abordaremos tres pilares fundamentales para que tu código no solo funcione, sino que trascienda en el tiempo:

1. Diseño y convenciones → Porque el código es un lenguaje compartido.
2. Pruebas y depuración → Porque prevenir errores es mejor que corregirlos.
3. Organización y control de versiones → Porque trabajar en equipo requiere estructura y orden.

🔧 Diseño limpio, pruebas confiables, y control de versiones bien gestionado son las herramientas invisibles 🛠️ que harán que tu día como desarrollador sea más ligero y productivo. 🚀

---

#### 🎯 Objetivo

- Reconocer la importancia de seguir convenciones de código y aplicar refactorización básica.
- Familiarizarte con JUnit 5, Mockito y logs con SLF4J para realizar pruebas unitarias y depuración.
- Aplicar buenas prácticas de organización del código y control de versiones usando Git y GitHub.

---

#### 📋 Instrucciones

Este Prework está diseñado para conocer el contenido que se practicará durante la sesión en vivo. **Por favor no lo omitas.**

Toma notas de lo que consideres relevante y guarda tus preguntas o dudas para resolverlas en la sesión.

Antes de arrancar, verifica que tu entorno de desarrollo esté listo. Es fundamental que tengas instalado IntelliJ IDEA Community Edition y el JDK (Java Development Kit) para trabajar sin interrupciones.

Si te surge alguna dificultad con la instalación o cualquier duda, no dudes en pedir ayuda a tu experto/a. ¡Estamos aquí para asegurarnos de que todo fluya sin problemas! 🚀

---

**Bienvenido/a**

Bienvenid@ al octavo Prework del módulo. A continuación, te presentamos el tiempo estimado de lectura por tema, para que puedas revisar todos los recursos al máximo: 

| **📖 Temario**                                            | **🕰️ Tiempo sugerido** |
|-----------------------------------------------------------|------------------------|
| Tema 01. Principios de diseño en Java                     | 5 min                 |
| Tema 02. Pruebas unitarias y depuración                   | 10 min                 |
| Tema 03. Organización del código y control de versiones   | 10 min                 |


**¡Comencemos! 🏁**

---
 
#### 📚 Tema 01. Principios de diseño en Java 
##### ⏳ 5 minutos de lectura

**📌 ¿Por qué importa el diseño del código?**

Cuando hablamos de diseño en código, no nos referimos solo a hacer que funcione 🟢, sino a hacerlo entendible, mantenible y escalable 🏗️.

💬 Piensa en esto  
Un código mal diseñado puede funcionar hoy, pero se convertirá en difícil de entender mañana (incluso por ti mismo 😅).  
Un buen diseño, en cambio, permite que otros puedan leerlo, modificarlo y mejorarlo sin temores.  

**🎯 Objetivo**  
Escribir código que sea tan fácil de leer como de ejecutar.  

**🔧 Convenciones de código en Java**

Seguir las convenciones de código es como hablar el mismo idioma en un equipo. Java tiene estándares ampliamente aceptados que te permiten escribir código uniforme.

🧪 Ejemplo: Nombres y estilos

- Clases: Usan UpperCamelCase → `Cliente`, `ProductoServicio`.
- Métodos y variables: Usan lowerCamelCase → `obtenerDatos()`, `totalCompra`.
- Constantes: Usan MAYÚSCULAS_CON_GUIONES → `PI`, `MAX_INTENTOS`.

Indentación: Usa 4 espacios por nivel (no tabs).

**🤓 ¿Qué aporta?**

1. Mejora la legibilidad 👀.
2. Facilita trabajar en equipo 🤝.
3. Reduce errores por confusiones 🚫.

💡 Herramientas recomendadas:

✅ Checkstyle o SonarLint → Analizan tu código y te avisan si no sigues las convenciones.

**🔧 Refactorización básica**

Refactorizar es el proceso de mejorar la estructura interna del código, sin cambiar lo que hace.
Se busca hacerlo más limpio, más legible y más fácil de mantener.

💬 Analiza esto:

```java
// Antes
if (edad >= 18) {
    System.out.println("Es mayor de edad");
} else {
    System.out.println("Es menor de edad");
}
```
```Java
// Después (refactorizado)
public void imprimirEstadoEdad(int edad) {
    String estado = (edad >= 18) ? "mayor" : "menor";
    System.out.println("Es " + estado + " de edad");
}
```

**🤓 ¿Qué se ganó?**

- Código más compacto y expresivo.
- Separación de lógica en métodos claros.

**🔥 Tip**  
Refactoriza constantemente mientras desarrollas. Es mejor hacer pequeños ajustes continuos que dejar que el código se deteriore con el tiempo.

**🔧 Introducción a patrones de diseño (GoF)**

Los patrones de diseño son soluciones probadas a problemas comunes en el desarrollo de software. Fueron documentados por los "Gang of Four" (GoF) en su famoso libro, y ayudan a:

- Organizar mejor el código 🏗️,
- Facilitar el mantenimiento 🛠️,
- Evitar reinventar la rueda 🔄.

**🧩 Ejemplo básico: Patrón Singleton**

🤔 ¿Qué resuelve?
Garantiza que solo exista una instancia de una clase.

```java
public class ConexionDB {
    private static ConexionDB instancia;

    private ConexionDB() {} // Constructor privado

    public static ConexionDB obtenerInstancia() {
        if (instancia == null) {
            instancia = new ConexionDB();
        }
        return instancia;
    }
}
```

🤓 ¿Cuándo usarlo?

- Para conexiones de base de datos,
- Configuraciones globales,
- O cuando una sola instancia debe controlar un recurso compartido.

**Resumen...**

Seguir convenciones de código, refactorizar regularmente, y conocer patrones de diseño son herramientas diarias que te permiten escribir código sostenible y fácil de mantener.

**🔥 Tip final**

✅ Asegúrate de que tu equipo acuerde un estándar de codificación y lo respete en todo el proyecto.

✅ No esperes a que el código esté desordenado: refactoriza poco a poco mientras desarrollas.

✅ Empieza por patrones de diseño sencillos (como Singleton o Factory), y adopta otros según las necesidades del proyecto.

---

#### 📚 Tema 02. Pruebas unitarias y depuración
##### ⏳ 10 minutos de lectura

**📌 ¿Qué rol juegan las pruebas y los logs en proyectos reales?**

Cuando trabajas en proyectos que crecen, las pruebas y los logs no son un extra, sino parte esencial del ciclo de desarrollo.

- 🧪✅ Las pruebas aseguran que cada parte funcione como se espera .
- 📝 Los logs te permiten entender qué está haciendo tu aplicación en cada momento .

**¿Por qué es tan importante?**

1. 💰 Porque el coste de arreglar un error es mucho menor si lo detectas pronto (fase de desarrollo) que si llega a producción.
2. 🧭 Y si llega a producción, los logs son tu mejor aliado para entender qué salió mal.

**🧩 Tipos de pruebas automáticas**

1. **Pruebas unitarias** → Verifican unidades pequeñas (ej. métodos).
2. **Pruebas de integración** → Verifican que varias partes del sistema trabajen juntas (ej. servicio + base de datos).
3. **Pruebas de extremo a extremo (E2E)** → Simulan flujos completos del usuario.

**🔥 Tip**  

✔️ Prioriza las pruebas unitarias para validar la lógica interna.  
✔️ Complementa con pruebas de integración para verificar que todo se conecte bien.  

**🧩 JUnit 5: Más allá de lo básico**

JUnit 5 es el framework estándar en Java para escribir pruebas unitarias 🧪.
Aquí no solo veremos cómo probar métodos simples, sino cómo cubrir escenarios más completos, como verificar excepciones o probar múltiples casos con una sola prueba. Esto te permitirá reforzar la calidad de tu código sin agregar esfuerzo innecesario.

**🛠️ Pruebas con excepciones**

Supongamos que tienes un método que lanza una excepción si el parámetro es nulo:

```java
public class Calculadora {
    public int dividir(int a, int b) {
        if (b == 0) {
            throw new IllegalArgumentException("No se puede dividir por cero");
        }
        return a / b;
    }
}
```

Prueba unitaria para excepciones:
```java
@Test
void pruebaDivisionPorCero() {
    Calculadora calc = new Calculadora();
    assertThrows(IllegalArgumentException.class, () -> calc.dividir(10, 0));
}
```

🤔 ¿Qué se valida?  
Que el método lance la excepción esperada si se intenta dividir por cero.  

**🛠️ Pruebas parametrizadas (mismo test con varios datos)**
```java
@ParameterizedTest
@CsvSource({
    "2, 3, 5",
    "10, 5, 15",
    "0, 0, 0"
})
void pruebaSumaParametrizada(int a, int b, int esperado) {
    Calculadora calc = new Calculadora();
    assertEquals(esperado, calc.sumar(a, b));
}
```

🤔¿Qué logras?

⚡Evitas repetir código de pruebas.  
⚡Ejecutas la misma prueba con diferentes datos.  

**🧩 Mockito: Más allá de los mocks simples**

En proyectos reales, probar la lógica de un servicio suele implicar depender de otros componentes (repositorios, APIs, etc.).  
Mockito es una herramienta que permite simular esas dependencias 🔌, para que pruebes en aislamiento solo lo que te interesa.  
Vamos a ver cómo crear mocks y verificar que las interacciones entre componentes ocurran como deberían.  

**🛠️ Validar interacciones entre servicios**

Supongamos que tu UsuarioService debe guardar un usuario y enviar una notificación:

```java
public class UsuarioService {
    private final UsuarioRepository repo;
    private final NotificacionService notificaciones;

    public UsuarioService(UsuarioRepository repo, NotificacionService notificaciones) {
        this.repo = repo;
        this.notificaciones = notificaciones;
    }

    public void registrarUsuario(Usuario usuario) {
        repo.save(usuario);
        notificaciones.enviarCorreo(usuario);
    }
}
```

Prueba con Mockito para validar interacciones:

```java
@Test
void pruebaRegistrarUsuario() {
    UsuarioRepository repoMock = mock(UsuarioRepository.class);
    NotificacionService notificacionesMock = mock(NotificacionService.class);
    UsuarioService servicio = new UsuarioService(repoMock, notificacionesMock);

    Usuario usuario = new Usuario(1L, "Luis");
    servicio.registrarUsuario(usuario);

    // Verifica que se llamó a los métodos esperados
    verify(repoMock).save(usuario);
    verify(notificacionesMock).enviarCorreo(usuario);
}
```

🤔 ¿Qué se valida?

Que el servicio:
- ⚡Guarda al usuario,
- ⚡Envía la notificación.

Esto garantiza el flujo de interacciones, sin necesidad de conectar servicios reales.

**🧩 Logs en contexto: Depuración avanzada**

Los logs son la ventana al comportamiento de tu aplicación en tiempo real 📜. Pero no basta con imprimir mensajes: necesitas organizar los niveles de log, agregar contexto relevante y adaptarlos al entorno. Para gestionar logs de forma profesional, Java utiliza frameworks de logging.

**🛠️ ¿Qué es SLF4J?**
- SLF4J (Simple Logging Facade for Java) es una fachada de logging, es decir, una capa intermedia que unifica la forma en la que escribes logs, sin importar qué framework de logging real uses detrás (puede ser Logback, Log4J, etc.).

💬 Piensalo asi:  
SLF4J es como una interfaz universal de enchufes. No importa si estás en Europa o América, SLF4J te da el mismo conector, y luego tú decides qué enchufe local usar (Logback, Log4J...).

🤔 ¿Por qué usar SLF4J?

✅ Porque te permite cambiar de backend de logging sin modificar tu código.  
✅ Es el estándar en proyectos Java modernos, especialmente en aplicaciones con Spring Boot (que usa SLF4J + Logback por defecto).  

**🛠️ Buenas prácticas en logging:**

1. No loguees todo indiscriminadamente (ej. no registres contraseñas).
2. Usa niveles adecuados (no pongas todo en `info`):
    - debug para desarrollo
    - warn para advertencias
    - error para fallos críticos.

Agrega contexto relevante: IDs, nombres, estados.

**Ejemplo aplicado con contexto:**
```java
logger.info("Guardando usuario: ID={}, nombre={}", usuario.getId(), usuario.getNombre());
```

🤔 ¿Por qué es útil?

- Si ocurre un error, sabes qué usuario estaba siendo procesado.
- Reduce tiempo de búsqueda cuando revisas los logs.

**🧠 ¿Cómo integrar pruebas y logs en tu flujo de trabajo?**

1. Automatiza las pruebas → Usa Maven o Gradle para ejecutar las pruebas antes de cada despliegue.
2. Configura logs por entorno →
    - Desarrollo: Usa `debug` para ver más detalles.
    - Producción: Usa `info`, pero registra errores críticos con `error`.

3. Incluye pruebas en tu CI/CD → Asegúrate de que el pipeline de despliegue no continúe si fallan las pruebas.

CI/CD son prácticas de automatización en el desarrollo de software que ayudan a integrar, probar y desplegar el código de forma continua. Son utiles por que detectan errores temprano 🧪, reducen los tiempos de entrega 🚀 y minimizan errores humanos en despliegues ⚠️

| 🏷️ Sigla     | 📖 Significado | ⚙️ ¿Qué hace?|
|---------------|---------------|----------------|
| **CI**   | Integración Continua | Automatiza la integración del código de todos los desarrolladores. Corre pruebas automáticas cada vez que subes cambios al repositorio (ej. GitHub). Esto detecta errores pronto.|
| **CD**   | Entrega/Despliegue Continua | Automatiza el despliegue del software en ambientes (desarrollo, pruebas, producción). Así puedes liberar nuevas versiones rápidamente y con menos riesgo.|

**🎨 Visualización del flujo de pruebas y depuración**
```plaintext
[Código fuente]
     │
[Pruebas unitarias automatizadas] ←→ [Logs estratégicos]
     │
  [Pipeline de despliegue]
     │
[Ambientes controlados (dev, prod)]
```

**Resumen...**

Las pruebas automáticas y los logs son pilares invisibles de cualquier proyecto robusto:

- JUnit 5 y Mockito permiten detectar errores en el momento correcto.
- SLF4J + Logback ofrecen visibilidad del comportamiento del sistema.

**🔥 Tip final**  
Integra pruebas en tu flujo de trabajo diario, y asegúrate de que los logs cuenten la historia completa de lo que ocurre en la aplicación.

Porque prevenir y detectar problemas temprano es lo que distingue un proyecto bien gestionado.

---

#### 📚 Tema 03. Organización del código y control de versiones
##### ⏳ 10 minutos de lectura

**📌 ¿Por qué es importante organizar el código y controlar versiones?**
Tener código bien organizado es como tener una oficina ordenada:

- 🗂️ Encuentras lo que buscas rápido 
- 🔄 Evitas duplicar archivos innecesarios 
- 🔍 Y si otra persona entra al proyecto, entiende cómo está estructurado sin perderse.

Pero no solo es cuestión de orden local. En proyectos reales, trabajas en equipo, y cada quien aporta cambios al código constantemente.  
Ahí es donde el control de versiones (Git) entra en acción: permite gestionar los cambios, combinarlos, revisarlos y retroceder si algo sale mal.  

💡 Juntos, la organización del código y el control de versiones hacen que tu proyecto escale sin caos.

**🏗️ Organización de proyectos en Java**  
Java sigue convenciones estándar para organizar el código. Aquí te muestro la estructura típica para un proyecto Java moderno con Spring Boot:

```plaintext
src/
 └── main/
      ├── java/
      │    └── com/miempresa/miproyecto/
      │          ├── controller/ (Controladores HTTP)
      │          ├── service/ (Lógica de negocio)
      │          ├── repository/ (Acceso a datos)
      │          └── model/ (Modelos de datos)
      └── resources/
           ├── application.properties (Configuración)
           └── static/ y templates/ (para archivos web si aplica)
```

**🛠️ Buenas prácticas de organización**

1. Separa las capas:
    - Controladores → Gestionan las peticiones HTTP.
    - Servicios → Contienen la lógica de negocio.
    - Repositorios → Acceden a la base de datos.
    - Modelos → Representan las entidades.

2. Respeta las convenciones de nombres:
    - controller, service, repository, etc.

3. Evita crear paquetes genéricos como "utils" sin sentido.
Solo crea módulos utilitarios específicos si realmente comparten lógica transversal.

**🔥 Tip**  
Si un paquete empieza a crecer demasiado, considera subdividirlo por función.  

**🔗 Control de versiones con Git: ¿cómo y por qué?**

Git es el sistema de control de versiones más usado 🐙. Permite:

- Guardar cada cambio en el código 📜.
- Volver atrás si algo falla 🔄.
- Trabajar en ramas separadas sin interferir con el trabajo de otros.

💬 Piensalo asi:
Git es como un historial de cambios en un documento:
- Puedes ver quién hizo qué,
- Comparar versiones,
- O recuperar una versión anterior si algo se rompe.

**🛠️ Flujo profesional con Git (básico):**

1. Clonar un repositorio:

```bash
git clone https://github.com/miempresa/miproyecto.git
```
2. Crear una rama para trabajar:

```bash
git checkout -b feature/agregar-servicio-usuario
```
3. Agregar y registrar cambios:

```bash
git add .
git commit -m "Agrega servicio para gestionar usuarios"
```

4. Enviar tus cambios al repositorio remoto:

```bash
git push origin feature/agregar-servicio-usuario
```

**🏷️ ¿Qué es un flujo Git profesional?**

Un flujo de trabajo típico es Git Flow o Trunk-based Development:

- Rama principal (`main`) → Siempre tiene el código estable y listo para producción.
- Ramas de features → Para desarrollar nuevas funcionalidades sin afectar main.
- Pull Requests (PRs) → Para revisar y aprobar los cambios antes de integrarlos.

**🎨 Visualización del flujo Git básico**
```plaintext
main  ◄───── merge ─────  feature/crear-reporte
 │                           ▲
 │                           │
 │                   desarrollo y commits
```

**🛠️ Buenas prácticas con Git:**

1. Haz commits pequeños y descriptivos 📝:
    - ❌ "Cambios varios"
    - ✅ "Corrige validación de correo en registro de usuarios"
2. Trabaja siempre en ramas (no en `main` directamente).
3. Sincroniza frecuentemente con el repositorio remoto 🔄 (evitas conflictos).
4. Revisa los cambios antes de hacer merge (Pull Requests).

**💡 Herramientas útiles**

- **GitHub / GitLab / Bitbucket**→ Gestionan repositorios remotos y PRs.
- **GitKraken, Sourcetree**→ Interfaces visuales para Git (por si prefieres evitar la línea de comandos).

**Resumen...**  
Mantener tu proyecto ordenado 🗂️ y tener un flujo de control de versiones bien gestionado 🐙 son las bases para trabajar en equipo sin caos,
y para que el proyecto crezca de manera sostenible.


**🔥 Tip final**

✅ Respeta las convenciones de estructura para que todo el equipo hable el mismo idioma.

✅ Usa Git de forma disciplinada: te ahorrará dolores de cabeza cuando los cambios se acumulen.

---

#### 🧠 Actividad de reforzamiento

**🎯 Objetivo**
- Identificar malas prácticas en la organización del código y estilo de programación en Java.
- Aplicar correcciones que mejoren la estructura, legibilidad y mantenibilidad del código.
- Justificar las decisiones de mejora, conectando con los principios de diseño y convenciones revisados.

**🧩 Instrucciones**
1. Analiza el siguiente fragmento de código mal organizado y detecta al menos 5 malas prácticas relacionadas con:
    - Convenciones de nombres.
    - Organización de métodos y responsabilidades.
    - Falta de separación entre capas (controlador, servicio, repositorio).

2. Corrige el código, aplicando las buenas prácticas aprendidas.
3. Justifica brevemente (en comentarios o aparte) por qué realizaste cada cambio.

Este es el codigo:

```java
package app;

import java.util.List;
import java.util.ArrayList;

public class usercontroller {

    private List<Usuario> listaUsuarios = new ArrayList<>();

    public void save(Usuario u){
        if(u.getName() == null){
            System.out.println("Error");
        } else {
            listaUsuarios.add(u);
        }
    }

    public void printUsers(){
        for(Usuario u : listaUsuarios){
            System.out.println(u.getName());
        }
    }

    public static void main(String[] args){
        usercontroller uc = new usercontroller();
        Usuario u = new Usuario();
        u.setName("Mario");
        uc.save(u);
        uc.printUsers();
    }
}

class Usuario {
    private String name;

    public String getName(){
        return name;
    }
    public void setName(String name){
        this.name = name;
    }
}
```

**💡 Sugerencia:**

- Aplica separación de capas → Crea una clase servicio para manejar la lógica de usuarios.

- Mejora los nombres → Usa UpperCamelCase para las clases y lowerCamelCase para métodos.

- Maneja los errores adecuadamente → Usa excepciones o mensajes claros.

---

#### **📝 Cierre**

A lo largo de esta sesión, exploraste cómo las buenas prácticas son el cimiento de un proyecto saludable y escalable.
No se trata solo de hacer que el código funcione, sino de cómo lo escribes, pruebas, organizas y gestionas a lo largo del tiempo.

- Aplicaste principios de diseño como el SRP, acoplamiento y cohesión, y inyección de dependencias, que permiten que tu código crezca sin volverse una carga.

- Integraste pruebas unitarias (JUnit 5) y mocks (Mockito) para prevenir errores y validar la lógica de negocio, apoyado por logs bien estructurados (SLF4J) que te ayudan a entender el comportamiento del sistema en cualquier entorno.

- Finalizaste revisando cómo organizar tu proyecto Java de manera profesional y cómo controlar las versiones con Git, para que trabajar en equipo o volver atrás sea seguro y predecible.


**🔥 Tip final**  
Antes de iniciar cualquier nueva funcionalidad, hazte estas tres preguntas:

1. ¿Está clara la responsabilidad de cada módulo que tocaré? (Diseño)

2. ¿Cómo voy a probar que lo que hago no rompe otra cosa? (Pruebas)

3. ¿Estoy versionando y documentando mis cambios correctamente? (Git)

Porque las buenas prácticas no solo mejoran tu código hoy, sino que facilitan el trabajo mañana, para ti y para tu equipo.

**🚀 Un proyecto ordenado y probado es un proyecto que avanza sin fricciones.**

---

⬅️ [**Anterior**](../../Sesion-07/Prework/Readme.md) | [**Siguiente**](../../Sesion-09/Prework/Readme.md)➡️  