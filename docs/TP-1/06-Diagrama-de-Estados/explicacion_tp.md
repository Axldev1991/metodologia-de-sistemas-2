# Explicación del Diagrama de Estados del TP-1

---

## 🎯 Objetivo en el Trabajo Práctico

Cumplir con el **Punto 6 de la consigna**, identificando una funcionalidad donde sea representativo aplicar una máquina de estados (ciclo de vida de las **Acciones del Usuario**), indicando estados, eventos, condiciones de guarda y acciones asociadas.

---

## 🔄 Estados Representados

De acuerdo con la consigna del dominio:
> *"Las acciones (copiar, borrar, renombrar) dadas por el Usuario tienen estados como por ejemplo: en espera, creada, en proceso, finalizada o con error."*

```
(● Inicio) ➔ [ Creada ] ➔ [ En espera ] ➔ [ En proceso ] ┬─► [ Finalizada ] ➔ (◉ Fin)
                                                         └─► [ Con error ]  ➔ (◉ Fin)
```

---

## 🛠️ Transiciones y Reglas de Negocio

1. **`(*) ➔ Creada`**
   - **Evento:** `solicitarAccion()`
   - **Descripción:** El usuario solicita una acción (copiar, borrar o renombrar).

2. **`Creada ➔ En espera`**
   - **Sintaxis:** `encolarAccion() / asignarID()`
   - **Descripción:** La acción entra a la cola de procesamiento del sistema.

3. **`En espera ➔ En proceso`**
   - **Sintaxis:** `despacharAccion() / reservarRecursos()`
   - **Descripción:** El sistema toma la acción de la cola y comienza la ejecución.

4. **`En proceso ➔ Finalizada`** *(Transición Exitosa)*
   - **Sintaxis:** `ejecutar() [valido == true] / notificarResultadoExitoso()`
   - **Descripción:** La operación se completa correctamente sin excepciones.

5. **`En proceso ➔ Con error`** *(Transición Fallida)*
   - **Sintaxis:** `ejecutar() [espacioInsuficiente == true] / generarAvisoError()`
   - **Descripción:** Ocurre una falla (por ejemplo, falta de espacio o archivo inexistente).

---

## 🛠️ ¿Cómo abrir y modificar el diagrama?
1. Abrí [`06_estados.drawio`](file:///home/axel/Escritorio/UTN/M%20de%20Sistemas%20II/docs/TP-1/06-Diagrama-de-Estados/06_estados.drawio) en VS Code.
