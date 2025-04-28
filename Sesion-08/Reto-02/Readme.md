🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 08**](../Readme.md) ➡️ / ⚡ `Reto 02: Sistema de reservas en restaurante`

---

## 🎯 Objetivo

⚒️ Desarrollar un **microservicio simple de reservas para un restaurante**, integrando **pruebas unitarias con JUnit 5**, **mocks con Mockito** y **logs con SLF4J** para registrar el comportamiento del sistema.

---

## 🧠 Contexto del reto

Imagina que eres parte del equipo de desarrollo de un **restaurante** que quiere automatizar las **reservas de mesas**.

- Cuando un cliente solicita una **reserva** para una fecha y número de personas, el sistema debe:
  - Consultar un **servicio externo de disponibilidad de mesas**.
  - Confirmar o rechazar la reserva según la **disponibilidad**.

El **equipo de operaciones** necesita que el sistema registre **logs detallados** sobre cada intento de reserva para dar seguimiento.

---

## 🛠️ Instrucciones

1. **Crea las siguientes clases:**

- `ReservaService`:
  - Método `realizarReserva(String fecha, int personas)` → devuelve `true` si la reserva fue confirmada, `false` si fue rechazada.
  - Este método debe:
    - Consultar a un `DisponibilidadService` (una interfaz que simula un **servicio externo**).
    - Si hay disponibilidad, confirma la reserva; si no, la rechaza.
    - **Registrar logs** con SLF4J indicando el resultado (confirmada o rechazada).

- `DisponibilidadService` (interfaz):
  - Método `boolean hayDisponibilidad(String fecha, int personas)`.

---

2. **Crea las pruebas unitarias con JUnit 5 y Mockito**:

- Simula diferentes escenarios usando **Mockito**:
  - ✅ Cuando **hay disponibilidad**, la reserva debe ser confirmada.
  - ❌ Cuando **no hay disponibilidad**, la reserva debe ser rechazada.

- Verifica:
  - Que **se llama correctamente** al método del `DisponibilidadService`.
  - Que el **resultado de la reserva** es el esperado.

---

3. **Agrega logs en contexto** con **SLF4J**:

- Log de **nivel info** que indique:

  - Fecha, número de personas, y si la reserva fue **confirmada** o **rechazada**.

  Ejemplo:

  ```
  INFO Reserva confirmada para 2 personas el 2025-05-01
  INFO Reserva rechazada para 5 personas el 2025-05-02 (sin disponibilidad)
  ```

---

## 📂 Código base sugerido

⚠️ Solo te comparto la estructura y firmas, **debes implementar la lógica**:

```java
// service/DisponibilidadService.java
public interface DisponibilidadService {
    boolean hayDisponibilidad(String fecha, int personas);
}
```

```java
// service/ReservaService.java
public class ReservaService {
    private final DisponibilidadService disponibilidadService;

    public ReservaService(DisponibilidadService disponibilidadService) {
        this.disponibilidadService = disponibilidadService;
    }

    public boolean realizarReserva(String fecha, int personas) {
        // Implementar lógica aquí (consultar disponibilidad y registrar logs)
        return false;
    }
}
```

---

## 📝 Recomendaciones

- Integra **SLF4J + slf4j-simple** para los logs.
- Usa **JUnit 5** y **Mockito** para las pruebas unitarias y mocks.

---

## 🚀 Desafío adicional (opcional)

💡 **Extiende la lógica** para permitir:

- Reservar solo si el número de personas está entre **1 y 10**.  
- Registrar un **log de advertencia (WARN)** si alguien intenta reservar para más de 10 personas.

---

## 🧪 ¿Cómo validar?

- **Corre el `Main` (si lo creas)** y observa los logs.  
- Ejecuta las pruebas unitarias (`mvn test` o desde IntelliJ IDEA).

---

⬅️ [**Anterior**](../Ejemplo-02/Readme.md) | [**Siguiente**](../Ejemplo-03/Readme.md)➡️  
