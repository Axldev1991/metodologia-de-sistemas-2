# Explicación del Diagrama de Secuencia del TP-1

---

## 🎯 Objetivo en el Trabajo Práctico

Cumplir con el **Punto 3 de la consigna**, modelando la interacción a lo largo del tiempo para el Caso de Uso **"Almacenar Archivo"**, incluyendo líneas de vida, mensajes, retornos, frames y el **Requisito PLUS (escenario de error)**.

---

## 👥 Líneas de Vida Participantes

1. `:Usuario` — Emite la solicitud de creación de archivo.
2. `:InterfazUsuario` — Captura los datos de entrada y presenta respuestas o avisos.
3. `:GestorArchivos` — Controla el flujo de negocio del sistema.
4. `:ModuloAlmacenamiento` — Encargado de la lógica de guardado y categorías.
5. `:SistemaOperativo` — Consulta y valida el espacio disponible en el disco físico.

---

## 🔁 Flujo de Mensajes y Fragmento Combinado `alt`

```
                                  [ Inicio de Solicitud ]
                                            │
                             1: crearArchivo(nombre, tipo, datos)
                                            │
                             2: procesarCreacion(nombre, tipo, datos)
                                            │
                             3: verificarEspacio(tamano)
                                            │
                             4: consultarEspacioDisponible()
                                            │
                           ┌────────────────┴────────────────┐
                           │          Frame ALT              │
                           ├─────────────────────────────────┤
                           │ [espacioSuficiente == true]     │
                           │   -> 6: guardarEnDisco()        │
                           │   -> 7: OK (archivoCreado)      │
                           ├─────────────────────────────────┤
                           │ [else: espacioSuficiente==false]│
                           │   -> 9: errorEspacioInsuficiente│
                           │   -> 10: mostrarAvisoError()    │
                           └─────────────────────────────────┘
```

---

## ⭐ Justificación del Requisito PLUS (Acción de Error)

En el fragmento `alt`, cuando el `:SistemaOperativo` devuelve que no hay espacio suficiente en disco (`espacioSuficiente == false`), la secuencia se desvía al bloque de error:
- El `:ModuloAlmacenamiento` emite el mensaje de retorno `errorEspacioInsuficiente`.
- El `:GestorArchivos` ordena a la `:InterfazUsuario` ejecutar `mostrarAvisoError("Sin espacio suficiente en disco")`.
- La interfaz despliega el mensaje de error al `:Usuario`, finalizando la interacción de forma limpia.

---

## 🛠️ ¿Cómo abrir y modificar el diagrama?
1. Abrí [`03_secuencia.drawio`](file:///home/axel/Escritorio/UTN/M%20de%20Sistemas%20II/docs/TP-1/03-Diagrama-de-Secuencia/03_secuencia.drawio) en VS Code.
