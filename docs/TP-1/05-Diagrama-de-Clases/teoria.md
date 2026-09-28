# Teórica Completa: Diagrama de Clases (UML 2.x)
**Bibliografía de Referencia:** Craig Larman, *UML y Patrones* (2ª Edición en Español), **Capítulo 9 (Págs. 119–140 / PDF 150–171) y Capítulo 19 (Págs. 287–310 / PDF 318–341)**.

---

## 📌 1. Introducción y Propósito en el Proceso Unificado (PU)

El **Diagrama de Clases** es el diagrama pilar de la Orientación a Objetos. Muestra la estructura estática del sistema modelando sus clases, atributos, operaciones, relaciones de asociación, herencia y dependencias.

> 💡 **Distinción Crítica de Perspectivas en Larman (Cap. 9 vs Cap. 19):**
> 1. **Modelo del Dominio / Perspectiva Conceptual (Cap. 9, Pág. 119):** Se crea en la fase de **Inicio/Elaboración**. Modela conceptos del mundo real. **NO incluye métodos de software, visibilidades ni tipos de datos de programación**.
> 2. **Diagrama de Clases de Diseño (DCD) / Perspectiva de Software (Cap. 19, Pág. 287):** Se crea en la fase de **Diseño**. Modela clases reales de código con visibilidades (`+`, `-`), firmas completas de métodos, tipos concretos, navegabilidad y tipos de colección.

---

## 📐 2. Elementos Notacionales y Reglas Visuales Estrictas (Larman, Cap. 19, Pág. 288)

### A. Anatomía de una Clase de Diseño (Caja de 3 Compartimientos)
```
+-------------------------------------------------------+
| NombreDeLaClase («abstract» / «interface»)           |
+-------------------------------------------------------+
| - atributoPrivado: Tipo = valorInicial                |
| # atributoProtegido: Tipo                             |
| + atributoPublico: Tipo                               |
+-------------------------------------------------------+
| + operacionPublica(param1: Tipo): TipoDevuelto        |
| + operacionAbstracta(): void                          |
+-------------------------------------------------------+
```

### B. Visibilidad de Miembros
- `-` **Privado:** Accesible únicamente dentro de la misma clase.
- `#` **Protegido:** Accesible por la clase y sus subclases heredadas.
- `+` **Público:** Accesible desde cualquier otra clase del sistema.
- `~` **Package/Paquete:** Accesible dentro del mismo namespace/paquete.

### C. Matriz Notacional de Relaciones entre Clases (Larman, Cap. 19, Pág. 295)

| Relación | Tipo de Trazo | Tipo de Punta / Rombo | Ubicación de la Flecha / Rombo | Semántica Notacional de Larman |
| :--- | :--- | :--- | :--- | :--- |
| **Asociación** | **Línea sólida continua** (`──`) | Flecha abierta `>` (opcional si hay navegabilidad) | Hacia la clase asociada | Relación estructural persistente entre instancias. |
| **Herencia (Generalización)** | **Línea sólida continua** (`──`) | **Triángulo blanco hueco** (`──▷`) | Apunta a la **Superclase / Padre** | Subclase hereda atributos y operaciones de la superclase. |
| **Agregación** | **Línea sólida continua** (`──`) | **Rombo blanco/transparente** (`◇──`) | Rombo del lado de la **Clase Contenedora** | Relación "Todo-Parte" débil (las partes viven sin el contenedor). |
| **Composición** | **Línea sólida continua** (`──`) | **Rombo negro/relleno** (`◆──`) | Rombo del lado de la **Clase Contenedora** | Relación "Todo-Parte" fuerte (destrucción en cascada de partes). |
| **Dependencia** | **Línea punteada** (`- - -`) | **Flecha abierta en V** (`- - >`) | Apunta a la clase usada | Uso temporal (parámetro de método o variable local). |

---

## 🧠 3. Semántica de Multiplicidad y Navegabilidad (Larman, Cap. 9, Pág. 129)

### A. Reglas de Multiplicidad
- `1` : Exactamente una instancia obligatoria.
- `0..1` : Cero o una instancia (opcional / nullable).
- `*` o `0..*` : Cero o muchas instancias (colección).
- `1..*` : Al menos una instancia obligatoria (uno o muchos).

### B. Agregación vs Composición (Cap. 19, Pág. 302)
- **Agregación (`◇`):** Una `Carpeta` contiene `Archivos`. Si borramos la carpeta, los archivos pueden seguir existiendo en el disco o moverse a otra carpeta.
- **Composición (`◆`):** Un `Archivo` contiene `BloquesDeMemoria`. Si se destruye el objeto `Archivo`, sus `BloquesDeMemoria` asociados son eliminados instantáneamente.

---

## 🛠️ 4. Metodología Paso a Paso para Construirlo (Larman)

1. **Identificar Clases del Dominio:** Extraer sustantivos relevantes de los casos de uso.
2. **Definir Atributos Básicos:** Añadir atributos primitivos (nombre, fecha, tamaño) a cada clase.
3. **Establecer Asociaciones y Multiplicidades:** Determinar las conexiones entre clases y sus cardinalidades reales.
4. **Refinar hacia Perspectiva de Software (DCD):** Convertir el modelo en clases de diseño agregando métodos, visibilidades (`-`, `+`) y navegabilidades.
5. **Aplicar Herencia o Interfaces:** Extraer clases abstractas o interfaces ante comportamientos polimórficos repetidos.

---

## ⚠️ 5. Errores Frecuentes en Evaluaciones (UTN / Larman)

| Error Frecuente | Por qué está mal según Larman | Forma Correcta |
| :--- | :--- | :--- |
| **Poner métodos en un Modelo del Dominio** | El modelo del dominio es conceptual, no incluye métodos de código. | Incluir métodos solo al crear el Diagrama de Clases de Diseño (DCD). |
| **Confundir el rombo de Composición con Agregación** | Usar `◇` en vez de `◆` para relaciones de vida dependiente. | Usar rombo **negro relleno `◆`** cuando las partes mueren con el todo. |
| **Invertir la flecha de herencia** | La flecha de herencia debe apuntar hacia el padre (superclase), no al hijo. | Apuntar el triángulo blanco hueco `──▷` a la Superclase. |

---

## 📦 6. Dominio de Clases de Cátedra ("Pedalea" - V1.0 a V1.3)

En el Diagrama de Clases de Diseño (DCD) para el **Sistema Pedalea**, se destacan las siguientes clases y relaciones:

- **`Usuario` (Clase Base / Abstracta):** `idUsuario: int`, `nombre: String`, `historialCompras: List<Pedido>`.
- **`ClienteBicicleta` (Subclase / Herencia `──▷ Usuario`):** Incluye lógica específica para la aplicación del 20% de descuento cuando su compra actual supera el promedio de las últimas tres.
- **`Pedido`:** `idPedido: int`, `montoTotal: double`, `estado: EstadoPedido` (`EnEspera`, `Procesando`, `Finalizado`, `Error`). Relación de composición `◆` con `ItemPedido`.
- **`Menu`:** `idMenu: int`, `nombre: String`, `precio: double`, `tipoMenu` (`Vegetariano`, `Vegano`, `SinGluten`, `Tradicional`), `disponible: boolean`.
- **`Restaurante`:** Contiene `Menu` mediante agregación `◇` y gestiona el stock diario.
- **`Encargado`:** Responsable de invocar la operación `procesarPedido()` y `confirmarEntrega()`.

---

## 🏭 7. Integración de Patrones Creacionales: Patrón Factory (Clase 05 - Cátedra UTN)

En la Clase 05 de la materia se evalúa la integración de patrones de diseño GoF (*Gang of Four*), específicamente el **Patrón Factory / Factory Method**:

### A. Caso de Estudio de Cátedra: "Reinos de Algoria"
El ejercicio oficial modela un Gremio que gestiona personajes (`Guerrero` y `Mago`):
- **`Personaje` (Clase Abstracta / Superclase):** `idJugador: int`, `nombre: String`, `apodo: String`, `anioCreacion: int`. Define el método abstracto `mostrarValorCombate()`.
- **`Guerrero` (Subclase):** `poderAtaqueBase`, `victoriasDuelo`, `bonoPorVictoria`. `fuerzaTotal = max(poderAtaqueBase, victorias * bono)`.
- **`Mago` (Subclase):** `reservaManaBase`. Calcula la bonificación según la antigüedad:
  - $< 3$ años: $0\%$ extra.
  - $3 \text{ a } 6$ años: $+4\%$ de maná extra sobre la base.
  - $> 6$ años: $+12\%$ de maná extra sobre la base.
- **`PersonajeFactory` (Fábrica Concreta / Creacional):** Encargada de instanciar guerreros o magos según los parámetros recibidos.

### B. Justificación Técnica y Beneficios según Larman y la Cátedra
1. **Desacoplamiento:** La clase `Gremio` no depende directamente de las clases concretas `Guerrero` o `Mago`, sino de la abstracción `Personaje` y de `PersonajeFactory`.
2. **Encapsulamiento Creacional:** Oculta la complejidad de los constructores y la lógica de inicialización.
3. **Principio Abierto/Cerrado (OCP):** Permite añadir nuevos tipos de personajes (ej. `Arquero`) creando una nueva subclase sin modificar el código de `Gremio`.

