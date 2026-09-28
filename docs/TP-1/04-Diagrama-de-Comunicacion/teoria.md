# Teórica Completa: Diagrama de Comunicación / Colaboración (UML 2.x / 1.x)
**Bibliografía de Referencia:** Craig Larman, *UML y Patrones* (2ª Edición en Español), **Capítulo 15, Sección 15.3 (Págs. 211–216 del libro impreso / Páginas 242–247 del PDF)**.

---

## 📌 1. Introducción y Propósito en el Proceso Unificado (PU)

El **Diagrama de Comunicación** (denominado *Diagrama de Colaboración* en UML 1.x y en la bibliografía de Craig Larman 2ª Edición) es un diagrama de interacción que ilustra el intercambio de mensajes entre objetos organizados en un grafo estático.

Según el libro de Craig Larman (**Cap. 15, Pág. 211 / PDF Pág. 242**):
> *“Los diagramas de colaboración ilustran la interacción entre objetos mediante un formato de grafo o red, en el que los objetos se sitúan en cualquier lugar del diagrama y los mensajes se muestran a lo largo de los enlaces entre ellos.”*

Dentro del **Proceso Unificado (PU)**, se utiliza de forma alternativa o complementaria al Diagrama de Secuencia durante la fase de **Elaboración**, para analizar la estructura espacial de los enlaces entre objetos de software.

---

## 📐 2. Elementos Notacionales y Reglas Visuales Estrictas (Larman, Pág. 212)

| Elemento | Figura / Contorno | Tipo de Trazo | Indicador / Flecha | Semántica Notacional de Larman |
| :--- | :--- | :--- | :--- | :--- |
| **Objeto / Instancia** | Rectángulo con texto subrayado `<u>:Clase</u>` o `<u>obj:Clase</u>` | Trazo sólido continuo | N/A | Instancia concreta de una clase participante en la interacción. |
| **Enlace (*Link*)** | N/A | **Línea sólida recta** (`──`) | **Sin flechas en los extremos de la línea** | Representa una ruta de comunicación o asociación existente entre 2 objetos. |
| **Mensaje de Invocación** | Texto al lado del enlace (ej. `1: registrar()`) | N/A | **Flecha pequeña limpia** (`➔`) alineada al texto | Invocación de método enviada en la dirección especificada por la flechita. |
| **Mensaje de Retorno** | Texto opcional al lado del enlace (ej. `2: «return» ok`) | N/A | **Flecha pequeña limpia** (`⬅`) alineada al texto | Devolución de control o datos hacia el objeto invocador. |
| **Secuencia Anidada** | Formato decimal en la etiqueta (ej. `1.1:`, `1.2:`) | N/A | N/A | Indica llamadas internas desencadenadas durante la ejecución del mensaje padre `1:`. |

---

## 🧠 3. Semántica y Comparativa: Secuencia vs Comunicación (Larman, Cap. 15, Pág. 215)

### Trade-offs y Diferencias Clave (Larman):

| Criterio | Diagrama de Secuencia | Diagrama de Comunicación / Colaboración |
| :--- | :--- | :--- |
| **Énfasis Principal** | **Secuencia temporal** limpia de arriba a abajo. | **Estructura espacial** y red de enlaces entre objetos. |
| **Facilidad de Lectura del Tiempo** | Muy alta (eje vertical explícito). | Moderada (requiere seguir los números de secuencia `1:`, `1.1:`, `2:`). |
| **Visualización de Acoplamiento** | Pobre (los objetos se repiten arriba). | **Excelente:** muestra de un vistazo cuántas conexiones tiene cada objeto. |
| **Consumo de Espacio** | Se expande horizontalmente a medida que agregás objetos. | **Muy compacto:** reutiliza el mismo rectángulo de objeto en el grafo. |

---

## 🛠️ 4. Metodología de Numeración de Secuencia (Larman, Pág. 213)

1. **Mensajes de Primer Nivel (`1:`, `2:`, `3:`):** Representan invocaciones directas desde el actor o controlador inicial.
2. **Mensajes Anidados (`1.1:`, `1.2:`):** Representan métodos invocados por el receptor del mensaje `1:` antes de responder.
3. **Anidamiento Profundo (`1.1.1:`):** Representa llamadas en cadena (ej. el servicio llama al repositorio y este a la BD).

---

## ⚠️ 5. Errores Frecuentes en Evaluaciones (UTN / Larman)

| Error Frecuente | Por qué está mal según Larman | Forma Correcta |
| :--- | :--- | :--- |
| **Poner la flecha grande al final de la línea del enlace** | Transforma la línea en una asociación dirigida o herencia, destruyendo la notación de enlace. | Mantener la línea del enlace limpia y poner una **flechita chica junto al texto del mensaje**. |
| **Olvidar subrayar el nombre del objeto** | En UML, el subrayado `<u>:Objeto</u>` es obligatorio para denotar una *instancia* (objeto) y no una clase estática. | Subrayar siempre la etiqueta del rectángulo. |
| **Olvidar los números de secuencia** | Sin los números `1:`, `2:`, `1.1:`, es imposible saber qué mensaje se envía primero. | Etiquetar cada mensaje con su número de secuencia exacto. |

---

## 📡 6. Grafo de Comunicación en el Dominio de Cátedra ("Pedalea")

A diferencia del Diagrama de Secuencia, el **Diagrama de Comunicación** permite visibilizar el acoplamiento estructural entre las instancias del sistema **Pedalea**:

- **Grafo de Enlaces:**
  `<u>:Cliente</u>` $\longleftrightarrow$ `<u>:PedidosController</u>` $\longleftrightarrow$ `<u>:HistorialService</u>` $\longleftrightarrow$ `<u>:Pedido</u>`

- **Secuencia Numerada de Invocación:**
  1. `1: crearPedido(datos)` enviada de `<u>:Cliente</u>` a `<u>:PedidosController</u>`
  2. `1.1: obtenerPromedio(idUsuario)` enviada de `<u>:PedidosController</u>` a `<u>:HistorialService</u>`
  3. `1.1.1: consultarComprasAnteriores()` enviada de `<u>:HistorialService</u>` al repositorio de base de datos.
  4. `1.2: aplicarDescuento(0.20)` enviada condicionalmente de `<u>:PedidosController</u>` a `<u>:Pedido</u>`.
  5. `1.3: «return» confirmacion` de vuelta al cliente.

