# Teórica Completa: Diagrama de Componentes (UML 2.x)
**Bibliografía de Referencia:** Craig Larman, *UML y Patrones* (2ª Edición en Español), **Capítulo 38, Sección 38.3 (Págs. 566–568 del libro impreso / Páginas 597–599 del PDF)**.

---

## 📌 1. Introducción y Propósito en el Proceso Unificado (PU)

El **Diagrama de Componentes** describe la organización y las dependencias entre los módulos de software físicos o lógicos.

Según el libro oficial de Craig Larman (**Cap. 38, Pág. 566 / PDF Pág. 597**):
> *“Un componente de UML representa un elemento físico y reemplazable de un sistema que empaqueta la implementación y se ajusta a un conjunto de interfaces que proporciona o utiliza.”*
> Ejemplos citados por Larman: *"Módulos ejecutables, ficheros DLL, ficheros JAR (como para un Enterprise Java Bean), un navegador o servidor HTTP, o una base de datos."*

Dentro del **Proceso Unificado (PU)**, se desarrolla durante la fase de **Elaboración / Arquitectura**, permitiendo definir la estructura modular del sistema antes de la codificación masiva.

---

## 📐 2. Elementos Notacionales y Reglas Visuales Estrictas (Larman, Pág. 567)

| Elemento | Figura / Contorno | Tipo de Trazo | Conector / Flecha | Semántica Notacional de Larman |
| :--- | :--- | :--- | :--- | :--- |
| **Componente** | Rectángulo con estereotipo `«component»` (o `«file»`, `«database»`, `«executable»`) | Trazo sólido continuo | N/A | Elemento físico reemplazable que empaqueta código o datos. |
| **Interfaz Provista** | Círculo completo (*Lollipop*) | Línea sólida continua desde el componente | Círculo lleno/blanco `◯` | Expone los métodos y API que el componente ofrece al exterior. |
| **Interfaz Requerida** | Semicírculo (*Socket*) | Línea sólida continua desde el componente | Semicírculo abierto `⊂` | Representa los servicios externos que el módulo necesita para funcionar. |
| **Dependencia** | N/A | **Línea punteada** (`- - -`) | Flecha abierta en V (`- - >`) con `«use»` o `«imports»` | Indica que un componente requiere de otro para completar sus tareas. |
| **Subsistema / Nodo** | Rectángulo envolvente | Trazo continuo o punteado grueso | N/A | Agrupa componentes dentro de un mismo entorno de despliegue. |

---

## 🧠 3. Semántica y Conceptos Arquitectónicos Clave (Larman, Cap. 38)

### A. Encapsulamiento y Ocultamiento de Información
Un componente **nunca expone su código interno ni sus estructuras de datos privadas**. Toda interacción ocurre exclusivamente a través de sus interfaces provistas y requeridas.

### B. Principio de Sustituibilidad
Cualquier componente se puede reemplazar por otra versión (ej. cambiar un módulo de persistencia local por uno cloud) sin afectar al resto del sistema, **siempre que la nueva versión respete la misma interfaz provista (`◯`)**.

### C. Acoplamiento Débil y Alta Cohesión
- **Alta Cohesión:** Las clases dentro de un componente colaboran para un único propósito funcional delimitado.
- **Acoplamiento Débil:** Las dependencias entre componentes no se realizan contra clases concretas, sino contra abstracciones/interfaces.

---

## 🛠️ 4. Metodología Paso a Paso para Construirlo (Larman)

1. **Identificar los Subsistemas del Sistema:** Analizar la arquitectura en capas (ej. GUI, Servicios de Negocio, Acceso a Datos).
2. **Definir Módulos Reutilizables:** Identificar bibliotecas externas (ej. Loggers, Parsers XML) y módulos centrales del dominio.
3. **Mapear Interfaces Provistas (`◯`):** Determinar qué contratos u operaciones expone cada componente hacia otros módulos.
4. **Mapear Interfaces Requeridas (`⊂`):** Determinar qué dependencias externas necesita cada componente para ejecutar sus responsabilidades.
5. **Trazar Enlaces de Acoplamiento:** Unir los conectores *Lollipop* (`◯`) y *Socket* (`⊂`) de los componentes colaboradores.

---

## ⚠️ 5. Errores Frecuentes en Evaluaciones (UTN / Larman)

| Error Frecuente | Por qué está mal según Larman | Forma Correcta |
| :--- | :--- | :--- |
| **Conectar componentes directamente sin interfaces** | Genera acoplamiento fuerte y viola el encapsulamiento. | Usar conectores *Lollipop* (`◯`) y *Socket* (`⊂`). |
| **Poner clases dentro del diagrama de componentes** | Mezcla el nivel de diseño de clases con el nivel arquitectónico modular. | Solo incluir componentes, subsistemas e interfaces. |
| **Invertir el sentido de la flecha de dependencia** | La flecha punteada debe apuntar al módulo que **brinda el servicio**, no al consumidor. | Emisor (Cliente) `- - >` Receptor (Servicio). |

---

## 🏬 6. Aplicación Práctica al Dominio de Cátedra ("Pedalea" - V1.3)

En el sistema de referencia de la materia (**Sistema Pedalea**), el Diagrama de Componentes organiza la arquitectura en subsistemas independientes desacoplados mediante interfaces provistas (`◯`) y requeridas (`⊂`):

1. **`«component» ComponenteUI / AppWeb`**: Interfaz de usuario utilizada por Clientes y Encargados. Requiere de la API del controlador de pedidos.
2. **`«component» PedidosService`**: Componente central de gestión de pedidos. Expone `◯ IPedido` y consume `⊂ IDescuento` e `⊂ ICocina`.
3. **`«component» DescuentosService`**: Módulo encargado de calcular el 20% de descuento comparando el costo actual contra el promedio de las últimas 3 compras del cliente. Expone `◯ IDescuento`.
4. **`«component» CocinaService`**: Módulo del restaurante que gestiona el stock de menús por día e inicia la preparación. Expone `◯ ICocina`.
5. **`«component» HistorialRepository`**: Componente de persistencia para consultar compras pasadas. Expone `◯ IHistorial`.

