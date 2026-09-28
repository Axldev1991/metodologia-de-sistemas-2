# Teórica Completa: Diagrama de Casos de Uso (UML 2.x)
**Bibliografía de Referencia:** Craig Larman, *UML y Patrones* (2ª Edición en Español), **Capítulo 6 (Págs. 63–102 del libro impreso / Páginas 94–133 del PDF)**.

---

## 📌 1. Introducción y Propósito en el Proceso Unificado (PU)

El **Modelo de Casos de Uso** describe los requerimientos funcionales del sistema desde la perspectiva de los actores externos. En el **Proceso Unificado (PU)**, es la disciplina central de las fases de **Inicio** y **Elaboración**.

> 💡 **Enfoque Doctrinal de Larman (Cap. 6, Pág. 63 / PDF Pág. 94):**
> *“Los casos de uso no son diagramas; son texto. El diagrama de casos de uso es secundario: proporciona un contexto visual simplificado para visualizar el límite del sistema y los actores.”*

---

## 📐 2. Elementos Notacionales y Reglas Visuales Estrictas (Larman, Pág. 97 / PDF Pág. 128)

| Elemento | Figura / Contorno | Tipo de Trazo | Conector / Flecha | Semántica Notacional de Larman |
| :--- | :--- | :--- | :--- | :--- |
| **Actor Primario** | Monigote de palo (*Stick figure*) o `«actor»` | Trazo sólido continuo | N/A | Entidad externa (usuario u organización) cuyo objetivo es cumplido por el sistema. |
| **Actor Secundario / Soporte** | Monigote o rectángulo `«actor»` | Trazo sólido continuo | N/A | Sistema externo que proporciona un servicio (ej. Pasarela de Pago, BD Externa). |
| **Caso de Uso** | Óvalo | Trazo sólido continuo | N/A | Funcionalidad completa etiquetada estrictamente con un **verbo en infinitivo**. |
| **Límite del Sistema** | Rectángulo envolvente | Trazo sólido continuo | N/A | Separa el interior del software de los actores del entorno. |
| **Asociación** | N/A | **Línea sólida continua** | **Sin flecha** | Comunicación bidireccional entre actor y el caso de uso en el que participa. |
| **Inclusión (`«include»`)** | N/A | **Línea punteada** (`- - -`) | Flecha abierta en V (`- - >`) | Apunta **hacia el CU incluido (obligatorio)**. Reutilización de subrutina común. |
| **Extensión (`«extend»`)** | N/A | **Línea punteada** (`- - -`) | Flecha abierta en V (`- - >`) | Apunta **hacia el CU base (opcional)**. Ejecución condicional en un punto de extensión. |
| **Generalización** | N/A | **Línea sólida continua** | **Triángulo blanco hueco** (`──▷`) | Especialización de roles de actores o de flujos de casos de uso. |

---

## 🧠 3. Semántica y Formatos de Casos de Uso (Larman, Cap. 6, Pág. 67)

### A. Formatos de Redacción según Larman:
1. **Breve:** Resumen de un párrafo del escenario principal de éxito.
2. **Informal:** Varios párrafos informalmente estructurados.
3. **Completo (*Fully Dressed* - Pág. 68):** Notación formal detallada con:
   - **Nombre en infinitivo** (ej. *Almacenar Archivo*).
   - **Actor Primario**, **Precondiciones** y **Garantías de Éxito / Postcondiciones**.
   - **Escenario Principal de Éxito** (flujo básico numerado paso a paso).
   - **Flujos Alternativos / Extensiones** (desviaciones o manejo de errores).

### B. Relaciones `«include»` vs `«extend»` (Larman, Pág. 98)
- **`«include»` (Inclusión Obligatoria):** El caso de uso origen **siempre** desencadena el caso de uso incluido. Evita duplicación de texto en pasos comunes.
- **`«extend»` (Extensión Condicional):** El caso de uso base se ejecuta normalmente, pero bajo cierta condición en un *Punto de Extensión*, el flujo se desvía al caso de uso de extensión.

---

## 🛠️ 4. Metodología Paso a Paso para Construirlo (Larman)

1. **Identificar el Límite del Sistema:** Definir claramente qué está dentro del software y qué queda afuera.
2. **Identificar Actores Primarios:** Responder: *¿Quiénes usan el sistema para lograr sus metas diarias?*
3. **Identificar Casos de Uso:** Para cada actor, definir sus metas de usuario redactadas en **verbo infinitivo** (ej. *Crear Carpeta*, *Eliminar Archivo*).
4. **Agregar Actores Secundarios:** Identificar sistemas externos, servidores de archivos o BDs con los que interactúa el sistema.
5. **Evaluar Factorización (`«include»` / `«extend»`):** Identificar comportamientos repetidos u opcionales sin sobre-diseñar el diagrama.

---

## ⚠️ 5. Errores Frecuentes en Evaluaciones (UTN / Larman)

| Error Frecuente | Por qué está mal según Larman | Forma Correcta |
| :--- | :--- | :--- |
| **Nombrar el CU como sustantivo** | Un CU es una acción o meta de usuario, no una entidad. | Usar verbos en infinitivo (ej. `Almacenar Archivo`, no "Almacenamiento"). |
| **Invertir la flecha de `«extend»`** | Confusión común: creen que la flecha señala hacia la extensión. | La flecha de `«extend»` apunta **hacia el CU base**. |
| **Modelar pasos de algoritmo como CU** | "Presionar Botón", "Validar Password" no son casos de uso; son pasos dentro de un texto. | Agrupar los pasos en un CU de alto nivel com valor para el usuario. |

---

## 🍕 6. Casos de Uso del Sistema de Cátedra ("Pedalea" - V1.0 a V1.3)

En el dominio de la materia (**Sistema Pedalea**), los Casos de Uso se estructuran según los siguientes roles y metas:

- **Actores del Sistema:**
  - **`Cliente` (Actor Primario):** Busca menús, crea pedidos, modifica pedidos y cancela pedidos.
  - **`Restaurante` (Actor Primario):** Gestiona la oferta de menús (crear, editar, eliminar y actualizar estado disponible/no disponible).
  - **`Encargado` (Actor de Soporte / Validador):** Toma el pedido, cambia el estado a *Procesando* y confirma la entrega del menú al cliente.

- **Inventario de Casos de Uso Clave (Notación Infinitivo):**
  1. **`Buscar Menú por Precio / Tipo`** (Vegetariano, Vegano, Sin Gluten, Tradicional).
  2. **`Crear Pedido`**: Incluye validación de disponibilidad del menú (`«extend»` notificación si no hay stock).
  3. **`Calcular Descuento por Historial`** (`«extend»` desde `Crear Pedido` si el cliente retira en bicicleta y la compra actual es mayor al promedio de las últimas 3).
  4. **`Gestionar Menús`**: Agrupa las operaciones ABM del Restaurante.
  5. **`Validar y Procesar Pedido`**: Ejecutado por el Encargado al iniciar la preparación.
  6. **`Cancelar Pedido`**: Permitido **únicamente** cuando el pedido se encuentra en estado *Procesando* (incrementa el stock diario de menús).

---

## 💸 7. Marco Teórico: Deuda Técnica en Requerimientos (Clase 01 - Rocío Castillo / Fowler)

En la Clase 01 de la materia se introduce el concepto fundamental de **Deuda Técnica** (*Technical Debt*), estrechamente vinculado a la calidad de la especificación de casos de uso y diseño de arquitectura:

### A. Origen y Definición (Ward Cunningham, 1992)
> *“Entregar código la primera vez es como tomar deuda. Un poco de deuda acelera el desarrollo en la medida que se paga rápidamente con recodificación... El peligro ocurre cuando la deuda no se paga. Cada minuto gastado en un código que no es correcto cuenta como interés de esa deuda.”*

### B. La Metáfora Financiera
- **Descuidar el diseño o los requerimientos:** Equivale a pedir dinero prestado para salir rápido al mercado.
- **Desarrollar más lento en el futuro:** Equivale a pagar **intereses** sobre la deuda acumulada.
- **Refactorizar el código / Clarificar Casos de Uso:** Equivale a pagar el **capital** de la deuda.

### C. Clasificación de Deuda Técnica (Rocío Castillo / Martin Fowler)
1. **Intencional vs No Intencional:**
   - **Intencional:** Se asume un atajo consciente a corto plazo para cumplir una entrega crítica, con plan de refactorización posterior.
   - **No Intencional:** Ocurre por descuido, falta de capacitación, mal análisis de casos de uso o código negligente.
2. **Cuadrante de Deuda Técnica de Martin Fowler:**
   - *Reckless / Deliberate* (Temeraria / Deliberada): "No tenemos tiempo para diseñar".
   - *Reckless / Inadvertent* (Temeraria / Inadvertida): "¿Qué son los patrones de diseño?".
   - *Prudent / Deliberate* (Prudente / Deliberada): "Debemos entregar ya y pagaremos la deuda en el siguiente sprint".
   - *Prudent / Inadvertent* (Prudente / Inadvertida): "Ahora que terminamos, comprendemos cómo debimos haberlo diseñado desde el inicio".

