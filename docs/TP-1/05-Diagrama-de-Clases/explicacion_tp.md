# Explicación del Diagrama de Clases del TP-1

---

## 🎯 Objetivo en el Trabajo Práctico

Cumplir con el **Punto 5 de la consigna**, diseñando la arquitectura estática completa para el sistema **Gestor de Archivos** con sus atributos, operaciones, multiplicidades y jerarquía de herencia.

---

## 🏛️ Clases Diseñadas y Justificación Técnica

### 1. `GestorArchivos` (Clase Controladora / Singleton)
- **Atributos:** `- espacioTotalBytes: long`, `- espacioDisponibleBytes: long`.
- **Operaciones:** `crearArchivo()`, `eliminarArchivo()`, `buscarPorNombre()`, `buscarPorTipo()`, `buscarPorFecha()`.
- **Justificación:** Centraliza la lógica de control del sistema de archivos y gestiona el espacio.

### 2. `Archivo` (Clase Abstracta)
- **Atributos:** `# id`, `# nombre`, `# fechaCreacion`, `# tamanoBytes`, `# visibilidad: EstadoVisibilidad`.
- **Justificación:** Es la superclase que abstrae el comportamiento común a todos los elementos guardados. Define el método abstracto `+ obtenerTipo(): String`.

### 3. Subclases de `Archivo` (Herencia Polimórfica)
- **`Imagen`:** Atributo especializado `- resolucion: String`.
- **`Documento`:** Atributo especializado `- cantPaginas: int`.
- **`Video`:** Atributo especializado `- duracionSeg: int`.
- **`Audio`:** Atributo especializado `- bitrate: int`.
- **Justificación:** Satisface el requisito del dominio: *"Almacenar diferentes tipos de archivos organizados por: imágenes, documentos, videos y audios"*.

### 4. `HistorialEliminados` y `RegistroBaja` (Composición y Auditoría)
- **`HistorialEliminados`:** Guarda una lista de `RegistroBaja`.
- **`RegistroBaja`:** Contiene los datos del archivo destruido (`idArchivo`, `nombreArchivo`, `fechaEliminacion`, `tamanoBytes`).
- **Justificación:** Satisface el requerimiento: *"Generar historial de archivos eliminados el cual se actualiza cuando se elimina un archivo"*.

### 5. `AccionUsuario` y Enumeraciones
- **`AccionUsuario`:** Representa operaciones asíncronas o en segundo plano (*copiar, borrar, renombrar*).
- **`EstadoVisibilidad` (`enumeration`):** `VISIBLE`, `OCULTO`.
- **`EstadoAccion` (`enumeration`):** `EN_ESPERA`, `CREADA`, `EN_PROCESO`, `FINALIZADA`, `CON_ERROR`.

---

## 🔗 Resumen de Relaciones y Multiplicidades

- `GestorArchivos` `1` **`◆──`** `*` `Archivo` *(Composición: El Gestor posee y administra los archivos)*.
- `GestorArchivos` `1` **`◆──`** `1` `HistorialEliminados` *(Composición: 1 a 1)*.
- `HistorialEliminados` `1` **`◇──`** `*` `RegistroBaja` *(Agregación: Contiene los registros de auditoría)*.
- `Archivo` **`──▷`** `Imagen`, `Documento`, `Video`, `Audio` *(Herencia UML)*.

---

## 🛠️ ¿Cómo abrir y modificar el diagrama?
1. Abrí [`05_clases.drawio`](file:///home/axel/Escritorio/UTN/M%20de%20Sistemas%20II/docs/TP-1/05-Diagrama-de-Clases/05_clases.drawio) en VS Code.
