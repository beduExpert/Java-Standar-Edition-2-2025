🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 08**](../Readme.md) ➡️ / 📝 `Ejemplo 02: Pruebas unitarias con JUnit y Mockito`

---

## 🎯 Objetivo

⚒️ Aplicar **pruebas unitarias** en Java usando **JUnit 5** y **Mockito** para simular dependencias externas, integrando **logs con SLF4J** para depurar y monitorear el comportamiento de un **servicio de cálculo de descuentos**.

---

## ⚙️ Requisitos

- JDK 17 o superior  
- IDE compatible con Java (IntelliJ IDEA, Eclipse, VSCode)  
- Maven instalado  

---

## 🔧 Dependencias necesarias (`pom.xml`)

```xml
<dependencies>
    <!-- JUnit 5 para pruebas unitarias -->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.12.2</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-engine</artifactId>
        <version>5.12.2</version>
        <scope>test</scope>
    </dependency>

    <!-- Mockito para mocks -->
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-core</artifactId>
        <version>5.17.0</version>
        <scope>test</scope>
    </dependency>

    <!-- SLF4J para logs -->
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>2.0.17</version>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-simple</artifactId>
        <version>2.0.17</version>
    </dependency>
</dependencies>
```

---

## 🧠 Contexto del ejemplo

Este ejemplo simula un **servicio de cálculo de descuentos** para un sistema de ventas. El descuento **depende de un servicio externo (`PromocionService`)**, que determina el **porcentaje de descuento** aplicado según el tipo de cliente o promoción.

Aquí aprenderás a:

- **Simular dependencias** con **Mockito**.
- Validar la lógica con **JUnit 5**.
- **Registrar logs en contexto** con **SLF4J**.

---

## 📂 Estructura del proyecto

```
Ejemplo-02/
├── src/
│   ├── main/
│   │   └── java/
│   │       ├── service/
│   │       │   ├── CalculadoraDescuentos.java
│   │       │   └── PromocionService.java
│   │       └── Main.java
│   └── test/
│       └── java/
│           └── service/
│               └── CalculadoraDescuentosTest.java
```

---

## 💻 Código completo

### 🧩 Servicio de promociones (interfaz)

```java
// src/main/java/service/PromocionService.java
package service;

public interface PromocionService {
    double obtenerPorcentajeDescuento();
}
```

---

### 🧩 Servicio de cálculo de descuentos

```java
// src/main/java/service/CalculadoraDescuentos.java
package service;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class CalculadoraDescuentos {

    private static final Logger logger = LoggerFactory.getLogger(CalculadoraDescuentos.class);

    private final PromocionService promocionService;

    public CalculadoraDescuentos(PromocionService promocionService) {
        this.promocionService = promocionService;
    }

    public double calcularDescuento(double precio) {
        double porcentaje = promocionService.obtenerPorcentajeDescuento();
        double descuento = precio * porcentaje;

        logger.info("🏷️ Aplicando descuento del {}% sobre ${}, descuento calculado: ${}",
                porcentaje * 100,
                String.format("%,.2f", precio),
                String.format("%,.2f", descuento));

        return descuento;
    }
}
```

---

### 🧩 Clase principal (Main.java)

```java
// src/main/java/Main.java
import service.CalculadoraDescuentos;
import service.PromocionService;

public class Main {
    public static void main(String[] args) {
        // Promoción fija del 10% para esta ejecución manual
        PromocionService promocionFija = () -> 0.10;

        CalculadoraDescuentos calculadora = new CalculadoraDescuentos(promocionFija);
        double descuento = calculadora.calcularDescuento(500.0);

        System.out.println("Descuento aplicado: $" + String.format("%,.2f", descuento));
    }
}
```

---

### 🧩 Pruebas unitarias con Mockito

```java
// src/test/java/service/CalculadoraDescuentosTest.java
package service;

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;
import static org.mockito.Mockito.*;

class CalculadoraDescuentosTest {

    @Test
    void pruebaDescuentoDel10PorCiento() {
        PromocionService promocionMock = mock(PromocionService.class);
        when(promocionMock.obtenerPorcentajeDescuento()).thenReturn(0.10);

        CalculadoraDescuentos calculadora = new CalculadoraDescuentos(promocionMock);
        double descuento = calculadora.calcularDescuento(500.0);

        assertEquals(50.0, descuento, 0.01);
        verify(promocionMock).obtenerPorcentajeDescuento();
    }

    @Test
    void pruebaSinDescuento() {
        PromocionService promocionMock = mock(PromocionService.class);
        when(promocionMock.obtenerPorcentajeDescuento()).thenReturn(0.0);

        CalculadoraDescuentos calculadora = new CalculadoraDescuentos(promocionMock);
        double descuento = calculadora.calcularDescuento(500.0);

        assertEquals(0.0, descuento, 0.01);
        verify(promocionMock).obtenerPorcentajeDescuento();
    }

    @Test
    void pruebaDescuentoVip() {
        PromocionService promocionMock = mock(PromocionService.class);
        when(promocionMock.obtenerPorcentajeDescuento()).thenReturn(0.20);

        CalculadoraDescuentos calculadora = new CalculadoraDescuentos(promocionMock);
        double descuento = calculadora.calcularDescuento(500.0);

        assertEquals(100.0, descuento, 0.01);
        verify(promocionMock).obtenerPorcentajeDescuento();
    }
}
```

---


## 🧪 ¿Cómo ejecutar el ejemplo?

#### Para correr el `Main`:

1. Abre `Main.java`.
2. Haz clic en el ícono verde ▶️ para ejecutarlo.

---

### 📝 Salida esperada (`Main`):

```
Descuento aplicado: $50.00
```

**Logs esperados en consola:**

```
INFO service.CalculadoraDescuentos - 🏷️ Aplicando descuento del 10.0% sobre $500.00, descuento calculado: $50.00
```

---

#### Para correr las pruebas unitarias:

Desde **IntelliJ IDEA**:

1. Abre `CalculadoraDescuentosTest.java`.
2. Haz clic en el ícono verde ▶️.

Desde la terminal:

```bash
mvn test
```

🔔 **Nota:**  
Si ves un error como:

```
mvn : El término 'mvn' no se reconoce...
```

Significa que **Maven no está instalado o no está en el PATH**.

- Puedes instalar Maven desde:  
  👉 [https://maven.apache.org/download.cgi](https://maven.apache.org/download.cgi)

- Asegúrate de agregar Maven al **PATH** del sistema para que el comando `mvn` funcione desde cualquier terminal.


---

### 📝 Salida esperada (pruebas unitarias):

```
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running service.CalculadoraDescuentosTest
[INFO] Tests run: 3, Failures: 0, Errors: 0, Skipped: 0
[INFO] -------------------------------------------------------
[INFO] BUILD SUCCESS
```

---

## 🚀 Resumen

Este ejemplo:

- **Integró dependencias simuladas** usando **Mockito**.
- **Validó la lógica de negocio** con **JUnit 5**.
- **Registró logs en contexto** con **SLF4J**.

> **Tip final:** Simular dependencias con **Mockito** permite **probar en aislamiento** y **controlar escenarios complejos** sin depender de componentes externos.

---

⬅️ [**Anterior**](../Ejemplo-01/Readme.md) | [**Siguiente**](../Ejemplo-03/Readme.md)➡️  