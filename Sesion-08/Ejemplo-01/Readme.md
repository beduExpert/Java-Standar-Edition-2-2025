🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 08**](../Readme.md) ➡️ / 📝 `Ejemplo 01: Aplicación de principios SOLID`

---

## 🎯 Objetivo

⚒️ Aplicar **principios SOLID** para mejorar el diseño de un sistema de **notificaciones** en Java. Identificarás un ejemplo con **malas prácticas** (violando SRP y DIP) y lo **refactorizarás** para lograr un código **modular, extensible y fácil de mantener**.

---

## ⚙️ Requisitos

- JDK 17 o superior  
- IDE compatible con Java (IntelliJ IDEA, Eclipse, VSCode)  
- Maven instalado (opcional, si deseas estructurar el proyecto como Maven)

---

## 🔤 ¿Qué es SOLID?

**SOLID** es un acrónimo que agrupa **cinco principios fundamentales del diseño orientado a objetos**, pensados para crear sistemas **flexibles, mantenibles y escalables**.

| Letra  | Principio                                      | ¿Qué significa?                                                           |
|--------|------------------------------------------------|---------------------------------------------------------------------------|
| **S**  | **Single Responsibility Principle (SRP)**      | Una clase debe tener **una única responsabilidad** o razón para cambiar.  |
| **O**  | **Open/Closed Principle (OCP)**                | El código debe estar **abierto a extensión, pero cerrado a modificación**.|
| **L**  | **Liskov Substitution Principle (LSP)**        | Las clases hijas deben poder **sustituir a las clases padres** sin romper el programa.|
| **I**  | **Interface Segregation Principle (ISP)**      | Evitar interfaces **grandes y generales**, mejor **interfaces pequeñas y específicas**.|
| **D**  | **Dependency Inversion Principle (DIP)**       | Depender de **abstracciones** (interfaces), no de implementaciones concretas.|

En este ejemplo, aplicaremos **SRP** y **DIP**, que son dos de los pilares más importantes para mantener el código **modular y desacoplado**.

---

## 🧠 Contexto del ejemplo

En el desarrollo diario es común encontrar clases que **hacen demasiadas cosas** (violando SRP) o que **dependen directamente de implementaciones concretas** (violando DIP).  
Esto **dificulta las pruebas, el mantenimiento y la extensión del código**.

En este ejemplo:

1. Verás un **NotificationService** que gestiona **varios tipos de notificaciones** de forma incorrecta (mezclando responsabilidades).
2. Refactorizaremos ese código **aplicando SRP (Single Responsibility Principle)** y **DIP (Dependency Inversion Principle)**.

---

## 📂 Estructura del proyecto

```
Ejemplo-01/
├── sin_solid/           <-- Código sin aplicar SOLID (mal diseño)
│   └── NotificationService.java
└── con_solid/           <-- Código refactorizado aplicando SRP y DIP
    ├── NotificationSender.java (Interfaz)
    ├── EmailSender.java (Implementación de correo)
    ├── SmsSender.java (Implementación de SMS)
    └── NotificationService.java (Servicio que usa la abstracción)
```

---

## 💻 Código

### 🔴 **Código inicial (sin SOLID)**

```java
// sin_solid/NotificationService.java
public class NotificationService {

    public void sendNotification(String message, String type) {
        if ("email".equals(type)) {
            System.out.println("Enviando correo: " + message);
            // Lógica específica de envío de email
        } else if ("sms".equals(type)) {
            System.out.println("Enviando SMS: " + message);
            // Lógica específica de envío de SMS
        } else {
            System.out.println("Tipo de notificación desconocido");
        }
    }
}
```

### 🚨 Problemas del diseño:

- ❌ **Viola SRP**: La clase gestiona múltiples tipos de notificaciones (correo y SMS).
- ❌ **Viola DIP**: Depende de detalles concretos (lógica interna de email y SMS).
- ❌ **Difícil de extender**: Si quieres agregar WhatsApp, Push, etc., tendrías que **modificar esta clase**.

---

### ✅ **Código refactorizado (aplicando SRP y DIP)**

#### **1. Interfaz NotificationSender**

```java
// con_solid/NotificationSender.java
public interface NotificationSender {
    void send(String message);
}
```

---

#### **2. Implementación de correo (EmailSender)**

```java
// con_solid/EmailSender.java
public class EmailSender implements NotificationSender {

    @Override
    public void send(String message) {
        System.out.println("Enviando correo: " + message);
        // Lógica específica de email
    }
}
```

---

#### **3. Implementación de SMS (SmsSender)**

```java
// con_solid/SmsSender.java
public class SmsSender implements NotificationSender {

    @Override
    public void send(String message) {
        System.out.println("Enviando SMS: " + message);
        // Lógica específica de SMS
    }
}
```

---

#### **4. Servicio de notificaciones (NotificationService)**

```java
// con_solid/NotificationService.java
public class NotificationService {

    private final NotificationSender sender;

    // Inyección de la abstracción (no depende de implementaciones concretas)
    public NotificationService(NotificationSender sender) {
        this.sender = sender;
    }

    public void sendNotification(String message) {
        sender.send(message);
    }
}
```

---

#### **5. Clase principal (Main)**

```java
// con_solid/Main.java
public class Main {
    public static void main(String[] args) {
        // Cambia la implementación sin modificar NotificationService
        NotificationSender emailSender = new EmailSender();
        NotificationService emailService = new NotificationService(emailSender);
        emailService.sendNotification("Bienvenido al sistema!");

        NotificationSender smsSender = new SmsSender();
        NotificationService smsService = new NotificationService(smsSender);
        smsService.sendNotification("Tu código es 1234.");
    }
}
```

---

## 📝 Comparación antes y después

| Aspecto                   | Sin SOLID                                   | Con SOLID                                  |
|---------------------------|---------------------------------------------|--------------------------------------------|
| **Responsabilidad**       | Mezcla lógica de varios tipos de envío      | Cada clase tiene una única responsabilidad |
| **Dependencias**          | Depende de detalles concretos (email, SMS)  | Depende de abstracciones (interfaces)      |
| **Extensibilidad**        | Difícil (se debe modificar la clase)        | Fácil (solo agregas nuevas implementaciones)|
| **Mantenibilidad**        | Baja (todo está acoplado)                   | Alta (código modular y flexible)           |

---

## 🚀 Resumen

Este ejemplo mostró cómo **aplicar SRP y DIP** permite crear un sistema de notificaciones **flexible y extensible**.  
Al depender de **abstracciones** (interfaces) y separar las responsabilidades, el código es más **modular** y fácil de mantener.

> **Tip final:** En proyectos reales, estos principios son esenciales para manejar la **complejidad** y facilitar la **evolución del software**.

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Reto-01/Readme.md)➡️  