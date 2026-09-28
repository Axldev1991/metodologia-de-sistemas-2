# Explicación del Diagrama de Componentes del TP-1

---

## 🎯 Objetivo en el Trabajo Práctico

Cumplir con el **Punto 1 de la consigna**, creando una visión general de arquitectura modular para el sistema **Gestor de Archivos**.

---

## 🧱 Componentes Diseñados y su Justificación

```
+-------------------------------------------------------------------------------+
|                        Gestor de Archivos (Sistema)                           |
|                                                                               |
|  +---------------------------+       +------------------------------------+   |
|  |   Módulo de Gestión y     | ----> |      Módulo de Almacenamiento      |   |
|  |        Búsqueda           |       | (Imágenes, Docs, Videos, Audios)   |   |
|  +---------------------------+       +------------------------------------+   |
|               |                                       |                       |
|               v                                       v                       |
|  +---------------------------+       +------------------------------------+   |
|  |    Módulo de Historial    |       |      Sistema Operativo / Disco     |   |
|  | (Registro de Eliminados)  |       |       (Subsistema Externo)         |   |
|  +---------------------------+       +------------------------------------+   |
+-------------------------------------------------------------------------------+
```

### 1. `Interfaz de Usuario` (Componente Externo)
- **Función:** Representa la consola o pantalla desde la cual el usuario interactúa.
- **Relación:** Envía solicitudes hacia el *Módulo de Gestión y Búsqueda*.

### 2. `Módulo de Gestión y Búsqueda` (Componente Interno)
- **Función:** Es el núcleo lógico del sistema. Recibe peticiones para crear, renombrar, eliminar, buscar y cambiar visibilidad (*visible / oculto*) de archivos.
- **Relación:** Depende del *Módulo de Almacenamiento* para guardar datos y del *Módulo de Historial* para auditar eliminaciones.

### 3. `Módulo de Almacenamiento` (Componente Interno)
- **Función:** Organiza los archivos según su tipo o categoría (*imágenes, documentos, videos, audios*).
- **Relación:** Consulta y delega al *Sistema Operativo* la estructura física en disco y el cálculo de espacio disponible.

### 4. `Módulo de Historial` (Componente Interno)
- **Función:** Almacena y actualiza el historial de bajas cada vez que se elimina un archivo.

### 5. `Sistema Operativo / Disco` (Componente Externo)
- **Justificación:** Exigido explícitamente en la consigna: *"El Sistema Operativo es el encargado de crear la estructura de los archivos, según el espacio disponible en el disco"*.

---

## 🛠️ ¿Cómo abrir y modificar el diagrama?

1. Abrí el archivo [`01_componentes.drawio`](file:///home/axel/Escritorio/UTN/M%20de%20Sistemas%20II/docs/TP-1/01-Diagrama-de-Componentes/01_componentes.drawio) en VS Code.
2. Editá los módulos o líneas según sea necesario.
3. Para exportar a PDF o PNG: Botón derecho en el canvas ➔ `Export` ➔ `PDF`.
