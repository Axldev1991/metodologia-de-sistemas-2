# Explicación del Diagrama de Casos de Uso del TP-1

---

## 🎯 Objetivo en el Trabajo Práctico

Cumplir con el **Punto 2 de la consigna**, seleccionando al menos dos componentes del sistema y desarrollando el gráfico de Casos de Uso con relaciones avanzadas (`«include»`, `«extend»`, herencia) y la especificación de 2 escenarios completos.

---

## 🎭 Actores Identificados

1. **`Usuario` (Actor Principal):** Representa a la persona que gestiona archivos (crear, buscar, modificar, eliminar).
2. **`Administrador` (Herencia de Actor):** Hereda todas las capacidades del `Usuario` con permisos adicionales de sistema.
3. **`Sistema Operativo` (Actor Secundario):** Sistema externo encargado de la gestión física de espacio en disco.

---

## ⚙️ Casos de Uso y sus Relaciones

| Caso de Uso Base | Relación | Caso de Uso Relacionado | Justificación |
| :--- | :---: | :--- | :--- |
| **`Crear Archivo`** | `«include»` | **`Verificar Espacio en Disco`** | Al intentar crear un archivo, el sistema **siempre** debe consultar al SO sobre el espacio disponible. |
| **`Notificar Falta de Espacio`** | `«extend»` | **`Crear Archivo`** | Es un flujo alternativo condicional que **solo se ejecuta si no hay espacio libre**. |
| **`Eliminar Archivo`** | `«include»` | **`Actualizar Historial de Eliminados`** | Cada vez que se elimina un archivo, la consigna exige actualizar automáticamente el historial. |
| **`Cambiar Visibilidad`** | `«extend»` | **`Modificar Archivo`** | El cambio de visibilidad (*visible / oculto*) es una opción especial del flujo de modificación. |

---

## 📝 Documento de Escenarios
Los dos escenarios explicados paso a paso (camino feliz, pre/post condiciones y flujos alternativos) están redactados en el archivo [`escenarios.md`](file:///home/axel/Escritorio/UTN/M%20de%20Sistemas%20II/docs/TP-1/02-Diagrama-de-Casos-de-Uso/escenarios.md).

---

## 🛠️ ¿Cómo abrir y modificar el diagrama?
1. Abrí [`02_casos_de_uso.drawio`](file:///home/axel/Escritorio/UTN/M%20de%20Sistemas%20II/docs/TP-1/02-Diagrama-de-Casos-de-Uso/02_casos_de_uso.drawio) en VS Code para interactuar gráficamente con el diagrama.
