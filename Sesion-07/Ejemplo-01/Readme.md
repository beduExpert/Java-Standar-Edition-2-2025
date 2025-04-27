🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 07**](../Readme.md) ➡️ / 📝 `Ejemplo 01: Comparativa entre monolito y microservicios`

## 🎯 Objetivo

🔍 Entender las **diferencias clave** entre una **arquitectura monolítica** y una **arquitectura de microservicios**, explorando cómo se organizan, despliegan y escalan las aplicaciones en cada enfoque.

---

## ⚙️ Requisitos

- Conocimientos básicos de desarrollo de software  
- Familiaridad con conceptos de arquitectura de aplicaciones  

---

## 🧠 Contexto del ejemplo

Imagina que desarrollas una **plataforma de experiencias en videojuegos de realidad virtual (VR)**. Esta plataforma permite a los usuarios **explorar un catálogo de juegos VR**, **registrar sus sesiones**, **gestionar perfiles de jugadores** y **analizar estadísticas de desempeño** (como tiempo de juego, calorías quemadas, etc.).

Exploraremos cómo se podría diseñar esta plataforma en dos arquitecturas:

1. **Monolito**: Toda la lógica (usuarios, catálogo, sesiones, estadísticas) en una sola aplicación.  
2. **Microservicios**: Cada módulo (usuarios, catálogo, sesiones, estadísticas) se gestiona como un servicio independiente.

Este ejemplo nos ayudará a visualizar cómo cambia la **escalabilidad**, **mantenimiento** y **flexibilidad** dependiendo de la arquitectura.

---

## 📂 Estructura del proyecto

```
Ejemplo-01/
│
├── Monolito/
│   └── PlataformaVRMonolito.java
│
└── Microservicios/
    ├── ServicioUsuarios.java
    ├── ServicioCatalogo.java
    ├── ServicioSesiones.java
    └── ServicioEstadisticas.java
```

---

## 💻 Código

### 🧩 Monolito

```java
// PlataformaVRMonolito.java
public class PlataformaVRMonolito {
    public void gestionarExperienciaVR() {
        System.out.println("👤 Gestionando perfil de usuario...");
        System.out.println("🎮 Mostrando catálogo de juegos VR...");
        System.out.println("🕶️ Registrando nueva sesión de juego...");
        System.out.println("📊 Actualizando estadísticas de rendimiento...");
    }

    public static void main(String[] args) {
        PlataformaVRMonolito app = new PlataformaVRMonolito();
        app.gestionarExperienciaVR();
    }
}
```

### 🧩 Microservicios

```java
// ServicioUsuarios.java
public class ServicioUsuarios {
    // Servicio encargado de gestionar los perfiles de usuario 🎮
    public void gestionarUsuario() {
        System.out.println("👤 Gestionando perfil de usuario...");
    }
}

// ServicioCatalogo.java
public class ServicioCatalogo {
    // Servicio que muestra el catálogo de juegos VR disponibles 🕹️
    public void mostrarCatalogo() {
        System.out.println("🎮 Mostrando catálogo de juegos VR...");
    }
}

// ServicioSesiones.java
public class ServicioSesiones {
    // Servicio que registra las sesiones de juego de los usuarios 🕶️
    public void registrarSesion() {
        System.out.println("🕶️ Registrando nueva sesión de juego...");
    }
}

// ServicioEstadisticas.java
public class ServicioEstadisticas {
    // Servicio que actualiza las estadísticas de los jugadores 📊
    public void actualizarEstadisticas() {
        System.out.println("📊 Actualizando estadísticas de rendimiento...");
    }
}
```

```java
// Main.java
public class Main {
    public static void main(String[] args) {
        ServicioUsuarios usuarios = new ServicioUsuarios();
        ServicioCatalogo catalogo = new ServicioCatalogo();
        ServicioSesiones sesiones = new ServicioSesiones();
        ServicioEstadisticas estadisticas = new ServicioEstadisticas();

        usuarios.gestionarUsuario();
        catalogo.mostrarCatalogo();
        sesiones.registrarSesion();
        estadisticas.actualizarEstadisticas();
    }
}
```

---

## 🧪 Resultado esperado

```
👤 Gestionando perfil de usuario...
🎮 Mostrando catálogo de juegos VR...
🕶️ Registrando nueva sesión de juego...
📊 Actualizando estadísticas de rendimiento...
```


---

## 📝 Conceptos clave utilizados

- **Monolito**: Toda la lógica (usuarios, catálogo, sesiones, estadísticas) se encuentra en una sola aplicación.
- **Microservicios**: Servicios separados que se comunican entre sí, cada uno enfocado en una funcionalidad específica.
- **Escalabilidad horizontal**: Capacidad para escalar servicios individuales (por ejemplo, estadísticas de sesiones VR que requieren procesamiento en tiempo real).
- **Despliegue independiente**: Cada servicio puede ser desplegado, actualizado o escalado por separado.

---

## 🔍 Comparativa rápida

| Característica     | Monolito                              | Microservicios                        |
|--------------------|---------------------------------------|---------------------------------------|
| **Despliegue**     | Único artefacto                       | Múltiples servicios independientes    |
| **Escalabilidad**  | Escalado completo                     | Escalado por servicio específico      |
| **Mantenimiento**  | Difícil en sistemas grandes           | Más sencillo al estar modularizado    |
| **Tecnologías**    | Una sola tecnología                   | Variedad por servicio (si se desea)   |
| **Comunicación**   | Interna                               | Red (HTTP, colas de mensajes, etc.)   |

---

## 📚 Recursos adicionales

- [Microservices vs Monolith – GeeksforGeeks](https://www.geeksforgeeks.org/monolithic-vs-microservices-architecture/)  
- [12 Factor App](https://12factor.net/)  
- [Microservices – A Practical Guide](https://dev.to/brilworks/building-microservices-in-java-a-practical-guide-49h8)  

---

## 🚀 Resumen

Este ejemplo mostró cómo una **plataforma de experiencias VR** puede estructurarse como un **monolito** o como una **arquitectura de microservicios**. Mientras el **monolito** puede ser más simple para aplicaciones pequeñas o con poca demanda, los **microservicios** permiten escalar y mantener partes específicas (como **estadísticas en tiempo real**) sin afectar el resto del sistema.

> **Tip final:** En sistemas que involucran **realidad virtual**, donde algunas partes requieren **procesamiento intensivo** (como estadísticas o sesiones), **los microservicios** permiten escalar esos componentes sin sobrecargar la plataforma completa.

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Ejemplo-02/Readme.md) ➡️  