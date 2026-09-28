# Explicación del Diagrama de Actividades del TP-1

---

## 🎯 Objetivo en el Trabajo Práctico

Cumplir con el **Punto 7 de la consigna**, diseñando los diagramas de actividad para dos Casos de Uso del sistema con **columnas de responsabilidad (Swimlanes)**, nodos de decisión y concurrencia (**Fork y Join**).

---

## 🌊 Diagrama 1: Caso de Uso "Crear y Almacenar Archivo"

### Columnas de Responsabilidad (Swimlanes):
1. **`Usuario`:** Solicita la creación ingresando nombre, tipo y datos.
2. **`Módulo de Gestión`:** Procesa la solicitud, evalúa la decisión `[espacioOK == true]` vs `[espacio == false]` y efectúa el guardado o el aviso de error.
3. **`Sistema Operativo`:** Realiza la comprobación física del espacio libre en disco.

---

## ⚡ Diagrama 2: Caso de Uso "Eliminar Archivo" (Concurrencia Fork / Join)

```
                       [ Usuario ] ──► (Solicitar baja de archivo)
                                                  │
                                                  v
                                           ❚❚❚ FORK ❚❚❚  (Barra de Concurrencia)
                                           ┌──────┴──────┐
                                           │             │
                                           v             v
                              [ Módulo Gestión ]   [ Módulo Historial ]
                              Retirar de lista     Crear registro de baja
                              activa               con timestamp
                                           │             │
                                           └──────┬──────┘
                                                  v
                                           ❚❚❚ JOIN ❚❚❚  (Barra de Sincronización)
                                                  │
                                                  v
                                           (Notificar baja completada)
```

### Justificación de la Concurrencia:
- **`FORK`:** Al confirmar la baja, el sistema dispara en paralelo dos acciones independientes:
  1. Retirar el archivo de la estructura de archivos activos en el *Módulo de Gestión*.
  2. Generar el registro de auditoría en el *Módulo de Historial*.
- **`JOIN`:** La notificación de confirmación al usuario solo se envía cuando **ambas tareas concurrentes finalizaron con éxito**.

---

## 🛠️ ¿Cómo abrir y modificar el diagrama?
1. Abrí [`07_actividades.drawio`](file:///home/axel/Escritorio/UTN/M%20de%20Sistemas%20II/docs/TP-1/07-Diagrama-de-Actividades/07_actividades.drawio) en VS Code.
