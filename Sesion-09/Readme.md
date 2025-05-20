🏠 [**Inicio**](../Readme.md) ➡️ / 📖 [**Sesión 09**](../Readme.md) ➡️ / 📝 `Sesión 09: Desarrollo del microservicio de préstamos personales`

---

## 🎯 Objetivo

Construir, ejecutar y probar un microservicio funcional en Java para la gestión de préstamos personales, integrando los conocimientos adquiridos en todas las sesiones previas de Java SE II: bases de datos (JPA + H2), concurrencia (CompletableFuture), programación funcional (Streams), logs en contexto (SLF4J) y pruebas unitarias (JUnit + Mockito).

---

## 🧱 Estructura del sistema

Durante la sesión, utilizaremos las siguientes clases y componentes:

| Clase                   | Descripción |
|--------------------------|-------------|
| `Prestamo` (modelo)       | Representa un préstamo personal (cliente, monto, estado). |
| `PrestamoRepository`      | Interfaz JPA para interactuar con la base de datos H2. |
| `PrestamoService`         | Lógica para crear préstamos, evaluarlos (de forma asíncrona) y cambiar su estado. |
| `PrestamoController`      | Exposición de endpoints REST para crear, consultar y filtrar préstamos. |
| `SLF4J`                   | Registro de logs en contexto durante la evaluación y los cambios de estado. |
| `JUnit + Mockito`         | Pruebas unitarias para validar la lógica del servicio y garantizar su correcto funcionamiento. |

---

## 🧭 Creación del proyecto con Spring Initializr

1. Ingresa a [https://start.spring.io](https://start.spring.io/)
2. Configura lo siguiente:
   - **Project**: Maven
   - **Language**: Java
   - **Spring Boot**: 3.2.x (última versión estable)
   - **Group**: `com.prestamos`
   - **Artifact**: `MicroservicioPrestamos`
   - **Java**: 17
3. Agrega estas dependencias:
   - Spring Web
   - Spring Data JPA
   - H2 Database
   - Spring Boot DevTools
   - Spring Boot Starter Test
4. Haz clic en "Generate" y abre el proyecto en IntelliJ IDEA.

---

## 📦 Configuración de dependencias adicionales (Maven)

Agrega estas dependencias manualmente en tu archivo `pom.xml`, ya que no vienen por defecto en Spring Initializr:

```xml
<dependencies>
    <!-- Reactor Core (para programación reactiva y uso de CompletableFuture más avanzado) -->
    <dependency>
        <groupId>io.projectreactor</groupId>
        <artifactId>reactor-core</artifactId>
        <version>3.6.11</version>
    </dependency>

    <!-- SLF4J API (para logs en contexto) -->
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>2.0.17</version>
    </dependency>

    <!-- SLF4J Simple (implementación básica de SLF4J para pruebas locales) -->
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-simple</artifactId>
        <version>2.0.17</version>
    </dependency>
</dependencies>
```

---

✅ **Notas finales de aclaración**:
- `Spring Boot Starter Test` **ya integra** JUnit 5 y Mockito, por eso no necesitas agregarlos manualmente.
- `reactor-core` se agrega porque vas a usar programación reactiva o modelos asincrónicos más robustos (`Mono`, `Flux`, etc.).
- `slf4j-api` + `slf4j-simple` son para controlar los logs en un ambiente simple (en producción deberías cambiar a Logback o Log4j si fuera necesario).

---

## 📦 Paso 2: Crear la entidad `Prestamo.java`

Aquí aplicamos:
- POO (atributos, métodos).
- JPA para mapear a base de datos.
- Enum para el estado del préstamo.

```java
package com.prestamos.model;

import jakarta.persistence.*;

@Entity
public class Prestamo {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String cliente;
    private double monto;

    @Enumerated(EnumType.STRING)
    private EstadoPrestamo estado;

    public Prestamo() {}

    public Prestamo(String cliente, double monto) {
        this.cliente = cliente;
        this.monto = monto;
        this.estado = EstadoPrestamo.PENDIENTE;
    }

    public Long getId() { return id; }
    public String getCliente() { return cliente; }
    public void setCliente(String cliente) { this.cliente = cliente; }
    public double getMonto() { return monto; }
    public void setMonto(double monto) { this.monto = monto; }
    public EstadoPrestamo getEstado() { return estado; }
    public void setEstado(EstadoPrestamo estado) { this.estado = estado; }
}
```
---

## 📂 Paso 3: Crear el enum `EstadoPrestamo.java`


```java
package com.prestamos.model;

//Enumeración que define los estados válidos que puede tener un préstamo.
//Esto permite restringir los posibles valores a un conjunto controlado evitando errores por escritura o validaciones manuales con cadenas de texto.
public enum EstadoPrestamo {

    // El préstamo está pendiente de evaluación. 
    // Estado inicial cuando el cliente solicita el préstamo.
    PENDIENTE,

    // El préstamo ha sido aprobado después de la evaluación crediticia.
    APROBADO,

    //El préstamo ha sido rechazado debido a que no cumple con los criterios de evaluación.
    RECHAZADO
}
```
---

## 🗂️ Paso 4: Crear el repositorio `PrestamoRepository.java`

```java
package com.prestamos.repository;

import com.prestamos.model.Prestamo;
import org.springframework.data.jpa.repository.JpaRepository;

//Repositorio de préstamos que extiende JpaRepository.
//Este repositorio proporciona métodos CRUD (Crear, Leer, Actualizar, Eliminar) de forma automática sin necesidad de escribir consultas SQL.

//JpaRepository<Prestamo, Long>:
// - Prestamo: la entidad que maneja el repositorio.
// - Long: el tipo de dato de la clave primaria (ID) de la entidad Prestamo.

public interface PrestamoRepository extends JpaRepository<Prestamo, Long> {
    // No es necesario definir métodos aquí a menos que requieras consultas personalizadas.
}
```
---

## ⚙️ Paso 5: Crear el servicio `PrestamoService.java`

Aquí aplicamos:

- Concurrencia con `CompletableFuture`.
- Logs en contexto con SLF4J.

```java
package com.prestamos.service;

// Importamos las clases necesarias para manejar préstamos, estados y repositorio
import com.prestamos.model.Prestamo;
import com.prestamos.model.EstadoPrestamo;
import com.prestamos.repository.PrestamoRepository;

// Importamos SLF4J para manejo de logs
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

// Importamos anotaciones de Spring y clases para concurrencia
import org.springframework.stereotype.Service;

import java.util.List;
import java.util.concurrent.CompletableFuture;

// Servicio encargado de manejar la lógica de negocio relacionada con los préstamos.
//Aquí se realizan operaciones como crear un préstamo, evaluarlo de manera asíncrona y filtrar préstamos por estado.

@Service  // Indica que esta clase es un servicio de Spring (gestiona lógica de negocio)
public class PrestamoService {

    // Inyección del repositorio para acceder a la base de datos
    private final PrestamoRepository prestamoRepository;

    // Logger para registrar mensajes durante la ejecución
    private static final Logger logger = LoggerFactory.getLogger(PrestamoService.class);

    //Constructor que permite inyectar el repositorio mediante dependencia.
    //Spring detecta automáticamente el repositorio gracias a la anotación @Service.
    public PrestamoService(PrestamoRepository prestamoRepository) {
        this.prestamoRepository = prestamoRepository;
    }

    //Método para crear un nuevo préstamo. Guarda el préstamo en la base de datos con estado PENDIENTE y luego inicia la evaluación crediticia de forma asíncrona.
    //@param cliente Nombre del cliente que solicita el préstamo.
    //@param monto   Monto solicitado por el cliente.
    //@return El préstamo creado.
    public Prestamo crearPrestamo(String cliente, double monto) {
        // Se crea un nuevo objeto Prestamo con el cliente y monto indicados
        Prestamo prestamo = new Prestamo(cliente, monto);

        // Se guarda el préstamo en la base de datos con estado PENDIENTE
        prestamoRepository.save(prestamo);

        // Se registra un log informativo indicando que se ha creado un nuevo préstamo
        logger.info("Préstamo creado para cliente: {}", cliente);

        // Se inicia la evaluación crediticia de forma asíncrona (no bloquea la ejecución)
        evaluarPrestamoAsync(prestamo);

        // Se retorna el préstamo creado
        return prestamo;
    }

    //Método privado que evalúa el préstamo en un hilo separado mediante CompletableFuture.
    //Determina si el préstamo se aprueba o rechaza según el monto solicitado.
    // @param prestamo El préstamo que será evaluado.
    private void evaluarPrestamoAsync(Prestamo prestamo) {
        // CompletableFuture.runAsync permite ejecutar una tarea en segundo plano (concurrencia)
        CompletableFuture.runAsync(() -> {
            // Log informando que se ha iniciado la evaluación del préstamo
            logger.info("Evaluando préstamo de forma asíncrona para cliente: {}", prestamo.getCliente());

            // Lógica sencilla de evaluación crediticia:
            // Si el monto es menor o igual a 5000, se aprueba; si es mayor, se rechaza.
            if (prestamo.getMonto() <= 5000) {
                prestamo.setEstado(EstadoPrestamo.APROBADO);
            } else {
                prestamo.setEstado(EstadoPrestamo.RECHAZADO);
            }

            // Guardamos el cambio de estado en la base de datos
            prestamoRepository.save(prestamo);

            // Log informando el resultado de la evaluación
            logger.info("Evaluación completada: Estado del préstamo es {}", prestamo.getEstado());
        });
    }

    //Método que retorna una lista de préstamos filtrados por su estado (APROBADO, RECHAZADO, PENDIENTE).
    //Utiliza programación funcional con Streams para procesar la lista.
    //@param estado Estado por el cual se filtrarán los préstamos.
    //@return Lista de préstamos que tienen el estado indicado.
    public List<Prestamo> obtenerPrestamosPorEstado(EstadoPrestamo estado) {
        // Obtenemos todos los préstamos, luego filtramos los que coinciden con el estado indicado
        return prestamoRepository.findAll()
                .stream()  // Iniciamos un flujo de datos (Stream)
                .filter(p -> p.getEstado() == estado)  // Filtramos por estado
                .toList();  // Convertimos el resultado en una lista
    }
}
```
---

## 🌐 Paso 6: Crear el controlador `PrestamoController.java`

```java
package com.prestamos.controller;

// Importamos las clases necesarias del proyecto
import com.prestamos.model.EstadoPrestamo;
import com.prestamos.model.Prestamo;
import com.prestamos.service.PrestamoService;

// Importamos anotaciones de Spring para definir controladores y rutas
import org.springframework.web.bind.annotation.*;

import java.util.List;

//Controlador REST que expone los endpoints para interactuar con el microservicio de préstamos.
//Permite crear préstamos y consultar préstamos filtrados por estado mediante peticiones HTTP.
@RestController  // Indica que esta clase es un controlador REST (maneja solicitudes HTTP y responde con JSON)
@RequestMapping("/api/prestamos")  // Define la ruta base para todos los endpoints de este controlador
public class PrestamoController {

    // Inyección del servicio que contiene la lógica de negocio
    private final PrestamoService prestamoService;

    //Constructor que permite inyectar el servicio PrestamoService.
    //Spring detecta automáticamente el servicio gracias a la anotación @RestController.
    public PrestamoController(PrestamoService prestamoService) {
        this.prestamoService = prestamoService;
    }

    //Endpoint para crear un nuevo préstamo.
    //Recibe los parámetros cliente y monto desde la solicitud HTTP (por URL o query parameters).
    // @param cliente Nombre del cliente que solicita el préstamo.
    // @param monto   Monto solicitado por el cliente.
    // @return El préstamo creado.
    
    //Ejemplo de solicitud (POST):
    //http://localhost:8080/api/prestamos?cliente=Juan&monto=3000
    
    @PostMapping  // Define que este método responde a peticiones HTTP POST
    public Prestamo crearPrestamo(@RequestParam String cliente, @RequestParam double monto) {
        // Llama al servicio para crear el préstamo y lo retorna como respuesta (en formato JSON)
        return prestamoService.crearPrestamo(cliente, monto);
    }

    // Endpoint para obtener una lista de préstamos filtrados por su estado (APROBADO, RECHAZADO, PENDIENTE).
    // @param estado Estado por el cual se filtrarán los préstamos (se obtiene desde la URL como variable de ruta).
    // @return Lista de préstamos con el estado indicado.
    
    //Ejemplo de solicitud (GET):
    // http://localhost:8080/api/prestamos/estado/APROBADO
    //
    
    @GetMapping("/estado/{estado}")  // Define que este método responde a peticiones HTTP GET en la ruta /estado/{estado}
    public List<Prestamo> obtenerPrestamosPorEstado(@PathVariable EstadoPrestamo estado) {
        // Llama al servicio para obtener los préstamos filtrados por estado y los retorna como respuesta (en formato JSON)
        return prestamoService.obtenerPrestamosPorEstado(estado);
    }
}
```
---

## 🧪 Paso 7: Crear una prueba unitaria `PrestamoServiceTest.java`

```java
package com.prestamos.service;

// Importamos las clases necesarias para el test
import com.prestamos.model.Prestamo;
import com.prestamos.repository.PrestamoRepository;

// Importamos JUnit 5 para crear las pruebas
import org.junit.jupiter.api.Test;

// Importamos Mockito para crear mocks (objetos simulados)
import org.mockito.Mockito;

import static org.mockito.Mockito.*;  // Importa utilidades de verificación de Mockito

/**
 * Clase de prueba unitaria para el servicio PrestamoService.
 * Se utiliza Mockito para simular el repositorio y enfocarse en probar la lógica de negocio
 * sin necesidad de conectarse a una base de datos real.
 */
class PrestamoServiceTest {

    /**
     * Prueba que valida que al crear un préstamo, este se guarde correctamente en el repositorio.
     * Se enfoca solo en verificar que el método save() se haya llamado al menos una vez.
     */
    @Test  // Indica que este método es una prueba unitaria
    void crearPrestamo_deberiaGuardarPrestamo() {
        // Creamos un mock (objeto simulado) del repositorio PrestamoRepository
        PrestamoRepository mockRepo = Mockito.mock(PrestamoRepository.class);

        // Creamos una instancia del servicio, inyectando el mock del repositorio
        PrestamoService service = new PrestamoService(mockRepo);

        // Ejecutamos el método que queremos probar: crear un préstamo para "Juan" por 3000
        Prestamo prestamo = service.crearPrestamo("Juan", 3000);

        /**
         * Verificamos que el método save() del repositorio haya sido llamado al menos dos veces
         * con el objeto prestamo. Esto asegura que el préstamo fue guardado.
         */
        verify(mockRepo, times(2)).save(any(Prestamo.class));

        // NOTA: Esta prueba no valida la lógica de evaluación asíncrona, solo la creación inicial.
        // Se podría expandir con pruebas más específicas para la evaluación si fuera necesario.
    }
}
```
**🔎 ¿Que estamos haciendo?**

- Mockito crea un mock (simulación) del `PrestamoRepository` para que la prueba no dependa de una base de datos real.

- Se verifica que, al llamar a `crearPrestamo`, el servicio guarda el préstamo usando `save()`.

- No se evalúa el proceso asíncrono (`CompletableFuture`) en esta prueba, pero se puede extender si quisieras probar la evaluación con algún delay controlado o Mockito.verify(timeout(...)).



---

## 🧠 Reflexión final

1. ¿Por qué usamos `CompletableFuture` para evaluar préstamos?
2. ¿Qué beneficios aporta filtrar préstamos usando Streams en el servicio?
3. ¿Cómo mejora el sistema el uso de logs en contexto?
4. ¿Qué garantiza realizar pruebas unitarias con Mockito en este microservicio?

---

## 🎉 Cierre

¡Felicidades por completar este work! 🎉 Hoy no solo construiste un microservicio robusto, sino que aplicaste prácticas modernas que se utilizan en el desarrollo de software profesional.

Este proyecto es un reflejo de tu crecimiento como desarrollador Java, y puedes seguir extendiéndolo o integrarlo en tu portafolio como una muestra sólida de tus habilidades.
