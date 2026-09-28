# Teórica Completa: Diagrama de Estados / Máquina de Estados (UML 2.x)
**Bibliografía de Referencia:** Craig Larman, *UML y Patrones* (2ª Edición en Español), **Capítulo 29 (Págs. 423–436 del libro impreso / Páginas 454–467 del PDF)**.

---

## 📌 1. Introducción y Propósito en el Proceso Unificado (PU)

El **Diagrama de Máquina de Estados** describe el ciclo de vida de un objeto reactivo o de una entidad del dominio, mostrando la secuencia de estados por los que pasa en respuesta a eventos del entorno durante su existencia.

Según el libro de Craig Larman (**Cap. 29, Pág. 423 / PDF Pág. 454**):
> *“Un diagrama de estados de UML muestra el ciclo de vida de un objeto reactivo al estado: los eventos que experimenta, sus transiciones y las respuestas.”*

En el **Proceso Unificado (PU)**, se aplica durante la fase de **Elaboración / Diseño** para objetos complejos cuyos comportamientos cambian radicalmente según su condición actual (ej. un `Archivo` o un `Documento` que puede estar *Borrador*, *Publicado*, *Archivado* o *Eliminado*).

---

## 📐 2. Elementos Notacionales y Reglas Visuales Estrictas (Larman, Pág. 424)

| Elemento | Figura / Contorno | Tipo de Trazo | Punta de Flecha | Semántica Notacional de Larman |
| :--- | :--- | :--- | :--- | :--- |
| **Estado Inicial** | Círculo negro sólido (`●`) | N/A | N/A | Indica el punto de origen del ciclo de vida del objeto. |
| **Estado Final** | Círculo negro con anillo exterior (`◉`) | N/A | N/A | Indica el fin o destrucción de la instancia del objeto. |
| **Estado** | **Rectángulo con esquinas redondeadas** | Trazo sólido continuo | N/A | Situación o condición en la que se encuentra el objeto satisfaciendo una invariante. |
| **Transición** | N/A | **Línea sólida continua** (`──`) | **Flecha abierta en V** (`──>`) | Transición de un estado a otro disparada por un evento o condición. |
| **Superestado / Estado Anidado** | Rectángulo redondeado contenedor | Trazo continuo o punteado | N/A | Agrupa sub-estados que comparten transiciones comunes. |

---

## 🧠 3. Semántica Formal de una Transición UML (Larman, Cap. 29, Pág. 425)

Según la norma UML y Larman, toda transición entre estados se etiqueta obligatoriamente respetando el siguiente formato canónico:

$$\text{Evento}(\text{parámetros}) \; [\text{CondiciónGuard}] / \text{Acción}(\text{parámetros})$$

### Componentes de la Etiqueta:
1. **Evento (*Trigger*):** El estímulo externo o llamada a método que dispara el intento de transición (ej. `solicitarAlmacenamiento()`).
2. **Condición de Guarda (`[guard]`):** Expresión booleana entre corchetes. Debe evaluarse como `true` en el instante del evento para que la transición ocurra (ej. `[espacioDisponible == true]`). Si se evalúa como `false`, la transición no ocurre y el objeto permanece en su estado actual.
3. **Acción (`/ accion`):** Operación ejecutable inmediata e atómica que se ejecuta **durante** la transición (ej. `/ registrarEnLog()`).

---

## 🛠️ 4. Metodología Paso a Paso para Construirlo (Larman)

1. **Identificar Objeto Reactivo:** Elegir la entidad del sistema cuyos métodos dependen drásticamente de su estado actual.
2. **Definir Estado Inicial (`●`) y Estado Final (`◉`):** Marcar cómo nace y cómo termina el objeto.
3. **Listar Estados Posibles:** Identificar los nombres de estados en participio/adjetivo (ej. *Creado*, *Procesando*, *Almacenado*, *Error*).
4. **Trazar Transiciones y Eventos Disparadores:** Unir los estados mediante flechas directas y definir el evento que las activa.
5. **Añadir Condición de Guarda y Acciones:** Especificar corchetes `[guard]` y acciones `/ accion` en transiciones condicionales.

---

## ⚠️ 5. Errores Frecuentes en Evaluaciones (UTN / Larman)

| Error Frecuente | Por qué está mal según Larman | Forma Correcta |
| :--- | :--- | :--- |
| **Dibujar estados con rectángulos de esquinas rectas** | Los rectángulos rectos corresponden a Clases o Componentes. | Usar obligatoriamente **rectángulos de esquinas redondeadas**. |
| **Olvidar los corchetes en la Condición de Guarda** | Los corchetes `[ ]` son requeridos por el estándar UML para distinguir un Guard de un Evento. | Escribir siempre `[condicion == true]`. |
| **Nombrar estados como verbos de acción** | Un estado es una *situación de espera*, no una tarea ejecutándose. | Usar participios/adjetivos (ej. `Almacenado`, no "Almacenar"). |

---

## 🔄 6. Ciclo de Vida y Máquina de Estados del Pedido ("Pedalea" - V1.0 a V1.3)

En las especificaciones oficiales de los trabajos de cátedra (PDF V1.0 a V1.3), el objeto reactivo central es el **`Pedido`**:

- **Estados Principales:** `En Espera` $\longrightarrow$ `Procesando` $\longrightarrow$ `Finalizado` / `Error`.

- **Reglas Estrictas de Transición del Dominio:**
  1. **Inicio (`●` $\rightarrow$ `En Espera`):** Disparado por la acción `crearPedido()`.
  2. **Toma de Pedido (`En Espera` $\rightarrow$ `Procesando`):** El Encargado valida el pedido y cambia su estado a `Procesando`, iniciando simultáneamente la preparación en cocina.
  3. **Conclusión (`Procesando` $\rightarrow$ `Finalizado`):** Se desencadena una vez completados **tanto** la preparación en cocina **como** el cálculo de descuento.
  4. **Regla Especial de Cancelación (PDF V1.2 y V1.3):**
     - La acción `cancelarPedido()` está permitida **únicamente desde el estado `Procesando`**.
     - **Acción en Transición (`/ accion`):** `cancelarPedido() / incrementarCantidadMenusPorDia()`. Al cancelar desde el estado *Procesando*, se actualiza el stock devolviendo e incrementando la disponibilidad de menús del día.

