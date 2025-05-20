🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 01**](../Readme.md) ➡️ / 📝 `Ejemplo 02: Uso de wildcards`

## 🎯 Objetivo

🔍 Comprender el uso de **wildcards (`?`)** y **restricciones** (`extends`, `super`) en genéricos, para crear métodos **flexibles y seguros** que manipulen listas de diferentes tipos relacionados, utilizando el ejemplo de **componentes aeroespaciales**.

---

## ⚙️ Requisitos

- JDK 17 o superior  
- IntelliJ IDEA o cualquier editor compatible con Java  
- Conocimientos básicos de **genéricos** en Java (`List<T>`, clases genéricas)

---

## 🧠 Contexto del ejemplo

En una **fábrica aeroespacial**, gestionas diferentes tipos de **componentes**:

- **Motores** (subtipo de componente).  
- **Alas** (otro subtipo).  

Algunos métodos deben **aceptar cualquier tipo de componente** o **limitarse a ciertos subtipos**. Usarás **wildcards (`?`)** para **flexibilizar o restringir** los tipos permitidos en listas de componentes.

---

## 📄 Código base

### 🧱 Paso 1: Crear la jerarquía de componentes

```java
// Superclase Componentes
public class Componente {
    private final String nombre;

    public Componente(String nombre) {
        this.nombre = nombre;
    }

    public String getNombre() { return nombre; }
}
```

```java
// Subclase Motor
public class Motor extends Componente {
    public Motor(String nombre) {
        super(nombre);
    }
}
```

```java
// Subclase Ala
public class Ala extends Componente {
    public Ala(String nombre) {
        super(nombre);
    }
}
```

---

### 🧱 Paso 2: Método flexible para imprimir cualquier tipo de componente

```java
import java.util.List;

public class InspeccionComponentes {

    // Método flexible: acepta cualquier tipo que sea Componente o subclase de Componente
    public static void imprimirComponentes(List<? extends Componente> componentes) {
        for (Componente c : componentes) {
            System.out.println("🔍 Inspeccionando componente: " + c.getNombre());
        }
    }

    public static void main(String[] args) {
        List<Motor> motores = List.of(new Motor("Motor Falcon 9"), new Motor("Motor Raptor"));
        List<Ala> alas = List.of(new Ala("Ala Delta"), new Ala("Ala Supersónica"));

        // ✅ Método acepta ambos tipos gracias a la wildcard con extends
        imprimirComponentes(motores);
        imprimirComponentes(alas);
    }
}
```

---

## 🧪 Resultado esperado

```
🔍 Inspeccionando componente: Motor Falcon 9
🔍 Inspeccionando componente: Motor Raptor
🔍 Inspeccionando componente: Ala Delta
🔍 Inspeccionando componente: Ala Supersónica
```

---

## 🔍 Conceptos clave utilizados

| Concepto               | Descripción |
|------------------------|-------------|
| `?` (wildcard)         | Representa **cualquier tipo desconocido**. |
| `? extends Componente` | Permite **Componente o cualquier subclase** (ej. `Motor`, `Ala`). Se usa para **leer elementos**. |
| `? super Motor`        | Permite **Motor o cualquier superclase** (ej. `Componente`). Se usa cuando quieres **insertar elementos**. |
| Flexibilidad           | Permite crear métodos que trabajen con diferentes tipos relacionados. |

---

## 📝 En resumen

- **Wildcards (`?`)** permiten crear métodos que trabajan con **diferentes tipos genéricos**.
- **`extends`** es ideal cuando **solo necesitas leer** (evitas romper el tipo).  
- **`super`** es útil cuando **insertas elementos** (garantiza compatibilidad hacia arriba).
- En este ejemplo, se inspeccionan diferentes **componentes aeroespaciales** (motores, alas) usando **wildcards con restricciones**.

> 💡 **Tip:** Si solo **lees elementos** en una lista → usa **`? extends Tipo`**.  
> Si necesitas **insertar elementos** → usa **`? super Tipo`**.

---

📘 Recursos adicionales:

- 🔗 [Guía de wildcards en Java – Baeldung](https://www.baeldung.com/java-generics-type-parameter-vs-wildcard)  
- 🔗 [Wildcards en Genéricos – Oracle Docs](https://docs.oracle.com/javase/tutorial/java/generics/wildcards.html)  

---

⬅️ [**Anterior**](../Reto-01/Readme.md) | [**Siguiente**](../Reto-02/Readme.md)➡️  