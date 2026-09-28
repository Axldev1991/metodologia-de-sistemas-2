# Teórica Completa: Diagrama de Secuencia (UML 2.x)
**Bibliografía de Referencia:** Craig Larman, *UML y Patrones* (2ª Edición en Español), **Capítulo 15, Sección 15.4 (Págs. 216–225 del libro impreso / Páginas 247–256 del PDF)**.

---

## 📌 1. Introducción y Propósito en el Proceso Unificado (PU)

El **Diagrama de Secuencia (DS)** es un diagrama de interacción de tipo dinámico que modela la colaboración entre objetos ordenada explícitamente a lo largo del tiempo.

Según el libro de Craig Larman (**Cap. 15, Pág. 216 / PDF Pág. 247**):
> *“Los diagramas de secuencia ilustran la interacción mostrando los objetos verticalmente y el tiempo que transcurre hacia abajo en el eje vertical, con los mensajes enviados entre objetos como líneas horizontales.”*

Dentro del **Proceso Unificado (PU)**, se genera durante la fase de **Elaboración / Diseño**, convirtiendo la narrativa textual de los Casos de Uso en invocaciones de métodos de software concreto.

---

## 📐 2. Elementos Notacionales y Reglas Visuales Estrictas (Larman, Pág. 217)

| Elemento | Figura / Contorno | Tipo de Trazo | Conector / Flecha | Semántica Notacional de Larman |
| :--- | :--- | :--- | :--- | :--- |
| **Línea de Vida (*Lifeline*)** | Rectángulo `:Clase` o `nombre:Clase` en la parte superior | **Línea vertical punteada** (`┊`) | N/A | Representa la existencia temporal del objeto durante la interacción. El tiempo fluye **de arriba hacia abajo**. |
| **Bloque de Activación** | Rectángulo vertical angosto sobre la línea de vida | Trazo sólido continuo | N/A | Período en el cual el objeto tiene el foco de control y está ejecutando un método. |
| **Mensaje Síncrono** | N/A | **Línea horizontal sólida** (`──`) | **Flecha negra llena** (`──►`) | Invocación de método donde el emisor **bloquea su ejecución** hasta recibir respuesta. |
| **Mensaje Asíncrono** | N/A | **Línea horizontal sólida** (`──`) | **Flecha abierta en V** (`──>`) | Invocación no bloqueante donde el emisor continúa su procesamiento. |
| **Mensaje de Retorno** | N/A | **Línea horizontal punteada** (`- -`) | **Flecha abierta en V** (`- - >`) | Devolución opcional de datos o transferencia de control al invocador. |
| **Creación de Objeto** | N/A | **Línea horizontal sólida o punteada** | Flecha abierta con `«create»` | Apunta directamente al rectángulo del objeto recién instanciado. |
| **Fragmentos (`alt / loop`)** | Rectángulo con etiqueta en la esquina superior izquierda | Trazo sólido con divisiones punteadas horizontales | N/A | Marcos de control lógico (`alt` para condicionales `if/else`, `loop` para iteraciones). |

---

## 🧠 3. Semántica y Conceptos Clave del Libro (Larman, Cap. 15)

### A. Mensajes del Sistema vs Mensajes entre Objetos
- **Diagrama de Secuencia del Sistema (SSD - Cap. 9):** Muestra al actor interactuando con el sistema como una "caja negra" (`:Sistema`).
- **Diagrama de Secuencia de Diseño (DSD - Cap. 15):** Descompone la "caja negra" mostrando las interacciones entre los objetos internos de software (`Controller`, `Service`, `Repository`, `Entity`).

### B. Notación de Mensajes y Autoflechas
- **Firma de Invocación:** `resultado := mensaje(param1: Tipo, param2: Tipo)`.
- **Autoflecha (*Self-Call*):** Una flecha que sale del bloque de activación de un objeto y vuelve al mismo objeto indica una llamada a un método privado o interno (`this.metodoInterno()`).

### C. Manejo de Errores con Fragments `alt`
Para cumplir con los requerimientos de la cátedra y Larman, las condiciones de error o falla (ej. *Espacio Insuficiente*, *Archivo No Encontrado*) deben modelarse en la división inferior de un marco `alt`, mostrando la interrupción del flujo y la emisión del mensaje de error hacia el cliente.

---

## 🛠️ 4. Metodología Paso a Paso para Construirlo (Larman)

1. **Tomar como insumo el texto de un Caso de Uso:** Elegir un escenario específico (ej. *Almacenar Archivo*).
2. **Identificar la Clase Controlador (GRASP Controller):** Crear el objeto de entrada del sistema (ej. `:GestorArchivosController`).
3. **Modelar la recepción del mensaje inicial:** Trazar la flecha síncrona desde el actor o GUI hacia el controlador.
4. **Distribuir Responsabilidades a Clases del Dominio/Servicio:** Trazar invocaciones sucesivas entre clases de negocio (ej. `:Directorio`, `:Archivo`, `:AlmacenamientoDrive`).
5. **Añadir Frames de Control (`alt` / `loop`):** Delimitar bloques condicionales para validar precondiciones y errores.

---

## ⚠️ 5. Errores Frecuentes en Evaluaciones (UTN / Larman)

| Error Frecuente | Por qué está mal según Larman | Forma Correcta |
| :--- | :--- | :--- |
| **Usar flecha sólida para el mensaje de retorno** | La flecha sólida indica una invocación de método nueva, no una devolución. | Usar **línea punteada** con flecha abierta (`- - >`). |
| **No incluir bloques de activación** | Sin el bloque de activación no se comprende qué objeto posee el foco de control ejecutivo. | Dibujar la cajita vertical sobre la línea punteada mientras el método esté activo. |
| **Cruzar líneas de tiempo hacia arriba** | El tiempo siempre fluye hacia abajo; una flecha horizontal ascendente es conceptualmente imposible. | Dibujar los mensajes estrictamente descendentes. |

---

## 🚴 6. Escenarios Prácticos de Secuencia de Cátedra ("Pedalea" - V1.1 a V1.3)

En las guías y consignas oficiales de la cátedra se requiere el modelado estricto de dos escenarios clave de interacción:

### Escenario A: Cálculo de Precio Final con Descuento (Usuario en Bicicleta)
1. El `:Cliente` invoca `crearPedido(datosPedido)` sobre `:PedidosController`.
2. `:PedidosController` consulta al `:HistorialService` enviando `obtenerUltimas3Compras(idUsuario)`.
3. `:HistorialService` calcula el `promedio` de los montos de las últimas 3 compras.
4. Marco `alt [montoActual > promedio]`:
   - Rama `true`: `:PedidosController` invoca `aplicarDescuento(0.20)` sobre el objeto `:Pedido` actual.
   - Rama `false` / `else`: Mantiene el precio sin bonificación.
5. Retorno `- - >` del precio final calculado hacia el `:Cliente`.

### Escenario B: Modificación de Pedido por el Usuario
1. El `:Cliente` invoca `modificarPedido(idPedido, nuevosItems)` sobre `:PedidosController`.
2. `:PedidosController` solicita a `:Menu` la verificación de disponibilidad (`validarDisponibilidad()`).
3. Marco `alt`:
   - **Si `disponible == false`**: Se emite la notificación de error hacia el cliente y se cancela la modificación.
   - **Si `disponible == true`**: Se actualizan los ítems del pedido y se recalcula el total.

