# Teórica Completa: Diagrama de Actividades (UML 2.x)
**Bibliografía de Referencia:** Craig Larman, *UML y Patrones* (2ª Edición en Español), **Capítulo 38, Sección 38.4 (Págs. 568–570 del libro impreso / Páginas 599–601 del PDF)**.

---

## 📌 1. Introducción y Propósito en el Proceso Unificado (PU)

El **Diagrama de Actividades** es un diagrama de comportamiento que modela el flujo de trabajo (*workflow*) secuencial o concurrente de un proceso de negocio o caso de uso complejo.

Según el libro de Craig Larman (**Cap. 38, Pág. 568 / PDF Pág. 599**):
> *“Un diagrama de actividades de UML ofrece una notación rica para representar una secuencia de actividades. Podría aplicarse a cualquier propósito, pero se considera especialmente útil para visualizar los flujos de trabajo y los procesos del negocio o casos de uso.”*

- **Definición Formal de Larman (Pág. 569):** *"Formalmente, un diagrama de actividad se considera un tipo especial de diagrama de estados de UML en el que los estados son acciones, y las transiciones de los eventos se disparan automáticamente al completarse la acción."*

---

## 📐 2. Elementos Notacionales y Reglas Visuales Estrictas (Larman, Pág. 569 / PDF Pág. 601)

| Elemento | Figura / Contorno | Tipo de Trazo | Conector / Flecha | Semántica Notacional de Larman |
| :--- | :--- | :--- | :--- | :--- |
| **Nodo Inicial** | Círculo negro sólido (`●`) | N/A | N/A | Inicia el flujo de control o flujo de datos de la actividad. |
| **Nodo Final** | Círculo negro con anillo exterior (`◉`) | N/A | N/A | Finaliza completamente la ejecución de la actividad. |
| **Acción / Actividad** | **Rectángulo de bordes redondeados** | Trazo sólido continuo | N/A | Paso ejecutable o tarea atómica dentro del flujo. |
| **Nodo de Decisión** | **Rombo** (`◇`) con 1 entrada y $N$ salidas | Trazo sólido continuo | Flechas etiquetadas `[guard]` | Bifurcación condicional exclusiva (*branch*). |
| **Nodo de Combinación** | **Rombo** (`◇`) con $N$ entradas y 1 salida | Trazo sólido continuo | N/A | Convergencia de rutas condicionales previamente bifurcadas (*merge*). |
| **Barra FORK (Bifurcación)** | **Barra rectangular negra gruesa** (`❚`) | Sólida negra rellena | 1 entrada y $N$ salidas | Inicia flujos de ejecución **concurrentes o en paralelo**. |
| **Barra JOIN (Sincronización)** | **Barra rectangular negra gruesa** (`❚`) | Sólida negra rellena | $N$ entradas y 1 salida | Sincroniza flujos paralelos: **espera a que TODOS concluyan** antes de avanzar. |
| **Swimlanes (Calles)** | Columnas / Filas rectangulares | Líneas continuas paralelas | N/A | Agrupan acciones según el actor o módulo responsable de ejecutarlas (*Área de responsabilidad*). |

---

## 🧠 3. Semántica de Ejecución y Tokens (Larman, Cap. 38)

### A. Semántica de Tokens de Control
Larman explica el flujo mediante la metáfora de **tokens de control**:
- Un nodo inicial emite un token.
- Al llegar a un **FORK**, la barra consume 1 token y emite $N$ tokens simultáneos hacia las ramas paralelas.
- Al llegar a un **JOIN**, la barra retiene los tokens hasta recibir los $N$ tokens esperados de todas las ramas; recién entonces los consume y emite 1 token de salida.

### B. Uso de Swimlanes (Particiones de Actividad - Larman, Pág. 569)
Las **Swimlanes** dividen visualmente el diagrama en columnas (ej. `Usuario`, `Sistema / Backend`, `Almacenamiento Cloud`). Cada acción debe colocarse estrictamente dentro de la calle del módulo que la realiza.

---

## 🛠️ 4. Metodología Paso a Paso para Construirlo (Larman)

1. **Definir el Alcance del Proceso:** Determinar qué Caso de Uso o proceso de negocio se va a diagramar.
2. **Establecer las Swimlanes:** Crear columnas para los actores o subsistemas participantes.
3. **Colocar Nodo Inicial (`●`) y Primera Acción:** Ubicar la tarea con la que arranca el flujo.
4. **Modelar Flujos Secuenciales y Condicionales:** Usar rombos (`◇`) con guardas `[si]` / `[no]` para caminos alternativos.
5. **Identificar Concurrencia (FORK / JOIN):** Usar barras gruesas cuando dos tareas puedan ejecutarse en paralelo (ej. *Subir Archivo* y *Generar Vista Previa*).
6. **Conectar al Nodo Final (`◉`):** Garantizar que todas las ramas finalicen correctamente.

---

## ⚠️ 5. Errores Frecuentes en Evaluaciones (UTN / Larman)

| Error Frecuente | Por qué está mal según Larman | Forma Correcta |
| :--- | :--- | :--- |
| **Confundir Nodo de Decisión con FORK** | Un rombo de decisión elige **un solo camino**; un FORK ejecuta **todos los caminos en paralelo**. | Usar **Rombo `◇`** para condicionales `if` y **Barra negra `❚`** para concurrencia. |
| **Olvidar el JOIN tras un FORK** | Si no se sincronizan las ramas en paralelo, el flujo continuará duplicado de manera indeterminada. | Cerrar siempre los flujos paralelos con una barra **JOIN `❚`**. |
| **Acciones cruzando Swimlanes sin orden** | Las acciones deben quedar contenidas dentro de la columna responsable. | Ajustar la posición vertical/horizontal de la acción en su calle adecuada. |
