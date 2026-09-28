# Explicación del Diagrama de Comunicación del TP-1

---

## 🎯 Objetivo en el Trabajo Práctico

Cumplir con el **Punto 4 de la consigna**, desarrollando el Diagrama de Comunicación para el Caso de Uso de **Crear / Almacenar Archivo**, identificando objetos, enlaces y la numeración secuencial de mensajes.

---

## 🔗 Objetos y Enlaces Representados

```
[ :Usuario ] ─────── (Enlace 1) ───────> [ :InterfazUsuario ]
                                                 │
                                             (Enlace 2)
                                                 │
                                                 v
[ :SistemaOperativo ] <─── (Enlace 4) ─── [ :GestorArchivos ]
                                                 │
                                             (Enlace 3)
                                                 │
                                                 v
                                    [ :ModuloAlmacenamiento ]
```

---

## 🔢 Secuencia de Mensajes Numerada

1. **`1: solicitarCreacionArchivo(datos) ➔`** (de `:Usuario` a `:InterfazUsuario`)
   - Inicia la interacción enviando los parámetros de la solicitud.
2. **`2: procesarCreacion(nombre, tipo, datos) ➔`** (de `:InterfazUsuario` a `:GestorArchivos`)
   - Traspasa la solicitud a la capa de control de negocio.
3. **`3: almacenarYClasificar(archivo) ➔`** (de `:GestorArchivos` a `:ModuloAlmacenamiento`)
   - Solicita clasificar el archivo en su categoría adecuada (*imágenes, docs, etc.*).
4. **`3.1: validarEspacioYEscritura() ➔`** (de `:ModuloAlmacenamiento` a `:SistemaOperativo`)
   - Invocación anidada enviada al SO para validar la disponibilidad física en disco.
5. **`4: «return» resultadoAlmacenamiento() ⬅`** (de `:ModuloAlmacenamiento` a `:GestorArchivos`)
   - Devuelve la confirmación del guardado.
6. **`5: «return» notificarResultado() ⬅`** (de `:GestorArchivos` a `:InterfazUsuario`)
   - Finaliza el ciclo notificando el éxito a la interfaz.

---

## 🛠️ ¿Cómo abrir y modificar el diagrama?
1. Abrí [`04_comunicacion.drawio`](file:///home/axel/Escritorio/UTN/M%20de%20Sistemas%20II/docs/TP-1/04-Diagrama-de-Comunicacion/04_comunicacion.drawio) en VS Code.
