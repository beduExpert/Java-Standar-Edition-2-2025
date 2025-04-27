🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 07**](../Readme.md) ➡️ / ⚡ `Reto 01: Expandiendo la API REST de empleados en RRHH`

## 🎯 Objetivo

⚒️ Extender una **API REST** con **Spring Boot** para incluir nuevas funcionalidades en la **gestión de empleados**, como **buscar empleados por puesto** o **eliminar registros**.  

Esto te permitirá practicar la creación de **nuevos endpoints REST** y aplicar buenas prácticas en el diseño de **APIs escalables**.

---

## 🧠 Contexto del reto

Imagina que el área de **Recursos Humanos (RRHH)** de tu empresa necesita **ampliar la API REST** desarrollada en el ejemplo anterior para ofrecer más funcionalidades:

1. 🔍 **Buscar empleados por puesto** (ejemplo: "Desarrollador Backend").  
2. 🗑️ **Eliminar empleados** por su **ID**.

Estas mejoras harán la API más completa y flexible, facilitando la **gestión de empleados** desde cualquier sistema.

---

## 📝 Instrucciones

1. **Agrega un nuevo endpoint GET** en `EmpleadoController`:

   - **Ruta**: `/api/empleados/puesto/{puesto}`  
   - **Funcionalidad**: Devuelve una **lista de empleados** que coincidan con el **puesto** especificado.

2. **Agrega un endpoint DELETE** en `EmpleadoController`:

   - **Ruta**: `/api/empleados/{id}`  
   - **Funcionalidad**: **Elimina** el empleado con el **ID** proporcionado.

3. **Modifica `EmpleadoService`** para incluir los métodos:

   - `List<Empleado> buscarPorPuesto(String puesto)`  
   - `void eliminarEmpleado(Long id)`

4. **Prueba los endpoints** utilizando **Postman** o **curl**:

   - Buscar por puesto (ejemplo):

     ```
     GET http://localhost:8080/api/empleados/puesto/Desarrollador Backend
     ```

   - Eliminar empleado por ID (ejemplo):

     ```
     DELETE http://localhost:8080/api/empleados/2
     ```

---

## 💪 Desafío adicional (opcional)

- Implementa una **validación** para que el endpoint DELETE devuelva un **mensaje de error** si el **ID** no existe.

---

## 💡 Ejemplo de salida esperada

```
🔍 Buscar empleados por puesto: "Desarrollador Backend"
[
  { "id": 2, "nombre": "Carlos Pérez", "puesto": "Desarrollador Backend", "salario": 45000 }
]

🗑️ Eliminar empleado con ID: 2
✅ Empleado con ID 2 eliminado correctamente.

📋 Lista actualizada de empleados:
[
  { "id": 1, "nombre": "Ana Gómez", "puesto": "Gerente de Marketing", "salario": 55000 }
]
```

---

🏆 Si logras **buscar y eliminar empleados** correctamente a través de la **API REST**, ¡reto completado!

---

⬅️ [**Anterior**](../Ejemplo-02/Readme.md) | [**Siguiente**](../../Sesion-08/Readme.md)➡️  