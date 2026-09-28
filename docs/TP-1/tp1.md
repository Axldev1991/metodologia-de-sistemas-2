# Metodología de Sistemas II
## Primer Trabajo Práctico Integrador (C141Q2)

---

## 📋 Pautas de Trabajo y Entrega

### Formación del Equipo
- Grupos de hasta **8 integrantes**.

### Condiciones y Requisitos de Entrega
- La entrega formal se realizará en un **documento único en formato PDF** mediante la tarea habilitada en el campus.
- **Subida:** Un **único integrante por grupo** debe subir el archivo.
- **Fecha Límite:** **Jueves 01/10** en el horario de cursada.

> [!IMPORTANT]
> **Contenido Obligatorio de la Portada:**
> 1. Datos de la materia, docente y alumnos integrantes del grupo.
> 2. **Cualquier integrante que no figure en la portada será considerado sin entrega del Primer Parcial.**

> [!WARNING]
> La entrega es **obligatoria** y requiere el cumplimiento total de las consignas obligatorias. Los grupos que no hayan entregado o incumplan con las condiciones no podrán presentarse a la evaluación del **01/10**.

---

## 📁 Dominio: Gestor de Archivos

Un **Gestor de Archivos** contiene un conjunto de archivos organizados jerárquicamente mediante una relación de inclusión. De cada archivo se conoce su **nombre**, **fecha de creación** y **tamaño en bytes**.

### Funciones del Sistema
- **Creación de archivos:** En caso de no haber espacio suficiente, el sistema muestra un aviso.
- **Gestión de archivos:** Listar, crear, modificar y eliminar archivos existentes.
- **Tipos de archivos:** Almacenamiento organizado por categorías: *Imágenes*, *Documentos*, *Videos* y *Audios*.
- **Búsqueda:** Búsqueda avanzada por *nombre*, *tipo* y *fecha de creación*.
- **Historial de eliminados:** Registro e historial de archivos eliminados que se actualiza automáticamente ante cada baja.
- **Estructura en disco:** El Sistema Operativo se encarga de crear la estructura de archivos según el espacio disponible en disco.
- **Estados de visibilidad:** Procesar cambios de estado del archivo (*visible*, *oculto*).
- **Control de estados de acciones:** Las acciones del usuario (*copiar*, *borrar*, *renombrar*) manejan estados (*en espera*, *creada*, *en proceso*, *finalizada*, *con error*).

---

## 📐 Actividades a Desarrollar

> [!NOTE]
> En todos los diagramas se deberá respetar estrictamente la semántica y sintaxis del **Lenguaje Unificado de Modelado (UML)** vistas en clase para garantizar claridad y rigor técnico.

1. **Diagrama de Componentes**
   - Elaborar una visión general de al menos tres (3) módulos o subsistemas del sistema asignado.

2. **Diagramas de Casos de Uso (CU)**
   - A partir del Diagrama de Componentes, elegir al menos **dos (2) componentes** y desarrollar su diagrama de CU (incluyendo actores, herencia, inclusión `«include»`, extensión `«extend»`, etc.).
   - Desarrollar al menos **dos (2) escenarios completos** respetando la notación (nombre en infinitivo, pre/post condiciones y flujos alternativos).

3. **Diagrama de Secuencia (DS)**
   - Seleccionar un Caso de Uso clave respecto a la interacción en el tiempo (ej.: *"Almacenar archivo"*, *"Buscar archivos"*).
   - Diseñar el DS mostrando líneas de vida, mensajes, retornos y frames.
   - ⭐ **PLUS:** Realizar un DS adicional donde la interacción finalice con una acción de *error*.

4. **Diagrama de Comunicación / Elaboración**
   - Seleccionar un Caso de Uso y desarrollar el Diagrama de Comunicación detallando objetos, enlaces y mensajes.

5. **Diagrama de Clases**
   - Realizar el diagrama de clases del sistema completo especificando atributos, operaciones, relaciones (asociaciones, herencias, dependencias) y multiplicidad.

6. **Diagrama de Estados**
   - Identificar una funcionalidad donde sea representativo aplicar estados. Indicar estados, eventos, disparadores, condiciones de guarda y acciones asociadas.

7. **Diagrama de Actividades**
   - Seleccionar **dos (2) Casos de Uso** y crear un Diagrama de Actividad para cada uno. Mostrar flujo de tareas, decisiones, concurrencia (`fork`, `join`) y columnas de responsabilidad (*swimlanes*) si corresponde.

---

## 💯 Pautas de Calificación

| Tipo de Aprobación | Requisitos |
| :--- | :--- |
| **Aprobación NO Directa** | Puntos **1 al 5** completados correctamente. |
| **Aprobación DIRECTA** | Puntos **1 al 7** completados correctamente. |