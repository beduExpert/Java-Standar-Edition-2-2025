🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 01**](../Readme.md) ➡️ / 📝 `Ejemplo 03: Métodos genéricos en acción`

## 🎯 Objetivo

🔍 Aplicar **genéricos** y **wildcards** en un contexto **financiero**, diferenciando entre **cuentas bancarias** (ahorro, corriente, inversión) y simulando **transacciones** con validaciones.

---

## ⚙️ Requisitos

- JDK 17 o superior  
- IntelliJ IDEA o cualquier editor compatible con Java  
- Conocimientos previos de **genéricos** (`List<T>`, wildcards)

---

## 🧠 Contexto del ejemplo

Imagina que trabajas en un **sistema bancario** donde debes:

- **Gestionar cuentas** de distintos tipos (**Ahorro**, **Corriente**, **Inversión**).  
- **Procesar transacciones** financieras como **depósitos** y **retiros**.  
- Validar operaciones usando **genéricos** y **wildcards** para **flexibilizar** los métodos.

---

## 📄 Código base: `GestionFinanciera.java`

```java
import java.util.*;

public class GestionFinanciera {

    // Superclase Cuenta
    static abstract class Cuenta {
        private final String titular;
        protected double saldo;

        public Cuenta(String titular, double saldoInicial) {
            this.titular = titular;
            this.saldo = saldoInicial;
        }

        public String getTitular() { return titular; }
        public double getSaldo() { return saldo; }

        public void mostrarEstado() {
            System.out.println("👤 " + titular + " - Saldo: $" + saldo);
        }
    }

    // Subclases de cuentas
    static class CuentaAhorro extends Cuenta {
        public CuentaAhorro(String titular, double saldoInicial) { super(titular, saldoInicial); }
    }

    static class CuentaCorriente extends Cuenta {
        public CuentaCorriente(String titular, double saldoInicial) { super(titular, saldoInicial); }
    }

    static class CuentaInversion extends Cuenta {
        public CuentaInversion(String titular, double saldoInicial) { super(titular, saldoInicial); }
    }

    // Método genérico para mostrar cuentas (wildcard extends)
    public static void mostrarCuentas(List<? extends Cuenta> cuentas) {
        System.out.println("📋 Estado de cuentas:");
        cuentas.forEach(Cuenta::mostrarEstado);
    }

    // Método para procesar depósitos (wildcard super)
    public static void procesarDepositos(List<? super CuentaCorriente> cuentas, double cantidad) {
        System.out.println("\n💰 Procesando depósitos...");
        cuentas.forEach(c -> {
            if (c instanceof CuentaCorriente) {
                CuentaCorriente cc = (CuentaCorriente) c;
                cc.saldo += cantidad;
                System.out.println("✅ Depósito de $" + cantidad + " en cuenta de " + cc.getTitular());
            }
        });
    }

    public static void main(String[] args) {
        List<CuentaAhorro> ahorros = List.of(
            new CuentaAhorro("Ana", 1500.0),
            new CuentaAhorro("Carlos", 2200.0)
        );

        List<CuentaCorriente> corrientes = List.of(
            new CuentaCorriente("Luis", 1200.0),
            new CuentaCorriente("Sofía", 1800.0)
        );

        List<CuentaInversion> inversiones = List.of(
            new CuentaInversion("Marta", 5000.0)
        );

        // 1️⃣ Mostrar cada tipo de cuenta
        mostrarCuentas(ahorros);              // Impresión 1-2
        mostrarCuentas(corrientes);           // Impresión 3-4
        mostrarCuentas(inversiones);          // Impresión 5

        // 2️⃣ Procesar depósitos en cuentas corrientes
        procesarDepositos(corrientes, 500.0); // Impresión 6-7

        // 3️⃣ Mostrar cuentas corrientes actualizadas
        mostrarCuentas(corrientes);           // Impresión 8-9

        System.out.println("\n🔍 Fin de la simulación financiera."); // Impresión 10
    }
}
```

> 💡 **Nota**: Es posible **separar este código en diferentes archivos**, organizando cada clase (como `Cuenta`, `CuentaAhorro`, `CuentaCorriente`, etc.) en su propio archivo para mejorar la **escalabilidad y mantenibilidad** del proyecto.  
> Sin embargo, en esta ocasión decidimos **mantener todo en un solo archivo** para **facilitar la comprensión** del ejemplo y enfocarnos en el uso de **métodos genéricos** y **wildcards** sin distraernos con detalles de estructura de carpetas o configuración adicional.  

---

## 🧪 Resultado esperado

```
📋 Estado de cuentas:
👤 Ana - Saldo: $1500.0
👤 Carlos - Saldo: $2200.0
📋 Estado de cuentas:
👤 Luis - Saldo: $1200.0
👤 Sofía - Saldo: $1800.0
📋 Estado de cuentas:
👤 Marta - Saldo: $5000.0

💰 Procesando depósitos...
✅ Depósito de $500.0 en cuenta de Luis
✅ Depósito de $500.0 en cuenta de Sofía

📋 Estado de cuentas:
👤 Luis - Saldo: $1700.0
👤 Sofía - Saldo: $2300.0

🔍 Fin de la simulación financiera.
```

---

## 🔍 Conceptos clave utilizados

| Concepto          | Descripción |
|-------------------|-------------|
| `List<? extends T>` | Permite **leer** objetos de tipo `T` o subtipos (para mostrar cuentas). |
| `List<? super T>`   | Permite **modificar o insertar** objetos de tipo `T` o supertipos (para depósitos). |
| Genéricos y subclases | Aplicado en **cuentas bancarias** para **flexibilizar métodos** según el contexto. |

---

## 📝 En resumen

- **Wildcards (`?`)** ayudan a **flexibilizar operaciones** sobre listas de **diferentes tipos relacionados**.
- **`extends`** → Usado para **leer** (ej. mostrar saldos de cualquier cuenta).
- **`super`** → Usado para **modificar** (ej. depositar en cuentas corrientes).
- Este patrón es común en **finanzas**, pero aplicable a **otros dominios** como logística, medicina, ingeniería, etc.


---

⬅️ [**Anterior**](../Reto-02/Readme.md) | [**Siguiente**](../../Sesion-02/Readme.md)➡️  